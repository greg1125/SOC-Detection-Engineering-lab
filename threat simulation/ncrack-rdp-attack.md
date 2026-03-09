---

## **Ncrack RDP Attack Simulation**

This attack simulation demonstrates how automated password guessing attacks can target Remote Desktop Protocol (RDP) services on Windows systems.

The attack is performed using **Ncrack**, a network authentication cracking tool designed to test password security for remote access services.

Within the lab environment, the Kali Linux attacker machine launches a series of login attempts against a Windows server endpoint.

---

## **Attack Command**

The following command was used to simulate an RDP brute-force attack against the Windows endpoint.

**ncrack -vv --user <TARGET_USERNAME> -P password-list.txt rdp://<TARGET_WINDOWS_IP>**


---

## **Command Breakdown**

`ncrack`  
Network authentication cracking tool used to test password security of remote services.

`--user <TARGET_USERNAME>`  
Specifies the username being targeted during the attack.

`-P password-list.txt`  
Defines the password wordlist used for the brute-force attempt.

`rdp://<TARGET_WINDOWS_IP>`  
Indicates the RDP service running on the target Windows system.

`-vv`  
Enables verbose output so authentication attempts can be monitored in real time.

---

## **Attack Method**

The attacker system initiates repeated authentication attempts against the RDP service running on the Windows endpoint.

Each attempt uses credentials from a predefined password list. Because the credentials are incorrect, the Windows system logs failed login attempts.

These failed login events are captured in Windows Security Event logs and forwarded to the Elastic Stack through the Elastic Agent installed on the endpoint.

---

## **Generated Telemetry**

The attack generates several types of security telemetry including:

- Failed authentication events
- Source IP address of the attacking system
- Username being targeted
- Timestamp of each login attempt

The most important Windows log generated during this attack is:

**Event ID 4625 — Failed Logon Attempt**

These events provide the data needed for detection rules to identify abnormal login patterns.

---

## **Detection Outcome**

Once the failed login threshold is exceeded, the **RDP brute-force detection rule** triggers an alert within the Elastic Security interface.

The alert includes contextual information such as:

- Source IP address
- Target username
- Affected host
- Number of failed login attempts
- Timestamp of the activity

This allows analysts to quickly identify the attack and begin investigation procedures.

---

## **Purpose in the Lab**

This simulation demonstrates how SOC monitoring platforms detect automated password attacks targeting remote management services.

It also provides an opportunity to validate detection rules, investigate authentication logs, and test alerting workflows within a controlled lab environment.
