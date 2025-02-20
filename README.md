# Infrastructure as Code with Terraform and Ansible

## Overview

This project documents my journey into Infrastructure as Code (IaC), using **Terraform** and **Ansible** to automate and manage cloud infrastructure. I learned how to create, manage, and provision infrastructure on AWS, leveraging the power of these amazing tools!

<h2 align="center">💻Technologies used</h2>
<p align="center">
   <a href="https://www.terraform.io/" target="_blank"><img alt="Terraform" src="https://img.shields.io/badge/Terraform-1.x-purple?logo=terraform"></a>
   <a href="https://www.ansible.com/" target="_blank"><img alt="Ansible" src="https://img.shields.io/badge/Ansible-2.x-red?logo=ansible"></a>
   <a href="https://aws.amazon.com/" target="_blank"><img alt="AWS" src="https://img.shields.io/badge/AWS-EC2-orange?logo=amazon-aws"></a>
</p>

## Objectives

- **Master Infrastructure as Code (IaC)**: Understand how to define, provision, and manage cloud infrastructure.
- **Hands-On Experience**: Create and configure AWS EC2 instances using Terraform and Ansible.
- **Automation and Efficiency**: Automate configuration management and infrastructure provisioning.

## Key Learning Areas

- **Terraform Basics**: Creating and managing infrastructure resources on AWS.
- **Ansible Playbooks**: Automating configuration, software installation, and file modifications.
- **AWS EC2**: Understanding virtual machines, SSH connections, and secure configurations.

## Getting Started with Terraform

Here’s a step-by-step guide to initialize and apply Terraform to create your infrastructure!

### 1️⃣ Prerequisites

- AWS account with IAM user credentials.
- AWS CLI installed and configured.
- Terraform installed.
- SSH key pair generated and available for your EC2 instance.

👉 **Generate SSH Key Pair:**
```bash
ssh-keygen -t rsa -b 2048 -f my-terraform-key
```
Move the private key to your Terraform directory:
```bash
mv my-terraform-key ~/.ssh/
chmod 400 ~/.ssh/my-terraform-key
```

👉 **Configure AWS CLI:**
```bash
aws configure
```
Provide your access key, secret key, region, and output format.

### 2️⃣ Create Terraform Configuration Files

- `main.tf`: Define your infrastructure resources (EC2, security groups, etc.).
- `variables.tf`: Manage dynamic inputs like AWS region, instance type, and key pair.
- `outputs.tf`: Capture and display important values (e.g., public IP of the instance).

👉 **Example of a basic EC2 instance definition:**
```hcl
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_pair
}
```

### 3️⃣ Initialize Terraform

👉 **Initialize your working directory:**
```bash
terraform init
```
✅ This command downloads and installs the necessary providers and sets up the Terraform backend.

### 4️⃣ Plan the Deployment

👉 **Preview the changes Terraform will apply:**
```bash
terraform plan
```
✅ This shows what resources will be created, modified, or destroyed without applying any changes.

### 5️⃣ Apply the Configuration

👉 **Create your infrastructure:**
```bash
terraform apply
```
✅ Terraform prompts for confirmation before creating resources.

### 6️⃣ Security Group Configuration

👉 **Allow SSH access:**
Ensure that your AWS security group allows inbound connections on port 22 for SSH:
```hcl
ingress {
  from_port   = 22
  to_port     = 22
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0", "::/0"]
}
```

## Ansible Playbook

Once the EC2 instance is up and running, you can use **Ansible** to automate provisioning!

👉 **Example Ansible playbook:**
```yaml
- name: Setup EC2 Instance
  hosts: all
  become: yes
  tasks:
    - name: Install required packages
      apt:
        name: ["nginx", "curl"]
        state: present

    - name: Create a new file
      copy:
        content: "Hello, Ansible!"
        dest: /home/ubuntu/hello.txt
```
✅ This playbook installs required packages, creates a file, and configures the EC2 instance.

## License

This project is licensed under the [MIT License](LICENSE).

---

✨ **Wrapping up:** With Terraform and Ansible, I learned how to automate infrastructure provisioning and configuration management, taking the first big step into the world of DevOps and Infrastructure as Code! Let’s build more! 🚀
