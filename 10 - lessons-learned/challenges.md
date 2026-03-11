# Challenges Encountered During the SOC Detection Lab

Building a functional SOC monitoring environment required integrating multiple technologies including virtualization, log collection, SIEM detection rules, dashboards, and ticketing automation.

Throughout the development of the lab, several technical challenges were encountered while configuring the environment and validating the detection pipeline.

---

# Resource Constraints in the Virtual Lab

The SOC environment was deployed using multiple virtual machines including:

- Elastic Stack server
- Fleet Server
- Windows endpoint
- Linux endpoint
- Kali attacker machine
- osTicket server

Running several systems simultaneously created resource limitations on the host machine.

High memory usage occasionally caused system instability or VM crashes when too many virtual machines were running simultaneously.

To resolve this issue, virtual machines were started only when required for a specific phase of testing.

For example:

- attack simulations required Kali and the target endpoint
- log analysis required only the Elastic server and endpoints
- ticketing integration required the osTicket server

This staged approach reduced overall system load while still allowing the full detection pipeline to operate.

---

# Limited External Traffic in the Lab Environment

Because the SOC environment operates within an isolated internal network, there is no exposure to real internet traffic.

This means that dashboards and detections initially contained very little telemetry.

To generate meaningful data for detection rules, attack simulations were performed manually using tools such as:

- Ncrack for authentication attacks
- Mythic for command-and-control activity

These simulations produced realistic log events that could be used to validate detection rules.

---

# Detection Rule Development

Detection rules required careful tuning in order to trigger alerts correctly.

Initial rules sometimes failed to trigger because:

- incorrect event fields were used
- queries did not match the exact log format
- event thresholds were set too high

For example, authentication detections required identifying the correct log fields such as:

```
event.code
user.name
source.ip
```

After identifying the correct fields, threshold-based rules were implemented to detect repeated authentication failures within a short time window.

---

# Log Visibility and Field Mapping

Another challenge involved understanding the structure of log data within Elastic.

Different operating systems generate logs with different field names.

Examples include:

Windows:

```
event.code
winlog.event_data.*
```

Linux:

```
system.auth.ssh.event
user.name
```

Understanding the mapping between these fields was necessary to correctly build detection queries.

Using the **Discover view in Kibana** was critical for identifying which fields were available in each log dataset.

---

# Webhook and Ticketing Integration

Integrating Elastic Security alerts with osTicket required configuring webhook connectors and ensuring the correct alert variables were included in the request payload.

Challenges included:

- formatting the XML payload correctly
- mapping alert fields to ticket content
- ensuring the API endpoint accepted requests from Elastic

Once properly configured, detection alerts were successfully converted into incident tickets.

---

# Dashboard Visualization

Building meaningful dashboards required identifying which log fields provided useful security insights.

Initial dashboard visualizations were too broad and did not clearly highlight suspicious activity.

By refining the visualizations to focus on:

- authentication failures
- process execution events
- network connections
- security control events

the dashboards became much more effective for monitoring potential threats.

---

# Lessons From These Challenges

Working through these challenges provided valuable experience with real-world SOC workflows.

Key takeaways include:

- detection rules must be carefully tuned to match log formats
- dashboards require meaningful telemetry to be effective
- SIEM integrations often require multiple iterations before functioning correctly
- lab environments must simulate realistic attack activity in order to validate detections

These challenges closely mirror the types of problems encountered when deploying and tuning security monitoring systems in production environments.
