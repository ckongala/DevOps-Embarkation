<div align="center">

# 🚀 DevOps Embarkation

### *Your Complete Journey to Mastering DevOps*

[![DevOps](https://img.shields.io/badge/DevOps-Learning_Path-0A66C2?style=for-the-badge&logo=azure-devops&logoColor=white)](https://github.com)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io)
[![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)](https://terraform.io)
[![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)](https://helm.sh)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io)

<br/>

**A comprehensive, structured learning repository covering essential DevOps concepts, tools, and best practices — from foundational principles to production-grade implementations.**

[12-Factor App](#-12-factor-app) •
[CI/CD](#-cicd-pipeline) •
[Kubernetes](#-kubernetes) •
[Helm](#-helm) •
[Terraform](#-terraform) •
[Monitoring](#-prometheus--monitoring)

---

<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/kubernetes/kubernetes-plain-wordmark.svg" width="80" height="80" alt="Kubernetes" />
&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/terraform/terraform-original.svg" width="80" height="80" alt="Terraform" />
&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original.svg" width="80" height="80" alt="Docker" />
&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/prometheus/prometheus-original.svg" width="80" height="80" alt="Prometheus" />
&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/jenkins/jenkins-original.svg" width="80" height="80" alt="Jenkins" />

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Learning Path](#-learning-path)
- [12-Factor App](#-12-factor-app)
- [CI/CD Pipeline](#-cicd-pipeline)
- [Kubernetes](#-kubernetes)
- [Helm](#-helm)
- [Terraform](#-terraform)
- [Prometheus & Monitoring](#-prometheus--monitoring)
- [Getting Started](#-getting-started)
- [Resources](#-resources)
- [Contributing](#-contributing)

---

## 🎯 Overview

**DevOps-Embarkation** is a curated knowledge base designed to take you from DevOps fundamentals to production-ready expertise. Whether you're a beginner or looking to solidify your understanding, this repository provides structured learning paths, detailed notes, and practical examples.

### What You'll Learn

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   📐 FOUNDATIONS          🔄 CI/CD              ☸️  ORCHESTRATION           │
│   ─────────────          ──────                ──────────────              │
│   • 12-Factor App        • Jenkins             • Kubernetes               │
│   • DevOps Culture       • GitOps              • Helm Charts              │
│   • Best Practices       • Security Scanning   • Service Mesh             │
│                                                                             │
│   🏗️  INFRASTRUCTURE      📊 MONITORING         🔐 SECURITY                 │
│   ──────────────         ──────────           ─────────                   │
│   • Terraform IaC        • Prometheus          • OWASP                    │
│   • Cloud Providers      • Node Exporter       • Vulnerability Scanning   │
│   • State Management     • Alerting            • Secret Management        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🗺️ Learning Path

<table>
<tr>
<td align="center" width="150">

### 1️⃣
**Foundations**

</td>
<td>

Start with understanding the **12-Factor App** methodology — the foundation of building modern, cloud-native applications that are scalable, maintainable, and portable.

</td>
</tr>
<tr>
<td align="center">

### 2️⃣
**Prerequisites**

</td>
<td>

Master the **DevOps prerequisites** including Linux, networking, scripting, and version control before diving into specialized tools.

</td>
</tr>
<tr>
<td align="center">

### 3️⃣
**CI/CD**

</td>
<td>

Learn to build **automated pipelines** with Jenkins, implement security scanning, containerization, and GitOps-based deployments.

</td>
</tr>
<tr>
<td align="center">

### 4️⃣
**Kubernetes**

</td>
<td>

Understand container orchestration with **Kubernetes** — pods, deployments, services, networking, and cluster management.

</td>
</tr>
<tr>
<td align="center">

### 5️⃣
**Helm**

</td>
<td>

Simplify Kubernetes deployments with **Helm** — the package manager for Kubernetes. Learn charts, templating, and release management.

</td>
</tr>
<tr>
<td align="center">

### 6️⃣
**Terraform**

</td>
<td>

Master **Infrastructure as Code** with Terraform — provision, manage, and version your infrastructure across multiple cloud providers.

</td>
</tr>
<tr>
<td align="center">

### 7️⃣
**Monitoring**

</td>
<td>

Implement observability with **Prometheus** and exporters — collect metrics, create dashboards, and set up alerting.

</td>
</tr>
</table>

---

## 📐 12-Factor App

> *The twelve-factor methodology for building modern, scalable, maintainable software-as-a-service applications.*

<table>
<tr>
<td width="50%">

| # | Factor | Description |
|:-:|:-------|:------------|
| 1 | **Codebase** | One codebase tracked in VCS, many deploys |
| 2 | **Dependencies** | Explicitly declare and isolate dependencies |
| 3 | **Config** | Store config in environment variables |
| 4 | **Backing Services** | Treat backing services as attached resources |
| 5 | **Build, Release, Run** | Strictly separate build and run stages |
| 6 | **Processes** | Execute app as stateless processes |

</td>
<td width="50%">

| # | Factor | Description |
|:-:|:-------|:------------|
| 7 | **Port Binding** | Export services via port binding |
| 8 | **Concurrency** | Scale out via the process model |
| 9 | **Disposability** | Maximize robustness with fast startup/shutdown |
| 10 | **Dev/Prod Parity** | Keep environments as similar as possible |
| 11 | **Logs** | Treat logs as event streams |
| 12 | **Admin Processes** | Run admin tasks as one-off processes |

</td>
</tr>
</table>

📁 **Explore:** [`01-12FactorApp/`](./01-12FactorApp/) — Detailed explanations for each factor

🔗 **Reference:** [12factor.net](https://12factor.net/)

---

## 🔄 CI/CD Pipeline

> *Automate your software delivery with continuous integration and continuous deployment.*

### Pipeline Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CONTINUOUS INTEGRATION (CI)                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   📝 Code Push    →    🔨 Build    →    🧪 Test    →    🔍 Scan            │
│                                                                             │
│   • Feature Branch     • Maven/npm       • Unit Tests      • SonarQube     │
│   • Pull Request       • Dependencies    • Coverage        • OWASP Check   │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   🐳 Dockerize    →    🔐 Security    →    📦 Push to Registry             │
│                                                                             │
│   • Build Image        • Trivy/Snyk       • ECR / Docker Hub               │
│   • Tag Version        • CVE Scan         • Artifact Storage               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                        CONTINUOUS DEPLOYMENT (CD)                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   🚀 Deploy (EC2)    →    🧪 Integration Tests    →    ✅ Create PR        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CONTINUOUS DELIVERY (CD)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ☸️  GitOps/ArgoCD    →    🔍 DAST    →    ✋ Approval    →    🌐 Prod    │
│                                                                             │
│   • K8s Deploy          • OWASP ZAP      • Manual Gate      • Lambda       │
│   • Helm Charts         • Runtime Scan   • Security Review  • Production   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Tools & Practices

| Stage | Tools | Purpose |
|:------|:------|:--------|
| **Build** | Maven, Gradle, npm | Compile code, manage dependencies |
| **Test** | JUnit, pytest, Mocha | Unit tests, code coverage |
| **SAST** | SonarQube, CodeQL | Static code analysis |
| **Container** | Docker, Buildah | Containerization |
| **Security** | Trivy, Snyk, Aqua | Container vulnerability scanning |
| **Registry** | ECR, Docker Hub, GCR | Image storage |
| **Deploy** | ArgoCD, Flux | GitOps-based deployments |
| **DAST** | OWASP ZAP | Dynamic security testing |

📁 **Explore:** [`CI-CD/`](./CI-CD/) — Complete CI/CD pipeline documentation

---

## ☸️ Kubernetes

> *Container orchestration for automating deployment, scaling, and management of containerized applications.*

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              KUBERNETES CLUSTER                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────────────────────── MASTER NODE ───────────────────────────┐ │
│   │                                                                       │ │
│   │   ┌──────────┐  ┌──────────┐  ┌────────────┐  ┌───────────┐          │ │
│   │   │   API    │  │   etcd   │  │ Controller │  │ Scheduler │          │ │
│   │   │  Server  │  │ (store)  │  │  Manager   │  │           │          │ │
│   │   └──────────┘  └──────────┘  └────────────┘  └───────────┘          │ │
│   │                                                                       │ │
│   └───────────────────────────────────────────────────────────────────────┘ │
│                                    │                                        │
│                                    ▼                                        │
│   ┌─────────────────────────── WORKER NODES ──────────────────────────────┐ │
│   │                                                                       │ │
│   │   ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐  │ │
│   │   │   Worker Node   │    │   Worker Node   │    │   Worker Node   │  │ │
│   │   ├─────────────────┤    ├─────────────────┤    ├─────────────────┤  │ │
│   │   │ ┌─────────────┐ │    │ ┌─────────────┐ │    │ ┌─────────────┐ │  │ │
│   │   │ │   Kubelet   │ │    │ │   Kubelet   │ │    │ │   Kubelet   │ │  │ │
│   │   │ └─────────────┘ │    │ └─────────────┘ │    │ └─────────────┘ │  │ │
│   │   │ ┌─────────────┐ │    │ ┌─────────────┐ │    │ ┌─────────────┐ │  │ │
│   │   │ │    Pods     │ │    │ │    Pods     │ │    │ │    Pods     │ │  │ │
│   │   │ └─────────────┘ │    │ └─────────────┘ │    │ └─────────────┘ │  │ │
│   │   └─────────────────┘    └─────────────────┘    └─────────────────┘  │ │
│   │                                                                       │ │
│   └───────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Core Concepts

<table>
<tr>
<td width="50%">

**🔧 Control Plane Components**

| Component | Function |
|:----------|:---------|
| **API Server** | Frontend for K8s, handles all REST requests |
| **etcd** | Distributed key-value store for cluster state |
| **Scheduler** | Assigns pods to nodes based on resources |
| **Controller Manager** | Runs controller processes |

</td>
<td width="50%">

**⚙️ Worker Node Components**

| Component | Function |
|:----------|:---------|
| **Kubelet** | Agent ensuring containers run in pods |
| **Kube-proxy** | Network proxy for service abstraction |
| **Container Runtime** | Docker, containerd, CRI-O |

</td>
</tr>
</table>

### Key Resources

| Resource | Description | Use Case |
|:---------|:------------|:---------|
| **Pod** | Smallest deployable unit | Run containers |
| **ReplicaSet** | Maintains stable set of pod replicas | High availability |
| **Deployment** | Declarative updates for pods | Rolling updates, rollbacks |
| **Service** | Exposes pods as network service | Load balancing, discovery |
| **ConfigMap** | Store non-confidential config | Environment configuration |
| **Secret** | Store sensitive information | Passwords, tokens, keys |

### Essential Commands

```bash
# Cluster Info
kubectl cluster-info
kubectl get nodes

# Pods
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl logs <pod-name>

# Deployments
kubectl create deployment <name> --image=<image>
kubectl rollout status deployment/<name>
kubectl rollout undo deployment/<name>

# Services
kubectl expose deployment <name> --type=NodePort --port=80
kubectl get services
```

📁 **Explore:** [`Kubernetes-Concept/`](./Kubernetes-Concept/) — Complete K8s documentation & PDF guide

---

## ⎈ Helm

> *The package manager for Kubernetes — simplify, share, and manage even the most complex applications.*

### Why Helm?

```
WITHOUT HELM                              WITH HELM
────────────                              ─────────
                                          
├── deployment.yaml                       helm install my-app ./chart
├── service.yaml                          
├── configmap.yaml                        ┌─────────────────────────┐
├── secret.yaml                           │  Single command deploys │
├── ingress.yaml         ──────────►      │  ALL resources with     │
├── pvc.yaml                              │  proper configuration   │
└── ...                                   └─────────────────────────┘
                                          
(Manage each file separately)             (Manage as ONE package)
```

### Helm Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                           HELM CHART                                 │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   📁 mychart/                                                        │
│   ├── 📄 Chart.yaml          # Chart metadata                       │
│   ├── 📄 values.yaml         # Default configuration values         │
│   ├── 📁 templates/          # Kubernetes manifest templates        │
│   │   ├── deployment.yaml                                           │
│   │   ├── service.yaml                                              │
│   │   ├── _helpers.tpl       # Template helpers                     │
│   │   └── NOTES.txt          # Post-install notes                   │
│   ├── 📁 charts/             # Dependency charts                    │
│   └── 📄 README.md                                                  │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### Key Concepts

| Concept | Description |
|:--------|:------------|
| **Chart** | Package of pre-configured Kubernetes resources |
| **Release** | Instance of a chart running in a cluster |
| **Revision** | Snapshot of a release (for rollbacks) |
| **Repository** | Collection of charts (like npm registry) |

### Essential Commands

```bash
# Repository Management
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo wordpress

# Installation
helm install my-release bitnami/wordpress
helm install my-release ./local-chart --values custom.yaml
helm install my-release bitnami/nginx --set service.type=LoadBalancer

# Management
helm list
helm status my-release
helm upgrade my-release bitnami/wordpress
helm rollback my-release 1

# Cleanup
helm uninstall my-release
```

📁 **Explore:** [`Helm-Concept/`](./Helm-Concept/) — Complete Helm documentation & PDF guide

---

## 🏗️ Terraform

> *Infrastructure as Code — provision and manage infrastructure across multiple cloud providers.*

### IaC Categories

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      INFRASTRUCTURE AS CODE (IaC)                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   📦 Configuration Management    🖼️  Server Templating    🏗️  Provisioning   │
│   ─────────────────────────     ──────────────────      ─────────────     │
│   • Ansible                      • Docker                • Terraform       │
│   • Puppet                       • Packer                • CloudFormation  │
│   • SaltStack                    • Vagrant               • Pulumi          │
│                                                                             │
│   Install & manage software      Create VM/container     Deploy cloud      │
│   on existing infrastructure     images                  resources         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Terraform Workflow

```
                    ┌─────────────────┐
                    │   Write (.tf)   │
                    │   HCL Config    │
                    └────────┬────────┘
                             │
                             ▼
┌─────────────┐     ┌─────────────────┐     ┌─────────────────┐
│             │     │                 │     │                 │
│  terraform  │────▶│   terraform     │────▶│   terraform     │
│    init     │     │     plan        │     │     apply       │
│             │     │                 │     │                 │
└─────────────┘     └─────────────────┘     └─────────────────┘
       │                    │                       │
       ▼                    ▼                       ▼
  Initialize           Preview              Apply changes
  providers            changes              to infrastructure
```

### Core Concepts

| Concept | Description |
|:--------|:------------|
| **Provider** | Plugin to interact with APIs (AWS, Azure, GCP) |
| **Resource** | Infrastructure component to create |
| **Data Source** | Query existing infrastructure |
| **Variable** | Input parameters for configuration |
| **Output** | Return values from configuration |
| **State** | Mapping of config to real resources |
| **Module** | Reusable configuration container |

### State Management

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        REMOTE STATE BACKEND                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────┐              ┌─────────────┐                             │
│   │   S3 Bucket │◄────────────▶│  DynamoDB   │                             │
│   │ State File  │   Locking    │  Lock Table │                             │
│   └─────────────┘              └─────────────┘                             │
│         │                                                                   │
│         │   • Automatic state sync                                          │
│         │   • State locking prevents conflicts                              │
│         │   • Team collaboration                                            │
│         │   • Secure storage                                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Essential Commands

```bash
# Initialization
terraform init
terraform validate
terraform fmt

# Planning & Applying
terraform plan
terraform apply
terraform apply -auto-approve

# State Management
terraform state list
terraform state show <resource>
terraform state rm <resource>

# Destruction
terraform destroy

# Workspace
terraform workspace list
terraform workspace new dev
terraform workspace select prod
```

📁 **Explore:** [`Terraform-Concept/`](./Terraform-Concept/) — Complete Terraform documentation & PDF guide

---

## 📊 Prometheus & Monitoring

> *Open-source monitoring and alerting toolkit designed for reliability and scalability.*

### Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         PROMETHEUS ECOSYSTEM                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                          ┌─────────────────┐                               │
│                          │   Prometheus    │                               │
│                          │     Server      │                               │
│                          │   (Scraping)    │                               │
│                          └────────┬────────┘                               │
│                                   │                                        │
│         ┌─────────────────────────┼─────────────────────────┐              │
│         │                         │                         │              │
│         ▼                         ▼                         ▼              │
│   ┌───────────┐            ┌───────────┐            ┌───────────┐         │
│   │   Node    │            │   cAdvisor │           │  Custom   │         │
│   │  Exporter │            │  (Docker)  │           │ Exporter  │         │
│   │  :9100    │            │   :8080    │           │           │         │
│   └───────────┘            └───────────┘            └───────────┘         │
│        │                         │                        │               │
│        ▼                         ▼                        ▼               │
│   ┌─────────┐              ┌─────────┐              ┌─────────┐           │
│   │  Linux  │              │ Docker  │              │   App   │           │
│   │  Host   │              │Containers│              │ Metrics │           │
│   └─────────┘              └─────────┘              └─────────┘           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Quick Setup (Systemd)

```bash
# 1. Create dedicated user
sudo useradd --no-create-home --shell /bin/false prometheus

# 2. Create directories
sudo mkdir -p /etc/prometheus /var/lib/prometheus

# 3. Set permissions
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus

# 4. Create systemd service
sudo vim /etc/systemd/system/prometheus.service
```

```ini
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus/

[Install]
WantedBy=multi-user.target
```

```bash
# 5. Start service
sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

### Access Points

| Service | Port | URL |
|:--------|:-----|:----|
| Prometheus | 9090 | `http://localhost:9090` |
| Node Exporter | 9100 | `http://localhost:9100/metrics` |
| Alertmanager | 9093 | `http://localhost:9093` |
| Grafana | 3000 | `http://localhost:3000` |

📁 **Explore:** [`Prometheus/`](./Prometheus/) — Setup guides for Prometheus & Node Exporter

---

## 🚀 Getting Started

### Prerequisites

- Basic Linux command line knowledge
- Understanding of networking concepts
- Familiarity with YAML syntax
- Git for version control

### Clone the Repository

```bash
git clone https://github.com/yourusername/DevOps-Embarkation.git
cd DevOps-Embarkation
```

### Recommended Learning Order

```
1. 📁 01-12FactorApp/           → Start here! Understand cloud-native principles
2. 📁 02-DevOps-Pre-Requisite/  → Fill any knowledge gaps
3. 📁 CI-CD/                    → Learn pipeline automation
4. 📁 Kubernetes-Concept/       → Master container orchestration
5. 📁 Helm-Concept/             → Simplify K8s deployments
6. 📁 Terraform-Concept/        → Infrastructure as Code
7. 📁 Prometheus/               → Monitoring & observability
```

---

## 📁 Repository Structure

```
DevOps-Embarkation/
│
├── 📁 01-12FactorApp/              # The 12-Factor App methodology
│   ├── 01-CodeBase/
│   ├── 02-Dependencies/
│   ├── 03-Concurrency/
│   ├── ... (all 12 factors)
│   └── README.md
│
├── 📁 02-DevOps-Pre-Requisite/     # Prerequisites & foundations
│   └── README.md
│
├── 📁 CI-CD/                       # CI/CD pipeline concepts
│   └── README.md                   # Jenkins, GitOps, Security scanning
│
├── 📁 Kubernetes-Concept/          # Kubernetes deep-dive
│   ├── KubernetesForBeginners.pdf
│   └── README.md                   # Pods, Deployments, Services, etc.
│
├── 📁 Helm-Concept/                # Helm package manager
│   ├── helm-deck.pdf
│   └── README.md                   # Charts, Templates, Releases
│
├── 📁 Terraform-Concept/           # Infrastructure as Code
│   ├── Terraform-Associate-1-1-1.pdf
│   └── README.md                   # HCL, Providers, State, Modules
│
├── 📁 Prometheus/                  # Monitoring & Alerting
│   ├── docker-setup/
│   └── README.md                   # Prometheus, Node Exporter setup
│
└── 📄 README.md                    # You are here!
```

---

## 📚 Resources

### Official Documentation

| Tool | Documentation |
|:-----|:--------------|
| Kubernetes | [kubernetes.io/docs](https://kubernetes.io/docs/) |
| Helm | [helm.sh/docs](https://helm.sh/docs/) |
| Terraform | [terraform.io/docs](https://www.terraform.io/docs/) |
| Prometheus | [prometheus.io/docs](https://prometheus.io/docs/) |
| Docker | [docs.docker.com](https://docs.docker.com/) |

### Additional Learning

- 🎓 [12 Factor App](https://12factor.net/) — Original methodology
- 🎓 [CNCF Landscape](https://landscape.cncf.io/) — Cloud Native ecosystem
- 🎓 [Artifact Hub](https://artifacthub.io/) — Helm charts repository

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve this learning resource:

1. **Fork** the repository
2. **Create** a feature branch
   ```bash
   git checkout -b feature/add-new-topic
   ```
3. **Commit** your changes
   ```bash
   git commit -m "docs: add new topic on service mesh"
   ```
4. **Push** and create a **Pull Request**

### Contribution Ideas

- [ ] Add AWS/Azure/GCP specific examples
- [ ] Include more hands-on labs
- [ ] Add GitLab CI/CD examples
- [ ] Expand monitoring with Grafana dashboards
- [ ] Add service mesh (Istio/Linkerd) section

---

<div align="center">

## ⭐ Star this repository if it helps your DevOps journey!

<br>

**Happy Learning! 🚀**

<sub>Built with ❤️ for the DevOps community</sub>

---

*"The only way to do great work is to love what you do."* — Steve Jobs

</div>
