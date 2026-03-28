# SOC Log Analysis

A collection of hands-on Security Operations Centre (SOC) and blue team log analysis projects using real-world tools such as Splunk.
This repository demonstrates practical skills in detection, investigation, and basic alerting across different log sources.

---

## 🧠 Overview

This repository is designed to showcase how raw logs can be transformed into meaningful security insights. Each project focuses on identifying suspicious behaviour, analysing patterns, and simulating real SOC workflows.

Key focus areas include:

* Log ingestion and parsing
* Field extraction using regex
* Detection of suspicious activity
* Investigation of attacker behaviour
* Visualisation through dashboards
* Alert creation for proactive monitoring

---

## 💼 Business Value

This project demonstrates how security log analysis can deliver tangible value to organisations by improving threat detection, operational efficiency, and risk reduction.

From a business perspective, the implemented workflows support:

* Early Threat Detection  
  Identifies brute-force attacks and automated scanning activity before successful compromise occurs.

* Reduced Investigation Time  
  Structured field extraction and targeted queries enable faster analysis compared to manual log review.

* Improved Security Monitoring  
  Dashboards provide clear visibility into authentication trends and attacker behaviour, supporting quicker decision-making.

* Proactive Defence through Alerting  
  Automated alerts allow security teams to respond to suspicious activity in near real-time.

*  Reduction of False Positives  
  Rule-based detection logic helps focus attention on meaningful events, improving analyst efficiency.

*  Scalable Security Operations  
  Demonstrates how SIEM tools like Splunk can be used to handle large volumes of log data in a structured and repeatable way.

Overall, this project reflects how technical log analysis translates into actionable security insights that support business continuity and risk management.

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
* Windows event log analysis
* Cloud / identity-based log analysis

---

## 🔍 Current Project

### SSH Brute Force Detection using Splunk

This project analyses SSH logs to identify potential brute-force login attempts and automated scanning activity.

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

## 📌 Future Improvements

* Additional log sources and datasets
* More advanced detection logic
* Correlation across multiple log types
* Enhanced dashboards
* Integration with cloud-based SIEM tools

---

## 📎 Notes

This repository is built for learning and portfolio demonstration purposes.
All datasets used are publicly available or simulated environments.

---

`#SOC` `#CyberSecurity` `#BlueTeam` `#Splunk` `#SIEM` `#LogAnalysis`
`#ThreatDetection` `#SecurityOperations` `#Regex` `#IncidentResponse`
