
# Automated Cloud Deployment with Terraform, Ansible, Docker, and GitHub Actions

## Overview
This project demonstrates an automated deployment pipeline for a cloud-based application on an Azure Virtual Machine (VM). Utilizing tools like Terraform, Ansible, Docker, and GitHub Actions, it provides an efficient, reproducible environment setup and deployment process, ensuring that each component of the infrastructure and application is automated for consistency and reliability.

## Project Structure
- Terraform**: Infrastructure as Code (IaC) to provision and configure the Azure VM and necessary networking.
- Ansible**: Configuration management to install Docker on the VM and ensure it runs on boot.
- Docker**: Containerization of the sample application (`app.py`), providing a consistent runtime environment.
- GitHub Actions**: CI/CD pipeline to build and deploy the Docker container to the Azure VM upon code changes.

## Setup and Deployment

1. Provision Infrastructure with Terraform
Navigate to the Terraform directory and run the following commands:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```
After deployment, retrieve the public IP of the Azure VM to update the Ansible inventory file.

2. Configure Server with Ansible
In the Ansible directory, update `inventory.ini` with the new IP address from the Terraform output. Then run:
   ```bash
   ansible-playbook -i inventory.ini docker-setup.yml
   ```
This playbook installs Docker and configures the VM environment.

3. Containerize the Application with Docker
A Dockerfile is included to build a container image of the sample application. Once the Docker container is created and running on the VM, the application is accessible through the public IP on the specified port.

4. Set Up CI/CD Pipeline with GitHub Actions
The GitHub Actions workflow (`.github/workflows/deploy.yml`) automatically builds and deploys the application upon code push to the main branch. It compresses the application code, transfers it to the VM, and deploys the Docker container.

## Prerequisites
- Azure account with access rights to create resources
- SSH key configured for VM access
- Docker and Ansible installed on the local machine
- GitHub repository with GitHub Actions enabled

## Directory Structure

├── terraform/               # Terraform scripts for provisioning
├── ansible/                 # Ansible playbooks and inventory
├── app/                     # Application code and Dockerfile
└── .github/workflows/       # GitHub Actions CI/CD pipeline


## Usage
1. Run Terraform scripts to provision the VM.
2. Update Ansible inventory and configure the VM.
3. Use GitHub Actions for automated deployment.
4. Access the app via `http://<vm_public_ip>:<port>`.