---
layout: single
title: Threat Scenarios: Client Endpoints
description: An open framework to assess security risk from an operational perspective
read_time: true
sidebar:
  nav: "docs"
---

*This document lists example threat scenarios for client endpoints (laptops, phones, workstations, etc.)*

It is recommended to read the [Threat Scenarios](../threat_scenarios.md) documentation on how threat scenarios can be defined, modified, extended, etc.
The following list is meant as a starting point to customize, for the risk assessments related to client endpoints.

Endpoint impacts can only be estimated when tied to a list of services the client endpoint can access. For the purpose of these threat scenarios, the impact is averaged to <span class="risk risk-medium">medium</span>, then adjusted with non-impact [Standard Levels](../standard_levels) ratings.


## Threat Scenarios

<span class="risk risk-high">high</span>
The attacker compromise a client endpoint with a web-browser vulnerability with sandbox escape, allowing them to execute arbitrary code on the machine as the user.

- **Attention**: Full attention from security team required  (<span class="risk risk-high">high</span>).
- **Impact**: Attacker's access is equivalent to user's access in most scenarios (<span class="risk risk-medium">medium</span>).
- **Effort**: Minimum effort required to fix (<span class="risk risk-medium">medium</span>).
- **Risk** acceptance: Should not be accepted (<span class="risk risk-maximum">maximum</span>).
- **SLO**: Fix now (<span class="risk risk-maximum">maximum</span>).
- **Result**: `(3+2+2+4+4)/5 = 3`, i.e. <span class="risk risk-high">high</span>
