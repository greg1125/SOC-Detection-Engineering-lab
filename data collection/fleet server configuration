---

## **Fleet Server Configuration**

Fleet Server was deployed to centrally manage Elastic Agents across the SOC Detection Lab environment. It acts as the control plane for agent communication, policy distribution, and endpoint monitoring.

Fleet Server allows administrators to manage all agents from a single interface, ensuring consistent telemetry collection across monitored systems.

---

## **Fleet Server Setup**

Fleet Server was installed on a dedicated Ubuntu virtual machine and connected to the Elasticsearch and Kibana services running on the Elastic Stack server.

During setup, the server was configured to accept agent enrollments and distribute policies to connected endpoints.

Once operational, Fleet Server became the central communication hub between Elastic Agents and the Elastic monitoring platform.

---

## **Agent Communication**

Elastic Agents communicate with Fleet Server over a secure connection to retrieve configuration policies and report system telemetry.

This communication model allows agents to receive updates or configuration changes without requiring manual modification on each endpoint.

As a result, the lab environment can scale easily while maintaining centralized control over endpoint telemetry collection.

---

## **Endpoint Management**

Fleet provides visibility into all enrolled agents, including their health status, operating system, policy assignment, and data ingestion activity.

Through the Fleet interface in Kibana, it is possible to:

- Verify agent connectivity
- Deploy or modify policies
- Monitor agent health
- Troubleshoot telemetry collection

This centralized management model reflects how modern SOC teams maintain control over thousands of monitored endpoints.
