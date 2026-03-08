# SOC-Detection-Engineering-lab

**Project Overview**

This project demonstrates the design and implementation of a simulated Security Operations Center (SOC) environment capable of detecting, analyzing, and responding to malicious activity within a controlled lab network. The goal of the lab is to replicate a simplified real-world security monitoring pipeline where endpoint activity is collected, analyzed by a SIEM platform, and escalated through an incident response workflow.

The environment simulates both attacker behavior and defensive monitoring, allowing detection rules to be developed and validated against realistic attack scenarios. Adversary activity is generated using a dedicated attack host and command-and-control infrastructure, while endpoint telemetry is collected by a centralized logging system. Detection rules in the SIEM identify suspicious behavior and automatically generate alerts that feed into an incident tracking system.

The result is a full attack → detection → alert → investigation → ticket workflow, which mirrors the operational processes used by many modern SOC teams.

****Objectives****

The primary objectives of this project were:

• Design and deploy a segmented SOC lab network
• Implement centralized log collection using a SIEM platform
• Simulate adversary techniques within the lab environment
• Develop detection rules capable of identifying malicious behavior
• Generate alerts and integrate them with an incident ticketing system
• Document investigation workflows and incident response procedures

By achieving these objectives, the project demonstrates the core technical skills required in SOC analysis, detection engineering, and security monitoring.

**High-Level Architecture**

The lab environment is built using virtual machines within a local hypervisor. Each component represents a typical system found in enterprise security environments.

The infrastructure consists of several key components:

Attacker Simulation Layer

A dedicated attack workstation is used to simulate adversary behavior. This system performs controlled attack scenarios against the lab endpoints to generate security telemetry.

These activities include:

• Brute force authentication attempts
• Command and control communication
• Endpoint compromise simulations

The purpose of this layer is to generate realistic security events that the monitoring stack must detect.

**Command and Control Infrastructure**

A command and control (C2) server is deployed within the lab environment to simulate post-compromise attacker behavior. Compromised endpoints establish beacon communication with this server, mimicking the behavior of malware communicating with an attacker-controlled system.

This enables the detection of:

• suspicious outbound network connections
• beaconing behavior
• unauthorized process execution
• abnormal endpoint activity

This layer introduces realistic adversary behaviors beyond simple authentication attacks.

**Endpoint Layer**

The lab includes both Windows and Linux servers that represent monitored endpoints within an enterprise network.

These systems generate telemetry such as:

• authentication attempts
• process execution events
• network connections
• system log activity

Endpoint monitoring agents are installed on these systems to collect and forward log data to the centralized monitoring platform.

**Telemetry Collection Layer**

Endpoint telemetry is collected using Elastic Agent, which operates as a unified data collection agent. The agent gathers system activity from each monitored host and forwards it to the central logging infrastructure.

The agents are centrally managed through Fleet Server, which provides:

• centralized policy management
• agent enrollment
• configuration distribution
• health monitoring

This architecture allows security telemetry from multiple endpoints to be aggregated into a single analysis platform.

**SIEM and Analysis Layer**

The core of the monitoring environment is the Elastic Stack, which functions as the Security Information and Event Management (SIEM) platform.

The stack consists of:

Elasticsearch
Stores and indexes all collected log data.

Kibana
Provides the visualization interface used to search logs, create dashboards, and build detection rules.

Within this platform, collected telemetry is analyzed to identify suspicious behavior using custom detection rules.

Detection Engineering

Detection rules were developed to identify several simulated attack techniques. These rules analyze log events and trigger alerts when suspicious patterns are observed.

Examples of detection logic implemented in this lab include:
**
SSH Brute Force Detection**

Multiple failed authentication attempts against a Linux server are monitored. When the number of failed login attempts exceeds a threshold within a short time window, the SIEM generates a detection alert.

This detection relies on Linux authentication logs and analyzes fields such as:

• username
• source IP address
• authentication result

**RDP Brute Force Detection
**
Windows authentication events are monitored to identify repeated failed login attempts against administrative accounts.

This detection analyzes Windows Security Event logs and identifies patterns such as:

• repeated Event ID 4625 failures
• login attempts targeting privileged accounts
• authentication attempts originating from a single source IP

**Command and Control Detection**

The lab also simulates endpoint compromise through C2 beacon activity. Detection rules monitor network and process events that may indicate communication with a command and control server.

This includes identifying:

• abnormal outbound network connections
• suspicious process behavior
• endpoint activity associated with remote command execution

**Alerting and Incident Workflow**

When a detection rule identifies suspicious behavior, the SIEM generates an alert containing detailed information about the event.

Each alert includes:

• the affected host
• source IP address
• user account involved
• detection rule name
• event timestamp
• associated log data

These alerts represent potential security incidents that require analyst investigation.

**Automated Ticketing Integration**

To simulate a real SOC incident response process, alerts generated by the SIEM are automatically forwarded to an incident tracking system.

This project integrates the monitoring platform with osTicket, an open-source ticketing system commonly used for IT service management.

When a detection rule triggers:

The SIEM generates an alert.

The alert triggers an automated action.

The alert information is sent to the ticketing system via webhook.

A new incident ticket is created for analyst investigation.

This workflow simulates how modern SOC teams convert detection alerts into trackable security incidents.

Security Monitoring Dashboards

Custom dashboards were created in the SIEM interface to visualize security activity within the environment.

These dashboards provide visibility into:

• authentication failures
• endpoint alerts
• network activity
• detection rule triggers
• host security events

Dashboards allow analysts to quickly identify unusual activity patterns and monitor the health of the environment.

Incident Investigation Workflow

When alerts are generated, analysts can investigate them through the SIEM interface by examining the associated log events.

Typical investigation steps include:

Reviewing the detection alert details

Identifying the affected host and user account

Examining related authentication or network logs

Determining whether activity represents malicious behavior

Escalating the incident through the ticketing system

This process simulates the typical triage workflow followed by SOC analysts.

Skills Demonstrated

This project demonstrates hands-on experience with several core cybersecurity disciplines:

Security Monitoring
Deploying a SIEM platform and collecting endpoint telemetry.

Detection Engineering
Creating detection rules capable of identifying adversary behavior.

Threat Simulation
Generating attack activity to test monitoring capabilities.

Incident Response Workflow
Escalating alerts into trackable security incidents.

Security Infrastructure Design
Designing and deploying a segmented SOC lab architecture.

Technologies Used

Elastic Stack (Elasticsearch, Kibana)
Elastic Agent
Fleet Server
Mythic Command and Control Framework
Kali Linux
Windows Server
Ubuntu Server
osTicket
VMware Workstation

Future Improvements

Several additional enhancements could expand the capabilities of this environment:

• Active Directory attack simulation
• lateral movement detection
• integration of endpoint detection and response tools
• automated response actions (SOAR workflows)
• honeypot deployment for threat intelligence collection

These improvements would further replicate enterprise SOC capabilities and expand the detection coverage of the lab.

Conclusion

This project demonstrates the complete lifecycle of security monitoring within a SOC environment. By combining adversary simulation with centralized log analysis and automated incident tracking, the lab replicates many of the workflows used by real-world security teams.

Through this implementation, the project showcases practical experience in building and operating a security monitoring environment capable of detecting, analyzing, and responding to suspicious activity.
