---

## **SSH Brute Force Simulation**

This attack simulation demonstrates how automated password guessing attacks can target Secure Shell (SSH) services on Linux systems.

The attack is performed using **Ncrack**, a network authentication cracking tool designed to test password security for remote access services.

Within the lab environment, the Kali Linux attacker machine launches a series of login attempts against a monitored Linux server endpoint.

---

## **Attack Command**

The following command was used to simulate an SSH brute-force attack against the Linux endpoint.

**ncrack -vv --user <TARGET_USERNAME> -P password-list.txt ssh://<TARGET_LINUX_IP>**


---

## **Command Breakdown**

`ncrack`  
Network authentication cracking tool used to test password security of remote services.

`--user <TARGET_USERNAME>`  
Specifies the username being targeted during the attack.

`-P password-list.txt`  
Defines the password wordlist used for the brute-force attempt.

`ssh://<TARGET_LINUX_IP>`  
Indicates the SSH service running on the target Linux system.

`-vv`  
Enables verbose output so authentication attempts can be monitored in real time.

---

## **Attack Method**

The attacker system initiates repeated authentication attempts against the SSH service running on the Linux endpoint.

Each attempt uses credentials from a predefined password list. Because the credentials are incorrect, the Linux system records failed authentication attempts in its system authentication logs.

These logs are collected by the Elastic Agent installed on the endpoint and forwarded to the Elastic Stack for analysis.

---

## **Generated Telemetry**

The attack generates several types of security telemetry including:

- Failed SSH authentication attempts
- Source IP address of the attacking system
- Username being targeted
- Timestamp of each login attempt

These events are typically recorded in the Linux authentication logs and ingested into Elasticsearch for monitoring and detection.

---

## **Detection Outcome**

Once the failed authentication threshold is exceeded, the **SSH brute-force detection rule** triggers an alert within the Elastic Security interface.

The alert includes contextual information such as:

- Source IP address
- Target username
- Affected host
- Number of failed login attempts
- Timestamp of the activity

This allows analysts to quickly identify suspicious login activity and begin investigation procedures.

---

## **Purpose in the Lab**

This simulation demonstrates how SOC monitoring platforms detect automated password attacks targeting Linux systems.

It also allows detection rules and alert workflows to be validated using realistic authentication telemetry generated inside the lab environment.
