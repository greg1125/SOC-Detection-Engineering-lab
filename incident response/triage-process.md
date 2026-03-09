# SOC Alert Triage Process

Alert triage is the process of evaluating security alerts to determine whether they represent legitimate threats or benign activity.

Because security monitoring platforms can generate large volumes of alerts, analysts must prioritize incidents based on risk and severity.

This document outlines the triage process used in the SOC Detection Lab.

---

# Initial Alert Review

When an alert appears in Elastic Security, analysts first review the alert summary information.

Important fields include:

```
kibana.alert.rule.name
kibana.alert.severity
kibana.alert.risk_score
host.name
source.ip
user.name
```

These fields provide the initial context required to begin the investigation.

---

# Triage Decision Tree

Analysts typically follow a decision-making workflow to classify alerts.

```
Alert Generated
      │
      ▼
Review Alert Metadata
      │
      ▼
Is Activity Suspicious?
      │
  ┌───┴───┐
  ▼       ▼
Yes       No
  │        │
Investigate   Close Alert
  │
  ▼
Confirm Incident
  │
  ▼
Escalate
```

This workflow ensures that analysts consistently evaluate alerts before taking action.

---

# Step 1 — Validate the Detection Rule

The first step in triage is confirming that the alert was triggered by a legitimate detection rule.

Example:

```
Rule: SSH-Brute-Force-Attempt
Severity: Medium
Risk Score: 47
```

Analysts must confirm that the rule correctly identified suspicious activity.

---

# Step 2 — Identify the Affected Host

Next, analysts determine which system generated the alert.

Example:

```
host.name: <TARGET_ENDPOINT>
```

This information helps determine whether the affected host is:

- a workstation
- a server
- a critical infrastructure component

The impact of the incident may vary depending on the system involved.

---

# Step 3 — Identify the Source of Activity

The source of the activity is determined using the `source.ip` field.

Example:

```
source.ip: <ATTACKER_IP>
```

Analysts should determine whether the source is:

- internal
- external
- known or unknown

Repeated suspicious activity from the same source may indicate an ongoing attack.

---

# Step 4 — Review Event Context

The next step is to review the surrounding event data.

Analysts may examine:

```
event.code
event.action
process.name
process.command_line
```

These fields provide insight into the nature of the activity.

---

# Step 5 — Determine Alert Priority

Alerts are prioritized based on severity and risk score.

Example severity levels:

| Severity | Priority |
|--------|--------|
| Low | Monitor |
| Medium | Investigate |
| High | Immediate response |
| Critical | Incident escalation |

In this lab environment:

- brute-force attacks generate **medium severity alerts**
- command-and-control detections generate **critical alerts**

---

# Step 6 — Escalation

If malicious activity is confirmed, the alert should be escalated according to the organization's incident response procedures.

Possible escalation actions include:

- opening an incident ticket
- isolating the affected endpoint
- blocking malicious IP addresses
- notifying the security team

---

# Integration With Ticketing

In this lab environment, confirmed alerts are automatically forwarded to the **osTicket ticketing system** through a webhook integration.

This ensures that security alerts are tracked through a structured incident response workflow.

---

# Importance of Triage

Effective alert triage allows security teams to:

- reduce alert fatigue
- prioritize critical threats
- respond to incidents faster
- improve overall security monitoring

The triage process demonstrated in this lab mirrors real-world SOC workflows used to manage large volumes of security alerts.
