# HTTP Threat Detection using Splunk

This project demonstrates how HTTP web logs can be analysed using Splunk SIEM to detect scanning activity, identify suspicious behaviour, and simulate real-world SOC (Security Operations Centre) workflows.

---

## 🧠 Project Overview

HTTP logs provide visibility into web traffic, including requests, response codes, user behaviour, and access patterns. Analysing these logs enables detection of web-based attacks such as:
- Directory traversal attempts
- Sensitive file access
- Automated scanning and enumeration
- High-frequency request patterns

In this project, raw HTTP logs were ingested into Splunk, parsed using regular expressions, and analysed to uncover indicators of malicious activity.

---

## 📂 Dataset

The dataset used in this project was adapted from:

* [Splunk SSH Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%233-analyzing-http-logs-using-splunk-siem.md)

Full credit to **Rajneesh Gupta (0xrajneesh)** for providing structured learning resources and sample datasets for Splunk log analysis projects. ([Splunk-([Splunk-Projects-For-Beginners][1])

---

🎯 Objectives

- Extract structured fields from raw HTTP logs
- Detect access to sensitive or restricted paths
-	Identify automated scanning tools (e.g. Nmap, DirBuster)
-	Analyse HTTP error patterns (403, 404, 500)
-	Detect repeated scanning behaviour
-	Identify top attacking source IPs and targeted hosts
-	Build a dashboard for monitoring
-	Implement alerting for abnormal activity

---



[1]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%233-analyzing-http-logs-using-splunk-siem.md "project#3-analyzing-http-logs-using-splunk-siem.md"
[2]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners "Splunk SIEM Log Analysis Projects"
