# 🚨 SOAR-Lite Incident Response Lab (Linux + LimaCharlie + Windows Sliver + Webhook Integration)

This project demonstrates a lightweight SOAR (Security Orchestration, Automation, and Response) lab setup using **LimaCharlie** for telemetry and detection, **Linux for scripting**, **Sliver C2 for red team simulation**, and **webhook integration** for alerting or automation workflows.

---

**Short Description:**
A compact, hands-on incident response setup simulating real-world attacks using Sliver C2 and capturing endpoint/network telemetry via LimaCharlie, with automation hooks for response and notifications.

---

## 🎯 Objectives

* Deploy LimaCharlie agent on Linux and Windows
* Simulate attacks using Sliver C2
* Capture and analyze telemetry via LimaCharlie Console
* Integrate webhooks for alert-based actions (e.g., Slack, custom APIs)
* Automate basic incident response workflows

## 🛠️ Tools Used

| Tool           | Purpose                                                   |
| -------------- | --------------------------------------------------------- |
| LimaCharlie    | Endpoint telemetry, detection & response                  |
| Sliver C2      | Adversary emulation (Red Team simulation)                 |
| Linux (Ubuntu) | SOAR scripting and webhook handler                        |
| Webhooks       | Trigger alerts to external systems (Slack, Discord, etc.) |

## 🧱 Architecture

```
+----------------+         +----------------+          +-------------------+
|  Linux (SOAR)  | <-----> |  LimaCharlie   | <------> | Windows + Sliver  |
| + Webhook API  |         |  Cloud Console |          |     Agent         |
+----------------+         +----------------+          +-------------------+
                                      |
                                      v
                               Alert & Automation
```

## 🚀 Setup Steps

### 1. LimaCharlie Setup

* Create account at [https://limacharlie.io/](https://limacharlie.io/)
* Create an **Organization** and generate **Sensor Installer**
* Deploy agent on:

  * **Linux (SOAR node)**
  * **Windows (target for simulation)**

### 2. Sliver C2 Deployment

* Install Sliver on Kali Linux or Linux system
* Generate Windows payload: `generate --mtls example.com --os windows`
* Execute payload on Windows VM (ensure LimaCharlie is monitoring it)

### 3. Telemetry & Detections

* Confirm endpoint telemetry on LimaCharlie dashboard
* Enable built-in detections or write custom detection rules (YARA/Telemetry based)

### 4. Webhook Integration

* Go to **LimaCharlie Console** → Automation → Webhooks
* Add webhook URL to your Linux server (Flask, FastAPI, or Node.js endpoint)
* Example Use Cases:

  * Post alerts to Slack
  * Trigger scripts to isolate endpoints
  * Send email or Discord notifications

### 5. SOAR Scripts (Linux)

* Python/Node scripts to:

  * Parse incoming alerts
  * Run response actions via LimaCharlie REST API (e.g., isolate host)
  * Log and store incident data

## 💥 Simulated Attack Scenarios (Using Sliver)

| Technique             | Description                         |
| --------------------- | ----------------------------------- |
| Command Execution     | Run `whoami`, `ipconfig`, `netstat` |
| Lateral Movement      | Use `psexec` or RDP simulation      |
| Credential Dumping    | Simulate `mimikatz`-like behavior   |
| Persistence           | Registry-based autorun payloads     |
| File Drop + Execution | Drop payloads and monitor with LC   |

## 📂 Project Structure

```
.
├── soar-scripts/
│   ├── webhook_handler.py
│   ├── lc_isolate_host.py
│   └── slack_notifier.py
├── configs/
│   └── lc-webhook-config.json
├── payloads/
│   └── sliver_payload.exe
└── README.md
```

## 📚 References

* [LimaCharlie Docs](https://doc.limacharlie.io/)
* [Sliver C2](https://github.com/BishopFox/sliver)
* [Python Flask Webhook Guide](https://flask.palletsprojects.com/)
* [LimaCharlie Automation](https://doc.limacharlie.io/docs/automations)

## 🚀 Future Enhancements

* 🧠 Add Sigma Rule correlation to LimaCharlie detections
* 🔗 Integrate with TheHive or Shuffle for case management
* 📊 Store and visualize incidents with ELK or Grafana
* 🚀 Use Ngrok/Cloudflare tunnel for public webhook URL

## 🤝 Contributing

Feel free to fork, improve detection logic, or add response integrations via pull requests.

## 📬 Contact

Maintained by [Your Name](https://github.com/yourusername)
📧 [your.email@example.com](mailto:your.email@example.com)
🔗 LinkedIn | GitHub | Twitter

