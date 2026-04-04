# SOC Log Analysis

A collection of hands-on Security Operations Centre (SOC) log analysis projects using Splunk, demonstrating real-world detection, investigation, and alerting workflows across multiple log sources.

---

## 🧠 Overview

![SOC Workflow](ssh-brute-force-splunk/screenshots/10-ssh-project-overview.png)

This repository demonstrates an end-to-end SOC workflow — from ingesting raw logs to detecting threats and triggering alerts.

Instead of manually reviewing logs, this project shows how analysts:

- Ingest and centralise logs into a single platform  
- Extract fields from unstructured data using regex  
- Detect suspicious behaviour using SPL queries  
- Investigate attacker activity and patterns  
- Visualise insights through dashboards  
- Configure alerts for proactive monitoring  

The workflow reflects how real SOC teams prioritise high-risk activity, reduce noise, and respond efficiently to potential threats.
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
