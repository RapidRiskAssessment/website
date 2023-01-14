---
title: Data Classification
description: A standard data classification which can be customized
sidebar:
  nav: "docs"
---

> **Data Classification** is the act of ranking data by sensitivity, audience, etc. and it is recorded in a dictionary.

A data classification label allows for rapidly triaging data types and understand their sensitivity and intended audience. It is recommended to use these classification labels when creating new documents, sending emails, etc. as necessary.

Alternatively, it is also useful to directly use labels in databases, issue trackers, etc.  automatically. This speeds up risk analysis as one can then query which classes of data are involved with their analysis.


{: .notice--info}
The following data classification is based on audience, then defines sensitivity for each audience. You may need to customize it for your needs, but it should work for most out of the box.<br/><br/>
It may be useful to annotate some labels specifically for PII (personally identifiable information), as it is often required for privacy and legal reasons.


---

<span class="risk risk-low">PUBLIC</span>

- Data that can be shared with the world.
- The information would have no negative effect if made public.
- May be at risk if modified maliciously.

_Examples_:
- Open source code.
- Test-only credentials.
- Public websites.

---

<span class="risk score-blue">INTERNAL CONFIDENTIAL</span>

- Data that can be shared with internally with all teams within an organization.
- This information is potentially sensitive and could have a negative impact if made public.

_Examples_:

- Internal meetings.
- Team members information.
- Aggregated survey data.

---

<span class="risk score-yellow">SPECIFIC WORKGROUPS ONLY</span>

- Data that can be shared with a specific group of people, such as a specific team.
- This information, if disclosed beyond the group, would expose information that is not necessary and/or should not be available to the rest of the company (e.g. "employee salary info").

_Examples_:

- SSN, addresses, staff performance data.
- Service credentials.
- Contracts, legal documents.

---

<span class="risk score-red">SPECIFIC INDIVIDUALS ONLY</span>

- Zero to minimal intentions of objective met.
- Data that can be shared only with specific individuals who have been granted access by the data owner.
- This information, if disclosed beyond the individuals, would have a significant negative effect on the organization or its users.

_Examples_:

- Security incidents.
- Attorney privileged conversations.
- User data.
