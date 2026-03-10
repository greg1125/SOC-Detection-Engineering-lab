---

# **Ncrack RDP Brute Force Simulation**

This simulation demonstrates how automated password guessing attacks can target Remote Desktop Protocol (RDP) services on Windows systems.

The attack is performed using **Ncrack**, a network authentication cracking tool designed to test password security for remote access services.

Within the SOC Detection Lab, a Kali Linux attacker machine repeatedly attempts to authenticate to a Windows endpoint using invalid credentials. These failed authentication attempts generate Windows Security logs that are collected by the Elastic Agent and forwarded to Elasticsearch.

The objective of this simulation is to generate authentication telemetry that can be detected by threshold-based brute-force detection rules within Elastic Security.

![RDP Brute Force Simulation](../screenshots/threat-simulation/rdp-bruteforce-attack.png)
---

## **Step 1 — Verify the Target Service**

Before launching the attack, the attacker verifies that the RDP service is accessible on the Windows endpoint.

```bash
nmap -p 3389 <TARGET_WINDOWS_IP>
```

This scan checks whether **TCP port 3389**, the default port used by RDP, is open.

Expected result:

- Port 3389 reported as **open**
- Service identified as **ms-wbt-server**

This confirms that the system is running an RDP service that can accept authentication attempts.

---

## **Step 2 — Prepare the Password Wordlist**

A password list is required for the brute-force attack. This file contains candidate passwords that Ncrack will attempt during authentication.

Example password list:

```
password
admin
welcome
letmein
123456
password123
```

The wordlist is saved locally on the attacker system as:

```
password-list.txt
```

---

## **Step 3 — Launch the RDP Brute Force Attack**

The brute-force attack is executed using the following Ncrack command.

```bash
ncrack -vv --user <TARGET_USERNAME> -P password-list.txt rdp://<TARGET_WINDOWS_IP>
```

This command instructs Ncrack to repeatedly attempt authentication against the RDP service using passwords from the wordlist.

---

## **Command Breakdown**

`ncrack`  
Network authentication cracking tool used to test password security of remote services.

`--user <TARGET_USERNAME>`  
Specifies the username targeted during authentication attempts.

`-P password-list.txt`  
Defines the password list used during the brute-force attempt.

`rdp://<TARGET_WINDOWS_IP>`  
Indicates that the attack targets the RDP service on the specified host.

`-vv`  
Enables verbose output so authentication attempts can be observed in real time.

---

## **Step 4 — Authentication Attempts**

Once executed, Ncrack begins sending repeated login attempts to the Windows RDP service.

For each password in the wordlist:

1. The attacker system sends an authentication request.
2. The Windows system evaluates the credentials.
3. The authentication request fails.
4. A failed login event is written to the Windows Security log.

This sequence is repeated until the wordlist is exhausted.

---

## **Step 5 — Generated Windows Security Events**

Each failed login attempt generates a **Windows Security Event ID 4625**.

Event 4625 includes:

- Username used during authentication
- Source IP address of the attacker
- Timestamp of the login attempt
- Logon type
- Failure reason

These logs represent the telemetry required for detecting brute-force attacks.

---

## **Step 6 — Log Collection by Elastic Agent**

The Windows endpoint runs **Elastic Agent**, which collects system logs including authentication events.

The agent forwards these events to Elasticsearch where they are indexed and made searchable within Kibana.

This allows the SOC monitoring platform to analyze authentication patterns across the environment.

---

## **Step 7 — Detection Rule Trigger**

The RDP brute-force detection rule monitors authentication events for suspicious behavior.

The rule uses **threshold-based detection logic**.

Example detection logic:

- **5 failed login attempts**
- **within a 6 minute window**
- **from the same source IP**

Once the threshold condition is met, Elastic Security generates a detection alert.

---

## **Step 8 — Alert Generation**

When the rule triggers, the alert includes investigation context such as:

- Source IP address
- Target Windows host
- Username being targeted
- Number of failed login attempts
- Timestamp of the activity

This information enables SOC analysts to begin investigating the attack.

---


## **Purpose of the Simulation**

This simulation demonstrates how brute-force attacks against RDP services generate authentication telemetry that can be detected by SIEM monitoring systems.

By reproducing this behavior within a controlled lab environment, the SOC Detection Lab demonstrates how detection rules identify password guessing attacks targeting remote management services.
