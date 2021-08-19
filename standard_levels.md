---
layout: default
title: Standard Levels
description: A standard risk level taxonomy which can be customized
---

# Standard Risk Levels
The goal of this document is to ensure consistency, coherence between security documents which measure risk, impact or scores security controls.
Each level is documented with the following infomation::
- Level color coding.
- Name or name schemes.
- Level expectations.
- Examples of usage.
- Timeframe for resolution.

The risk levels are *qualitative* risk buckets, with clearly defined *quantitative* ranges where applicable. They are generally used to display risk, risk impact, risk probability, or importance.
The scores are used to score security preventive or detection controls.

# Levels definitions

*The risk levels also represent a simplified ISO 31000 equivalent (and are non-compliant with ISO 31000*.

<table>
<thead>
<tr class="header">
<th><p>Risk Level</p></th>
<th><p>Expectations</p></th>
<th><p>Rationale</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span class="risk risk-maximum">MAXIMUM Risk</span></p><p><span class="risk-color-code">HTML Color code #d04437</span></p></td>
<td><p><em>This is the most important level, where the risk is especially great.</em></p>
<ul>
<li><strong>Attention</strong>: Full attention from all concerned parties required.</li>
<li><strong>Impact</strong>: High or maximum impact.</li>
<li><strong>Effort</strong>: All resources engaged on fixing issues. Following standard/guidelines is required.</li>
<li><strong>Risk acceptance</strong>: Rarely accepted as residual risk, must be discussed, and must be mitigated or remediated.</li>
<li><strong>Exception time (SLA)</strong>: Recommend fixing <strong>immediately</strong>.</li>
</ul></td>
<td><ul>
<li>Red signifies &quot;most important&quot;.</li>
<li>Maximum is a level. Critical is not.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk risk-high">HIGH Risk</span></p><p><span class="risk-color-code">HTML Color code #ffd351</span></p></td>
<td><ul>
<li><strong>Attention</strong>: Full attention from all concerned parties required.</li>
<li><strong>Impact</strong>: Medium, high or maximum impact.</li>
<li><strong>Effort</strong>: Some key resources engaged on fixing the issue. Following standard/guidelines is required.</li>
<li><strong>Risk acceptance</strong>: Risk must be discussed, and must at least be mitigated.</li>
<li><strong>Exception time (SLA)</strong>: Recommend remediation within <strong>7 days</strong>.</li>
</ul></td>
<td><ul>
<li>Yellow generally signifies &quot;warning&quot;. In our case it correlates to &quot;important&quot;.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><span class="risk risk-medium">MEDIUM Risk</span></p><p><span class="risk-color-code">HTML Color code #4a6785</span></p></td>
<td><ul>
<li><strong>Attention</strong>: Attention from all concerned parties.</li>
<li><strong>Impact</strong>: Low, medium or high impact.</li>
<li><strong>Effort</strong>: <em>Best effort</em>. Following standard/guidelines is required.</li>
<li><strong>Risk acceptance</strong>: Risk should be discussed, and at least mitigated.</li>
<li><strong>Exception time (SLA)</strong>: Recommend remediation within <strong>90 days</strong>.</li>
</ul></td>
<td><ul>
<li>Blue is calm and neutral.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk risk-low">LOW Risk</span></p><p><span class="risk-color-code">HTML Color code #cccccc</span></p></td>
<td><ul>
<li><strong>Attention</strong>: Expected but not required.</li>
<li><strong>Impact</strong>: Low or medium impact.</li>
<li><strong>Effort</strong>: <em>Best effort</em> and <strong>best practices</strong> expected.</li>
<li><strong>Risk acceptance</strong>: Risk may often be accepted as residual risk.</li>
<li><strong>Exception time (SLA)</strong>: Indefinitely.</li>
</ul></td>
<td><ul>
<li>Gray is a low contrast color, which signifies not too important. It's also less catchy.</li>
<li>Green is not used as green means &quot;ok to do&quot;, which is not a level.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><span class="risk risk-unknown">UNKNOWN Risk</span></p><p><span class="risk-color-code">HTML Color code #ffffff</span></p></td>
<td><ul>
<li>Data collection is expected.</li>
<li>This level is expected to change to one of the other levels.</li>
</ul></td>
<td><ul>
<li>White represent the emptiness/lack of data.</li>
</ul>
<p>This is <strong>not a true level</strong>, it is used when there to represent that we do not have enough data to correctly assess the level (i.e. data collection work is required).</p>
<p>Note: communicating the risk of not knowing is challenging and prone to failure, in particular when once data has been gathered, the risk appears to in fact be low.</p>
<p>This concept is also known as <em>&quot;trust, but verify&quot;</em> - i.e. unknown does not distrust (by assign it a higher risk) the service, user, etc. by default.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

# Scoring

The following scores are intended to provide a grade for a particular objective. The scoes map back to the standard risk level definitions so that automatic risk mapping can be performed if necessary.
Scores are useful to grade security controls, hardware qualitues, implementation, etc. 
These scoring levels are used, for example, on the [https://observatory.mozilla.org](Mozilla Observatory).

NOTE: The use of **+** and **-** modifiers in front of scores (e.g. "A+") is allowed if necessary. These are added to represent going slightly above or below expectations.


<table>
<thead>
<tr class="header">
<th><p>Level</p></th>
<th><p>Expectations</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span class="risk score-green">A+, A, A-</span></p></td>
<td><p><em>Highest possible grade</em>.</p>
<ul>
<li>Support all features and controls.</li>
<li>All intentions of objective met.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk score-blue">B+, B, B-</span></p></td>
<td><ul>
<li>Supports most important features and controls.</li>
<li>Some outliers need attention.</li>
<li>Most intentions of objective met.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><span class="risk score-yellow">C+, C, C-</span></p>
<p><span class="risk score-yellow">D+, D, D-</span></p></td>
<td><p><em>Score may moderately contribute to risk</em>.</p>
<ul>
<li>Potential service blocker.</li>
<li>Needs attention and features need to be enabled/controls added.</li>
<li>Minimal to moderate intentions of objective met.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><span class="risk score-red">F</span></p></td>
<td><p><em>Lowest possible grade, score may greatly contribute to risk</em>.</p>
<ul>
<li>Zero to minimal intentions of objective met.</li>
<li>Immediate attention and action are required.</li>
<li>Score likely to block the service.</li>
</ul></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>
