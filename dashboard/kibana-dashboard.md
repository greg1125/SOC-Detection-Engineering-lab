# Kibana SOC Monitoring Dashboard

The SOC Detection Lab includes several custom Kibana dashboards designed to provide centralized visibility into authentication activity, endpoint telemetry, and security events occurring across monitored systems.

Dashboards are a critical component of Security Operations Centers because they allow analysts to quickly observe patterns in large volumes of security telemetry without manually querying logs.

The dashboards created for this project aggregate authentication logs, endpoint telemetry, and security alerts into a single monitoring interface.

---

# Dashboard Overview

The dashboard environment contains multiple visualizations designed to monitor different aspects of system activity:

Authentication Monitoring
Endpoint Process Monitoring
Network Connection Activity
Security Control Events

These visualizations provide analysts with immediate visibility into abnormal behavior that may indicate malicious activity.

---

# SOC Monitoring Dashboard

![SOC Monitoring Dashboard](../screenshots/soc-monitoring-dashboard.png)

---

# Authentication Monitoring Panels

The first set of dashboard panels focuses on authentication activity across both Windows and Linux endpoints.

Authentication logs are extremely valuable for detecting unauthorized access attempts, credential abuse, and brute-force attacks.

The dashboard includes four panels that monitor login activity.

---

## RDP Failed Authentications

This panel displays failed Remote Desktop Protocol (RDP) authentication attempts against the monitored Windows endpoint.

The table displays:

- targeted username
- source IP address initiating the login attempt
- number of failed authentication events

Relevant fields include:

```
user.name
source.ip
event.code
```

In Windows environments, failed login attempts generate **Event ID 4625**.

A large number of failed attempts from a single IP address strongly indicates a brute-force attack attempting to guess valid credentials.

During the attack simulation phase of the lab, the Kali attacker system generated repeated failed login attempts using Ncrack. These repeated attempts produced the spike visible in this panel.

---

## RDP Successful Authentications

This panel displays successful Remote Desktop login events.

Successful logins correspond to **Windows Event ID 4624**, which indicates that a user has successfully authenticated to the system.

This panel allows analysts to identify:

- which accounts successfully logged in
- where the login originated from
- whether successful authentication followed repeated failures

If a successful login occurs immediately after multiple failed attempts, this may indicate that an attacker successfully guessed the password.

---

## SSH Failed Authentications

This panel displays failed SSH login attempts against the monitored Linux endpoint.

SSH authentication failures are recorded in Linux authentication logs and forwarded to the Elastic Stack through the Elastic Agent.

Displayed fields include:

```
user.name
source.ip
event.dataset
```

A high number of failed attempts originating from a single IP address strongly suggests automated credential guessing.

During the attack simulation phase, the Kali attacker machine used Ncrack to perform repeated SSH authentication attempts, which generated the high event count visible in this panel.

---

## SSH Successful Authentications

This panel displays successful SSH login events.

Monitoring successful SSH logins helps analysts detect unusual access patterns such as:

- logins from unfamiliar IP addresses
- access outside normal working hours
- successful login following repeated failures

Unexpected successful logins may indicate compromised credentials.

---

# Endpoint Activity Dashboard

A second dashboard focuses on endpoint telemetry collected from monitored systems.

This dashboard highlights process execution activity, network connections initiated by processes, and security control events.

These visualizations provide deeper insight into system behavior beyond authentication activity.

---

# Endpoint Activity Dashboard

![Endpoint Activity Dashboard](../screenshots/endpoint-activity-dashboard.png)

---

# Process Creation Monitoring

## Process Created (PowerShell, CMD, Rundll32)

This panel displays process creation events captured from the Windows endpoint.

The visualization includes important fields such as:

```
hostname
user
parent process
process image
parent command line
```

Process creation events allow analysts to track program execution across monitored systems.

Special attention is given to processes commonly abused by attackers, including:

- PowerShell
- Command Prompt
- Rundll32

These utilities are often used in **Living Off the Land (LOLBins)** techniques, where attackers abuse legitimate system tools to execute malicious commands.

Monitoring process creation helps detect suspicious behavior such as:

- unexpected PowerShell execution
- suspicious parent-child process relationships
- unusual command-line arguments

---

# Network Connection Activity

## Process Initiated Network Connections

This panel displays network connections initiated by processes on the endpoint.

Displayed fields include:

```
process image
source IP
destination IP
destination port
connection count
```

Monitoring network activity at the process level allows analysts to detect potential command-and-control communication.

Suspicious indicators may include:

- processes initiating connections to unknown external IP addresses
- unusual outbound network traffic
- unexpected network activity from system processes

For example, malware often communicates with remote command-and-control servers using outbound HTTP or HTTPS connections.

Process-level network telemetry provides critical insight into how applications interact with the network.

---

# Security Control Monitoring

## Microsoft Defender Disabled Events

This panel monitors events indicating that Microsoft Defender Antivirus was disabled.

The visualization displays:

```
host.hostname
security product name
event.code
```

Event code **5001** indicates that Microsoft Defender Antivirus was disabled.

Security tools being disabled may indicate:

- administrative configuration changes
- malicious attempts to bypass endpoint protection
- attacker activity attempting to evade detection

Because disabling endpoint protection is a common attacker tactic, these events should always be investigated.

---

# Why These Dashboards Matter

Dashboards allow SOC analysts to quickly identify suspicious activity without manually querying raw log data.

By visualizing authentication events, process activity, and network behavior in one interface, analysts gain immediate visibility into potential threats.

These dashboards enable analysts to detect:

- brute-force authentication attacks
- suspicious process execution
- unusual network connections
- disabled security controls

Combining these data sources provides a comprehensive view of system activity and significantly improves threat detection capabilities.

---

# Analyst Workflow Using Dashboards

SOC analysts typically use dashboards as an initial monitoring tool before performing deeper investigations.

A common workflow includes:

1. Monitor dashboard activity
2. Identify abnormal spikes or suspicious patterns
3. Investigate relevant events
4. pivot into detailed log searches
5. escalate confirmed incidents

This workflow mirrors how real Security Operations Centers monitor enterprise environments.

---

# Lab Environment Considerations

Because this SOC environment operates within a controlled internal network, the majority of events displayed in the dashboards originate from simulated attack scenarios.

In production environments, dashboards would also display telemetry generated by:

- internet-facing attacks
- vulnerability scans
- malware detections
- user authentication across enterprise systems

Despite the smaller dataset, the dashboards demonstrate how security teams use centralized monitoring platforms to observe system activity and detect potential threats.

---
