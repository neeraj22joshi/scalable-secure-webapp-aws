# Auto-Scalable Web Hosting Platform with Nginx on AWS

---

## Project Overview

This project demonstrates how to build a **highly available**, **auto-scalable** web hosting environment on AWS using **Nginx**.  
It leverages core AWS services including EC2, Auto Scaling Group, Application Load Balancer, and AWS WAF for security.

---

## Repository Structure

<img width="603" height="169" alt="image" src="https://github.com/user-attachments/assets/03501d8b-daef-4ef7-8cd6-f1efb0d1cfee" />

---

## Key Components

- **Ubuntu EC2 Instance:** Base instance with Nginx installed and configured via user-data script.
- **Custom AMI:** Created from the configured EC2 instance to ensure consistent deployments.
- **Launch Template:** Defines instance configurations using the custom AMI.
- **Auto Scaling Group (ASG):** Automatically scales EC2 instances based on demand.
- **Application Load Balancer (ALB):** Distributes incoming HTTP/HTTPS traffic to healthy instances.
- **AWS WAF:** Protects the ALB from malicious traffic and bots.

---

## Quick Start

1. Launch an Ubuntu EC2 instance using the user-data script located at `user-data/nginx-install.sh` to install and configure Nginx automatically.
2. Create a custom AMI from this instance (`docs/ami-creation.md`).
3. Configure the Launch Template and Auto Scaling Group with the custom AMI, targeting your desired capacity and scaling policies (`docs/asg-setup.md`).
4. Set up an Application Load Balancer and integrate it with your ASG (`docs/alb-config.md`).
5. Enable AWS WAF to secure your environment (`docs/waf-setup.md`).
6. Access your web application via the ALB DNS name to verify functionality.

---

## User-Data Script (nginx-install.sh)

The user-data script automates the installation and setup of Nginx on an Ubuntu EC2 instance. It:

- Updates package lists and upgrades installed packages.
- Installs Nginx.
- Starts and enables Nginx service.
- Configures the firewall to allow HTTP and HTTPS traffic.
- Creates a sample web page.

---

Happy scaling with AWS and Nginx! 🚀
