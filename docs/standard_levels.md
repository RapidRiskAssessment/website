---
title: Standard Risk Levels
description: A standard risk level taxonomy which can be customized
sidebar:
  nav: "docs"
toc: true
toc_sticky: true
---

[Skip to level definitions](#levels-definitions){: .btn .btn--inverse} [Skip to scores](#scoring){: .btn .btn--inverse}

> A **Standard Level** represents a formalized and concise measure for risk, risk impact, probability indicators, mitigation recommendations and control scores.

The goal of this document is to ensure consistency, coherence between security documents which measure risk, impact or scores security controls.

Each level is documented with the following information:
- **Level color coding** (and name / name schemes).
- **Level expectations**:
  - Attention
  - Impact
  - Effort
  - Risk acceptance _(and whom should accept)_
  - Timeframe for resolution or SLA/SLO (Service Level Agreement/Objective)
  - Any of your organization customizations (mappings to other frameworks, etc.)
- **Justification** of impacts in terms of it affects:
  - Reputation _(includes legal)_
  - Productivity
  - Finances _(includes loss due to productivity loss, e.g. `10 team members * "100K USD" / 365 = loss per day`, for 10 team members)_
  - Competitive Advantage

The risk levels are *qualitative* risk buckets, with clearly defined *quantitative* ranges where applicable. They are generally used to display risk, risk impact, risk probability, or importance.
The scores are used to score security preventive or detection controls.

{: .notice--info}
When implementing these levels, you will want to customize them for your own risk tolerance. For example, how much financial, reputation, etc. damage maps to which level. To make this easier, the values to changes are <u>underlined</u>.

{: .notice--warning}
**This is important**: When using the levels for assessing risk impact or probability, it is very strongly recommended to justify the level by providing your own justification of impacts with [threat scenarios](threat_scenarios). When unsure which level to choose, it can be helpful to think in terms of "Why Not Higher" and "Why Not Lower", i.e. try to justify at a lower or high level and see if it makes sense. Pick the closest.

# Levels definitions

*The risk levels also represent a simplified ISO 31000 equivalent (and are non-compliant with ISO 31000*.

---

<span class="risk risk-maximum">MAXIMUM</span> <span class="risk-color-code">Color code: #d04437</span>
<!-- Red signifies "most important" colloquially. Maximum is a level, "critical" is not. -->

- __Attention__: Full attention from all concerned parties required.
- __Impact__: Severe degradation in or loss of mission capability to an extent and duration that the organization is not able to perform one or more of its primary functions.
- __Effort__: All resources engaged on fixing issues.
- __Risk acceptance__: Rarely accepted as residual risk, must be discussed, and must be mitigated or remediated. <u>CSO, VP or board</u> approval required.
- __SLO__: Recommend fixing <u>immediately (P0)</u>.

_Justification of impacts:_
- __Reputation__: Significant degradation of public trust in the organization and/or it's products. Prominent (mainstream media) press coverage, long-term negative media coverage <u>> 4 weeks</u>, Political/regulatory investigation, <u>1+</u> customer lawsuit, [SEC](https://www.sec.gov/) sanctions.
- __Productivity__: Most team members in one or many product areas cannot perform their normal day to day work.
- __Finances__: Organization or customer revenue impact of <u>> $100M+ USD/year</u> or in a single year.
- __Competitive advantage__: Loss of competitive advantage in relevant industry, Competitors will understand the internal product & strategy, <u>80%+</u> users or customers impacted.

_Examples:_
- Substantial damage to organizational assets.
- Immediate, systematic compromise of systems and users.
- Severe or catastrophic harm to individuals involving loss of life or serious life-threatening injuries.

---

<span class="risk risk-high">HIGH</span> <span class="risk-color-code">Color code: #ffd351</span>
<!-- Yellow generally signifies "warning". In our case it correlates to "important". -->

- __Attention__: Full attention from all concerned parties required.
- __Impact__: Significant degradation in mission capability to an extent and duration that the organization is able to perform its primary functions, but the effectiveness of the functions is significantly reduced.
- __Effort__: Some key resources engaged in fixing the issue.
- __Risk acceptance__: Rarely accepted as residual risk, must be discussed, and must be mitigated or remediated. <u>VP or director</u> approval required.
- __SLO__: Recommend fixing within the next <u>7 days (P1)</u>.

_Justification of impacts:_

- __Reputation__: Limited press coverage (technical news only), medium term negative media coverage <u> < 1 week</u>, political/regulatory scrutiny, <u>1 or no</u> customer lawsuits.
- __Productivity__: Large groups (<u>20+</u>) of team members cannot perform their day to day work.
- __Finances__: Organization or customer revenue impact of <u>$10M to $100M USD/year</u> or in a single year.
- __Competitive advantage__: Some loss of competitive advantage, competitors may understand internal product & strategy. Some services' external user base impacted (<u>50% or less</u> of user base).

_Examples:_

- Considerable damage to organizational assets.
- Serious compromise of a team member or sensitive team's systems.
- Significant financial loss or result in significant harm to individuals that does not involve loss of life or serious life-threatening injuries.

---

<span class="risk risk-medium">MEDIUM</span> <span class="risk-color-code">Color code: #4a6785</span>
<!-- Blue is calm and neutral -->

- __Attention__: Attention from all concerned parties.
- __Impact__: Degradation in mission capability to an extent and duration that the organization is able to perform its primary functions, but the effectiveness of the functions is noticeably reduced.
- __Effort__: Best effort. Following standards and guidelines is still required.
- __Risk acceptance__: Risk should be discussed, and at least mitigated. May request approvals from <u>manager or team lead</u>.
- __SLO__: Recommend remediation within <u>90 days (P2)</u>.

_Justification of impacts:_

- __Reputation__: Internal chatter (issue tracker, chatrooms, ...), limited or no press coverage (only Tweets, blogs, etc.), short term negative media coverage <u>< 2 days</u>, no political/regulatory scrutiny, <u>no</u> customer lawsuits.
- __Productivity__: Small groups (<10) of team members cannot perform _some_ their work for a <u>few days (less than a week)</u>
- __Finances__: Organization or customer revenue impact of <u>< $1M USD/year</u> or in a single year.
- __Competitive advantage__: No loss of competitive advantage, No exposure of internal product & strategy, Limited external user base impacted (<u>15% or less</u> of user base).

_Examples:_

- Limited damage to organizational assets.
- Violation of security properties that are relied upon for user or system access decisions, which does not lead to direct compromise of sensitive data.
- Minor financial loss.
- No or very little harm to individuals.

---

<span class="risk risk-low">LOW</span> <span class="risk-color-code">Color code: #cccccc</span>
<!-- Gray is a low contract color which signifies it's not too important, and it's also less catchy. Green is not used here, as green means "OK to do", which is not a level. -->

- __Attention__: Expected but not required.
- __Impact__: Insignificant degradation in mission capability, effectiveness of the functions is potentially reduced.
- __Effort__: Best effort and best practices expected.
- __Risk acceptance__: Risk may often be accepted as residual risk without any approval.
- __SLO__: No time limit <u>(P3, P4+)</u>.

_Justification of impacts:_

- __Reputation__: No press coverage, no internal chatter, no political/regulatory scrutiny, 0 customer lawsuits.
- __Productivity__: Small groups (<u><5</u>) of team members cannot perform some of their work for a limited amount of time (<u>24h</u>).
- __Finances__: Organization or customer revenue impact of less than <u>$1M USD/year</u> or in a single year.
- __Competitive advantage__: No loss of competitive advantage, no exposure of internal product & strategy, little or no external user base impacted (less than <u>1%</u> of user base).

_Examples:_

- No noticeable damage to organizational assets, finances, or harm to individuals.
- Violation of expected security properties or best practices, but does not lead to compromise or does not lead to an escalation of privileges.

---

<span class="risk risk-unknown">UNKNOWN</span> <span class="risk-color-code">Color code: #ffffff</span>
<!-- White represent the emptiness/lack of data, often interpreted as "not a color". -->

- Data collection is expected.
- This level is expected to change to one of the other levels once data is collected.

This is not a __real level__, it is used when there to represent that we do not have enough data to correctly assess the level (i.e. data collection work is required).

{: .notice--info}
Communicating the risk of not knowing is challenging and prone to failure, in particular when once data has been gathered, the risk appears to in fact be low.<br/><br/>
This concept is also known as _"trust, but verify"_ - i.e. unknown does not distrust (by assign it a higher risk) the service, user, etc. by default.

# Scoring

The following scores are intended to provide a grade for a particular objective. The scores map back to the standard risk level definitions so that automatic risk mapping can be performed if necessary.
Scores are useful to grade security  prevention & detection controls implementation, fleet coverage, etc. 

These scoring levels are also used, for example, on the [Mozilla Observatory](https://observatory.mozilla.org).

{: .notice--info}
The use of **+** and **-** modifiers in front of scores (e.g. "A+") is allowed _if necessary_. These are added to represent going slightly above or below expectations.


---

<span class="risk score-green">A</span> <span class="risk-color-code">Color code: #14892c</span>
<!-- Highest possible grade. You may also use A+,A,A- for example -->

The A grade is the highest possible grade.

- __Prevention, detection controls__: Clear story for how the threat is prevented or detected. Bypassing the control would require a  zero-day vulnerability, or compromise of another system.
- __Fleet coverage__: 100% of controls are applied in the fleet, and this can be verified.
- Support all known features, processes, mitigations and controls.
- No recommendations or backlogged work items.
- All intentions of objective met.
- Well maintained, well defined, well measured.

---

<span class="risk score-blue">B</span> <span class="risk-color-code">Color code: #4a6785</span>

- __Prevention, detection controls__: There may be known residual risks in the threat model that aren’t covered by the control, but they require very sophisticated attackers or special access to exploit.
- __Fleet coverage__: 90%+ of controls are applied in the fleet, and the fleet is not expected to grow without the controls being applied.
- Supports most important features, processes, mitigations and controls.
- There may be <span class="risk risk-low">LOW</span> or <span class="risk risk-medium">MEDIUM</span> recommendations that have not yet been followed.
- Some outliers need attention.
- Most intentions of objective met.

---

{: .notice--warning}
The following scores may moderately contribute to risk.

<span class="risk score-yellow">C</span> <span class="risk-color-code">Color code: #ffd351</span>

- __Prevention, detection controls__: Opportunistic controls for the most important threats.
- __Fleet coverage__: 60%+ of controls are applied to the fleet. Some devices are protected, and there is have a clear path forward to increasing adoption.
- Potential service blocker.
- Needs attention and features need to be enabled/controls added.
- There may be <span class="risk risk-low">LOW</span> or <span class="risk risk-medium">MEDIUM</span> recommendations that have not yet been followed.
- May relate to a significant amount of risk.
- Minimal to moderate intentions of objective met.

---

<span class="risk score-yellow">D</span> <span class="risk-color-code">Color code: #ffd351</span>

- __Prevention, detection controls__: There are large known gaps in the security posture regarding this control.
- __Fleet coverage__:  30%+ of controls are applied in the fleet. Some devices are protected, but there is no clear path to universal adoption of the control.
- Potential service blocker.
- Needs attention and features need to be enabled/controls added.
- There may be <span class="risk risk-low">LOW</span>, <span class="risk risk-medium">MEDIUM</span> or <span class="risk risk-high">HIGH</span> recommendations that have not yet been followed.
- May relate to a significant amount of risk.
- Minimal to moderate intentions of objective met.

---

{: .notice--important}
Lowest possible grade, score may greatly contribute to risk.

<span class="risk score-red">F</span> <span class="risk-color-code">Color code: #d04437</span>

- __Prevention, detection controls__:There are little to no controls to mitigate threats.
- __Fleet coverage__: Unknown or low amount of controls are applied in the fleet.
- Zero to minimal intentions of objective met.
- Immediate attention and action are required.
- There may be many recommendations that have not yet been followed, including <span class="risk risk-maximum">MAXIMUM</span> recommendations.
- May relate to a great amount of risk.
- Score likely to block the service or project.
