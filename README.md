# **SOC Detection Engineering Lab – Elastic SIEM + Adversary Simulation**

---

## **Project Overview**

This project demonstrates the design and implementation of a simulated **Security Operations Center (SOC)** environment capable of detecting, analyzing, and responding to malicious activity within a segmented lab network.

The lab simulates both attacker behavior and defensive monitoring, allowing detection rules to be tested against realistic attack scenarios. Malicious activity is generated using an adversary simulation host and command-and-control infrastructure, while endpoint telemetry is collected through centralized logging agents deployed across monitored systems.

The end result is a complete **attack → detection → alert → investigation → ticket** workflow, mirroring the security monitoring pipeline used in real-world SOC environments.

---

## **Project Objectives**

The primary goal of this project was to design and deploy a working SOC monitoring environment capable of detecting malicious behavior within a controlled network.

Key objectives included:

- Designing a segmented virtual SOC lab network
- Deploying centralized log collection using Elastic SIEM
- Simulating attacker behavior within the environment
- Creating detection rules to identify malicious activity
- Generating alerts based on detection logic
- Automating incident ticket creation through osTicket

By completing these objectives, the project demonstrates practical experience in security monitoring, detection engineering, and SOC incident response workflows.

---

## **Lab Architecture**

The environment is built using multiple virtual machines deployed within a local hypervisor. Each system represents a component typically found in enterprise security monitoring environments.

The architecture is composed of several functional layers responsible for generating telemetry, collecting logs, analyzing events, and escalating incidents.

### **Attack Simulation Layer**

A dedicated adversary simulation host is used to generate malicious activity within the environment. This system performs controlled attack scenarios against monitored endpoints in order to produce realistic security telemetry.

Examples of simulated attack activity include:

- Brute force authentication attempts
- Remote command execution
- Command and control beaconing

These activities allow the monitoring infrastructure to detect and respond to behavior that resembles real adversary techniques.

### **Command and Control Infrastructure**

A command and control (C2) server is deployed within the lab environment to simulate the behavior of compromised endpoints communicating with attacker infrastructure.

After compromise, the endpoint establishes outbound communication with the C2 server, mimicking the behavior of malware communicating with attacker-controlled infrastructure.

This enables the monitoring system to detect behaviors such as:

- Suspicious outbound network connections
- Beaconing activity
- Unauthorized command execution

### **Endpoint Layer**

The monitored environment includes both **Windows and Linux systems** that represent enterprise endpoints within the network.

These systems generate telemetry including:

- Authentication events
- Process creation activity
- Network connections
- System logs

Each endpoint runs a telemetry collection agent that forwards system activity to the centralized monitoring platform.

### **Telemetry Collection Layer**

Endpoint telemetry is collected using **Elastic Agent**, which acts as a unified data collection agent capable of gathering logs from multiple sources.

Agents are centrally managed through **Fleet Server**, which provides centralized management for agent enrollment, configuration, and policy enforcement.

Fleet enables administrators to:

- Enroll monitoring agents
- Deploy configuration policies
- Monitor agent health
- Update data collection rules

### **SIEM and Log Analysis Layer**

The central monitoring platform used in this project is the **Elastic Stack**, which functions as the Security Information and Event Management (SIEM) system.

The stack consists of two primary components:

**Elasticsearch**  
Stores and indexes all collected security telemetry, allowing large volumes of event data to be searched and analyzed efficiently.

**Kibana**  
Provides the visualization and analysis interface used to search logs, build dashboards, create detection rules, and investigate alerts.

---

## **Detection Engineering**

Custom detection rules were created within the SIEM platform to identify adversary behavior generated during attack simulations.

### **SSH Brute Force Detection**

This detection identifies repeated failed authentication attempts against a Linux server.

If multiple login failures occur within a short time window from the same source IP, the SIEM generates an alert indicating a potential brute force attack.

Relevant fields analyzed include:

- Username
- Source IP address
- Authentication result

### **RDP Brute Force Detection**

Windows authentication logs are monitored to detect repeated failed login attempts targeting privileged accounts.

The detection logic analyzes Windows Security Event logs to identify patterns such as:

- Repeated Event ID 4625 login failures
- Login attempts targeting administrative accounts
- Authentication attempts originating from a single source IP

### **Command and Control Detection**

The lab environment also simulates compromised endpoint behavior through command and control communication.

Detection rules monitor endpoint telemetry for suspicious outbound network activity and abnormal process behavior that may indicate remote command execution.

---

## **Alerting and Incident Workflow**

When a detection rule identifies suspicious behavior, the SIEM generates an alert containing detailed information about the event.

Each alert may include:

- Affected host
- Source IP address
- User account involved
- Detection rule name
- Event timestamp

These alerts represent potential security incidents that require investigation.

---

## **Automated Incident Ticketing**

To simulate a real SOC workflow, alerts generated by the SIEM are automatically forwarded to **osTicket**, an open-source incident tracking system.

When a detection rule triggers:

1. The SIEM generates an alert
2. The alert triggers a webhook action
3. Alert data is forwarded to osTicket
4. A new incident ticket is created

This demonstrates how alerts become trackable incidents within SOC operations.

---

## **Security Monitoring Dashboards**

Custom dashboards were created within the SIEM interface to visualize security activity across the environment.

These dashboards provide visibility into:

- Authentication failures
- Detection rule triggers
- Endpoint alerts
- Network activity

Dashboards help analysts quickly identify suspicious patterns and monitor the health of the environment.

---

## **Skills Demonstrated**

This project demonstrates hands-on experience in:

- SIEM deployment and configuration
- Detection rule engineering
- Endpoint telemetry collection
- Threat simulation
- SOC incident response workflows
- Security automation

---

## **Technologies Used**

- Elastic Stack (Elasticsearch, Kibana)
- Elastic Agent
- Fleet Server
- Mythic C2 Framework
- Kali Linux
- Windows Server
- Ubuntu Server
- osTicket
- VMware Workstation

---

## **Future Improvements**

Planned enhancements for this environment include:

- Active Directory attack simulations
- Lateral movement detection
- Honeypot integration
- SOAR automation workflows

---

## **Conclusion**

This project demonstrates the full lifecycle of security monitoring within a SOC environment. By combining adversary simulation, centralized log analysis, detection engineering, and automated incident tracking, the lab replicates many of the workflows used by modern security operations teams.

Through this implementation, the project showcases practical experience in building and operating a security monitoring environment capable of detecting, analyzing, and responding to malicious activity.
