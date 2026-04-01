# SOC Log Analysis

A collection of hands-on Security Operations Centre (SOC) and blue team log analysis projects using real-world tools such as Splunk.
This repository demonstrates practical skills in detection, investigation, and basic alerting across different log sources.

---

## 🧠 Overview

This repository demonstrates how raw security logs can be transformed into actionable security insights using real-world SOC workflows.

Key focus areas include:

* Log ingestion and parsing
* Field extraction using regex
* Detection of suspicious activity
* Investigation of attacker behaviour
* Visualisation through dashboards
* Alert creation for proactive monitoring

---

## 🔍 SOC Workflow Overview

This diagram illustrates the end-to-end SOC workflow implemented in this project, from log ingestion to threat detection and alerting.

![SOC Workflow](ssh-brute-force-splunk/screenshots/10-ssh-project-overview.png)

![SOC](https://img.shields.io/badge/SOC-blue)
![CyberSecurity](https://img.shields.io/badge/CyberSecurity-blue)
![BlueTeam](https://img.shields.io/badge/BlueTeam-blue)
![Splunk](https://img.shields.io/badge/Splunk-blue)
![SIEM](https://img.shields.io/badge/SIEM-blue)
![LogAnalysis](https://img.shields.io/badge/LogAnalysis-blue)
![ThreatDetection](https://img.shields.io/badge/ThreatDetection-blue)
![SecurityOperations](https://img.shields.io/badge/SecurityOperations-blue)
![Regex](https://img.shields.io/badge/Regex-blue)
![IncidentResponse](https://img.shields.io/badge/IncidentResponse-blue)
---

## 💼 Business Value

This project demonstrates how effective log analysis can improve organisational security operations:

- **Improved Threat Detection**  
  Identifies brute-force attacks and suspicious behaviour early

- **Reduced Mean Time to Respond (MTTR)**  
  Structured queries and dashboards enable faster investigation

- **Reduced Alert Fatigue**  
  Detection logic filters noise and highlights meaningful threats

- **Centralised Visibility**  
  Aggregates logs into a single platform for efficient monitoring

- **Proactive Security Posture**  
  Alerts allow teams to respond before incidents escalate

---

## 📂 Project Structure

```
soc-log-analysis/
├── README.md
├── ssh-brute-force-splunk/
│   ├── README.md
│   ├── screenshots/
│   └── queries/
```

More projects will be added over time, including:

* Web traffic (HTTP) analysis
* DNS log analysis

---

## 🔍 Current Project

### SSH Brute Force Detection using Splunk

This project simulates a real-world brute-force attack investigation using SSH logs in Splunk.

**Key components:**

* Detection of high-volume failed login attempts
* Identification of top attacking source IPs
* Investigation of authentication outcomes (failure vs success)
* Detection of automated tools (e.g. Nmap)
* Dashboard visualisation for SOC monitoring
* Alert implementation for real-time detection

---

## 🛠️ Tools & Technologies

* Splunk Enterprise
* SPL (Search Processing Language)
* Regular Expressions (regex)
* GitHub

---

## 🧩 Skills Demonstrated

* Log analysis and interpretation
* Detection engineering fundamentals
* Threat identification and behaviour analysis
* Data visualisation (dashboards)
* Basic alert configuration
* Security-focused problem solving

---

## 🚨 Example Use Cases

* Detecting brute-force authentication attempts
* Identifying suspicious source IP behaviour
* Recognising automated scanning tools (e.g. Nmap)
* Monitoring authentication trends
* Creating alerts for abnormal activity

---

## 🎯 Why This Matters

In real-world environments, analysts cannot manually review every log entry.  
Detection logic, dashboards, and alerts are essential to identify threats efficiently and prioritise investigations.

---

## 📎 Notes

This repository is built for learning and portfolio demonstration purposes.
All datasets used are publicly available or simulated environments.
