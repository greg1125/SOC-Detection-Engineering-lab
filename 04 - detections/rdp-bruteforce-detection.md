---

## **RDP Brute Force Detection**

This detection rule identifies repeated failed Remote Desktop Protocol (RDP) login attempts against a Windows server. RDP brute-force attacks occur when an attacker repeatedly attempts to guess valid credentials to gain remote access to a Windows system.

In the lab environment, this attack is simulated using a Kali Linux system running password guessing tools against the Windows Server endpoint.

---

## **Detection Logic**

The detection rule monitors Windows Security Event Logs for repeated failed login attempts associated with Remote Desktop authentication.

The rule triggers when multiple authentication failures occur within a defined time window, indicating that an automated password guessing attack may be underway.

This method helps distinguish normal login mistakes from malicious brute-force activity.

---

## **Relevant Log Source**

The rule relies on Windows Security Event Logs collected from the monitored Windows Server endpoint.

Important authentication events such as failed logins and account authentication attempts are forwarded to the Elastic Stack by the Elastic Agent installed on the system.

These logs provide the telemetry needed to detect abnormal authentication patterns.

---

## **Alert Context**

When the detection rule triggers, the alert includes investigation details such as:

- Source IP address performing the login attempts
- Username being targeted
- Host receiving the authentication attempts
- Event timestamps and frequency

This context allows analysts to quickly understand the scope and origin of the attack.

---

## **Purpose in the Lab**

This detection demonstrates how Windows authentication telemetry can be used to identify brute-force attacks targeting remote access services.

It also highlights the importance of monitoring authentication events when defending systems that expose remote management protocols such as RDP.
