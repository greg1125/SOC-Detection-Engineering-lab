---

## **Virtual Machine Specifications**

The SOC Detection Lab is composed of several virtual machines that simulate monitoring infrastructure, production endpoints, attacker systems, and incident response tooling. Each system was allocated resources based on its operational role while ensuring the environment could run reliably on a single host system.

The SOC lab environment was deployed using multiple virtual machines running inside VMware Workstation.

![SOC Lab Virtual Machines](../screenshots/infrastructure/vm-lab-environment.png)
---

## **Elastic Stack Server**

Role: Central SIEM platform responsible for log ingestion, indexing, search, and visualization.

OS: Ubuntu Server  
CPU: 4 vCPU  
Memory: 8 GB RAM  
Purpose: Runs Elasticsearch and Kibana to store and analyze security telemetry collected from endpoints.

---

## **Fleet Server**

![VM Resources](vm-resources(fleet).png)

as an example of the resources used to spin up the servers, fleet allocation is listed.

Role: Central management server for Elastic Agents.

OS: Ubuntu Server  
CPU: 2 vCPU  
Memory: 4 GB RAM  
Purpose: Manages agent enrollment, policy distribution, and telemetry forwarding from monitored systems to Elasticsearch.

---

## **Windows Server Endpoint**

Role: Monitored Windows system used to generate authentication and system logs.

OS: Windows Server  
CPU: 2 vCPU  
Memory: 4 GB RAM  
Purpose: Target system for RDP brute-force simulations and Windows event log collection.

---

## **Linux Server Endpoint**

Role: Monitored Linux system used for SSH logging and Linux telemetry.

OS: Ubuntu Server  
CPU: 2 vCPU  
Memory: 2 GB RAM  
Purpose: Generates SSH authentication logs used for brute-force detection scenarios.

---

## **Kali Linux Attack System**

Role: Red team simulation host used to launch attack scenarios.

OS: Kali Linux  
CPU: 2 vCPU  
Memory: 2 GB RAM  
Purpose: Executes attack tools such as Ncrack to simulate brute-force attempts against monitored endpoints.

---

## **Mythic Command and Control Server**

Role: Adversary command-and-control infrastructure used for post-exploitation simulation.

OS: Ubuntu Server  
CPU: 2 vCPU  
Memory: 4 GB RAM  
Purpose: Hosts the Mythic C2 framework to simulate malicious beaconing and command execution activity.

---

## **osTicket Server**

Role: Incident response ticketing system used for alert tracking and case management.

OS: Windows Server  
CPU: 2 vCPU  
Memory: 2 GB RAM  
Purpose: Receives alerts from the Elastic detection pipeline and converts them into incident response tickets.
