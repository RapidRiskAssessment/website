---
title: Threat Scenarios
description: A description of how Threat Scenarios are created
sidebar:
  nav: "docs"
---

> A Threat Scenario is a short sentence describing a probable malicious action an attacker could take, that impacts an asset or service.

A typical Threat Scenario is constructed as such:

`[`<span class="risk risk-low">low</span>, <span class="risk risk-medium">medium</span>, <span class="risk risk-high">high</span>, <span class="risk risk-maximum">maximum</span>`] [Attacker/Actor]` compromises `[asset/system/service/project]` with `[vulnerability]` which causes `[description of impact, with standard level justification]`.

## How are Threat Scenarios defined?

{: .notice--info}
Figuring out the right threats is an exercise of it's own which can be fairly rapid to get a general idea, but take days to fine tune.


### 1. Figure out the threats

Threat Scenarios are generally defined through a threat model or risk assessment, such as the [RRA for Services](rapid_risk_assessment.md). When existing threat models exist with various "attack models", "tree", "scenarios", or equivalent examples - these can and should be reformated as Threat Scenarios. In other words, Threat Scenarios are [defined by humans](primer#human-versus-machine) through specifically focused brain-storming exercises.

{% capture notice-2 %}
- Concise, to the point. Just a line or so, _not a paragraph_.
- High level example of a threat that could be realized, without too much technical details.
- Not a [MITRE TTP](https://attack.mitre.org/) (However: TTPs can be tied to Threat Scenarios).
- The level represents the probable worse-case impact, _not risk_. It's also called "risk impact" (_not risk_).
- The justification of impact does not need to be part of the Threat Scenario when shared, but the **justification exercise needs to be recorded**.
{% endcapture %}
<div class="notice--info">{{ notice-2 | markdownify }}</div>

At this point you should end up with a list of Threat Scenarios extracted from your threat models - many may be similar (and effectively are derivate of other scenarios - think of them as aliases or variants). You goal is to deduplicate these scenarios and justify them with adequate levels. It's up to you to brainstorm and select the most appropriate scenario. Keep in mind that you can and may improve these over time!

#### Example

- __[Selected]__ An attacker picks up an item at the supermarket, hides it on their person and walks out of the store.
- __[Variant]__ A group of attackers enter the store and pick up various items then exit the store without paying.
- __[Variant]__ An employee regularly picks up an item from the store and exits without paying.

### 2. Justify the selected Threat Scenario

In order to justify the Threat Scenario is correct and be able to rank it with [Standard Levels](standard_levels), you must go through each categories described by the levels: Reputation, Productivity, Finances, Competitive Advantage.

#### Example

An attacker picks up an item at the supermarket, hides it on their person and walks out of the store.

- **Reputation**: <span class="risk risk-medium">medium</span> Internal chatter expected but no lawsuits, customers are unlikely to notice or remember.
- **Productivity**: <span class="risk risk-low">low</span> Filling policy report, low impact on the supermarket workforce.
- **Finances**: <span class="risk risk-medium">medium</span> The attacker generally can't pick-up more than a few items without being intercepted which caps our worse-case to about 1000 USD of loss, that we consider medium impact per event on our scale.
- **Competitive Advantage**: N/A.

{: notice--info}
Some of these justifications involve some type of likelihood, but are not used to calculate or declare the probability of the Threat Scenario itself.

### 3. Rank the Threat Scenario itself

Ranking the Threat Scenario's risk impact is simple: take the highest level selected for any of the justifications and assign it. In our examples, the highest is <span class="risk risk-medium">medium</span> and so that's what we'll select:


{: .notice--success}
<span class="risk risk-medium">medium</span> An attacker picks up an item at the supermarket, hides it on their person and walks out of the store.
