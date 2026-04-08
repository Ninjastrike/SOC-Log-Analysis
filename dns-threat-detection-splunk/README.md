# DNS Threat Detection using Splunk

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

## 🔍 Log Analysis Workflow

### 1. Log Ingestion

DNS logs were uploaded into Splunk using the Add Data feature.

---

### 2. Field Extraction Approach

The DNS dataset used in this project is unstructured and does not contain predefined headers. As a result, Splunk treats each log entry as raw data (`_raw`) during ingestion and does not automatically extract fields such as source IP, destination IP, or queried domain.

To address this, fields were extracted at search time using regular expressions (`rex`).

This reflects real-world SOC workflows, where analysts frequently work with unstructured logs and perform on-the-fly field extraction for investigation and threat detection.

#### 🔍 Regex Extraction Query

```spl
| rex field=_raw “^(?\S+)\s+(?\S+)\s+(?<src_ip>\S+)\s+(?<src_port>\S+)\s+(?<dest_ip>\S+)\s+(?<dest_port>\S+)\s+(?\S+)\s+(?<trans_id>\S+)\s+(?\S+)\s+(?\S+)\s+(?<qclass_name>\S+)\s+(?\S+)\s+(?<qtype_name>\S+)\s+(?\S+)\s+(?<rcode_name>\S+)”
```

This extracts structured fields such as:

- `ts` (timestamp)  
- `src_ip` (source IP)  
- `dest_ip` (destination DNS server)  
- `query` (domain requested)  
- `qtype_name` (query type)  
- `rcode_name` (response code)  

#### Regex Explanation

- `\S+` matches non-whitespace values (each column)  
- `\s+` matches spaces between fields  
- `(?<field_name>...)` creates named fields in Splunk  

This enables efficient filtering, aggregation, and detection using SPL queries.

---

### 3. Detection: Top Queried Domains

```spl
| where dest_port=53
| stats count by query
| sort - count
```

Identifies frequently queried domains to establish baseline DNS behaviour and detect anomalies.

---

### 4. Detection: NXDOMAIN Analysis

```spl
| where dest_port=53 AND rcode_name=“NXDOMAIN”
| stats count by src_ip query
| sort - count
```

Identifies failed DNS queries, which may indicate attempts to contact non-existent or malicious domains.

---

### 5. Detection: Long Domain Names

```spl
| where dest_port=53
| eval domain_length=len(query)
| where domain_length > 40
| table src_ip query domain_length
| sort - domain_length
```

Identifies unusually long domains, which may indicate DNS tunnelling or encoded data exfiltration.

---

### 6. Investigation: DNS Beaconing Behaviour

```spl
| where dest_port=53
| eval _time=ts
| bin _time span=5m
| stats count by src_ip query _time
| where count > 20
| sort - count
```

Detects repeated DNS queries from the same source, which may indicate automated communication with external infrastructure.

---

## 📸 Analysis Walkthrough

### 1. Field Extraction

![Field Extraction](screenshots/1-field-extraction.PNG)

Raw DNS logs were parsed into structured fields for analysis.

---

### 2. Top Queried Domains

![Top Domains](screenshots/2-filter-relevant-dns-traffic.PNG)

Common domains observed:

- google.com  
- apple.com  
- microsoft.com  

These indicate normal DNS activity.

---

### 3. NXDOMAIN Detection

![NXDOMAIN](screenshots/3-detection-queries.PNG)

Failed DNS queries were identified.

Suspicious domains include:

- rootshell-security.net  
- xtral.gpsonextra.net  
- data.t00ls.org  

These may indicate malicious or unknown infrastructure.

---

### 4. Long Domain Detection

![Long Domains](screenshots/4-long-domain-detection.PNG)

Long or complex domains may indicate:

- DNS tunnelling  
- Encoded data exfiltration  

---

### 5. DNS Beaconing Detection

![Beaconing](screenshots/5-beaconing-detection.PNG)

Source IP:

**10.10.117.210**

shows repeated queries at regular intervals, indicating automated behaviour.

---

### 6. Query Type Analysis

![Query Types](screenshots/6-query-type-analysis.PNG)

Most queries are:

- A  
- AAAA  
- PTR  

This provides baseline behaviour.

---

### 7. Detection Rule (Alert Query)

![Alert Query](screenshots/7-alert-query.PNG)

Detection logic:

- 5-minute window  
- Count repeated queries  
- Trigger if threshold exceeded  

---

### 8. Alert Configuration

![Alert Config](screenshots/8-alert-config.PNG)

Configuration:

- Every 5 minutes  
- Last 5 minutes window  
- Trigger when results > 0  
- Severity: Medium  

---

### 9. Dashboard

![Dashboard](screenshots/9-dashboard.PNG)

Provides visibility into:

- Top domains  
- NXDOMAIN results  
- Long domains  
- Beaconing behaviour  

---

## 📝 Incident Summary

Suspicious DNS activity was identified, including repeated NXDOMAIN responses and beaconing patterns. These behaviours may indicate command-and-control (C2) communication or automated malware activity.

The activity was detected using threshold-based detection logic and further validated through behavioural analysis of repeated queries and abnormal domain patterns.

---

## 🎯 Why This Matters

DNS traffic is often overlooked but plays a critical role in detecting malicious activity. Attackers commonly use DNS for command-and-control (C2) communication, data exfiltration, and maintaining persistence.

C2 (Command-and-Control) refers to attacker-controlled infrastructure used to communicate with compromised systems and issue commands.

Detecting anomalies such as repeated NXDOMAIN responses, beaconing behaviour, and unusual domain patterns helps identify potential threats early.

This project demonstrates how SOC analysts can use DNS logs to uncover hidden malicious activity and support proactive threat detection.

---

## ⚠️ Challenges & Limitations

- Unstructured logs required regex extraction  
- High DNS noise  
- NXDOMAIN is not always malicious  
- Detection does not confirm compromise  

---

## 🚩 Indicators of Compromise (IOCs)

### Suspicious Domains

- rootshell-security.net  
- xtral.gpsonextra.net  
- data.t00ls.org  

### Suspicious Source IP

- 10.10.117.210  

### Behavioural Indicators

- Repeated DNS queries  
- High NXDOMAIN frequency  
- Long domain queries  

---

## 🚀 Key Takeaways

- DNS logs provide strong visibility into network behaviour  
- Behaviour patterns are key indicators  
- Detection enables proactive monitoring

[1]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners/blob/main/Project%231-analyzing-dns-log-using%20splunk-siem.md "Project#1-analyzing-dns-log-using splunk-siem.md"
[2]: https://github.com/0xrajneesh/Splunk-Projects-For-Beginners "Splunk SIEM Log Analysis Projects"
