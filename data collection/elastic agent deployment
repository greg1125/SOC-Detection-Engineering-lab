---

## **Elastic Agent Deployment**

Elastic Agents were installed on all monitored endpoints in the lab environment to collect system telemetry and forward it to the Elastic Stack. These agents act as the primary data collectors, gathering logs related to authentication activity, process execution, and network connections.

Installing Elastic Agent allows the SOC monitoring platform to receive real-time telemetry from endpoints and provides the visibility necessary to detect suspicious activity.

---

## **Agent Installation**

Elastic Agents were installed on both Windows and Linux endpoints using the installation packages provided through the Fleet interface in Kibana.

During installation, each agent was configured to run as a system service so that it would start automatically and continuously collect telemetry from the host machine.

Once installed, the agent began collecting logs related to system activity, authentication attempts, and network communication.

---

## **Fleet Enrollment**

After installation, each Elastic Agent was enrolled into the Fleet management system using an enrollment token generated in Kibana.

Enrollment allows the agent to securely register with the Fleet Server and receive configuration policies that define what data should be collected.

Once successfully enrolled, the endpoint appears in the Fleet interface where its status, telemetry, and health can be monitored.

---

## **Agent Policies**

Agents are managed using policies that determine which integrations and log sources are enabled on each system.

In this lab, policies were configured to collect:

- Windows security events from the Windows endpoint
- Linux authentication logs from the Linux server
- System process activity
- Network connection events

These policies ensure that the Elastic platform receives the telemetry required to support detection rules and incident investigations.
