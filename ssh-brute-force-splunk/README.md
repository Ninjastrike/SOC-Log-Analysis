# SSH Brute Force Detection using Splunk

This project demonstrates how SSH authentication logs can be analysed using Splunk SIEM to detect brute-force attacks, identify suspicious behaviour, and simulate real-world SOC (Security Operations Centre) workflows.

---

## 🧠 Project Overview

SSH (Secure Shell) logs contain critical information about remote access attempts, including authentication successes and failures, as well as connection details. Analysing these logs allows security analysts to detect unauthorised access attempts and potential brute-force attacks. ([Splunk-Projects-For-Beginners][1])

In this project, raw SSH logs were ingested into Splunk, parsed with regular expressions, and analysed to uncover suspicious activity patterns.

---

## 📂 Dataset

The dataset used in this project was adapted from:

* [Splunk SSH Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%234-analyzing-ssh-logs-using-splunk-siem.md)

Full credit to **Rajneesh Gupta (0xrajneesh)** for providing structured learning resources and sample datasets for Splunk log analysis projects. ([Splunk-Projects-For-Beginners][2])

---

## 🎯 Objectives

* Detect high-volume failed SSH login attempts
* Identify top attacking source IP addresses
* Analyse authentication outcomes (failure vs success)
* Detect automated scanning tools (e.g. Nmap)
* Build a dashboard for visual monitoring
* Implement an alert for brute-force detection

---

## 🛠️ Tools & Technologies

* Splunk Enterprise
* SPL (Search Processing Language)
* Regular Expressions (regex)
* GitHub

---

## 🔍 Log Analysis Workflow

### 1. Log Ingestion

SSH log files were uploaded into Splunk using the **Add Data** feature and indexed for analysis.

---

### 2. Field Extraction (Regex)

Custom fields such as:

* `src_ip`
* `dest_ip`
* `status`
* `timestamp`

were extracted from raw logs using regex.

```spl id="1"}
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<status>\S+)"
```

---

### 3. Detection: Top Attacking IPs

```spl id="2"}
| search status="failure"
| stats count by src_ip
| sort - count
```

Identifies IP addresses generating the most failed login attempts.

---

### 4. Investigation: Suspicious IP Behaviour

```spl id="3"}
| search src_ip="X.X.X.X"
| stats count by status
```

Used to determine whether login attempts were successful or failed.

---

### 5. Tool Detection (Nmap)

```spl id="4"}
| search client_ssh="*Nmap*"
| stats count by src_ip dest_ip
```

Detection of Nmap signatures such as:

* `SSH-2.0-Nmap-SSH2-Hostkey`
* `SSH-1.5-NmapNSE_1.0`

These indicate automated scanning activity rather than legitimate user behaviour.

---

## 📊 Dashboard

A Splunk dashboard was created to provide a visual overview of SSH activity.

### Panels:

* **Top Attacking Source IPs**
* **SSH Authentication Outcomes**
* **Detected Nmap Scanning Activity**

📸 *(Insert dashboard screenshot here)*

---

## 📸 Analysis Walkthrough
1. Field Extraction

Raw SSH logs were parsed using a regular expression (rex) to extract structured fields such as:

Source IP (src_ip)

Destination IP (dest_ip)

Authentication status (status)

Timestamp (ts)

This step is essential because Splunk initially treats logs as unstructured text. Field extraction enables efficient searching, filtering, and aggregation for further analysis.

2. Identifying Top Attacking Source IPs

The analysis revealed that 192.168.202.141 generated the highest number of failed login attempts (~2365 attempts).

This is a strong indicator of a brute-force attack, as legitimate users typically do not generate such high volumes of authentication failures.

3. Investigating Suspicious Source IP

Further investigation of the suspicious IP showed repeated login attempts over time against multiple destination systems.

The absence of successful logins suggests that the attacker was unable to compromise the system but continued attempting access.

4. Authentication Outcome Breakdown

The breakdown of authentication results showed:

A very high number of failures

Minimal undetermined events

No successful logins for the attacker

This pattern is consistent with brute-force behaviour, where repeated login attempts fail due to incorrect credentials.

5. Target System Analysis

The attacker primarily targeted:

192.168.229.101

This indicates a focused attack on a specific system rather than random scanning across the network.

Such behaviour may suggest that the attacker identified a high-value or exposed target.

6. Detection of Automated Scanning Tools (Nmap)

The presence of SSH client signatures such as:

SSH-2.0-Nmap-SSH2-Hostkey

SSH-1.5-NmapNSE_1.0

confirms that automated tools were used.

This indicates reconnaissance activity rather than manual login attempts, strengthening the conclusion that the traffic is malicious.

7. Brute Force Detection Query

A detection query was implemented to identify brute-force behaviour by:

Grouping events into 5-minute time windows

Counting failed login attempts per source IP

Flagging IPs exceeding a threshold (≥20 attempts)

This simulates real-world detection logic used in SOC environments.

8. Alert Configuration

An alert was configured based on the detection query with the following settings:

Schedule: Every 5 minutes

Time range: Last 5 minutes

Trigger condition: Results > 0

Severity: Medium

This enables continuous monitoring and automatic detection of brute-force activity.

9. Dashboard Visualisation

A dashboard was created to provide a consolidated view of SSH activity, including:

Top attacking source IPs

Authentication outcome distribution

Indicators of automated scanning (Nmap)

This improves situational awareness and allows analysts to quickly identify suspicious patterns.

---

## 🚨 Alert Implementation

An alert was configured to detect brute-force activity.

### Detection Logic

Triggers when:

* A source IP generates **20 or more failed login attempts**
* Within a **5-minute window**

### Alert Query

```spl id="5"}
| eval _time=ts
| search status="failure"
| bin _time span=5m
| stats count by src_ip _time
| where count >= 20
```

### Configuration

* Schedule: Every 5 minutes
* Time range: Last 5 minutes
* Trigger condition: Results > 0
* Severity: Medium

📸 *(Insert alert configuration screenshot here)*

---

## 🧠 Key Findings

* A single source IP generated a significantly high number of failed login attempts
* No successful logins were observed, indicating unsuccessful brute-force attempts
* Presence of Nmap signatures confirmed automated scanning behaviour
* Multiple destination IPs were targeted, suggesting reconnaissance activity

---

## 🧩 Skills Demonstrated

* Log ingestion and parsing
* Regex-based field extraction
* Threat detection and analysis
* SOC investigation workflow
* Dashboard creation
* Alert configuration

---

## 🚀 Key Takeaways

* Raw logs can be transformed into actionable security insights
* Detection logic is essential for identifying abnormal behaviour
* Visualisation improves situational awareness
* Alerts enable proactive monitoring in SOC environments

---

## 🏷️ Tags

`#SOC` `#CyberSecurity` `#BlueTeam` `#Splunk` `#SIEM`
`#LogAnalysis` `#ThreatDetection` `#BruteForce` `#Nmap` `#SecurityOperations`

---

[1]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%234-analyzing-ssh-logs-using-splunk-siem.md?utm_source=chatgpt.com "project#4-analyzing-ssh-logs-using-splunk-siem.md"
[2]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners?utm_source=chatgpt.com "Splunk SIEM Log Analysis Projects"

