# AWS Infrastructure Provisioning (Terraform + Ansible)

![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/ansible-%23990000.svg?style=for-the-badge&logo=ansible&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

Infrastructure provisioning and configuration management project using **Terraform (IaaS)** and **Ansible**.
## Project Objective

The goal is to implement **Infrastructure as Code (IaC)** to ensure reproducibility and speed of deployment. By replacing manual console actions with Terraform and Ansible, the infrastructure becomes version-controlled, enabling rapid disaster recovery and eliminating human configuration errors.

### Technical Comparison: PaaS vs. IaaS

| Feature | Elastic Beanstalk (PaaS) | Terraform + Ansible (IaaS) |
| :--- | :--- | :--- |
| **Execution Speed** | **Slow.** Initial setup and updates involve waiting for platform events and health checks. | **Fast.** Terraform interacts directly with the AWS API, spawning instances and networks immediately without platform overhead. |
| **Disaster Recovery** | **Manual.** Restoring a corrupted environment often requires manual reconfiguration through the UI and increases downtime. | **Automated.** The entire infrastructure is defined in code, allowing the exact setup to be destroyed and rebuilt in minutes. |
| **Infrastructure Visibility** | **Abstracted.** AWS automatically orchestrates resources (LBs, ASGs) behind the scenes. | **Explicit.** Every component (subnet, firewall rule, instance) is strictly defined in code, ensuring full transparency of the architecture. |
| **Configuration Method** | **Proprietary.** Advanced OS tuning requires AWS-specific configuration files (`.ebextensions`) which are hard to test locally. | **Standardized.** Ansible uses universal, readable modules that can be verified on local containers or VMs before deployment. |

## Technology Stack

* **Provisioning:** Terraform
* **Configuration:** Ansible
* **Cloud Provider:** AWS

## Key Features

* **Dynamic Inventory Generation:** Terraform automatically extracts the Public IPs of created instances and generates an `inventory.ini` file for Ansible.
* **Security Automation:** The script detects the deployer's public IP and restricts SSH access in the AWS Security Group to that specific IP only.
* **Modular Ansible Roles:**
    * `docker`: Installs system dependencies, sets up the Docker daemon, and configures user permissions.
    * `webapp`: Clones the project repository and executes the container startup sequence.

## Prerequisites

Before running the project, ensure you have the following installed:

* **AWS CLI** (configured with credentials)
* **Terraform**
* **Ansible**
* **SSH Key Pair** (generated and available in `~/.ssh/`)

## Deployment Workflow

**1. Clone the repository**
```bash
git clone https://github.com/KurosuSama/aws-terraform-ansible.git
cd aws-terraform-ansible/terraform
```
**2. Provision Infrastructure (Terraform) Initialize the provider, preview the changes, and apply the configuration to AWS**
```bash
terraform init
terraform plan
terraform apply
```
**3. Configure Servers (Ansible) Navigate to the ansible directory and execute the playbook**
```
cd ../ansible
ansible-playbook playbook.yml
```
