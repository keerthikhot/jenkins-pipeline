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
```

---

## step 3: Install Jenkins on EC2
```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
Start and enable Jenkins:
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
---

## Step 4: Configure Security Group (Inbound Rules)
| Port | Purpose    |
| ---- | ---------- |
| 22   | SSH        |
| 8080 | Jenkins UI |
| 80   | HTTP       |

---

## Step 5: Jenkins Initial Setup
1) Open Jenkins in browser
2) Get initial admin password
3) Install Suggested Plugins
4) Create Jenkins admin user
5) install docker pipeline plugin

---

## Step 6: Install Docker on EC2
```bash
sudo apt update
sudo apt install docker.io
```
Add Jenkins and Ubuntu users to Docker group:
```bash
sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
---

## Step 7: Create Jenkinsfile and Push to GitHub
```bash
git clone <repository-url>
cd <repository-name>
git status
git add Jenkinsfile
git commit -m "Add Jenkins pipeline"
git push origin main
```

---

## Step 8: Create Jenkins Pipeline Using SCM
1) Jenkins Dashboard → New Item
2) Select Pipeline
3) Under Pipeline Definition, choose:
   Pipeline script from SCM
4) Configure:
  SCM: Git
  Repository URL: GitHub repository URL
  Branch: main
  Script Path: Jenkinsfile
  Save → Click Build Now

---

## Result
Jenkins pulls the Jenkinsfile from GitHub (SCM)
A Docker container is created
Pipeline stages execute
Docker container stops after execution

<img width="1231" height="526" alt="Screenshot 2025-12-14 at 12 45 54 PM" src="https://github.com/user-attachments/assets/1a578dd7-6ab1-4939-9a6c-22e91fcec309" />


<img width="923" height="97" alt="Screenshot 2025-12-14 at 1 02 50 PM" src="https://github.com/user-attachments/assets/6e88e564-08d2-4466-a4f3-d08932534107" />

