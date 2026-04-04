# 🌐 DNS Threat Detection using Splunk

This project demonstrates how DNS logs can be analysed using Splunk SIEM to detect suspicious activity such as domain anomalies, NXDOMAIN patterns, and potential DNS beaconing behaviour.

---

## 🧠 Project Overview

DNS (Domain Name System) logs provide visibility into how systems resolve domain names. Analysing DNS activity allows security analysts to detect abnormal behaviour such as:

- Communication with suspicious domains  
- Failed DNS resolutions (NXDOMAIN)  
- Unusual query patterns  
- Potential command-and-control (C2) communication  

In this project, raw DNS logs were ingested into Splunk, parsed using regular expressions, and analysed to identify potential threats and anomalous behaviour.

---

## 📂 Dataset

The dataset used in this project was adapted from:

- https://github.com/0xrajneesh/Splunk-Projects-For-Beginners

Full credit to **Rajneesh Gupta (0xrajneesh)** for providing structured learning resources and datasets.

---

## 🎯 Objectives

- Extract structured fields from raw DNS logs  
- Identify top queried domains  
- Detect NXDOMAIN (failed DNS resolutions)  
- Identify suspicious or uncommon domains  
- Detect long or abnormal domain names  
- Identify potential DNS beaconing activity  
- Build a monitoring dashboard  
- Implement an alert for suspicious DNS behaviour  

---

## 🔍 Log Analysis Workflow

---

### 1. Log Ingestion

DNS logs were uploaded into Splunk using the **Add Data** feature and indexed for analysis.

---

### 2. Field Extraction Approach

The DNS dataset is unstructured, so Splunk does not automatically extract fields.

Fields were extracted at search time using regex.

#### 🔍 Regex Extraction Query

```spl
| rex field=_raw "^(?<ts>\S+)\s+(?<uid>\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?<proto>\S+)\s+(?<trans_id>\S+)\s+(?<query>\S+)\s+(?<qclass>\S+)\s+(?<qclass_name>\S+)\s+(?<qtype>\S+)\s+(?<qtype_name>\S+)\s+(?<rcode>\S+)\s+(?<rcode_name>\S+)"
| eval readable_time=strftime(ts, "%Y-%m-%d %H:%M:%S")
