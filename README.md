# Jenkins Pipeline Setup on AWS EC2 with Docker

This project demonstrates a complete end-to-end setup of **Jenkins Pipeline** on an **AWS EC2 Ubuntu instance**, integrated with **GitHub (SCM)** and **Docker**.  
All steps, commands, and a sample `Jenkinsfile` are included in this single file.

---

## Architecture Overview
- AWS EC2 (Ubuntu)
- Jenkins
- GitHub (SCM)
- Docker
- Jenkins Pipeline (Jenkinsfile)

---

## Prerequisites
- AWS account
- Ubuntu EC2 instance
- GitHub account
- Basic understanding of Linux, Git, and CI/CD

---

## Step 1: Create EC2 Instance
- Launch an **Ubuntu** EC2 instance
- Instance type: `t2.micro` (Free Tier)
- Create or select a key pair
- Assign a security group (rules added later)

---

## Step 2: Install Java (JDK & JRE)
Jenkins requires Java to run.

```bash
sudo apt update
sudo apt install openjdk-17-jre
java --version
