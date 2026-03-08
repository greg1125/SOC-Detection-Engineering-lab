<u>SOC Detection Engineering Lab – Elastic SIEM + Adversary Simulation</u>
<u>Project Overview</u>

    This project demonstrates the design and implementation of a simulated Security Operations Center (SOC) environment capable of detecting, analyzing, and responding to malicious activity within a segmented lab network. The environment replicates the operational workflow used by modern security teams by collecting endpoint telemetry, analyzing events through a centralized Security Information and Event Management (SIEM) platform, and escalating incidents through an automated ticketing system.

    The lab environment simulates both attacker behavior and defensive monitoring, allowing detection rules to be tested against realistic attack scenarios. Malicious activity is generated using an adversary simulation host and command-and-control infrastructure, while endpoint telemetry is collected through centralized logging agents deployed across monitored systems.

    The end result is a complete attack → detection → alert → investigation → ticket workflow, mirroring the security monitoring pipeline used in real-world SOC environments.

<u>Project Objectives</u>

    The primary goal of this project was to design and deploy a working SOC monitoring environment capable of detecting malicious behavior within a controlled network.

    Key objectives included:

    • Designing a segmented virtual SOC lab network
    • Deploying centralized log collection using Elastic SIEM
    • Simulating attacker behavior within the environment
    • Creating detection rules to identify malicious activity
    • Generating alerts based on detection logic
    • Automating incident ticket creation through osTicket

    By completing these objectives, the project demonstrates practical experience in security monitoring, detection engineering, and SOC incident response workflows.

<u>Lab Architecture</u>

    The environment is built using multiple virtual machines deployed within a local hypervisor. Each system represents a component typically found in enterprise security monitoring environments.

    The architecture is composed of several functional layers responsible for generating telemetry, collecting logs, analyzing events, and escalating incidents.

Attack Simulation Layer

    A dedicated adversary simulation host is used to generate malicious activity within the environment. This system performs controlled attack scenarios against monitored endpoints in order to produce realistic security telemetry.

    Examples of simulated attack activity include:

    • brute force authentication attempts
    • remote command execution
    • command and control beaconing

    These activities allow the monitoring infrastructure to detect and respond to behavior that resembles real adversary techniques.

Command and Control Infrastructure

    A command and control (C2) server is deployed within the lab environment to simulate the behavior of compromised endpoints communicating with attacker infrastructure.

    After a system is compromised, it establishes outbound communication with the C2 server, replicating the behavior of malware that periodically contacts attacker-controlled systems.

    This enables the monitoring system to detect behaviors such as:

    • suspicious outbound network connections
    • beaconing activity
    • unauthorized command execution

Endpoint Layer

    The monitored environment includes both Windows and Linux systems that represent enterprise endpoints within the network.

    These systems generate telemetry including:

    • authentication events
    • process creation activity
    • network connections
    • system logs

    Each endpoint runs a telemetry collection agent that forwards system activity to the centralized monitoring platform.

Telemetry Collection Layer

    Endpoint telemetry is collected using Elastic Agent, which acts as a unified data collection agent capable of gathering logs from multiple sources.

    Agents are centrally managed through Fleet Server, which provides centralized management for agent enrollment, configuration, and policy enforcement.

    Fleet enables administrators to:

    • enroll and manage monitoring agents
    • deploy configuration policies
    • monitor agent health
    • update data collection rules

    This architecture allows telemetry from multiple systems to be aggregated into a single analysis platform.

SIEM and Log Analysis Layer

    The core monitoring platform used in this project is the Elastic Stack, which functions as the Security Information and Event Management (SIEM) system.

    The stack consists of two primary components:

    Elasticsearch

    Elasticsearch stores and indexes all collected security telemetry, allowing large volumes of event data to be searched and analyzed efficiently.

    Kibana

    Kibana provides the visualization and analysis interface used to search logs, build dashboards, create detection rules, and investigate alerts.

    Together, these tools allow analysts to monitor system activity and identify suspicious behavior across the environment.

<u>Detection Engineering</u>

    Custom detection rules were created within the SIEM platform to identify specific adversary behaviors generated during attack simulations.

    These rules analyze event logs and trigger alerts when suspicious patterns are detected.

SSH Brute Force Detection

    This detection rule identifies repeated failed authentication attempts against a Linux server.

    If multiple login failures occur within a short time window from the same source IP address, the SIEM generates a detection alert indicating a potential brute force attack.

    Relevant log fields include:

    • username
    • source IP address
    • authentication result

RDP Brute Force Detection

    Windows authentication logs are monitored to detect repeated failed login attempts targeting privileged accounts.

    The detection logic analyzes Windows Security Event logs to identify patterns such as:

    • repeated Event ID 4625 login failures
    • login attempts targeting administrative accounts
    • authentication attempts originating from a single source IP

Command and Control Detection

    The lab environment also simulates compromised endpoint behavior through command and control communication.

    Detection rules monitor endpoint telemetry for suspicious outbound network activity and abnormal process behavior that may indicate remote command execution.

<u>Alerting and Incident Workflow</u>

    When a detection rule identifies suspicious behavior, the SIEM generates an alert containing detailed information about the event.

    Each alert includes:

    • affected host
    • source IP address
    • user account involved
    • detection rule name
    • event timestamp

    These alerts represent potential security incidents that require investigation.

<u>Automated Incident Ticketing</u>

    To simulate a real SOC incident response workflow, alerts generated by the SIEM are automatically forwarded to osTicket, an open-source ticketing system.

    When a detection rule triggers:

    1. The SIEM generates an alert.
    2. The alert triggers a webhook action.
    3. Alert data is forwarded to osTicket.
    4. A new incident ticket is created.

    This automation demonstrates how security alerts are converted into trackable incidents within SOC operations.

<u>Security Monitoring Dashboards</u>

    Custom dashboards were created within the SIEM interface to visualize security activity across the environment.

    These dashboards provide visibility into:

    • authentication failures
    • detection rule triggers
    • endpoint alerts
    • network activity

    Dashboards enable analysts to quickly identify suspicious patterns and monitor the health of the environment.

<u>Skills Demonstrated</u>

    This project demonstrates hands-on experience in several key cybersecurity disciplines:

    • Security Information and Event Management (SIEM) deployment
    • Detection rule engineering
    • Endpoint telemetry collection
    • Threat simulation and adversary emulation
    • Incident response workflows
    • Security automation

<u>Technologies Used</u>

    Elastic Stack (Elasticsearch, Kibana)
    Elastic Agent
    Fleet Server
    Mythic Command and Control Framework
    Kali Linux
    Windows Server
    Ubuntu Server
    osTicket
    VMware Workstation

<u>Future Improvements</u>

    Several enhancements could further expand the capabilities of this environment:

    • Active Directory attack simulation
    • lateral movement detection
    • honeypot deployment for threat intelligence collection
    • automated response actions (SOAR integration)

<u>Conclusion</u>

    This project demonstrates the full lifecycle of security monitoring within a SOC environment. By combining adversary simulation, centralized log analysis, detection engineering, and automated incident tracking, the lab replicates many of the workflows used by modern security operations teams.

    Through this implementation, the project showcases practical experience in building and operating a security monitoring environment capable of detecting, analyzing, and responding to malicious activity.
