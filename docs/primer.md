---
title: Why does it work?
description: An explanation of why the RRA works the way it works
sidebar:
  nav: "docs"
toc: true
toc_sticky: true
read_time: true
---

<!--
1. Review notes
- Taylorism => Checklist => Nopers
- Risk analysis is not "data science"
- Sec principles => Guides => Checklists
                 => RRA  /
- Talk about NIST?
- 80% Good is important
- Controls? What (yes) vs How (meh)
- Impact: Qualify it
- Likelihood: Quantify it

2. Split implementations to their own page
-->

![robot-arm](/assets/img/arm.png){: .align-left}
This document summarizes the fundamental concepts, requirements and technical details behind the Rapid Risk Assessment (RRA).

We call the way the RRA works a "Threat Scenario based risk assessment".

Through this document, we will discuss why we believe this model works well.

{: .text-nowrap}

# History

Risk assessments are based on threat models, which attempt to view a system, service, etc. as an attacker in order to ensure the right controls (or mitigations) are implemented in order to reduce risk. To some degree, the assessments attempt to *predict* bad outcomes. This can be very difficult to get right.

![pile-of-paper](/assets/img/pile.jpg){: .align-right}
To standardize the assessments, [ISO 31000](https://infogalactic.com/info/ISO_31000) was created in 2009 (for context, a previous effort such as the French [EBIOS](https://infogalactic.com/info/EBIOS) was created in 1995).

Frameworks based on ISO 3100 tend to aim for correctness and require strict, extensive data collection before the analysis can be performed. The analysis itself is also extensive. It is typical for a full analysis to take weeks or even years (!).

Because this does not scale well for fast-paced development, and because the risk may have been realized in practice before the analysis is completed, several variations are usually implemented by software development companies and government bodies, for example:

- [NIST SP 800-30](https://csrc.nist.gov/publications/detail/sp/800-30/rev-1/final), [NIST CyberSecurity Framework](https://www.nist.gov/cyberframework), where the former is a more typical risk assessment process and the latter focuses on response to incidents regardless of risk, but does not directly integrate to the development lifecycle of systems, products, etc.
- [STRIDE](https://infogalactic.com/info/STRIDE_(security)), [DREAD](https://infogalactic.com/info/DREAD_(risk_assessment_model)) for software development. These simply list threat categories, or types, that you should think about when writing software specifically. It's definitely useful, though it generally only works for the software aspect of risk analysis specifically. It does not tell you how much money it's going to cost or how the company reputation may be affected if the software breaks, for example.
- Vulnerability-based assessments, such as [CVSS](https://www.first.org/cvss/) which works well to standardize the impact of vulnerabilities, and includes some probability factors (e.g.: "can this be exploited locally, via network?" which are used to estimate how likely it is for the vulnerability to be exploited)
- Technique-based assessments, such as [ATT&CK](https://attack.mitre.org/) where threats are categorized by attack type and generalized techniques, and very detailled sub-techniques and procedures (e.g. "The file `/Library/Preferences/com.apple.loginwindow.plist` is modified by an attacker [...]". While an interesting list of possible techniques, these are not based on a threat model and do not provide much flexibility, and therefore tends to be more useful to characterize and remediate to incidents rather than be used for risk discovery, as a threat model or risk assessment normally would.
- Checkbox or survey based assessments ("Do you do x?, do you have z?") which are feature based (e.g.: If your door has a lock it passes. But how good is the lock, and in what context are generally not answered by these frameworks.)
  - A sub-category of checkbox-based assessments, such as [ICTM](https://github.com/defuse/ictm) which ignores the brainstorming (threat) models in favor of "security invariants", which are proponents of using checkbox-based assessments as a __complete replacement__ to threat models. Note that the invariants themselves (i.e. control requirements) are produced through a brainstorming exercice.
  - Another sub-category, which is effectively an advanced version of checkbox-based assessments, which are then certified by 3rd parties, such as [Common Criterias](https://www.commoncriteriaportal.org/) or 1970's [Orange book (ITSEC)](https://infogalactic.com/info/Trusted_Computer_System_Evaluation_Criteria).
- Frameworks which attempt to address specific issues with assessing risk accurately (e.g [FAIR](https://infogalactic.com/info/Factor_analysis_of_information_risk)), though these tend to focus on making all aspects of risk quantifiable (usually through assigning a somewhat precise dollar amount, or a fixed number from 0 to 100).


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
*We specifically singled out some lessons learned, in particular our ability as humans to assess impact vs probability.*

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

> A **Standard Level** represents a formalized and concise measure for risk, risk impact, [probability indicators](indicators), mitigation recommendations and control scores.

Risk is generally estimated according to different scales, such as `"low, medium, high"` or `"0 to 100, 0.0 to 1.0"`. However, how these levels are set are very differently from person to person depending on their background, experience, risk appetite and so on.


The RRA instead embraces the idea that pure risk quantification is usually impossible, and perhaps counter-productive. Decisions maker are informed with numbers that look authoritative, but are defined by gut-feelings. 

### Quantitative vs Qualitative

- Quantitative analysis indicates that a quantity (number, measurable) is associated with the impact and likelihood.
- Qualitative analysis indicates that the impact and likelihood are qualified (estimated, using a list of indicators or rules).

### Levels and bucketing by range

However, in practice, we generally observe that either analysis tend to produce results that require additional context for a decision maker to really understand the risk. Rather than forcing analysts to find numbers (which may be really incorrect), or guesstimate according to their internal knowledge, the RRA embrace the fact that numbers will not be exactly accurate, and not always measurable.

The RRA [Standard Levels](standard_levels) effectively bucket risk (<span class="risk risk-low">low</span>, <span class="risk risk-medium">medium</span>, <span class="risk risk-high">high</span>, <span class="risk risk-maximum">maximum</span>) according to ranges by impact categories (reputation, productivity, financial, legal), f.e.:

- If you guesstimate __or__ measure the financial loss to be __between__ 1,000 USD and 10,000 USD, you go into bucket [low, medium, ...]
- If you guesstimate __or__ measure the reputation loss to be represented as showing up in the technical news (hackernews, etc.), but not mainstream news, you go into bucket [low, medium, ...]

And so on. The actual range and level combination must be customized for your organization. Indeed, a loss of 10,000 USD may be nothing for some, or the end of the company for others.

See the RRA [Standard Levels](standard_levels) for the template and default examples that you can directly use.

## Threat Scenarios

> A **Threat Scenario** is a short sentence describing a _probable_ malicious action an attacker could take, that impacts an asset or service.

The Threat Scenarios ignore the security controls and focuses on the outcome or objective, if an attacker were to be successful with their attack. In essence, it is an example (a scenario!) of what could happen. The Threat Scenario is then measured in terms of impacts with a [Standard Level](standard_levels).


A typical Threat Scenario is constructed as such:

`[`<span class="risk risk-low">low</span>, <span class="risk risk-medium">medium</span>, <span class="risk risk-high">high</span>, <span class="risk risk-maximum">maximum</span>`] [Attacker/Actor]` compromises `[asset/system/service/project]` with `[vulnerability]` which causes `[description of impact, with standard level justification]`.

See [Threat Scenarios](threat_scenarios) for more details on how to create Threat Scenarios.

## Control scoring

> A **Control Score** is similar to a standard risk level, but utilized for scoring controls effectiveness and coverage. Controls are mitigating risk for their associated Threat Scenarios.

Controls are divided into 2 categories:
- **Prevention** (blocks the action from occuring, e.g. "Firewall")
- **Detection** (alerts or log when the action is occuring).

Usually it is best to have both control types for a threat scenario as all controls can fail.

Controls are scored by the [Standard Levels](standard_levels): <span class="risk score-green">A</span>, <span class="risk score-blue">B</span>, <span class="risk score-yellow">C</span>, <span class="risk score-yellow">D</span>,<span class="risk score-red">F</span>.

## Data Classification, dictionary

> **Data Classification** is the act of ranking data by sensitivity, audience, etc. and it is recorded in a dictionary.

All Threat Scenarios (and risk in general) are based on the data - is a configuration file, a pdf, an image, a website, etc. sensitive? How sensitive?

To speed things up, the RRA uses a [data classification](data_classification) that is mainly based on the audience of the data: <span class="risk risk-low">PUBLIC</span>, <span class="risk score-blue">INTERNAL CONFIDENTIAL</span>,<span class="risk score-yellow">SPECIFIC WORKGROUPS ONLY</span>, <span class="risk score-red">SPECIFIC INDIVIDUALS ONLY</span>.

## Recommendations

> **Recommendations** are a list of mitigating actions, ranked in terms of priority by a Standard Level.

The mitigating actions may be about implementing a control, changing a setting, performing a longer analysis (which will lead to additional recommendations).

It is extremely useful to rank these by priority using the Standard Levels. Generally, the recommendations should help increase the control scores for a particular Threat Scenario, effectively, reducing the risk. However, some recommendations may be tangential to risk reduction: performing a deeper analysis, performing the control scoring if it has not been done, etc.

Normally, <span class="risk risk-maximum">MAXIMUM</span> and <span class="risk risk-high">HIGH</span> recommendations are expected to be completed (as per [Standard Levels](standard_levels)) or a disruptive measure is to be taken in order to ensure the additional risk of not following the recommendation is reasonable (e.g. "escalate to the director, project manager, etc." for decision).

# Risk Implementations

Various implementation of Rapid Risk Assessments have been implemented using these fundamentals. The original version is called the RRA (Rapid Risk Assessments) and is used to perform a lightweight threat model for services.

## RRA for Services

See the [Rapid Risk Assessments for Services](rapid_risk_assessment) guide.

_Use it when:_
 - A quick threat model is adequate (30min+)
 - You have less than a few hundred of reviews a year (depending on your team's size and skill level, it may be difficult to scale above a few thousand a year)
 - You need to be able to triage quickly, and you may dive deeper on some of the RRAs (hours, days instead of minutes for a few of them, possibly transforming them into custom threat models)
 - You are reviewing services (the RRA also works for "security risk questions", but most valuable for services)

## FA-RRA

The Functional Area Rapid Risk Assessment will be documented soon!

## Large scale risk assessment

For projects with a large, but relatively consistent threat model (issued from an RRA or not), it is useful to use the RRA fundamental primitives described above. These generally address the scaling issue, where issuing a single, human-run RRA document for a service is not realistic.

Such projects generally provide their own risk register/exploration table, which uses these concepts, for example:

### Threat Scenarios

<span class="risk risk-high">HIGH</span> An attacker ...
- Affects Integrity of the product
- 5 Associated MITRE TTP identified
- Would result in
  - < 1 week of press coverage on technical websites
  - no legal issues expected
  - 2 teams will have to deal with press and patching the issue and the company will likely stop working to ask questions and read the news for a a few hours
  - may cost up to $10M in damages due to ...
  - no direct loss of competitive advantage

[...]

### Control Scores

This may be in a parsed document or table, for example:

- **Control: Process Sandbox**
  - Prevention Score: <span class="risk score-blue">B</span>
    - 90% of the fleet is covered [query here]
    - The sandbox currently contains 7 RPC calls which could contain vulnerabilities
    - The sandbox achieves most objectives, but it's still possible to exfiltrate data out of the sandbox when compromising another system which the sandbox can communicate with (i.e. 2+ compromises)
  - Detection Score: <span class="risk score-yellow">C</span>
    - There is a system which checks if the sandbox code is properly integrated into the product.
    - The logging indicates if the sandbox is running, but not if issues are detected yet, for example if an invalid IPC call is seen
    - The logging does not currently trigger a detection investigation

[...]

### Risk mapping

| Threat Scenario                                                | Residual Risk                                  | Control Name                | Prevention Score                          | Detection Score                            |
|----------------------------------------------------------------|------------------------------------------------|-----------------------------|-------------------------------------------|--------------------------------------------|
| <span class="risk risk-high">HIGH</span> An attacker [...]     | <span class="risk risk-medium"> MEDIUM </span> | Process Sandbox             | <span class="risk score-blue">B</span>    | <span class="risk score-yellow">C</span>   |
| <span class="risk risk-medium">MEDIUM</span> An attacker [...] | <span class="risk risk-low"> LOW </span>       | Hardware-backed credentials | <span class="risk score-green"> A </span> | <span class="risk score-yellow"> C </span> |
| ...                                                            | ...                                            | ...                         | ...                                       | ...                                        |

The risk mapping (or register, exploration) table generally includes additional columns for your own use-case, such as tagging for other frameworks, environment selection, mitigation tracking (recommendation), etc.

## Roll-your-own

Nothing here fits, but you believe in the RRA Fundamental's values? It's always possible to roll out your own model based on the Threat Scenarios, Standard Levels, Controls Scoring and their Data Classification. Most of these are inspirared by the "Large scale risk assessment" described above.

If you do, please [let us know](https://github.com/orgs/RapidRiskAssessment/discussions)!

## Notes on inter-framework compatibility

It is possible to map the RRA data back with various frameworks, as long as:

1. The Standard Levels can be made to match.
2. Threat Scenarios can be used to describe an overall threat.

Generally, a table will include the various tags or other elements to map the models. For example, you can map your Threat Scenarios to the [MITRE ATT&CK framework](https://attack.mitre.org/) by tagging each Threat Scenario with one or many TTP. Similarly, the [NIST Cyberframework Function/Category IDs](https://www.nist.gov/cyberframework/online-learning/components-framework) may be used, or each Threat Scenario tied to an incident can be tagged with [VERIS labels](https://github.com/vz-risk/veris/blob/master/verisc-labels.json) in various ways.
