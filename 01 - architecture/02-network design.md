---

## **Network Design**

The SOC Detection Lab network is designed to simulate a realistic enterprise security monitoring environment while remaining fully contained within a private virtualization infrastructure. All systems run as virtual machines on a local hypervisor and communicate through isolated virtual networks. This architecture allows attacker activity, endpoint behavior, and security monitoring to occur in a controlled environment without exposing any systems directly to the public internet.

The network is intentionally segmented into multiple layers that represent different operational zones commonly found in real enterprise environments. These layers separate monitoring infrastructure, production endpoints, and attacker systems while still allowing controlled communication between them. This segmentation enables the lab to simulate lateral movement, brute-force attacks, and command-and-control traffic while maintaining clear boundaries between infrastructure components.

By designing the network in this way, the lab replicates the flow of telemetry from endpoints to monitoring systems, allowing security alerts to be generated, investigated, and escalated through an incident response workflow.

---

## **Virtual Network Segmentation**

The lab network is divided into multiple virtual network segments using VMware virtual switches (VMnets). Each network segment serves a specific role in the architecture and helps replicate the separation of systems typically found in enterprise environments.

The main network segments include a monitoring network, an internal endpoint network, an attacker simulation network, and a NAT network used for controlled internet access. Each segment isolates specific systems while still allowing security telemetry to reach the monitoring infrastructure.

This segmentation is important because it allows attacks to occur internally between systems without exposing the lab to external threats. It also helps demonstrate how different parts of an infrastructure interact with centralized security monitoring platforms.

---

## **VMnet1 – Host-Only Monitoring Network**

VMnet1 is configured as a **host-only network**, meaning that communication occurs only between the host machine and the virtual machines connected to that network. This network segment is primarily used for management and monitoring infrastructure within the lab environment.

The Elastic Stack server and Fleet Server communicate across this network to receive logs from monitored endpoints. Because the network is isolated from the outside world, it ensures that sensitive monitoring infrastructure remains protected while still allowing the host system to access services such as Kibana dashboards and Elastic management interfaces.

Using a host-only network for monitoring infrastructure mirrors real-world security architecture where logging and monitoring systems are placed on protected management networks that are not directly accessible from external environments.

---

## **VMnet2 – Internal Endpoint Network**

VMnet2 represents the **internal production network** where monitored endpoints reside. Systems connected to this network include the Windows Server endpoint and the Linux server endpoint, both of which generate security telemetry that is collected by Elastic Agents.

This network segment simulates the internal systems that a Security Operations Center would normally monitor in a real organization. Authentication attempts, process execution events, and network activity occurring on these machines are forwarded to the Elastic Stack for analysis.

Because the endpoints share this network, attacker activity such as password guessing and unauthorized access attempts can be simulated against them. These events generate logs that allow detection rules to trigger alerts within the monitoring platform.

---

## **VMnet3 – Attack Simulation Network**

VMnet3 is used as the **attack simulation network**, where adversary infrastructure is deployed. Systems on this network include the Kali Linux machine used to perform attack simulations and the Mythic command-and-control server used to simulate post-exploitation activity.

This network segment allows the attacker systems to interact with monitored endpoints in a controlled manner. Activities such as SSH brute-force attempts, RDP password guessing, and command-and-control communications originate from this network.

By separating attacker systems onto their own network segment, the lab architecture clearly distinguishes malicious traffic sources while still allowing attacks to reach targeted endpoints for detection testing.

---

## **VMnet8 – NAT Internet Access Network**

VMnet8 is configured as a **NAT network**, which provides virtual machines with outbound internet access while preventing external systems from directly reaching the lab environment.

This network is primarily used for tasks such as downloading software packages, installing updates, and retrieving dependencies required for tools like Elastic Stack, Mythic, and operating system updates.

Because the NAT network only allows outbound connectivity, it reduces the risk of exposing lab systems to the public internet while still allowing the environment to function normally during installation and maintenance operations.

---

## **Traffic Flow Through the Architecture**

Security telemetry flows through the lab environment in a structured pipeline. Endpoint systems generate authentication logs, process activity, and network events that are collected by Elastic Agents installed on those machines.

These agents forward logs to the Fleet Server and Elasticsearch infrastructure over the monitoring network. The logs are indexed and analyzed by Elastic Security, where detection rules identify suspicious behavior such as brute-force login attempts or command-and-control activity.

When a detection rule triggers, an alert is generated within Kibana. These alerts can then be investigated by reviewing the associated logs, host information, and event timelines, simulating the investigation workflow used in a real Security Operations Center.

---

## **Why This Network Architecture Matters**

This segmented architecture demonstrates several core concepts used in real-world security environments. It shows how monitoring infrastructure can be isolated from operational systems, how endpoints generate security telemetry, and how attacker behavior can be simulated safely within a controlled network.

By recreating these relationships inside a home lab environment, the project provides practical experience with detection engineering, log analysis, and incident response workflows. This allows the lab to serve not only as a learning platform but also as a portfolio demonstration of SOC detection capabilities.
