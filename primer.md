---
layout: default
title: Primer
description: An explanation of why the RRA works the way it works
---

# Why does it work?

This document summarizes the concepts, requirements and technical details behind the Rapid Risk Assessment (RRA). We call the way the RRA works a threat Scenario based risk assessment.
In other words, it exposes why we think this works well.

# History

Risk assessments are based on threat models, which attempt to view a system, service, etc. as an attacker in order to ensure the right controls (or mitigations) are implemented in order to reduce risk. To some degree, the assessments attempt to *predict* bad outcomes. This can be very difficult to get right.

- [ISO 31000](https://infogalactic.com/info/ISO_31000)-based frameworks tend to aim for correctness and require a strict, extensive data collection before the analysis can be performed. The analysis itself is also extensive. It is typical for a full analysis to take weeks or even years. Because of this does not scale well for fast-paced development, or because the risk may have been realized in practice before the analysis is completed, several variations are usually implemented by organizations:
- [NIST SP 800-30](https://csrc.nist.gov/publications/detail/sp/800-30/rev-1/final), [NIST CyberSecurity Framework](https://www.nist.gov/cyberframework), where the former is a more typical risk assessment process and the later focuses on response to incidents regardless of risk but doe not directly integrate to the development lifecycle of systems, products, etc.
- [STRIDE](https://infogalactic.com/info/STRIDE_(security)), [DREAD](https://infogalactic.com/info/DREAD_(risk_assessment_model)) for software development. These simply list threat categories, or types, that you should think about when writing software specifically. It's definitely useful, though it generally only works for the software aspect of risk analysis specifically. It does not tell you how much money it's going to cost if the software break, for example.
- Checkbox or survey based assessments ("Do you do x?, do you have z?")
- Some other frameworks, which attempt to address specific issues with assessing risk properly (e.g [FAIR](https://infogalactic.com/info/Factor_analysis_of_information_risk))

The Rapid Risk Assessment was created through several iterations (~6 years) and tests in real company and community environments at [Mozilla](https://www.mozilla.org) by security engineers who had previously practiced standard risk analysis for computer systems and industrial systems. The resulting process is licensed under the [MPL](LICENSE-MPL).

## Lessons learned

*This a TL;DR of what was learned along the years.*

Positive things:
- Engineers value the direct help of security specialists as they aim to create good software, systems, services, processes that they can be proud of.
- Humans are good at estimating the probable worse case loss scenarios, i.e. impact.
- The process must directly provide value the creators, owners of the software, systems, services, etc. rather than security engineers or compliance teams.
- The ratio of value to time spent rapidly diminushes after the first 30 minutes (!)

Negative things:
- Excessive specialized language is rarely called out and is a diservice to the process (Threat actor, target of evaluation, etc.).
- Humans often confuse risk and impact, including security specialists. Yup.
- Humans are bad at estimating probability.
- Surveys and fully automated analysis systems don't work well. Engineers want to talk to humans that they can talk to about ideas, issues, worries.

# Key Concepts

## Human versus machine
*We specifically singled out some of the lesson learned, in particular our ability as humans to assess impact vs probability.*

> Risk is assessed by humans *and* machines.

If we assert that humans are:
- Slow at processing large amount of information.
- Good at rationalizing datasets in creative ways.
- Are subject matter experts in specific domains.

And machines are:
- Fast at processing large amount of information.
- Bad at rationalizing datasets other than by following a model.
- Do not understand the data itself.

We can then make the hypothesis that humans will be better at assessing large problems, such as by crafting threat scenarios (how an attacker would exploit a system) and rationalizing overall impacts, or scoring ideal control effectiveness.
By contrast, machines will be better at parsing all vulnerability data, coverage, event data, etc. and assess the probability of an existing, *human-defined* threat scenario to occur. Machines are also good at ranking threat scenario and control lists themselves, of course.

TL;DR: As a result, the threat scenario based risk assessment focuses on impact assessment for humans, and heavily emphasizes on the quality and accuracy of that impact assessment.


# Risk Calculation

TBD.

# Fundamentals

## Standard Levels
TBD.

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
