# HTTP Threat Detection using Splunk

This project demonstrates how HTTP web logs can be analysed using Splunk SIEM to detect scanning activity, identify suspicious behaviour, and simulate real-world SOC (Security Operations Centre) workflows.

---

## 🧠 Project Overview

HTTP logs provide visibility into web traffic, including requests, response codes, user behaviour, and access patterns. Analysing these logs enables detection of web-based attacks such as:

* Directory traversal attempts  
* Sensitive file access  
* Automated scanning and enumeration  
* High-frequency request patterns  

In this project, raw HTTP logs were ingested into Splunk, parsed using regular expressions, and analysed to uncover indicators of malicious activity.

---

## 📂 Dataset

## 📂 Dataset

The dataset used in this project was adapted from:

* [Splunk SSH Log Analysis Project by 0xrajneesh](https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%233-analyzing-http-logs-using-splunk-siem.md)

Full credit to **Rajneesh Gupta (0xrajneesh)** for providing structured learning resources and sample datasets for Splunk log analysis projects. ([Splunk-([Splunk-Projects-For-Beginners][1])

---

## 🎯 Objectives

* Extract structured fields from raw HTTP logs  
* Detect sensitive path access  
* Identify automated scanning tools  
* Analyse HTTP error patterns  
* Detect repeated scanning behaviour  
* Identify top attackers and targets  
* Build a monitoring dashboard  
* Implement alerting logic  

---

## 🔍 Log Analysis Workflow

This section outlines the technical steps used to process and analyse HTTP logs.

---

### 1. Log Ingestion

HTTP logs were uploaded into Splunk using the **Add Data** feature and indexed under:

```spl
index=main
```

---

### 2. Field Extraction Approach

The HTTP dataset is unstructured and does not contain predefined headers. Splunk treats each log entry as raw data (`_raw`).

To enable analysis, fields were extracted at search time using regular expressions (`rex`).

This reflects real-world SOC workflows where analysts frequently parse logs dynamically.

#### 🔍 Regex Extraction Query

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| eval readable_time=strftime(ts, "%Y-%m-%d %H:%M:%S")
| table readable_time src_ip dest_ip method host uri
```

---

### 3. Detection: Sensitive Path Access

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| search uri="*etc/passwd*" OR uri="*boot.ini*" OR uri="*.git*" OR uri="*.svn*" OR uri="*_vti_*" OR uri="*manager/html*" OR uri="*host-manager*" OR uri="*axis2-admin*"
| stats count by src_ip dest_ip uri
| sort - count
```

Detects attempts to access sensitive files and administrative endpoints.

---

### 4. Detection: Scanner / Tool Activity

```spl
index=main
| search "Nmap Scripting Engine" OR "DirBuster" OR "Nikto" OR "sqlmap"
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| stats count by src_ip dest_ip method uri
| sort - count
```

Identifies automated scanning tools based on behaviour and signatures.

---

### 5. Detection: HTTP Error Analysis

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)\s+(?<referrer>\S+)\s+(?<user_agent>.+?)\s+(?<req_len>\S+)\s+(?<resp_len>\S+)\s+(?<status_code>\d{3})"
| where status_code IN (403,404,500)
| stats count by src_ip uri status_code
| sort - count
| head 20
```

Highlights enumeration activity through HTTP error patterns.

---

### 6. Detection: Repeated Scanning Behaviour

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| eval _time=ts
| bin _time span=1m
| stats count by src_ip dest_ip _time
| where count > 20
| sort - count
```

Detects high-frequency request patterns typical of automated attacks.

---

### 7. Detection: Top Targeted Hosts

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| stats count by dest_ip
| sort - count
```

Identifies the most targeted systems.

---

### 8. Detection: Top Attacking Source IPs

```spl
index=main
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<trans_depth>\S+)\s+(?<method>\S+)\s+(?<host>\S+)\s+(?<uri>\S+)"
| stats count by src_ip
| sort - count
```

Identifies the most active attackers.

---

## 📸 Analysis Walkthrough

This section follows a typical SOC workflow: Detection → Investigation → Validation → Monitoring.

---

### 1. Field Extraction

![Field Extraction](http-threat-detection-splunk/screenshots/1-field-extraction.PNG)

Raw HTTP logs were parsed into structured fields such as:

- src_ip  
- dest_ip  
- method  
- uri  

This enables efficient filtering, aggregation, and threat detection within Splunk.

---

### 2. Sensitive Path Access

![Sensitive Path](http-threat-detection-splunk/screenshots/2-sensitive-path-access.PNG)

Suspicious URI patterns were detected, including:

- `/manager/html`  
- `/host-manager/html`  
- `/etc/passwd`  

These indicate:

- Directory traversal attempts  
- Attempts to access admin panels  
- Potential reconnaissance activity  

---

### 3. Scanner / Tool Detection

![Scanner Detection](http-threat-detection-splunk/screenshots/3-scanner-or-tool-detection.PNG)

Multiple requests were identified using HTTP methods such as:

- OPTIONS  
- GET  

High-frequency requests across multiple targets suggest:

- Automated scanning tools  
- Enumeration activity  

---

### 4. HTTP Error Analysis

![HTTP Errors](http-threat-detection-splunk/screenshots/4-http-error-analysis.PNG)

Frequent HTTP error codes observed:

- 404 (Not Found)  
- 403 (Forbidden)  

This indicates:

- Resource probing  
- Directory enumeration  
- Attempted access to non-existent or restricted files  

---

### 5. Repeated Scanning Behaviour

![Scanning Behaviour](http-threat-detection-splunk/screenshots/5-repeated-scanning-behaviour.PNG)

Source IP:

**192.168.202.110**

generated a high volume of requests within short time intervals.

This pattern strongly indicates:

- Automated scanning  
- Script-based enumeration  
- Non-human behaviour  

---

### 6. Top Targeted Hosts

![Top Targets](http-threat-detection-splunk/screenshots/6-top-targeted-hosts.PNG)

Most targeted systems include:

- 192.168.23.202  
- 192.168.26.202  
- 192.168.24.202  

This suggests:

- Focused targeting rather than random scanning  
- Potential high-value systems being probed  

---

### 7. Top Attacking Source IPs

![Top Attackers](http-threat-detection-splunk/screenshots/7-top-attacking-source-ips.PNG)

Top attacking sources:

- **192.168.202.102**  
- **192.168.202.110**  

These IPs generated the highest number of requests, indicating:

- Primary scanning sources  
- Potential compromised or attacker-controlled systems  

---

### 8. Detection Rule (Alert Query)

![Alert Query](http-threat-detection-splunk/screenshots/8-alert-query.PNG)

Detection logic:

- Group events into 1-minute windows  
- Count requests per source and destination  
- Trigger when threshold exceeds **20 requests**  

This helps identify abnormal request spikes.

---

### 9. Alert Configuration

![Alert Config](http-threat-detection-splunk/screenshots/9-alert-config.PNG)

Configuration:

- Schedule: Every 5 minutes  
- Time range: Last 24 hours  
- Trigger: Results > 0  
- Severity: Medium  

This enables continuous monitoring for scanning behaviour.

---

### 10. Dashboard

![Dashboard](http-threat-detection-splunk/screenshots/10-dashboard.PNG)

The dashboard provides a consolidated view of:

- Sensitive path access  
- Scanner/tool activity  
- Repeated scanning behaviour  
- Top attackers and targets  

This improves situational awareness and supports faster incident response.

---

## 📝 Incident Summary

Multiple source IPs generated extremely high volumes of HTTP requests targeting specific systems.

Indicators such as:

* Directory traversal attempts  
* Admin panel probing  
* High-frequency requests  
* HTTP error patterns  

strongly indicate automated reconnaissance and web scanning activity.

---

## ⚠️ Challenges & Limitations

- Unstructured logs requiring regex extraction  
- No ground truth for confirmed compromise  
- High data volume requiring filtering  
- Detection based on behaviour, not confirmation  

---

## 🚩 Indicators of Compromise (IOCs)

### 🔺 Suspicious Source IPs

* 192.168.202.102  
* 192.168.202.110  

---

### 🔺 Targeted Hosts

* 192.168.23.202  
* 192.168.26.202  

---

### 🔺 Suspicious URIs

* /etc/passwd  
* /manager/html  
* /host-manager  

---

### 🔺 Behavioural Indicators

* High request frequency  
* Repeated requests within short intervals  
* Large number of HTTP errors  

---

## 🧩 Skills Demonstrated

* Splunk (SPL)  
* Regex field extraction  
* Log analysis  
* Threat detection  
* SOC workflow  
* Dashboard creation  
* Alert configuration  

---

## 🚀 Key Takeaways

* HTTP logs reveal attacker behaviour clearly  
* Detection logic is essential for SOC operations  
* Dashboards improve visibility  
* Alerts enable proactive monitoring 

[1]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/project%233-analyzing-http-logs-using-splunk-siem.md "project#3-analyzing-http-logs-using-splunk-siem.md"
[2]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners "Splunk SIEM Log Analysis Projects"
