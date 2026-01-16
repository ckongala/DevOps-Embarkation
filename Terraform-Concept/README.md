<div align="center">

# 🏗️ Terraform - Infrastructure as Code

### *Build, Change, and Version Infrastructure Safely and Efficiently*

[![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)](https://terraform.io)
[![HashiCorp](https://img.shields.io/badge/HashiCorp-000000?style=for-the-badge&logo=hashicorp&logoColor=white)](https://hashicorp.com)
[![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com)
[![GCP](https://img.shields.io/badge/GCP-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white)](https://cloud.google.com)

---

*Terraform enables you to safely and predictably create, change, and improve infrastructure using declarative configuration files.*

</div>

---

## 📑 Table of Contents

- [Traditional Infrastructure](#-traditional-infrastructure-model)
- [Infrastructure as Code (IaC)](#-infrastructure-as-code-iac)
- [Why Terraform?](#-why-terraform)
- [How Terraform Works](#-how-terraform-works)
- [Core Concepts](#-core-concepts)
- [Configuration Files](#-configuration-files)
- [State Management](#-state-management)
- [Lifecycle Rules](#-lifecycle-rules)
- [Data Sources](#-data-sources)
- [Meta-Arguments](#-meta-arguments)
- [Remote Backend](#-remote-backend)
- [Provisioners](#-provisioners)
- [Commands Reference](#-commands-reference)

---

## 🏢 Traditional Infrastructure Model

### The Old Way

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    TRADITIONAL INFRASTRUCTURE WORKFLOW                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌───────────────┐                                                        │
│   │   Business    │ "We need a new application deployed"                   │
│   │   Request     │                                                        │
│   └───────┬───────┘                                                        │
│           │                                                                 │
│           ▼                                                                 │
│   ┌───────────────┐                                                        │
│   │   Business    │ Gather needs, analyze requirements                     │
│   │   Analyst     │ Convert to high-level technical specs                  │
│   └───────┬───────┘                                                        │
│           │                                                                 │
│           ▼                                                                 │
│   ┌───────────────┐                                                        │
│   │   Solution    │ Design architecture, specify server types              │
│   │   Architect   │ Determine count and specifications                     │
│   └───────┬───────┘                                                        │
│           │                                                                 │
│           ▼                                                                 │
│   ┌───────────────────────────────────────────────────────────────────┐    │
│   │                     INFRASTRUCTURE TEAM                            │    │
│   │                                                                    │    │
│   │   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │    │
│   │   │   Field     │  │  System/NW  │  │  Storage    │              │    │
│   │   │  Engineers  │  │   Admins    │  │   Admins    │              │    │
│   │   │ Rack & Stack│  │  Configure  │  │ Assign Disk │              │    │
│   │   └─────────────┘  └─────────────┘  └─────────────┘              │    │
│   │                                                                    │    │
│   │   ┌─────────────┐  ┌─────────────┐                               │    │
│   │   │   Backup    │  │ Application │                               │    │
│   │   │   Admins    │  │    Team     │                               │    │
│   │   │  Setup BKP  │  │   Deploy    │                               │    │
│   │   └─────────────┘  └─────────────┘                               │    │
│   └───────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│   ⏱️  Weeks to Months!                                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Problems with Traditional Approach

| Issue | Impact |
|:------|:-------|
| ⏰ **Time-consuming** | Weeks or months to provision |
| 👤 **Human Error** | Manual steps lead to mistakes |
| 📈 **Hard to Scale** | Complex to scale up/down quickly |
| 💰 **High Cost** | Multiple teams, equipment, maintenance |
| 🔀 **Inconsistency** | Different environments, different configs |
| 🗑️ **Wasted Resources** | Over-provisioning to be "safe" |

### Cloud Era

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        CLOUD INFRASTRUCTURE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────┐    ┌─────────┐    ┌─────────┐                               │
│   │   AWS   │    │  Azure  │    │   GCP   │                               │
│   └─────────┘    └─────────┘    └─────────┘                               │
│                                                                             │
│   ✅ No physical hardware management                                       │
│   ✅ On-demand provisioning                                                │
│   ✅ Pay-as-you-go                                                         │
│   ✅ Global availability                                                   │
│                                                                             │
│   ❌ Still: Human Error (clicking in console)                              │
│   ❌ Still: Inconsistency (manual configurations)                          │
│                                                                             │
│   Solution: Automate with scripts (Shell, Python, Ruby, PowerShell)        │
│   Better Solution: Infrastructure as Code!                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📜 Infrastructure as Code (IaC)

### Three Categories of IaC Tools

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      INFRASTRUCTURE AS CODE TYPES                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1️⃣  CONFIGURATION MANAGEMENT                                              │
│   ────────────────────────────                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  Tools: Ansible, Puppet, Chef, SaltStack                            │  │
│   │                                                                      │  │
│   │  • Install and manage software on existing servers                  │  │
│   │  • Maintain standard structure across machines                      │  │
│   │  • Version controlled                                               │  │
│   │  • Idempotent (run multiple times, same result)                    │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│   2️⃣  SERVER TEMPLATING                                                     │
│   ─────────────────────                                                    │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  Tools: Docker, HashiCorp Packer, Vagrant                           │  │
│   │                                                                      │  │
│   │  • Create custom images of VMs or containers                        │  │
│   │  • Pre-installed software and dependencies                          │  │
│   │  • Immutable infrastructure (replace, don't modify)                 │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│   3️⃣  PROVISIONING TOOLS                                                    │
│   ──────────────────────                                                   │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  Tools: Terraform, CloudFormation, Pulumi                           │  │
│   │                                                                      │  │
│   │  • Deploy immutable infrastructure resources                        │  │
│   │  • Servers, databases, networks, etc.                               │  │
│   │  • Multiple cloud providers                                         │  │
│   │  • Declarative configuration                                        │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 💡 Why Terraform?

### Key Advantages

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        WHY CHOOSE TERRAFORM?                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  📝 DECLARATIVE LANGUAGE (HCL)                                      │  │
│   │     Define WHAT you want, not HOW to get there                      │  │
│   │     Terraform handles the steps to reach desired state              │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  ☁️  MULTI-CLOUD SUPPORT                                             │  │
│   │     AWS, Azure, GCP, Oracle, Alibaba, and 100+ providers            │  │
│   │     Even on-premises (vSphere, OpenStack)                           │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  🆓 FREE & OPEN SOURCE                                               │  │
│   │     Large community, extensive documentation                        │  │
│   │     Enterprise version available for organizations                  │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐  │
│   │  ⚡ FAST & SIMPLE                                                    │  │
│   │     Single binary installation                                      │  │
│   │     Quick execution: build, manage, destroy                         │  │
│   └─────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ How Terraform Works

### The Three Phases

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       TERRAFORM WORKFLOW                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────┐         ┌─────────────┐         ┌─────────────┐         │
│   │    INIT     │ ──────► │    PLAN     │ ──────► │   APPLY     │         │
│   └─────────────┘         └─────────────┘         └─────────────┘         │
│         │                       │                       │                  │
│         │                       │                       │                  │
│         ▼                       ▼                       ▼                  │
│   ┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐        │
│   │ • Download      │   │ • Read current  │   │ • Execute the   │        │
│   │   providers     │   │   state         │   │   planned       │        │
│   │ • Initialize    │   │ • Compare with  │   │   changes       │        │
│   │   backend       │   │   desired       │   │ • Update state  │        │
│   │ • Prepare       │   │ • Show what     │   │   file          │        │
│   │   working dir   │   │   will change   │   │ • Provision     │        │
│   │                 │   │ • Preview only  │   │   resources     │        │
│   └─────────────────┘   └─────────────────┘   └─────────────────┘        │
│                                                                             │
│                                                                             │
│   DRIFT DETECTION:                                                         │
│   If infrastructure drifts from desired state, running `terraform apply`  │
│   will bring it back to the desired state automatically!                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Declarative vs Imperative

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 DECLARATIVE vs IMPERATIVE                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   IMPERATIVE (Shell Script)           DECLARATIVE (Terraform)              │
│   ─────────────────────────           ───────────────────────              │
│                                                                             │
│   #!/bin/bash                         resource "aws_instance" "web" {      │
│   # Create VPC                          ami           = "ami-123456"       │
│   aws ec2 create-vpc ...                instance_type = "t2.micro"         │
│   # Create subnet                     }                                    │
│   aws ec2 create-subnet ...                                                │
│   # Create instance                   # Just describe WHAT you want       │
│   aws ec2 run-instances ...           # Terraform figures out HOW         │
│   # Handle errors...                                                       │
│   # Check if exists...                                                     │
│                                                                             │
│   ❌ Define every step                 ✅ Define desired end state          │
│   ❌ Handle edge cases                 ✅ Terraform handles complexity      │
│   ❌ Not idempotent                    ✅ Idempotent                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🧩 Core Concepts

### Key Components

| Concept | Description |
|:--------|:------------|
| **Provider** | Plugin to interact with cloud/service APIs (AWS, Azure, GCP) |
| **Resource** | Infrastructure component to create/manage |
| **Data Source** | Query existing infrastructure (read-only) |
| **Variable** | Input parameters for configuration |
| **Output** | Return values from configuration |
| **State** | Mapping of config to real-world resources |
| **Module** | Reusable, encapsulated configuration |

### HCL Syntax (HashiCorp Configuration Language)

```hcl
# Provider configuration
provider "aws" {
  region = "us-east-1"
}

# Resource definition
resource "aws_instance" "web_server" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"

  tags = {
    Name        = "WebServer"
    Environment = "Production"
  }
}

# Variable definition
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

# Output definition
output "instance_ip" {
  value       = aws_instance.web_server.public_ip
  description = "Public IP of the instance"
}

# Data source (read existing resource)
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]  # Canonical

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

---

## 📁 Configuration Files

### Standard File Structure

```
my-terraform-project/
│
├── 📄 main.tf              # Main configuration (resources)
├── 📄 variables.tf         # Variable definitions
├── 📄 outputs.tf           # Output definitions
├── 📄 providers.tf         # Provider configurations
├── 📄 terraform.tfvars     # Variable values (don't commit secrets!)
│
├── 📄 terraform.tfstate    # State file (auto-generated)
├── 📄 terraform.tfstate.backup
│
├── 📁 modules/             # Reusable modules
│   └── 📁 vpc/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
│
└── 📄 .terraform.lock.hcl  # Dependency lock file
```

### Example Files

**main.tf**
```hcl
resource "aws_vpc" "main" {
  cidr_block = var.vpc_cidr
  
  tags = {
    Name = var.project_name
  }
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type
  subnet_id     = aws_subnet.main.id
  
  tags = {
    Name = "${var.project_name}-web"
  }
}
```

**variables.tf**
```hcl
variable "project_name" {
  description = "Name of the project"
  type        = string
}

variable "vpc_cidr" {
  description = "CIDR block for VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}
```

**outputs.tf**
```hcl
output "vpc_id" {
  value       = aws_vpc.main.id
  description = "ID of the VPC"
}

output "instance_public_ip" {
  value       = aws_instance.web.public_ip
  description = "Public IP of web server"
}
```

---

## 💾 State Management

### What is State?

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         TERRAFORM STATE                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   State File = Blueprint of your infrastructure                            │
│                                                                             │
│   ┌─────────────────┐                    ┌─────────────────┐               │
│   │   Configuration │                    │   Real World    │               │
│   │   (.tf files)   │                    │  (Cloud Infra)  │               │
│   └────────┬────────┘                    └────────┬────────┘               │
│            │                                      │                         │
│            │         ┌─────────────────┐         │                         │
│            └────────►│  STATE FILE     │◄────────┘                         │
│                      │ (terraform.     │                                    │
│                      │    tfstate)     │                                    │
│                      │                 │                                    │
│                      │ Maps config to  │                                    │
│                      │ real resources  │                                    │
│                      └─────────────────┘                                    │
│                                                                             │
│   State provides:                                                          │
│   • Mapping of config to real-world resources                              │
│   • Metadata tracking                                                      │
│   • Performance optimization (caching)                                     │
│   • Collaboration support (remote state)                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### State is Critical!

> ⚠️ **State file is the single source of truth!**
> - Contains sensitive data
> - Must be kept secure
> - Should be stored remotely for teams
> - Never edit manually!

---

## 🔄 Lifecycle Rules

### Immutable Infrastructure

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    IMMUTABLE INFRASTRUCTURE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Default Terraform Behavior:                                              │
│   ───────────────────────────                                              │
│                                                                             │
│   When you change a resource configuration:                                │
│                                                                             │
│   1. DELETE old resource    ──────►   2. CREATE new resource               │
│      [Old Instance]                      [New Instance]                    │
│          ❌                                  ✅                             │
│                                                                             │
│   This can cause issues! What if you need the old one running while       │
│   creating the new one?                                                    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Lifecycle Rules Override Default Behavior

```hcl
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = var.instance_type

  lifecycle {
    # Create new resource before destroying old one
    create_before_destroy = true
    
    # Prevent resource from being destroyed
    prevent_destroy = true
    
    # Ignore specific attribute changes
    ignore_changes = [
      tags,
      ami,
    ]
    # Or ignore all changes
    # ignore_changes = all
  }
}
```

### Lifecycle Rules Summary

| Rule | Behavior |
|:-----|:---------|
| `create_before_destroy = true` | Create new resource first, then delete old |
| `prevent_destroy = true` | Prevent accidental destruction (except `terraform destroy`) |
| `ignore_changes = [attr]` | Ignore specific attribute changes |
| `ignore_changes = all` | Ignore all attribute changes |

> ⚠️ **Note:** `prevent_destroy` does NOT prevent `terraform destroy` — it only prevents replacement during normal operations.

---

## 📊 Data Sources

> *Data sources allow Terraform to read information about existing infrastructure.*

### Data Source vs Resource

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    RESOURCE vs DATA SOURCE                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   RESOURCE                              DATA SOURCE                        │
│   ────────                              ───────────                        │
│                                                                             │
│   resource "aws_instance" "web" {       data "aws_ami" "ubuntu" {          │
│     ami           = "ami-123"             most_recent = true               │
│     instance_type = "t2.micro"            owners      = ["canonical"]      │
│   }                                     }                                  │
│                                                                             │
│   ✅ CREATE                              ✅ READ                            │
│   ✅ UPDATE                              ❌ Cannot create                   │
│   ✅ DELETE                              ❌ Cannot update                   │
│   ✅ Managed by Terraform                ❌ Cannot delete                   │
│                                          ✅ Query existing infrastructure  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Data Source Example

```hcl
# Query existing VPC
data "aws_vpc" "existing" {
  id = "vpc-abc123"
}

# Query latest Ubuntu AMI
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]  # Canonical

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-*-amd64-server-*"]
  }
}

# Use data source in resource
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"
  subnet_id     = data.aws_vpc.existing.id
}
```

---

## 🔧 Meta-Arguments

> *Meta-arguments change the behavior of resources.*

### Common Meta-Arguments

<table>
<tr>
<td width="50%">

**count**

Create multiple instances of a resource:

```hcl
resource "aws_instance" "server" {
  count = 3
  
  ami           = "ami-123456"
  instance_type = "t2.micro"
  
  tags = {
    Name = "server-${count.index}"
  }
}

# Access: aws_instance.server[0]
#         aws_instance.server[1]
#         aws_instance.server[2]
```

</td>
<td width="50%">

**for_each**

Create resources from a map or set:

```hcl
resource "aws_instance" "server" {
  for_each = toset(["web", "app", "db"])
  
  ami           = "ami-123456"
  instance_type = "t2.micro"
  
  tags = {
    Name = each.value
  }
}

# Access: aws_instance.server["web"]
#         aws_instance.server["app"]
#         aws_instance.server["db"]
```

</td>
</tr>
<tr>
<td>

**depends_on**

Explicit dependency declaration:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  
  # Wait for S3 bucket to be created
  depends_on = [
    aws_s3_bucket.data
  ]
}
```

</td>
<td>

**provider**

Use specific provider configuration:

```hcl
provider "aws" {
  alias  = "west"
  region = "us-west-2"
}

resource "aws_instance" "west_server" {
  provider = aws.west
  
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

</td>
</tr>
</table>

---

## ☁️ Remote Backend

### Why Remote State?

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    LOCAL vs REMOTE STATE                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   LOCAL STATE                           REMOTE STATE                       │
│   ───────────                           ────────────                       │
│                                                                             │
│   ❌ Not shareable                       ✅ Team collaboration             │
│   ❌ No locking                          ✅ State locking                  │
│   ❌ Risk of conflicts                   ✅ Prevents conflicts             │
│   ❌ Sensitive data on disk              ✅ Encrypted storage              │
│   ❌ Risk of accidental deletion         ✅ Versioning & backup            │
│                                                                             │
│   Problems with Git for state:                                             │
│   • Contains sensitive data                                                │
│   • Forget to push/pull latest                                             │
│   • No state locking support                                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### AWS Remote Backend (S3 + DynamoDB)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    AWS REMOTE BACKEND ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────────┐                                                      │
│   │  Developer 1    │──┐                                                   │
│   └─────────────────┘  │                                                   │
│                        │      ┌───────────────────┐                        │
│   ┌─────────────────┐  │      │                   │                        │
│   │  Developer 2    │──┼─────►│    S3 BUCKET      │◄──── State Storage    │
│   └─────────────────┘  │      │  (terraform.      │                        │
│                        │      │     tfstate)      │                        │
│   ┌─────────────────┐  │      │                   │                        │
│   │  CI/CD Pipeline │──┘      └───────────────────┘                        │
│   └─────────────────┘                 │                                    │
│                                       │                                    │
│                               ┌───────▼───────────┐                        │
│                               │                   │                        │
│                               │   DYNAMODB        │◄──── State Locking    │
│                               │  (Lock Table)     │                        │
│                               │                   │                        │
│                               └───────────────────┘                        │
│                                                                             │
│   S3: Store state file with encryption                                     │
│   DynamoDB: Prevent concurrent modifications                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Backend Configuration

```hcl
# backend.tf
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-state-lock"
  }
}
```

```hcl
# Create S3 bucket and DynamoDB table first
resource "aws_s3_bucket" "terraform_state" {
  bucket = "my-terraform-state-bucket"
  
  versioning {
    enabled = true
  }
  
  server_side_encryption_configuration {
    rule {
      apply_server_side_encryption_by_default {
        sse_algorithm = "AES256"
      }
    }
  }
}

resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-state-lock"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"
  
  attribute {
    name = "LockID"
    type = "S"
  }
}
```

---

## 🔨 Provisioners

> *Provisioners execute scripts on local or remote machines as part of resource creation or destruction.*

### Types of Provisioners

```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  
  # Execute on the remote instance
  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx",
      "sudo systemctl start nginx"
    ]
    
    connection {
      type        = "ssh"
      user        = "ubuntu"
      private_key = file("~/.ssh/id_rsa")
      host        = self.public_ip
    }
  }
  
  # Execute on local machine
  provisioner "local-exec" {
    command = "echo ${self.public_ip} >> inventory.txt"
  }
  
  # Copy files to remote
  provisioner "file" {
    source      = "app/"
    destination = "/home/ubuntu/app"
    
    connection {
      type        = "ssh"
      user        = "ubuntu"
      private_key = file("~/.ssh/id_rsa")
      host        = self.public_ip
    }
  }
}
```

> ⚠️ **Best Practice:** Use provisioners as a last resort. Prefer:
> - Cloud-init / user_data for EC2
> - Configuration management tools (Ansible)
> - Pre-built AMIs (Packer)

---

## 📋 Commands Reference

### Core Commands

```bash
# Initialize working directory
terraform init

# Preview changes
terraform plan

# Apply changes
terraform apply
terraform apply -auto-approve     # Skip confirmation

# Destroy infrastructure
terraform destroy
terraform destroy -auto-approve

# Show current state
terraform show
terraform show -json

# Format configuration files
terraform fmt

# Validate configuration
terraform validate
```

### State Commands

```bash
# List resources in state
terraform state list

# Show specific resource
terraform state show aws_instance.web

# Move resource in state
terraform state mv aws_instance.old aws_instance.new

# Remove resource from state (doesn't destroy)
terraform state rm aws_instance.web

# Pull remote state
terraform state pull

# Push state (dangerous!)
terraform state push
```

### Other Useful Commands

```bash
# Show outputs
terraform output
terraform output instance_ip

# Show providers
terraform providers

# Import existing infrastructure
terraform import aws_instance.web i-1234567890abcdef0

# Create dependency graph
terraform graph | dot -Tsvg > graph.svg

# Refresh state
terraform apply -refresh-only

# Plan without refresh
terraform plan -refresh=false

# Show version
terraform version
```

### Quick Reference

| Command | Description |
|:--------|:------------|
| `terraform init` | Initialize working directory |
| `terraform plan` | Preview changes |
| `terraform apply` | Apply changes |
| `terraform destroy` | Destroy infrastructure |
| `terraform fmt` | Format code |
| `terraform validate` | Validate configuration |
| `terraform output` | Show outputs |
| `terraform state list` | List state resources |
| `terraform import` | Import existing resources |

---

## 📚 Additional Resources

| Resource | Link |
|:---------|:-----|
| Terraform Docs | [terraform.io/docs](https://www.terraform.io/docs) |
| Terraform Registry | [registry.terraform.io](https://registry.terraform.io/) |
| HashiCorp Learn | [learn.hashicorp.com/terraform](https://learn.hashicorp.com/terraform) |
| AWS Provider | [registry.terraform.io/providers/hashicorp/aws](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |

---

<div align="center">

## 🚀 Ready to Continue?

**[← Back to Main](../README.md)** | **[Kubernetes →](../Kubernetes-Concept/README.md)** | **[Helm →](../Helm-Concept/README.md)**

---

*"Infrastructure as Code is the practice of treating infrastructure the same way developers treat code."*

</div>

```
:::Personal Notes:::
Objective:
	Intro IaC:
	Types of Iac:
	Why Terraform:
	HCL Basics:
	Provision update and Destroy:
	Providers:
	Input Variables:
	Output Variables:
	Resource Attributes:
	Resource Dependencies:
	Terraform State:
	Commands:
	Mutable Vs Immutable:
	Lifecycle Rules:
	Datasources:
	Meta-arguments:
	count:
	for-each:
	version constraints:
	AWS Basics
		Programmatic Access, IAM, ec2, S3, DynamoDB
	
	Remote State:
	State Locking:
	Remote Backend with s3:
	State Commands
	Provisioners
	
	Terraform Taints:
	Debugging
	Terraform import
	Modules
	Functions
	Conditional Expression
	Workspaces
	Terraform cloud
	
====
::Tradational Infra Model::
Business(Req for app) >> 
Busibess Analyst(Gather needsa and analyze it, convert into high level technical req) >>  
Solution Architect/Technical Lead(desigh architrct for the deploy of app, include type spec and count of server) >> 
Infrastructure Team
	Field Engineers(rack and stack of equipment),
	System/NW Admins(perform initial config)(make system avaliable on the network),
	Storage Admins(asssign storage tot he servers), 
	Backup Admins(Backup), 
	Application Team(To deploy the app in those servers)
Drawback:
Time, Human error, not easy to sclae up down, cost high, inconsist in env, wasted resource,

Now Infra is taking care of Cloud(AWS, AZURE, GCP)
only two drawbacks Human Error, Inconsisty
to slove this use different approach; >> shell, Python, ruby, perl, powershell
====
:::IaC:::
Brodly divide into 3 types:
1. Configuration Managment : Ansible, Puppet, SALTSTACK,
	Design to install and manage software
	maintains standard structure
	version control
	idempotent
2. Server Templating: Docker Hashicorp Packer, Hashicorp Vagrant
	used to create a custom image of a VM or a container
	preinstalled software and dependencies
	immutable infrastructure
3. Provisioning Tools: Hashicorp Terraform, Cloudformation
	Deploy immutable infra resource 
	servers, databases, network comp tec..,
	multiple providers
====
Why Terraform??
	simple declarative lang(The code we define want to be infra struct in)(currrent state)
		
		
	support multiple cloud providers (include on-premis vSphere cluster), 
	Free open source, 
	install as single binary, setup very fast, execution(build, manage, destroy)infra also very fast
	
Works:
	Declarative >> take care of what is req, to go from current state to the desired state.
	3 phases: init, plan, apply;
	init  ==> initilize the project and identify the providers to be used for target env.
	plan ==> draft the plan to the target stage.
	apply ==> make necessary changes req on the target env to bring ot to desired state.
		(if some reason env shift from the desired state then a sebsequent terraform apply will bring back to desired state. by only fixing the missing comp)
resourece, 
lifecycle

statefile is a blue print
	mappinf congif to real world, tracking of metadata, performance, collaboration
====
conf Dir:
	statefiles;
	data from configuration files(use to provision and manage infra);
	main.tf, variables.tf, outputs.tf, provider.tf
	
best way: Statefile(Single source of truth) keep it in remote!! 
	Non-optional feature in terraform
====
if you do any changes in files(Infra) and run terraform apply, firstly it will delete old and create a new one
Reason:-
	It follows 'immutable'
what if you want to chage those steps, 
"Lifecycle Rules": comes into the picture,
	create first and then delete ==> lifecycle { create_before_destroy = true}
	create only no delete ==> lifecycle {prevent_destroy = true }
	ignore changes ==> lifecycle{ ignore_changes = all or [ tags,... ] }
<terraform destory will destory, it dosent prevent destroy>
====
Data Sources:
	allow terraform to read attribute from resources which are provision outside its control,
	syntax:- data "XX" "XX" { ... } simply instead of 'resource' use 'data'
A data source once created, can be used to create, update, and destroy infrastructure ==> False
===
Meta-arguments in terraform:
	used within any resource block to change behaviour of resources,
	ex:- depends_on, lifecycle, count, length, for_each, toset(),
===
Remote state
if youn run terraform apply at same time in 2 different(State lock) 
once done by one goes to next
not good to store in github (contains sensitive data, what if forget to push/pull latest, only one person has to update(not support Statelock))
so we use remote backend (S3, DynamoDB)
	Automatically load and upload state file, 
	may backends supports state locking
	security
s3 bucket & dynamoDb table to configure a remote backend for terraform config
S3 ==> to store Terraform state, 
DynamoDB ==> State Locking & consisty checks.
=====

Provisiioners









:::CMD:::
Terraform follows an immutable infrastructure approach, the file was recreated although the contents are the same.
terrafrom init ==>
terraform plan ==> 
terraform apply ==> 
terraform show -json ==>
terraform output/ terraform output <name/arg> ==>
terraform plan --refresh=false
terraform apply -refresh-only
terraform validate ==>
terraform fmt ==> 
terraform providers ==> 
terraform providers mirror <path> ==>
terraform graph | dot -Tsvg > graph.svg

State Commands:
terraform state <subcmd> [options] [args]
subcmd: list, mv, pull, rm, show

```
