# 🔐 **SOC Analyst Lab Project: SSH Brute Force Attack Detection & Incident Response Using Splunk SIEM**

## 📌 **Project Overview**
This hands-on SOC analyst lab project demonstrates **real-world SIEM detection and incident response skills** by identifying, investigating, and documenting an **SSH brute force attack** using **Splunk Enterprise**.

The project simulates a **real SOC scenario** where Linux authentication logs are ingested into Splunk, suspicious login patterns are detected, attacker behavior is analyzed, and a **successful compromise following brute force attempts** is confirmed and reported.

This project reflects **actual responsibilities of a Tier-1 / Tier-2 SOC Analyst**.

---

## 🎯 **Project Objectives**

* ✅ Ingest Linux OpenSSH authentication logs into Splunk
* ✅ Detect large-scale SSH failed login attempts
* ✅ Identify attacker IP addresses and targeted usernames
* ✅ Correlate failed logins with successful authentication
* ✅ Visualize brute force activity over time
* ✅ Document findings in a professional SOC Incident Report
* ✅ Demonstrate SIEM-based threat detection skills

---

## 🛠️ **Technologies & Tools Used**

| Tool                                 | Purpose                 | Version             |
| ------------------------------------ | ----------------------- | ------------------- |
| **Splunk Enterprise**                | SIEM & log analysis     | 10.2.0              |
| **OpenSSH Logs**                     | Authentication evidence | Linux               |
| **Linux Secure Logs**                | Source data             | `/var/log/auth.log` |
| **Regex (rex)**                      | Field extraction        | SPL                 |
| **SPL (Search Processing Language)** | Detection & correlation | Splunk              |
| **Windows / Linux Host**             | Splunk deployment       | Localhost           |

---

## 🧪 **Lab Environment**

| Component         | Details                     |
| ----------------- | --------------------------- |
| **SIEM Platform** | Splunk Enterprise (Local)   |
| **Log Source**    | OpenSSH authentication logs |
| **Host Analyzed** | `LAPTOP-A8Q63675`           |
| **Attack Type**   | SSH Brute Force             |
| **Attack Vector** | Repeated failed SSH logins  |
| **Log Type**      | `linux_secure`              |

---

## 🚀 **Project Workflow**

### **1️⃣ Log Ingestion**

* Imported OpenSSH authentication logs into Splunk
* Verified correct parsing under `linux_secure` sourcetype
* Confirmed log visibility and timestamps

📸 *Screenshot:* `01_raw_openssh_log_events.png`

---

### **2️⃣ Detection of Failed SSH Logins**

* Queried logs for `"Failed password"` events
* Identified high-volume authentication failures

```spl
source="OpenSSH_2k.log" sourcetype=linux_secure "Failed password"
```

📸 *Screenshot:* `02_failed_ssh_login_events.png`

---

### **3️⃣ Attacker IP & Username Analysis**

* Extracted source IPs and usernames using regex
* Identified most targeted accounts (`admin`, `root`, etc.)

```spl
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| rex "user (?<user>\S+)"
| stats count by src_ip, user
| sort -count
```

📸 *Screenshot:* `03_attacker_ip_user_analysis.png`

---

### **4️⃣ SSH Brute Force Detection**

* Applied thresholds to identify brute force behavior
* Flagged IPs with excessive failed attempts

```spl
| stats count by src_ip
| where count > 10
```

📸 *Screenshot:* `04_ssh_bruteforce_detection.png`

---

### **5️⃣ Timeline Analysis**

* Visualized attack frequency over time
* Confirmed automated attack behavior

```spl
| timechart span=1m count
```

📸 *Screenshot:* `05_bruteforce_timeline.png`

---

### **6️⃣ Successful Login After Brute Force**

* Correlated failed attempts with successful authentication
* Confirmed **security compromise**

```spl
("Failed password" OR "Accepted password")
```

📸 *Screenshot:* `06_success_after_bruteforce.png`

---

## 🚨 **Incident Summary**

| Field                   | Details                    |
| ----------------------- | -------------------------- |
| **Incident Type**       | SSH Brute Force Attack     |
| **Severity**            | High                       |
| **Status**              | Confirmed Compromise       |
| **Primary Attacker IP** | `183.62.140.253`           |
| **Attack Method**       | Credential brute force     |
| **Affected Service**    | SSH                        |
| **Impact**              | Unauthorized system access |

---

## 🧠 **Key Learning Outcomes**

### **Technical Skills Gained**

* SIEM log ingestion & parsing
* SPL query writing
* Regex-based field extraction
* Brute force detection logic
* Attack correlation & validation
* Incident documentation

### **SOC Analyst Skills Demonstrated**

* Alert triage
* Threat investigation
* IOC identification
* Timeline reconstruction
* Incident reporting
* Security monitoring workflows

---

## 📊 **Why This Project Matters**

| Feature                  | SOC Relevance            |
| ------------------------ | ------------------------ |
| Real authentication logs | ✔ Real-world data        |
| Brute force detection    | ✔ Common SOC alert       |
| Correlation logic        | ✔ Tier-1/Tier-2 skill    |
| Incident report          | ✔ Enterprise requirement |
| SIEM hands-on            | ✔ Resume-ready           |

---

## 📄 **Incident Report**

📥 **Professional SOC Incident Report (PDF)**
➡️ *Included in this repository*

This report follows:

* SOC documentation standards
* Incident lifecycle methodology
* Clear executive & technical sections

---

## 📈 **Career Application**

### **This project proves I can:**

* Work with SIEM tools (Splunk)
* Analyze Linux security logs
* Detect credential-based attacks
* Investigate security incidents
* Produce professional SOC reports

💼 **Perfect for:**

* SOC Analyst (L1 / L2)
* Blue Team roles
* Cybersecurity internships

---

## 📚 **References**

* [Splunk Documentation](https://docs.splunk.com/)
* [MITRE ATT&CK – Brute Force (T1110)](https://attack.mitre.org/techniques/T1110/)
* [Linux SSH Security Guide](https://www.ssh.com/academy/ssh/security)
* [SANS SOC Resources](https://www.sans.org)

---

## ⚠️ **Disclaimer**

This project was conducted in a **controlled lab environment** using sample logs.
All activities are for **educational and defensive security purposes only**.

---

## 🌟 **Star This Repository**

If this project helped you learn SOC skills or prepare for interviews, consider starring ⭐ the repo!

---

## 📞 **Connect With Me**

* **LinkedIn:** [https://www.linkedin.com/in/batraju-sairam-016801267/](https://www.linkedin.com/in/batraju-sairam-016801267/)
* **GitHub:** [https://github.com/Batraju-Sairam](https://github.com/Batraju-Sairam)

---

## 🏆 **Portfolio Ready – SOC Approved**

This project is **interview-ready**, **resume-worthy**, and demonstrates **real SOC analyst capability**.

> *“Good SOC analysts don’t just detect alerts — they explain attacks.”*

