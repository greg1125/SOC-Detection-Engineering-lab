---

# **SSH Brute Force Simulation**

This simulation demonstrates how attackers attempt to compromise Linux systems by repeatedly guessing credentials against the Secure Shell (SSH) service.

The attack is performed using **Ncrack** from the Kali Linux attacker machine. Multiple failed authentication attempts are generated against the Linux endpoint, producing authentication logs that are collected by Elastic Agent.

These logs allow the Elastic Security platform to detect brute-force login attempts targeting SSH services.

---

## **Step 1 — Verify SSH Service Availability**

Before launching the attack, the attacker confirms that the SSH service is running on the Linux endpoint.

```bash
nmap -p 22 <TARGET_LINUX_IP>
```

Port **22** is the default port used by SSH.

If the port is open, Nmap will report the service as **ssh**, confirming that the host is accepting remote login attempts.

---

## **Step 2 — Prepare the Password Wordlist**

A password list is required for the brute-force attack.

Example password list:

```
password
admin
root
letmein
123456
password123
```

The password list is saved on the attacker system as:

```
password-list.txt
```

---

## **Step 3 — Launch the SSH Brute Force Attack**

The attack is executed using the following Ncrack command.

```bash
ncrack -vv --user <TARGET_USERNAME> -P password-list.txt ssh://<TARGET_LINUX_IP>
```

This command instructs Ncrack to attempt repeated authentication requests against the SSH service.

---

## **Command Breakdown**

`ncrack`  
Network authentication cracking tool used to test password security of remote services.

`--user <TARGET_USERNAME>`  
Specifies the username targeted during authentication attempts.

`-P password-list.txt`  
Defines the password wordlist used during the attack.

`ssh://<TARGET_LINUX_IP>`  
Specifies the SSH service running on the target Linux system.

`-vv`  
Enables verbose output showing authentication attempts.

---

## **Step 4 — Authentication Attempts**

During execution, Ncrack attempts each password contained in the wordlist.

For every incorrect credential:

1. The SSH server rejects the authentication request.
2. The system records a failed login event.
3. The attacker tool proceeds to the next password.

This process simulates the behavior of automated password guessing attacks.

---

## **Step 5 — Generated Linux Authentication Logs**

Failed SSH authentication attempts are recorded in the Linux authentication log.

Typical log file location:

```
/var/log/auth.log
```

These logs contain information including:

- Username used during login attempt
- Source IP address
- Timestamp of the attempt
- Authentication failure message

---

## **Step 6 — Log Collection**

The monitored Linux endpoint runs **Elastic Agent**, which collects authentication logs and forwards them to Elasticsearch.

Once ingested into Elasticsearch, these logs can be analyzed through Kibana dashboards and detection rules.

---

## **Step 7 — Detection Rule Trigger**

The SSH brute-force detection rule monitors authentication logs for repeated login failures.

Example detection logic:

- Multiple failed login attempts
- Same source IP address
- Same username
- Within a defined time window

When the threshold condition is reached, the detection rule generates an alert.

---

## **Step 8 — Alert Generation**

The generated alert includes important investigation context such as:

- Source IP address of the attacker
- Target Linux host
- Username being targeted
- Number of failed login attempts
- Timestamp of the activity

This information allows analysts to quickly identify brute-force attacks against SSH services.

---


## **Purpose of the Simulation**

This simulation demonstrates how brute-force authentication attacks generate system telemetry that can be detected by security monitoring platforms.

By reproducing SSH brute-force activity inside a controlled lab environment, the SOC Detection Lab demonstrates how SIEM detection rules identify credential guessing attacks targeting Linux systems.
