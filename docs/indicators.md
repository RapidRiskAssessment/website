---
title: Probability Indicator
description: A description of Probability (likelihood) indicator and their usage.
sidebar:
  nav: "docs"
---

> A **Probablity Indicator**[^1] is a piece of information with it's [Standard Level](standard_levels) which indicates how a _measurement_ may affect the probability of a [Threat Scenario](threat_scenarios) to occur.

[^1]: Also called Likelihood Indicator (deprecated).

Probability Indicators are issued from measurements generally performed [by machines](primer#human-versus-machine), such as vulnerability scanners, configuration reports, automatic threat hunting tools, usage metrics, etc.

## Structure of indicators

Each Probability Indicator can be customized to fit the needs, however, it requires a few mandatory pieces of information:

```json
"uuid": "unique indicator identifier",
"assetid": "an asset identifier, should be unique",
"ts": "timestamp at measurement, UTC",
"source": "the system event source, must be unique",
"indicator": "Standard Level",
[OPTIONAL]"details": {"custom data"}
```

### Example

```json
"uuid": 2139-4039-4032-2393,
"assetid": "test.domain.com",
"ts": 1673654215,
"source": "test-indicator.domain.com",
"indicator": "HIGH"
"details": {
 "detection_score": 0.754,
 "CVE": "2023-01-01",
 "CVSS": "9.9",
 "description": "Vulnerability detected on test.domain.com"
}
```

See also this real-world ([implementation example](https://github.com/mozilla/service-map/blob/master/models/v1/indicators/indicator.py#L61-L89)).

## Mapping indicators levels


### Scored measurements

When a measurement score is used (0.00 to 1.00 for example), it can be mapped to the [Standard Levels](standard_levels) scores (A to F). In turn, these map directly to Probability Indicator levels, which is the same logic as any other Standard Level:

|------------------------------------------|------------------------------------------------|
| <span class="risk score-green">A</span>  | <span class="risk risk-low">LOW</span>         |
| <span class="risk score-blue">B</span>   | <span class="risk risk-medium">MEDIUM</span>   |
| <span class="risk score-yellow">C</span> | <span class="risk risk-high">HIGH</span>       |
| <span class="risk score-yellow">D</span> | <span class="risk risk-high">HIGH</span>       |
| <span class="risk score-red">F</span>    | <span class="risk risk-maximum">MAXIMUM</span> |

Note that it is up to the implemented to map their internal scoring to the A-F scale from the Standard levels, using the [available guidance](standard_levels).

### Manually ranked measurements

When no scoring measurement is available, it may be more difficult to decide on the correct Probability Indicator level. The following guidance is used in order to manually rank or map values to Standard Levels.

- <span class="risk risk-low">LOW</span>: The absence of control, measure of positive result is _unlikely_ to cause any Threat Scenario to manifest. It may cause incident response to be slower or more difficult, but not cause be the cause of an incident.
- <span class="risk risk-medium">MEDIUM</span>: The absence of control or measure of positive result may cause a Threat Scenario to manifest _in the coming year_ (365+ days). It may be the cause of an incident, though it's difficult to clearly assess.
- <span class="risk risk-high">HIGH</span>: The absence of control or measure of positive result may cause a Threat Scenario to manifest _during the coming year_ (365 days or less). It is likely to be the cause of an incident and we can clearly justify it, for example, it has happened in the past year(s) when the same indicator triggered.
- <span class="risk risk-maximum">MAXIMUM</span>: The absence of control or measure of positive result will cause a Threat Scenario to manifest soon (weeks or months). We believe it will be the direct cause of an incident and we can clearly justify it, for example, it has happened this year or this past month or week, or is a well known, easy to reproduce issue that we know attackers are utilizing every day. 
