<div align="center">

# ⎈ Helm - The Kubernetes Package Manager

### *Simplify, Share, and Manage Complex Kubernetes Applications*

[![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)](https://helm.sh)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io)
[![CNCF](https://img.shields.io/badge/CNCF-Graduated-00ADD8?style=for-the-badge&logo=cncf&logoColor=white)](https://www.cncf.io/)

---

*Helm helps you manage Kubernetes applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application.*

</div>

---

## 📑 Table of Contents

- [What is Helm?](#-what-is-helm)
- [Why Use Helm?](#-why-use-helm)
- [Helm 2 vs Helm 3](#-helm-2-vs-helm-3)
- [Core Components](#-core-components)
- [Chart Structure](#-chart-structure)
- [Templating](#-templating)
- [Chart Hooks](#-chart-hooks)
- [Lifecycle Management](#-lifecycle-management)
- [Packaging & Distribution](#-packaging--distribution)
- [Commands Reference](#-commands-reference)

---

## 🎯 What is Helm?

**Helm** is the package manager for Kubernetes. It helps ease deployment and lifecycle management of applications deployed on a Kubernetes cluster.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         WITHOUT HELM vs WITH HELM                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   WITHOUT HELM                           WITH HELM                         │
│   ────────────                           ─────────                         │
│                                                                             │
│   📄 deployment.yaml                     $ helm install my-app ./chart     │
│   📄 service.yaml                                                          │
│   📄 configmap.yaml                      ┌─────────────────────────────┐   │
│   📄 secret.yaml            ──────►      │  ✅ Single command          │   │
│   📄 ingress.yaml                        │  ✅ All resources deployed  │   │
│   📄 pvc.yaml                            │  ✅ Versioned releases      │   │
│   📄 hpa.yaml                            │  ✅ Easy rollbacks          │   │
│   ...                                    └─────────────────────────────┘   │
│                                                                             │
│   ❌ Manage each file separately         ✅ Manage as ONE package          │
│   ❌ Manual dependency tracking          ✅ Automatic dependency mgmt      │
│   ❌ No versioning                       ✅ Release versioning             │
│   ❌ Complex rollbacks                   ✅ One-command rollback           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Helm's Capabilities

| Feature | Description |
|:--------|:------------|
| 📦 **Package Manager** | Install/uninstall applications with a single command |
| 🔄 **Release Manager** | Upgrade and rollback applications easily |
| 📝 **Templating** | Dynamic configuration with Go templates |
| 🔗 **Dependency Management** | Manage chart dependencies automatically |
| 🌐 **Repository Support** | Share and distribute charts via repositories |

---

## 💡 Why Use Helm?

### The Problem

Kubernetes is great at managing complex infrastructure, but applications can become very complicated:

```
A Simple Application Requires:
├── Deployment
├── Service
├── ConfigMap
├── Secret
├── PersistentVolume
├── PersistentVolumeClaim
├── Ingress
├── HorizontalPodAutoscaler
└── ... and more
```

**Challenges without Helm:**
- 📄 Separate YAML file for each object
- 🔗 Manual connection management between objects
- ✏️ Repetitive edits across multiple files
- 🔄 Complex upgrade/rollback processes
- 🚫 Kubernetes treats each object independently

### The Solution

**Helm treats your application as a single package:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              HELM ANALOGY                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   📱 Mobile Game Installation                ⎈ Helm Installation           │
│   ─────────────────────────                  ──────────────────            │
│                                                                             │
│   Game consists of:                          App consists of:              │
│   • Graphics                                 • Deployments                 │
│   • Music                                    • Services                    │
│   • Data files                               • ConfigMaps                  │
│   • Config                                   • Secrets                     │
│                                                                             │
│   You don't install each                     You don't apply each          │
│   component separately!                      YAML separately!              │
│                                                                             │
│   Just: "Install Game" ─────────────────►    Just: "helm install app"      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Benefits

- ✅ **Single command** to install entire application (even with thousands of objects)
- ✅ **Automatic object creation** without managing individual YAML files
- ✅ **Centralized configuration** via `values.yaml`
- ✅ **Easy upgrades and rollbacks** with single commands
- ✅ **Reusable charts** for consistent deployments

---

## 🔄 Helm 2 vs Helm 3

### Architecture Comparison

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         HELM 2 ARCHITECTURE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────┐                    ┌──────────────────────────────────┐ │
│   │  Helm CLI    │ ◄───────────────►  │         Kubernetes Cluster       │ │
│   │  (Client)    │                    │  ┌────────────────────────────┐  │ │
│   └──────────────┘                    │  │         TILLER             │  │ │
│         │                             │  │    (Server Component)      │  │ │
│         │                             │  │                            │  │ │
│         └─────────────────────────────│──│  • God mode privileges     │  │ │
│                                       │  │  • Security concerns       │  │ │
│                                       │  │  • Single point of failure │  │ │
│                                       │  └────────────────────────────┘  │ │
│                                       └──────────────────────────────────┘ │
│                                                                             │
│   ❌ Requires Tiller in cluster                                            │
│   ❌ Security vulnerabilities (Tiller had admin privileges)                │
│   ❌ No native RBAC support                                                │
│   ❌ 2-way merge (only compares revisions)                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                         HELM 3 ARCHITECTURE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────┐                    ┌──────────────────────────────────┐ │
│   │  Helm CLI    │ ◄───────────────►  │         Kubernetes Cluster       │ │
│   │  (Client)    │     Direct API     │                                  │ │
│   └──────────────┘     Connection     │     No Tiller Required! ✅       │ │
│         │                             │                                  │ │
│         │                             │     Uses K8s RBAC directly       │ │
│         └─────────────────────────────│     Secrets store release info   │ │
│                                       │                                  │ │
│                                       └──────────────────────────────────┘ │
│                                                                             │
│   ✅ No Tiller required                                                    │
│   ✅ Native RBAC support (uses K8s permissions)                            │
│   ✅ CRD support                                                           │
│   ✅ 3-way strategic merge patch                                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Feature Comparison

| Feature | Helm 2 | Helm 3 |
|:--------|:-------|:-------|
| **Tiller** | ❌ Required | ✅ Removed |
| **RBAC** | ❌ Limited | ✅ Native K8s RBAC |
| **CRD Support** | ❌ Limited | ✅ Full support |
| **Merge Strategy** | 2-way merge | 3-way merge |
| **Security** | ⚠️ Concerns | ✅ Improved |
| **Release Storage** | ConfigMaps | Secrets |

### 3-Way Strategic Merge Patch

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     2-WAY vs 3-WAY MERGE                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   HELM 2 (2-Way Merge)                 HELM 3 (3-Way Merge)                │
│   ────────────────────                 ────────────────────                │
│                                                                             │
│   Compares:                            Compares:                           │
│   • Previous revision                  • Previous revision                 │
│   • New revision                       • New revision                      │
│                                        • LIVE STATE ✅                     │
│                                                                             │
│   Problem Scenario:                    Solution:                           │
│   ─────────────────                    ─────────                           │
│   1. helm install (rev 1)              1. helm install (rev 1)             │
│   2. Manual kubectl edit               2. Manual kubectl edit              │
│   3. helm rollback                     3. helm rollback                    │
│      │                                    │                                │
│      └─► No change detected!              └─► Detects live state diff!     │
│          (Only compares revisions)            Properly reverts changes     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🧩 Core Components

### Component Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          HELM COMPONENTS                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────┐     install      ┌─────────────┐                         │
│   │             │ ───────────────► │             │                         │
│   │    CHART    │                  │   RELEASE   │ ──── Revision 1         │
│   │             │                  │             │ ──── Revision 2         │
│   └─────────────┘                  └─────────────┘ ──── Revision 3         │
│         │                                │                                  │
│         │                                │                                  │
│         ▼                                ▼                                  │
│   ┌─────────────┐                  ┌─────────────┐                         │
│   │    REPO     │                  │  METADATA   │                         │
│   │  (Storage)  │                  │ (K8s Secret)│                         │
│   └─────────────┘                  └─────────────┘                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Detailed Components

<table>
<tr>
<td width="50%">

**📦 Charts**

A chart is a collection of files containing all instructions Helm needs to create Kubernetes objects.

```
Chart = Package of K8s Resources
├── Templates (YAML with Go templating)
├── Values (Configuration)
├── Metadata (Chart info)
└── Dependencies (Sub-charts)
```

**Think of it as an instruction manual for Helm.**

</td>
<td width="50%">

**🚀 Releases**

A release is a single installation of an application using a Helm chart.

```bash
# Two releases from same chart
helm install my-site-1 bitnami/wordpress
helm install my-site-2 bitnami/wordpress

# Each release:
# • Has its own name
# • Tracked independently
# • Has its own revisions
```

</td>
</tr>
<tr>
<td>

**📝 Revisions**

Each change creates a new revision (snapshot) of the release.

```
Release: my-wordpress
├── Revision 1 (Initial install)
├── Revision 2 (Upgrade replicas)
├── Revision 3 (Update image)
└── Revision 4 (Rollback to rev 2)
```

</td>
<td>

**🗄️ Repositories**

Collections of charts available for download.

| Repository | URL |
|:-----------|:----|
| Bitnami | `https://charts.bitnami.com/bitnami` |
| Artifact Hub | `https://artifacthub.io` |

```bash
helm repo add bitnami https://...
helm search repo wordpress
```

</td>
</tr>
</table>

### values.yaml

The central configuration file for customizing chart deployments:

```yaml
# values.yaml - Single source of configuration
replicaCount: 3

image:
  repository: nginx
  tag: "1.21"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80

resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 50m
    memory: 64Mi
```

---

## 📁 Chart Structure

### Standard Directory Layout

```
mychart/
│
├── 📄 Chart.yaml          # Chart metadata (name, version, description)
├── 📄 Chart.lock          # Dependency lock file
├── 📄 values.yaml         # Default configuration values
├── 📄 values.schema.json  # JSON Schema for values validation
├── 📄 LICENSE             # License information
├── 📄 README.md           # Chart documentation
├── 📄 .helmignore         # Patterns to ignore when packaging
│
├── 📁 templates/          # Template files
│   ├── 📄 deployment.yaml
│   ├── 📄 service.yaml
│   ├── 📄 ingress.yaml
│   ├── 📄 configmap.yaml
│   ├── 📄 _helpers.tpl    # Template helpers (partial templates)
│   ├── 📄 NOTES.txt       # Post-install instructions
│   └── 📁 tests/          # Test files
│       └── 📄 test-connection.yaml
│
├── 📁 charts/             # Dependency charts
│   └── 📁 postgresql/
│
└── 📁 crds/               # Custom Resource Definitions
```

### Chart.yaml

```yaml
apiVersion: v2
name: my-application
description: A Helm chart for my application
type: application
version: 1.0.0        # Chart version
appVersion: "2.3.1"   # Application version

keywords:
  - web
  - application

maintainers:
  - name: Your Name
    email: your@email.com

dependencies:
  - name: postgresql
    version: "11.x.x"
    repository: "https://charts.bitnami.com/bitnami"
    condition: postgresql.enabled
```

---

## 🔧 Templating

### Basic Syntax

```yaml
# templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-deployment
  labels:
    app: {{ .Values.app.name }}
spec:
  replicas: {{ .Values.replicaCount }}
  template:
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          ports:
            - containerPort: {{ .Values.service.port }}
```

### Built-in Objects

| Object | Description | Example |
|:-------|:------------|:--------|
| `.Values` | Values from values.yaml | `{{ .Values.replicaCount }}` |
| `.Release` | Release information | `{{ .Release.Name }}` |
| `.Chart` | Chart.yaml content | `{{ .Chart.Version }}` |
| `.Files` | Access non-template files | `{{ .Files.Get "config.ini" }}` |
| `.Capabilities` | K8s cluster info | `{{ .Capabilities.KubeVersion }}` |

### Template Functions

<table>
<tr>
<td width="50%">

**Common Functions**

```yaml
# default - Set default value
image: {{ .Values.image | default "nginx" }}

# quote - Add quotes
env: {{ .Values.env | quote }}

# upper/lower - Case conversion
name: {{ .Values.name | upper }}

# replace - String replacement
{{ .Values.name | replace "-" "_" }}

# required - Fail if empty
{{ required "Name is required" .Values.name }}
```

</td>
<td width="50%">

**Pipeline Chaining**

```yaml
# Chain multiple functions
image: {{ .Values.image.repo | default "nginx" | quote }}

# Complex pipeline
labels:
  app: {{ .Values.app | lower | replace " " "-" | trunc 63 }}

# Indent for YAML formatting
annotations:
{{ .Values.annotations | toYaml | indent 4 }}
```

</td>
</tr>
</table>

### Control Structures

```yaml
# Conditionals
{{- if .Values.ingress.enabled }}
apiVersion: networking.k8s.io/v1
kind: Ingress
# ... ingress definition
{{- end }}

# If-Else
{{- if .Values.production }}
replicas: 5
{{- else }}
replicas: 1
{{- end }}
```

### With Blocks (Scope)

```yaml
# Instead of repeating .Values.app everywhere
{{- with .Values.app }}
metadata:
  name: {{ .name }}
  labels:
    version: {{ .version }}
    environment: {{ .env }}
{{- end }}

# Access root scope inside with block using $
{{- with .Values.app }}
  name: {{ .name }}
  release: {{ $.Release.Name }}  # $ refers to root
{{- end }}
```

### Range (Loops)

```yaml
# Loop through a list
env:
{{- range .Values.env }}
  - name: {{ .name }}
    value: {{ .value | quote }}
{{- end }}

# Loop with index
{{- range $index, $region := .Values.regions }}
  - region-{{ $index }}: {{ $region | quote }}
{{- end }}
```

### Named Templates (_helpers.tpl)

```yaml
# _helpers.tpl - Reusable template snippets
{{- define "mychart.labels" -}}
app.kubernetes.io/name: {{ .Chart.Name }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/version: {{ .Chart.AppVersion }}
{{- end -}}

{{- define "mychart.selectorLabels" -}}
app.kubernetes.io/name: {{ .Chart.Name }}
app.kubernetes.io/instance: {{ .Release.Name }}
{{- end -}}
```

```yaml
# Using in deployment.yaml
metadata:
  labels:
    {{- include "mychart.labels" . | nindent 4 }}
spec:
  selector:
    matchLabels:
      {{- include "mychart.selectorLabels" . | nindent 6 }}
```

> 💡 **Note:** Files starting with `_` are skipped when rendering K8s manifests but can contain helper templates.

---

## 🪝 Chart Hooks

Hooks allow you to intervene at certain points in a release's lifecycle.

### Hook Lifecycle

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          HELM HOOK LIFECYCLE                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   INSTALL                                                                   │
│   ───────                                                                   │
│   helm install ──► verify ──► render ──► pre-install ──► INSTALL ──► post-install
│                                              │                    │         │
│                                              ▼                    ▼         │
│                                         [Run Jobs]           [Resources]    │
│                                                                             │
│   UPGRADE                                                                   │
│   ───────                                                                   │
│   helm upgrade ──► verify ──► render ──► pre-upgrade ──► UPGRADE ──► post-upgrade
│                                              │                              │
│                                              ▼                              │
│                                         [DB Backup]                         │
│                                                                             │
│   DELETE                                                                    │
│   ──────                                                                    │
│   helm uninstall ──► pre-delete ──► DELETE ──► post-delete                 │
│                          │                         │                        │
│                          ▼                         ▼                        │
│                     [Cleanup]               [Notifications]                 │
│                                                                             │
│   ROLLBACK                                                                  │
│   ────────                                                                  │
│   helm rollback ──► pre-rollback ──► ROLLBACK ──► post-rollback            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Available Hooks

| Hook | Description |
|:-----|:------------|
| `pre-install` | Runs before any resources are installed |
| `post-install` | Runs after all resources are installed |
| `pre-upgrade` | Runs before upgrade (e.g., backup database) |
| `post-upgrade` | Runs after upgrade completes |
| `pre-delete` | Runs before deletion (e.g., cleanup) |
| `post-delete` | Runs after deletion |
| `pre-rollback` | Runs before rollback |
| `post-rollback` | Runs after rollback |
| `test` | Runs when `helm test` is invoked |

### Hook Example

```yaml
# templates/pre-upgrade-job.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: {{ .Release.Name }}-db-backup
  annotations:
    "helm.sh/hook": pre-upgrade           # Hook type
    "helm.sh/hook-weight": "-5"           # Priority (lower = first)
    "helm.sh/hook-delete-policy": hook-succeeded
spec:
  template:
    spec:
      containers:
        - name: backup
          image: backup-tool:latest
          command: ["./backup.sh"]
      restartPolicy: Never
  backoffLimit: 1
```

### Hook Weights

```yaml
# Execute email notification first, then backup
annotations:
  "helm.sh/hook": pre-upgrade
  "helm.sh/hook-weight": "-10"    # Runs first (email)

annotations:
  "helm.sh/hook": pre-upgrade
  "helm.sh/hook-weight": "-5"     # Runs second (backup)
```

---

## 🔄 Lifecycle Management

### Release Lifecycle

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        RELEASE LIFECYCLE                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                              ┌───────────┐                                  │
│                              │  INSTALL  │                                  │
│                              └─────┬─────┘                                  │
│                                    │                                        │
│                                    ▼                                        │
│   ┌──────────┐              ┌───────────┐              ┌──────────┐        │
│   │ ROLLBACK │ ◄─────────── │  RUNNING  │ ───────────► │ UPGRADE  │        │
│   └──────────┘              └─────┬─────┘              └──────────┘        │
│        │                          │                          │             │
│        │                          │                          │             │
│        └──────────────────────────┼──────────────────────────┘             │
│                                   │                                         │
│                                   ▼                                         │
│                             ┌───────────┐                                   │
│                             │ UNINSTALL │                                   │
│                             └───────────┘                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Customizing Chart Parameters

**Method 1: Using `--set` flag**
```bash
helm install my-app bitnami/nginx \
  --set replicaCount=3 \
  --set service.type=LoadBalancer \
  --set image.tag=1.21
```

**Method 2: Using custom values file**
```bash
# Create custom-values.yaml
helm install my-app bitnami/nginx \
  --values custom-values.yaml
```

**Method 3: Pull, modify, install**
```bash
# 1. Pull chart
helm pull bitnami/nginx --untar

# 2. Edit values.yaml locally
vim nginx/values.yaml

# 3. Install from local path
helm install my-app ./nginx
```

### Important Notes

> ⚠️ **Rollback doesn't restore data!** When you rollback, only Kubernetes objects are reverted. Database data is NOT automatically backed up or restored. Use hooks for data backup!

---

## 📦 Packaging & Distribution

### Packaging Charts

```bash
# Package a chart
helm package ./mychart

# Output: mychart-1.0.0.tgz

# Package with specific version
helm package ./mychart --version 2.0.0

# Package to specific directory
helm package ./mychart --destination ./releases
```

### Chart Signing (Provenance)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          CHART SIGNING FLOW                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Developer                                        Consumer                 │
│   ─────────                                        ────────                 │
│                                                                             │
│   ┌─────────────┐                                  ┌─────────────┐         │
│   │ Private Key │                                  │ Public Key  │         │
│   └──────┬──────┘                                  └──────┬──────┘         │
│          │                                                │                 │
│          ▼                                                ▼                 │
│   ┌─────────────┐     Upload      ┌──────────┐    ┌─────────────┐         │
│   │   Sign      │ ──────────────► │   Repo   │ ──►│   Verify    │         │
│   │   Chart     │                 │          │    │   Chart     │         │
│   └─────────────┘                 └──────────┘    └─────────────┘         │
│          │                                                │                 │
│          ▼                                                ▼                 │
│   mychart-1.0.0.tgz                              ✅ Verified & Trusted     │
│   mychart-1.0.0.tgz.prov                                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

```bash
# Sign a chart
helm package --sign --key 'mykey' --keyring ~/.gnupg/pubring.gpg ./mychart

# Verify a chart
helm verify mychart-1.0.0.tgz
```

---

## 📋 Commands Reference

### Repository Commands

```bash
# Add a repository
helm repo add bitnami https://charts.bitnami.com/bitnami

# List repositories
helm repo list

# Update repository cache
helm repo update

# Remove repository
helm repo remove bitnami

# Search in repos
helm search repo wordpress

# Search in Artifact Hub
helm search hub wordpress
```

### Installation Commands

```bash
# Install chart from repo
helm install my-release bitnami/nginx

# Install with custom values
helm install my-release bitnami/nginx --values custom.yaml

# Install with --set
helm install my-release bitnami/nginx --set replicaCount=3

# Install in specific namespace
helm install my-release bitnami/nginx --namespace prod --create-namespace

# Dry-run (preview without installing)
helm install my-release bitnami/nginx --dry-run

# Generate manifests only
helm template my-release bitnami/nginx > manifests.yaml
```

### Management Commands

```bash
# List all releases
helm list
helm list --all-namespaces

# Get release status
helm status my-release

# Get release history
helm history my-release

# Get values of a release
helm get values my-release
helm get values my-release --all      # Include defaults

# Get manifests of a release
helm get manifest my-release
```

### Upgrade & Rollback

```bash
# Upgrade release
helm upgrade my-release bitnami/nginx

# Upgrade with new values
helm upgrade my-release bitnami/nginx --values new-values.yaml

# Upgrade or install if not exists
helm upgrade --install my-release bitnami/nginx

# Rollback to previous revision
helm rollback my-release

# Rollback to specific revision
helm rollback my-release 2
```

### Cleanup Commands

```bash
# Uninstall release
helm uninstall my-release

# Uninstall and keep history
helm uninstall my-release --keep-history
```

### Development Commands

```bash
# Create new chart
helm create mychart

# Lint chart
helm lint ./mychart

# Package chart
helm package ./mychart

# Pull chart
helm pull bitnami/nginx
helm pull bitnami/nginx --untar

# Show chart info
helm show chart bitnami/nginx
helm show values bitnami/nginx
helm show readme bitnami/nginx
```

### Quick Reference Table

| Command | Description |
|:--------|:------------|
| `helm version` | Show Helm version |
| `helm help` | Get help |
| `helm repo add` | Add chart repository |
| `helm repo update` | Update repository cache |
| `helm search repo` | Search in repositories |
| `helm install` | Install a chart |
| `helm upgrade` | Upgrade a release |
| `helm rollback` | Rollback to previous revision |
| `helm list` | List releases |
| `helm history` | Show release history |
| `helm uninstall` | Remove a release |
| `helm create` | Create new chart |
| `helm package` | Package chart for distribution |
| `helm lint` | Validate chart |
| `helm template` | Render templates locally |

---

## 📚 Additional Resources

| Resource | Link |
|:---------|:-----|
| Helm Official Docs | [helm.sh/docs](https://helm.sh/docs/) |
| Artifact Hub | [artifacthub.io](https://artifacthub.io/) |
| Helm Charts Best Practices | [helm.sh/docs/chart_best_practices](https://helm.sh/docs/chart_best_practices/) |
| Bitnami Charts | [github.com/bitnami/charts](https://github.com/bitnami/charts) |

---

<div align="center">

## 🚀 Ready to Continue?

**[← Back to Main](../README.md)** | **[Kubernetes →](../Kubernetes-Concept/README.md)** | **[Terraform →](../Terraform-Concept/README.md)**

---

*"Simplicity is the ultimate sophistication."* — Leonardo da Vinci

</div>


` Personal Note: `
```
:::HELM:::
	Helps ease deployment and lifecycle managment of application deployed on a Kubernetes cluster.
	works as a package/release manager, with install/uninstall wizard, help us to upgrade/rollback applications.
	it treat k8 apps as app instead of just a collection of obj.(no need to micro manage each and every obj)
	Obj:-
		Arch, Comp (Charts, repo, releases, revisions), writing charts, templating, functions, piplines, 
		conditionals, with block, Raange, Chart hooks, chart tests, provenance, Packaging&Signing, uploading,
		
==========================================
What/Why/ is helm?
	Kubernetes is good at managing complex infra, app that we deploy in k8's clusters can become very complicated.
	a app is usually made up of a collection of obj that need to interconnect to make everything work.
	ex:- simple app requires
		Deployment, services, Persiesnt volume, persistence volume claim, store(secret) , (backup, job ...so on)
		for every obj we need seperate YAMl file and apply those and make sure of connection b/w obj, and 
		what if we need to modify some thing in yaml, we need to go back to the file and need to do necessary edits what if it is a repetative task? and what if mess with some thing wrong?
	K8's doesn't really care about our app as a whole, it only know that we declear various obj, and it proceeds to make of them exist in our cluster
	it dosen't know that this is PV and that deployment and that secret store, service are all part of simple app,, it will take care individually.

	To address this issues 'HELM'
	Package manager for k8's, it looks those obj as part of a big package as a group, while performa a action, me only mention a package(simple app) not for the individual objects.
	Ex:-
	let's take game app in playstore, game consist of lot of things(music, graphic, ..so on) to run the app 
	we don't want to install all those seperately we get a gamm installer, we run it, we choose the dir to install and done.	
	Helm also doing the similar thing and more for the k8 objects.
	single cmd to install our entire app, even if their is thousands of objects.
	it automatically add every necessary obj to k8 without bothering us with details, 
	we can customize the settings we want for our app or package by specifing desired values at install time, but instead of having to edit, 
	we have a single location where we can declare every custom settings in a file like "values.yaml".
	We can upgrade/rollback with single cmd
==========================================
Helm 2 vs 3

	In Helm2:
		CLI client installed inlocal machiane helps to helm specific actions aganist k8 cluster, 
		lack of RBAC, and custom resource defination, 
		to work properly, 'tiller' had to be installed in the k8 cluster,
		whenever user want to perform a helm specific operations, our helm client communicated with tiller that was running on server, 
		tiller will communicate with k8 and processed to take actions to make req happen.(middleman).
		some security concerns, by default tiller is in god mode(had privileges to do anything wanted) (not good for all the user to have adminaccess)
		
		dosen't support 3-way strategic merge patch(only looks at revision not on chart and  current state)
		explain:-
		let's assume		
		install >> new revison added as revision 1(revision is nothing but snapshot)
		upgrade >> revision 2
		rollback >> create a new revision as revision 3 and compare revision 2 with revision 1 and make the necessary changesand finally 
		 made revison 3 (doesn't goes back to revision 1, but all the config as same as revision 1)
		senario:
			install >> revision 1
			upgrade done by manually by the user in k8's not through helm, then this update doesn't consider as new revision, 
			and then did rollback what happens?
			we have only one revision of the helm, it comapre with the old one,  so their is no change
		
	In Helm3:
		CLI client installed inlocal machiane helps to helm specific actions aganist k8 cluster, 
		No tiller, 
		RBAC, custom resource defination support,
		whatever RBAC permissions of k8 users we have same applicable to helm as well,(restrict the user by specific access to do the task)
		support 3-way stratehic merge patch.(looks at revision, on chart and current state)
		explain:
		same senario as above:
		it compares the chart currently in use if we had created a revision that is which we didn't the chart we want to revert to. 
		and alsothe live state how our k8 obj currently looks like their declaration in yamol form.
		by also looking live state, it notice the image version
==========================================
::Components::
	has multiple components we'll be working,
		charts are collection of files, contains all the instructions that helm needs to know to be able to create the collection of objects that you need in our k8 cluster.
		by using chart and adding the obj, acc to the specific instruction in the chart, Helm in a way installs application into cluster, when chart is appllied to cluster a new release is created.
		release is a single installation of an application using helm chart. each release we have multiple revisions/snapshot of application.
		every time a change is made to app(ie., upgrade of image or chnage of replicas or configuration a new revision is created....
		to keep track of what did in cluster(release, chart used, revision state ...so on) helm will need to place a save data(METADATA),
		helm is storing metadata in k8 cluster secrete, so that authorized user has access, and know the exact status,   
		
		We have lot of chart avalible in internet we can directly download and use it but the main thing is 
		values.yaml(setting file or input file for helm), it is where the defination chnages as per the application, we can customize as our own.
		
		when a chat is applied a release is created,
		helm install my-site-1 bitnami/wordpress
		make sure to give name, why?,  we can install multiple release based on the same chart. 
		so we can lauch a second app with a command,
		helm install my-site-2 bitnami/wordpress		
		two release they are seperate and have their own revisions, and tracked seperately and changes independently. even though they are based on same chart.
		
		helm repo has lot of charts to deploy as a new chart, let's say deploy redis or prometheus goes to helm repo and install those.
		helm repo comes into picture.
		lot of charts are already avaliable at different helm repo
		providers of helm repo are appscode, truecharts, bitnami, community operatores >> all this repo,chart are located in artifacthub.io
==========================================
:::HELM Charts:::
	HELM easy to use command line tool,(automation tool), but how it knows to do the task, by using charts.
	charts are like instructions manual for it. By reading and intrepreting the content, it then knows exactly ehat it has to do to fulfill a user's request.
	chart.yaml >> it contains info about chart itself, 
	chart structure:
		templates/ >> template directory
		value.yaml >> config values
		chart.yaml >> chart info
		license
		readme
		charts/ >> dependency chart.
==========================================
::cutomize chart parameters::
while installing we can customize chart parameters, 
1. by using 'set' option
	helm install --set .. --set .. <> <>
	
2. create cusom.yaml file and add all these and pass while installling.
	helm install --values <yamlfile>

3. break install into 2 cmds, 
	1.pull the chart
		helm pull <> >> pull in archive/compress form
		helm pull --untar <>
	2. then we ahve files and then edit our necessary things and 
	now run install but give the local path that we have edited yaml file.
==========================================
::Lifecycle Managment in HELM::
	each time we pull in a chart and install it, a new release will created(release similar to app, but more specific it represent a package or a collections of k8 objs)
	sincel heml know what k8 obj are relate to release, it can do things like upgrade, downgrade or uninstalls without touching obj that might belong to other release.
	each release can be managed independently, even aif they all based on same chart
	
	BY using rollback the data won't be backedup or restored.
	
==========================================
Writing a files, 
Nothing much just add the deploy.yaml and service.yaml files int he helm telplate directory and make sure the no static definations in the file, 
everthying has to be taken from values.yaml for custom.yaml or directly from the helm but no static definations.
reason, 
	if deployment name is static, we will release a chart by using that deployment, if want to again deploy the chart release from the same deployment file,
it through an error telling that chart is deployment is already there, so we can't reuse it, for that sake we always prefer template rendering(dynamic)  
		
what if you defined and forget to pass the value in values.yaml ?
ex: image: ____, then we need some default values.
in deployment.yaml fiel we can use {{default "nginx" ......}}

funtions:
 default
 upper ex;- {{ upper.Values.image.repository }}
 quote.
 replace.
 shuffle. ..and so on refer doc

Pipeline:
  {{ Values.image.repository | upper | quote | .. }}

conditionals:

Blocks:
	no need to metion everytime, simple like a scope, if this ".Values.app." is a app level scope no need to metion each and every argument, 
	we can simple use this
	instead we can use 
	{{- with .Values.app}}
	....
	{{- end }}
	Now want if we want to use from the root level inside the app scope simple use "$"

Ranges:
	nothing but loops.
	{{- range.Values.regions }}
	-{{ . | quote }}
	{{- end }}
	
Named Templates:
TEMPLATE ACTION
INCLUDE FUNCTION
	
	to remove duplication, re-use code,
	create _helpers.tpl in the template directory(where depoly and services files are here)
	all files start with '_' are skiped by helm while converted into a k'8 manifest file.
	in _helpers.tpl we can start with this
	{{- define "lables" }}
	 app.k8's.io/name : nginx
	{{- end }}
	and we can simple use this by {{- template "lables" }} in our deploy.yaml/service.yaml file
	if you use '.' in {{- template "lables" . }} then we can make dynamic from helper file as well
		{{- define "lables" }}
		app.k8's.io/name: .Release.Name
		{{- end }}
	
	Make sure same indentation across all the files, to make intedentation properly we can use "{{- include "lables" . | indent 2}}", 
	

:::CHART HOOKS:::
before our cmd execute, we need to do some thing before,
ex: use rollback, before the cmd execute, we need to store the data db backup, 
or else sending email before and after, 
these extra actions are implemented know as hooks
ex:-
	in general:
		helm upgrade >> verify >> render >> upgrade 
	by using hooks
	 helm upgrade >> verify >> render >> (pre-upgrade) >> upgrade >> (post upgrade)
	 helm upgrade >> verify >> render >> (pre-install) >> upgrade >> (post install)
	 helm upgrade >> verify >> render >> (pre-delete) >> upgrade >> (post delete)
	 helm upgrade >> verify >> render >> (pre-rollback) >> upgrade >> (post rollback)

to run continuosly we create a pod (kind = pod)
to trigger we use job, (kind = job)
so k8 obj pods and jobs that we configure hooks in helm charts.
so create a job.yaml file and keep this in templates folder hellm will take care of it.
but we need to tell that it is pre or post process, it is not a general yaml file, for that we use "annotations"
Annotations are a way for us to add additional metadata to an object which may be used by client of k8 in this case helm to store data about that obj and perform some kind of actions.

we add annotations with "helm.sh/hook" and values as pre-upgrade, 
what if multiple pre-upgrade hooks configure? ex:email, backup, so email first and backup next,
we can set weights to each other to priortize

:::Packaging and signing charts:::
to package >> helm package <path>
upload to chart repo,
	1st we need to sign in, and then upload, 
	crypto graphy security >>>  private key only chart developer have access with this key digital signature produces provenance file, 
	now whoever download the files, must have public key, 
		
==========================================
:::CMD:::
	helm version
	helm --help
	helm install <release-name> <chart-url>


	helm search (hub or repo) wordpress
	
Deploy app in two commds:
	helm repo add <repo-name> <repo-url>
	helm install <release-name> <path-to-local-chart>
or
	helm install <release-name> <repo-name>/<chart-name>
	
	
	helm repo update
	
	helm upgrade <release-name> <chart-name> [flags]
	
	helm list >> to get all the relaese
	
	helm uninstall <release_name> >> to delete the release
	
	helm history <chart_name>

	helm rollback <release-name> <revision-number>
	
	helm uninstall <release_name>
	
	helm package <path>

```
