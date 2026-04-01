=TEXTJOIN("¦",FALSE,A2,B2,C2,D2,E2,K2,L2,M2,N2,O2,P2,Q2,R2,S2,T2,U2,V2,W2,X2,Y2,Z2,AA2,AB2,AC2,AD2,AE2,AF2,AG2,AH2,AI2,AJ2,AK2,AL2,AM2,AN2,AO2,AP2,AQ2,AR2,AS2,AT2,AU2,AV2,AW2,AX2,AY2,AZ2,BA2,BB2,BC2,BD2,BE2,BF2,BG2,BH2,BI2,BJ2,BK2,BL2,BM2,BN2,BO2,BP2,BQ2,BR2,BS2,BT2,BU2,BV2,BW2,BX2,BY2,BZ2,CA2,CB2,CC2,CD2,CE2,CF2,CG2,CH2,CI2,CJ2,CK2,CL2,CM2,CN2,CO2,CP2,CQ2,CR2,CS2,CT2,CU2,CV2,CW2,CX2,CY2,CZ2,DA2,DB2,DC2,DD2,DE2,DF2,DG2,DH2,DI2,DJ2,DK2,DL2,DM2,DN2,DO2,DP2,DQ2,DR2,DS2,DT2,DU2,DV2,DW2,DX2,DY2,DZ2,EA2,EB2,EC2,ED2,EE2,EF2,EG2,EH2,EI2,EJ2,EK2,EL2,EM2,EN2,EO2,EP2,EQ2,ER2,ES2,ET2,EU2,EV2,EW2,EX2,EY2,EZ2)

=IF(COUNTIF(Old!$FA:$FA,FA2)=0,"Changed or New","Exists in Old")

=FILTER(Current!A:FB,Current!FB:FB="Changed or New","No differences")

=IF(COUNTIF(Old!$A:$A,A2)=0,"New Entry","Existing Entry")

=FILTER(Current!A:EZ,COUNTIF(Old!$A:$A,Current!A:A)=0,"No new entries")

=IF(COUNTIF(Old!$A:$A,A2)>0,"Keep","Omit New")

=FILTER(Current!A:EZ,COUNTIF(Old!$A:$A,Current!A:A)>0,"No matching old rows")

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
