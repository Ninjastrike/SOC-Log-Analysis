# SOC Log Analysis

A practical SOC portfolio demonstrating how raw logs are transformed into actionable security insights using Splunk SIEM to support threat detection, investigation, and response.
Focused on real-world detection, investigation, and alerting workflows across SSH, DNS, and HTTP log sources.

##

![SOC Workflow](ssh-brute-force-splunk/screenshots/10-ssh-project-overview.png)

This repository demonstrates an end-to-end SOC workflow — from ingesting raw logs to detecting threats and triggering alerts.

Instead of manually reviewing logs, this project shows how analysts:

- Ingest and centralise logs into a single platform  
- Extract fields from unstructured data using regex  
- Detect suspicious behaviour using SPL queries  
- Investigate attacker activity and patterns  
- Visualise insights through dashboards  
- Configure alerts for proactive monitoring  

This reflects how real SOC teams prioritise high-risk activity, reduce noise, and respond efficiently to potential threats.

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

These capabilities align with key SOC performance metrics and operational objectives.
This project demonstrates how effective log analysis supports real-world Security Operations Centre (SOC) objectives and improves organisational security posture.

- **Improved Threat Detection**  
  Identifies brute-force attacks, scanning activity, and anomalous behaviour early using structured detection logic.

- **Reduced Mean Time to Detect (MTTD)**  
  Aggregated queries and dashboards enable faster identification of suspicious patterns across large volumes of logs.

- **Reduced Mean Time to Respond (MTTR)**  
  Clear visualisations and focused queries allow analysts to investigate incidents efficiently and prioritise high-risk activity.

- **Reduced Alert Fatigue**  
  Detection rules filter noisy data and highlight meaningful threats, improving signal-to-noise ratio for SOC analysts.

- **Centralised Visibility**  
  Multiple log sources (SSH, DNS, HTTP) are analysed within a single platform, providing a unified view of network activity.

- **Proactive Security Monitoring**  
  Alerts simulate real-time detection workflows, enabling early response before threats escalate into incidents.

- **Real-World SOC Workflow Alignment**  
  Demonstrates end-to-end processes including ingestion, parsing, detection, investigation, and alerting.

---

## 📊 Project Overview

| Project | Focus Area | Key Detection | Skill Focus |
|--------|------------|--------------|-------------|
| SSH Brute Force | Authentication logs | Brute-force attacks, Nmap scanning | Detection engineering |
| DNS Threat Detection | DNS logs | NXDOMAIN anomalies, beaconing activity | Threat hunting |
| HTTP Threat Detection | Web traffic logs | Directory traversal, scanning tools | Web attack analysis |

Explore each project for detailed analysis and findings:

- [SSH Brute Force Detection](ssh-brute-force-splunk/)
- [DNS Threat Detection](dns-threat-detection-splunk/)
- [HTTP Threat Detection](http-threat-detection-splunk/)

---

## 📂 Dataset

The dataset used in this project was adapted from:

* [Splunk SSH Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%234-analyzing-ssh-logs-using-splunk-siem.md)
* [Splunk DNS Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/Project%231-analyzing-dns-log-using%20splunk-siem.md)
* [Splunk HTTP Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%233-analyzing-http-logs-using-splunk-siem.md)

Full credit to **Rajneesh Gupta (0xrajneesh)** for providing structured learning resources and sample datasets for Splunk log analysis projects. [Splunk Projects For Beginners](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners)

---

## 🛠️ Tools & Technologies

- Splunk Enterprise  
- SPL (Search Processing Language)  
- Regular Expressions (regex)  
- GitHub  

---

## 🧩 Skills Demonstrated

- Log analysis and interpretation  
- Detection engineering fundamentals  
- Threat behaviour analysis  
- Dashboard visualisation  
- Alert configuration  
- Security-focused problem solving  

---

## 📎 Notes

This repository is built for learning and portfolio demonstration purposes.  
All datasets are publicly available or simulated environments.
