# 🚀 kubespray-observability

A **production-ready observability and monitoring stack** for Kubernetes clusters — combining **Prometheus**, **Grafana**, **Loki**, and **Alertmanager**, all deployed with **Helm**.  
It enables unified metrics, logs, and alerting visibility across workloads running in enterprise Kubernetes environments.

---

## 🌐 Overview

Modern Kubernetes environments demand centralized, scalable observability.  
This project delivers a complete monitoring stack that helps platform and DevOps teams:

- Gain real-time insight into cluster and application health  
- Collect metrics, logs, and alerts in one place  
- Integrate alert notifications to Slack or Microsoft Teams  
- Visualize infrastructure and workloads using Grafana dashboards  

---

## 🧩 Tech Stack

| Tool | Purpose |
|------|----------|
| **Kubernetes** | Container orchestration platform |
| **Prometheus** | Metrics collection and alerting |
| **Grafana** | Visualization and dashboards |
| **Loki** | Log aggregation |
| **Helm** | Deployment and management |
| **Alertmanager** | Notification routing (Slack, Teams, Email) |

---

## 🎯 Key Features

✅ Unified observability for Kubernetes clusters  
✅ Preconfigured dashboards and alert rules  
✅ Log aggregation via Loki, integrated in Grafana  
✅ Slack / Teams alert notifications  
✅ Sample workloads for quick testing  
✅ Simple Helm-based deployment  
✅ Production-grade and easily extensible  

---
## 🏗️ Architecture

+-------------------------------------------+

Kubernetes Cluster
Pods • Metrics • Logs
+-------------------------------------------+

markdown
Copy code
                │
                ▼
+-------------------------------------------+
| Prometheus + Alertmanager |
| (Metrics collection & alerting) |
+-------------------------------------------+
│
▼
+-------------------------------------------+
| Grafana + Loki Integration |
| (Visualization & log aggregation) |
+-------------------------------------------+
│
▼
+-------------------------------------------+
| Dashboards + Notifications |
| (Slack / Teams / Email integrations) |
+-------------------------------------------+

Copy code


## 🚀 Quick Start

### 1️⃣ Prerequisites

- A running Kubernetes cluster  
- Helm installed (`helm version`)  
- `kubectl` configured to access your cluster  

---

### 2️⃣ Deploy Prometheus Stack

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install kube-observe prometheus-community/kube-prometheus-stack \
  -n monitoring --create-namespace

3️⃣ Deploy Loki and Grafana
helm repo add grafana https://grafana.github.io/helm-charts
helm install loki grafana/loki-stack -n monitoring

4️⃣ Configure Alertmanager (Slack / Teams)

Example (edit alerts/alertmanager-config.yaml):

receivers:
  - name: 'slack'
    slack_configs:
      - channel: '#k8s-alerts'
        send_resolved: true
        api_url: '<YOUR_SLACK_WEBHOOK_URL>'


Apply it:

kubectl apply -f alerts/

5️⃣ Access Grafana
kubectl port-forward svc/kube-observe-grafana -n monitoring 3000:80


Then open → http://localhost:3000

(Default user: admin, password: prom-operator)

📊 Dashboards Included

Cluster Overview Dashboard

Node & Pod Resource Metrics

Namespace Performance

Kubernetes Control Plane Health

Loki Log Explorer

All dashboards are preloaded in Grafana under the “Kubernetes Observability” folder.

📦 Repository Structure
📁 kubespray-observability/
 ├── helm/                # Helm values and custom chart configs
 ├── dashboards/          # Grafana dashboard JSON files
 ├── alerts/              # Alertmanager configuration files
 ├── sample-workloads/    # Example workloads for testing
 ├── docs/                # Documentation and setup guides
 └── README.md

🧠 Future Enhancements

🔍 Add Tempo for distributed tracing

📈 Integrate OpenTelemetry collector

🧩 Add Service Mesh observability (Istio / Linkerd)

💰 Include cost and capacity dashboards

🔐 RBAC & SSO integration for Grafana

🤝 Contributing

Contributions are welcome!
You can submit pull requests for:

New dashboards

Improved alert rules

Additional integrations

Documentation improvements

💡 Maintainer

kubespray-observability
Developed and maintained by Your Name

For feedback or questions, please open an issue.
