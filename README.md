# 🛡️ SOC Automation Lab: Elastic SIEM & Custom SOAR Engine

## 📖 Project Overview
This project demonstrates the design and deployment of a hybrid Security Operations Center (SOC) environment. It features real-time threat detection using **Elastic Security (SIEM)** and automated incident response (SOAR) powered by a custom **Python-based engine**. 

The goal is to transition from reactive monitoring to active, zero-touch threat mitigation.

## 🏗️ Architecture & Tech Stack
* **Target Environment:** Ubuntu Server
* **Attacker Machine:** Kali Linux (Hydra Bruteforce)
* **SIEM & Log Management:** Elastic Stack (Elasticsearch, Kibana, Elastic Agent)
* **SOAR / Orchestration:** Custom Python Flask Webhook receiver + Bash scripts
* **Firewall (Mitigation):** UFW (Uncomplicated Firewall)

## 🚀 Key Features & Workflow

1. **Detection (SIEM):** Elastic Security rules monitor logs in real-time. A threshold rule detects SSH Bruteforce anomalies (e.g., `>= 10 failed logins in 2 minutes`).
2. **Orchestration (Webhook):** Upon detection, Kibana automatically triggers a Webhook (POST request) containing the malicious payload and the attacker's IP address.
3. **Automated Response (SOAR):** * The Python server (`soar.py`) intercepts the Webhook alert.
   * It extracts the attacker's IP dynamically.
   * It executes an OS-level bash playbook (`block_ip.sh`) to update firewall rules and block the IP instantly.
   * It archives the event in `incidents.log` and generates a standardized `report.txt`.

## 📂 Repository Structure
```text
SOC-Automation-Lab/
├── README.md                   <-- Project Architecture & Overview
├── requirements.txt            <-- Python dependencies (Flask)
├── playbooks/                  <-- SOAR Engine & Automation Scripts
│   ├── soar.py                 (Webhook receiver logic)
│   └── block_ip.sh             (Bash script for UFW mitigation)
├── reports/                    <-- Incident logs and auto-generated reports
└── screenshots/                <-- Visual proof of execution
