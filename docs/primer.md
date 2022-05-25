---
title: Why does it work?
description: An explanation of why the RRA works the way it works
sidebar:
  nav: "docs"
toc: true
toc_sticky: true
---

<!--
- Threats need to be rationalized
- Taylorism => Checklist => Nopers
- Risk analysis is not "data science"
- Sec principles => Guides => Checklists
                 => RRA  /
- Talk about NIST?
- 80% Good is important
- Controls? What (yes) vs How (meh)
- Impact: Qualify it
- Likelihood: Quantify it
-->

![robot-arm](/assets/img/arm.png){: .align-left}
This document summarizes the fundamental concepts, requirements and technical details behind the Rapid Risk Assessment (RRA).

We call the way the RRA works a "Threat Scenario based risk assessment".

Through this document, we will discuss why we believe this model works well.

![]()

# History

Risk assessments are based on threat models, which attempt to view a system, service, etc. as an attacker in order to ensure the right controls (or mitigations) are implemented in order to reduce risk. To some degree, the assessments attempt to *predict* bad outcomes. This can be very difficult to get right.

![pile-of-paper](/assets/img/pile.jpg){: .align-right}
To standardize the assessments, [ISO 31000](https://infogalactic.com/info/ISO_31000) was created in 2009 (for context, a previous effort such as the French [EBIOS](https://infogalactic.com/info/EBIOS) was created in 1995).

Frameworks based on ISO 3100 tend to aim for correctness and require strict, extensive data collection before the analysis can be performed. The analysis itself is also extensive. It is typical for a full analysis to take weeks or even years (!).

Because this does not scale well for fast-paced development, and because the risk may have been realized in practice before the analysis is completed, several variations are usually implemented by software development companies and government bodies, for example:

- [NIST SP 800-30](https://csrc.nist.gov/publications/detail/sp/800-30/rev-1/final), [NIST CyberSecurity Framework](https://www.nist.gov/cyberframework), where the former is a more typical risk assessment process and the later focuses on response to incidents regardless of risk but doe not directly integrate to the development lifecycle of systems, products, etc.
- [STRIDE](https://infogalactic.com/info/STRIDE_(security)), [DREAD](https://infogalactic.com/info/DREAD_(risk_assessment_model)) for software development. These simply list threat categories, or types, that you should think about when writing software specifically. It's definitely useful, though it generally only works for the software aspect of risk analysis specifically. It does not tell you how much money it's going to cost or how the company reputation may be affected if the software breaks, for example.
- Vulnerability-based assessments, such as [CVSS](https://www.first.org/cvss/) which works well to standardize the impact of vulnerabilities, and includes some probability factors (e.g.: "can this be exploited locally, via network?" which are used to estimate how likely it is for the vulnerability to be exploited)
- Technique-based assessments, such as [ATT&CK](https://attack.mitre.org/) where threats are categorized by attack type and generalized techniques, and very detailled sub-techniques and procedures (e.g. "The file `/Library/Preferences/com.apple.loginwindow.plist` is modified by an attacker [...]". While an interesting list of possible techniques, these are not based on a threat model and do not provide much flexibility, and therefore tends to be more useful to characterize and remediate to incidents rather than be used for risk discovery, as a threat model or risk assessment normally would.
- Checkbox or survey based assessments ("Do you do x?, do you have z?") which are feature based (e.g.: If your door has a lock it passes. But how good is the lock, and in what context are generally not answered by these frameworks.)
- Some other frameworks, which attempt to address specific issues with assessing risk properly (e.g [FAIR](https://infogalactic.com/info/Factor_analysis_of_information_risk)), though these tend to focus on making all aspects of risk quantifiable (usually through assigning a somewhat precise dollar amount, or a fixed number from 0 to 100).


The Rapid Risk Assessment was created through several iterations (~6 years) and tests, practicing it in real company and community environments at [Mozilla](https://www.mozilla.org) by security engineers who had previously practiced standard risk analysis for computer systems and industrial systems. It aims to provide "80% good" risk assessments in less than an hour and can be seen as a risk socialization tool for non-specialists.

The resulting process is licensed under the [MPL](/LICENSE).

## Lessons learned

*This a TL;DR of what we learned along the years.*

**Positive learnings**:
- Engineers value the direct help of security (and other) specialists as they aim to create good software, systems, services, processes that they can be proud of.
- Humans are good at estimating ("qualifying") the probable worse case loss scenarios, i.e. impact when something goes wrong.
- The process *must* directly provide value the creators and owners of the software, systems, services, etc. rather than security engineers or compliance teams.
- The ratio of value to time spent rapidly diminushes after the first 30 minutes (!)

**Negative learnings**:
- Excessive specialized language is rarely called out and is a diservice to the process as it leads to misunderstandings (Threat actor, target of evaluation, etc.).
- Humans often confuse risk, likelihood and impact, including security specialists. Yup.
- Humans are bad at estimating probability.
- Surveys and fully automated analysis systems don't work well as they do not carry much context, or not concise enough for pratical use. Engineers want to talk to humans that they can talk to about ideas, issues, worries.

## Human versus machine
*We specifically singled out some of the lesson learned, in particular our ability as humans to assess impact vs probability.*

> Risk is assessed by humans **and** machines.

If we assert that humans are:
- Slow at processing large amounts of information.
- Good at rationalizing datasets in creative ways.
- Are subject matter experts in specific domains.

And machines are:
- Fast at processing large amounts of information.
- Bad at rationalizing datasets other than by following a model.
- Not able to understand the data itself.

We can then make the hypothesis that humans will be better at assessing large problems, such as by crafting Threat Scenarios (i.e. how an attacker would exploit a system) and rationalizing overall impacts, or scoring <u>ideal</u> control effectiveness.

By contrast, machines will be better at parsing all vulnerability data, coverage, event data, etc. and assess the probability of an existing, <u>human-defined</u> Threat Scenario to occur. Machines are also good at *ranking* Threat Scenarios and control lists, of course.

{: .notice--info}
TL;DR: As a result, the Threat Scenario based risk assessment focuses on impact assessment for humans, and heavily emphasizes on the quality and accuracy of that impact assessment.


# Fundamentals
This section describes the fundamental concepts utilized by the RRA. These concepts can be used as **building blocks** for various types of risk assessments while retaining the value of the RRA. The main implementation of the RRA is [RRA for Services](rapid_risk_assessment)

## Standard Levels

Risk is generally estimated according to different scales, such as `"low, medium, high"` or `"0 to 100, 0.0 to 1.0"`. However, how these levels are set are very differently from person to person depending on their background, experience, risk appetite and so on.


The RRA instead embraces the idea that pure risk quantification is usually impossible, and perhaps counter-productive. Decisions maker are informed with numbers that look authoritative, but are defined by gut-feelings. 

### Quantitative vs Qualitative

- Quantitative analysis indicates that a quantity (number, measurable) is associated with the impact and likelihood.
- Qualitative analysis indicates that the impact and likelihood are qualified (estimated, using a list of indicators or rules).

### Levels and bucketing by range

However, in practice, we generally observe that either analysis tend to produce results that require additional context for a decision maker to really understand the risk. Rather than forcing analysts to find numbers (which may be really incorrect), or guesstimate according to their internal knowledge, the RRA embrace the fact that numbers will not be exactly accurate, and not always measurable.

The RRA standard levels effectively bucket risk (<span class="risk risk-low">low</span>, <span class="risk risk-medium">medium</span>, <span class="risk risk-high">high</span>, <span class="risk risk-maximum">maximum</span>) according to ranges by impact categories (reputation, productivity, financial, legal), f.e.:

- If you guesstimate __or__ measure the financial loss to be __between__ 1,000 USD and 10,000 USD, you go into bucket [low, medium, ...]
- If you guesstimate __or__ measure the reputation loss to be represented as showing up in the technical news (hackernews, etc.), but not mainstream news, you go into bucket [low, medium, ...]

And so on. The actual range and level combination must be customized for your organization. Indeed, a loss of 10,000 USD may be nothing for some, or the end of the company for others.

See the RRA [Standard Levels](standard_levels) for the template and default examples that you can directly use.


----
The following are upcoming categories.

## Control scoring
TBD.

## Data Classification and dictionary

TBD.

## Threat Scenarios

TBD.

## Recommendations

TBD.

# Implementations

## RRA

TBD.

## Roll-your-own

TBD.

## Notes on inter-ramework compatibility

TBD.
