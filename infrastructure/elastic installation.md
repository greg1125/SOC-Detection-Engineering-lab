---

## **Elastic Installation**

The Elastic Stack was installed as the core monitoring platform for the SOC Detection Lab. It serves as the central location where logs are collected, indexed, visualized, and analyzed for suspicious behavior.

The installation process involved setting up the main Elastic components required for security monitoring, including Elasticsearch for data storage and search, Kibana for dashboards and investigations, Fleet for centralized agent management, and Elastic Agent for endpoint telemetry collection.

Documenting the installation process is important because it shows how the monitoring environment was built from the ground up and how each component contributes to the overall SOC workflow.

---

## **Installing Elasticsearch**

Elasticsearch was installed first because it functions as the backend data store for the entire monitoring platform. It receives logs from agents, stores them in indices, and makes them searchable for dashboards, detections, and investigations.

This component is critical because every alert, event, and dashboard in the environment depends on Elasticsearch being operational. During setup, system resources, service status, and connectivity were validated to ensure that the node could reliably process incoming telemetry.

Installing Elasticsearch established the foundation of the lab’s logging pipeline and made it possible to build the rest of the monitoring stack on top of it.

---

## **Installing Kibana**

Kibana was installed next as the primary interface used to interact with the Elastic environment. It provides dashboards, alert views, detection rule management, log exploration, and investigation capabilities.

Through Kibana, the lab operator can review incoming events, create and tune detection rules, inspect alerts, and analyze activity across endpoints. It is effectively the main SOC analyst workspace within the project.

Once Kibana was connected to Elasticsearch and confirmed operational, it became possible to begin building the actual detection and monitoring workflow that powers the rest of the lab.

---

## **Setting Up Fleet**

Fleet was configured to centrally manage Elastic Agents across the lab environment. Rather than configuring each agent independently, Fleet provides a structured way to deploy policies, manage integrations, and monitor agent health from a single interface.

This is an important part of the architecture because it mirrors how modern security teams manage endpoint telemetry collection at scale. In the lab, Fleet allows Windows and Linux endpoints to be enrolled into the Elastic environment with consistent configurations.

By setting up Fleet, the project demonstrates not only how logs are collected, but also how centralized endpoint management improves efficiency and visibility in a SOC environment.

---

## **Adding Elastic Agents**

Elastic Agents were installed on the monitored endpoints to collect system telemetry and forward it to the Elastic platform. These agents are responsible for capturing logs related to authentication events, process execution, network activity, and other security-relevant behavior.

Each agent was enrolled into Fleet using the appropriate enrollment configuration so that it could begin forwarding data under a managed policy. Once connected, the agents made it possible to observe real endpoint behavior inside Kibana and validate that detections were working as expected.

Adding Elastic Agents transformed the environment from a static infrastructure build into an active security monitoring lab capable of generating meaningful alerts and investigations.

---

## **Security Monitoring Outcome**

Once Elasticsearch, Kibana, Fleet, and Elastic Agents were fully configured, the lab had a complete telemetry pipeline in place. Endpoint events could now flow from Windows and Linux systems into the Elastic platform, where they could be visualized, searched, and analyzed.

This made it possible to begin testing threat simulations such as SSH brute-force attempts, RDP login attacks, and Mythic-related command-and-control activity. The monitoring stack was no longer just installed—it was functioning as an operational SOC platform capable of supporting detection engineering and incident response workflows.

This stage of the project is significant because it marks the point where infrastructure setup transitions into active defensive operations.

---

## **Why This Installation Matters**

The Elastic installation process demonstrates practical experience with deploying a modern SIEM and security monitoring platform in a lab environment. It shows an understanding of how different Elastic components work together to ingest, manage, and analyze endpoint telemetry.

From a portfolio perspective, this section proves that the environment was not merely theoretical. It shows that the monitoring stack was actually built, configured, and used to support realistic detection scenarios.

This makes the project stronger because it highlights both infrastructure implementation and the operational use of that infrastructure within a SOC-focused workflow.
