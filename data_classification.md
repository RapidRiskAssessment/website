---
layout: default
title: Data Classification
description: A standard data classification which can be customized
---

# Data Classification

A data classification allows for rapidly triaging data types and understand their sensitivity and intended audience. It is recommended to use these classification labels when creating new documents, sending emails, etc. as necessary.
Alternatively, it is also useful to directly label data in databases, automatically. This speeds up risk analysis as one can then query which classes of data are involved with their analysis.

<table>
<thead>
<tr class="header">
<th><p>Classification label</p></th>
<th><p>Definition</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span class="risk risk-low">PUBLIC</span></p></td>
<td>
<ul>
<li>Data that can be shared with the world..</li>
<li>The information would have no negative effect if made public.</li>
<li>May be at risk if modified maliciously.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk score-blue">INTERNAL CONFIDENTIAL</span></p></td>
<td><ul>
<li>Data that can be shared with internally with all teams within an oraganization/</li>
<li>This information is potentially sensitive and could have a negative impact if made public.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><span class="risk score-yellow">SPECIFIC WORKGROUPS ONLY</span></p>
<td>
<ul>
<li>Data that can be shared with a specific group of people, such as a specific team.</li>
<li>This information, if disclosed beyond the group, would expose information that is not necessary and/or should not be available to the rest of the company (e.g. "employee salary info").</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk score-red">SPECIFIC INDIVIDUALS ONLY</span></p></td>
<td>
<ul>
<li>Zero to minimal intentions of objective met.</li>
<li>Data that can be shared only with specific individuals who have been granted access by the data owner.</li>
<li>This information, if disclosed beyond the individuals, would have a significant negative effect on the organization or its users.</li>
</ul></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>
