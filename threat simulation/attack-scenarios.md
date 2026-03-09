---

## **Attack Scenarios**

The SOC Detection Lab includes several controlled attack scenarios designed to generate realistic security telemetry for detection testing and incident response practice.

These scenarios simulate common adversary techniques such as brute-force authentication attempts and command-and-control activity. Each attack is executed within an isolated lab network to ensure that no systems outside the environment are affected.

The goal of these simulations is to generate logs that can be collected by the Elastic Stack and analyzed using detection rules and investigation workflows.

---

## **Scenario 1 — SSH Brute Force Attack**

In this scenario, an attacker system repeatedly attempts to authenticate to a Linux server using incorrect credentials. This activity generates failed SSH login events within the Linux authentication logs.

These logs are collected by Elastic Agent and forwarded to the Elastic Stack where detection rules identify abnormal login behavior.

This scenario demonstrates how SOC analysts can detect password guessing attacks targeting SSH services.

---

## **Scenario 2 — RDP Brute Force Attack**

This scenario simulates an attacker attempting to gain access to a Windows server using Remote Desktop Protocol (RDP).

Multiple login attempts are performed against the system using automated password guessing tools. Failed login attempts generate Windows Security Event logs that are collected and analyzed by the Elastic platform.

Detection rules monitor these events to identify abnormal authentication patterns that indicate a brute-force attack.

---

## **Scenario 3 — Command and Control Activity**

This scenario simulates post-exploitation activity using a command-and-control framework.

A Mythic C2 server is deployed within the lab environment to simulate adversary infrastructure. When a simulated agent communicates with the server, telemetry is generated that can be analyzed by the monitoring platform.

This scenario demonstrates how SOC analysts detect suspicious endpoint behavior and potential command-and-control communication.

---

## **Purpose of Threat Simulation**

Threat simulation allows the lab environment to generate realistic security events without requiring external attack sources.

By intentionally creating malicious activity inside the environment, the lab demonstrates how detection rules, alerts, and incident response workflows function in a real SOC environment.
