# Proof of Concept (PoC): Hybrid Intrusion Detection System (HIDS)

## 1. Introduction
The **Hybrid Intrusion Detection System (HIDS)** is designed to provide an efficient and scalable security monitoring solution by integrating:
- **Signature-based detection** (Suricata) for known threats.
- **Anomaly-based detection** (Event-driven log analysis) to identify suspicious patterns.
- **Security Orchestration, Automation, and Response (SOAR)** for **automated mitigation**.
- **Lightweight deployment using Docker & MicroK8s/K3s** instead of full Kubernetes.

---

## 2. Objectives
- **Detect threats efficiently within hardware limitations**.
- **Leverage SOAR automation** to reduce manual intervention.
- **Use lightweight containerized components** instead of resource-heavy stacks.
- **Reduce false positives** through intelligent log correlation.

---

## 3. Problem Statement
Traditional Intrusion Detection Systems (IDS) suffer from:
- **High false positives** in anomaly-based models.
- **Heavy resource consumption** for deep packet inspection.
- **Manual response overhead** without automated mitigation.


---

## 4. Conceptual Architecture

### **Key Components**
1. **Network Traffic Monitoring (Suricata)**
   - Captures network traffic but focuses on **event-driven analysis** instead of full packet inspection.
   - Uses **custom rulesets** for detecting known attack patterns.

2. **Anomaly Detection (Log & Event-Based)**
   - Uses **log-based behavior analysis** instead of computationally expensive real-time ML models.
   - Processes logs from **Suricata, system events, and authentication logs**.

3. **Security Orchestration & Automated Response (SOAR)**
   - **Correlates Suricata alerts + system logs** to **prioritize real threats**.
   - **Automates responses** (e.g., isolate a machine, trigger alerts).
   - Uses **custom SOAR playbooks** for incident handling.

4. **Dashboard & Alerting**
   - Uses **lightweight ELK Stack** (Elasticsearch, Logstash, Kibana) with **filtered logs** to reduce storage load.
   - Displays **only actionable alerts**, avoiding information overload.

---

## 5. Data Flow & Working

1. **Traffic Capture**  
   - Suricata monitors network activity but processes **only relevant events** (reducing CPU load).  
   - Logs are forwarded to the **anomaly detection system**.

2. **Anomaly Detection & Correlation**  
   - Analyzes Suricata alerts, system logs, and authentication logs.  
   - Uses event-driven logic to **detect deviations from normal behavior**.

3. **Automated Response (SOAR)**
   - SOAR ingests **filtered alerts** and **executes predefined playbooks**:
     - **Flag suspicious IPs** in a blocklist.
     - **Trigger alerts** for high-risk activity.
     - **Initiate containment actions** if required.

4. **Dashboard & Monitoring**
   - **Kibana visualizes threat intelligence** from Suricata + anomaly detection logs.
   - Provides **real-time security insights** without high resource consumption.

---

## 6. Integrations & Technologies

| **Component**     | **Technology Used** |
|------------------|--------------------|
| **IDS Engine**  | Suricata (Signature-based) |
| **Anomaly Detection**  | Event-driven log analysis (Syslog, Suricata logs) |
| **Security Orchestration**  | SOAR (Custom Playbooks) |
| **Threat Intelligence**  | MISP (Manually updated for cost efficiency) |
| **Log Management & Dashboard**  | ELK Stack (Lightweight deployment) |

---

## 7. Expected Outcomes
✅ **Efficient Intrusion Detection** → Optimized to run within hardware constraints.  
✅ **Reduced False Positives** → Log correlation instead of deep learning models.  
✅ **Automated Threat Mitigation** → SOAR automates responses.  
✅ **No Extra Costs** → Uses **open-source, locally deployed tools**.  

---

## 8. Future Enhancements
- **Integrate lightweight machine learning models** (only if performance allows).  
- **Enhance SOAR playbooks** for more dynamic incident response.  
- **Optimize Suricata rule tuning** for higher detection accuracy.  

---

## Next Steps
- **Fine-tune Suricata rule sets** for **event-driven processing**.  
- **Develop efficient SOAR playbooks** to automate **response workflows**.  
- **Optimize ELK Stack for low storage usage**.  
- **Test system with simulated attacks**
