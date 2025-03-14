# 🚀 MobSF Installation Script for Kali Linux

## Overview

The **Mobile Security Framework (MobSF)** is an open-source tool designed for
automated static and dynamic analysis of mobile applications. It supports
Android, iOS, and Windows platforms, making it an essential tool for mobile
app security testing. MobSF simplifies the process of analyzing application
code, identifying security vulnerabilities, and ensuring app security best
practices are followed. This script aims to provide a streamlined and
hassle-free installation process for MobSF on Kali Linux using Docker. By
following the steps below, you can quickly set up a secure and efficient
environment for mobile application security assessments.

## Features

✅ Automated installation  
✅ Safe and efficient setup  
✅ Easy-to-use script  

## Installation Steps

#### 1. Add Docker Repository
Add Docker's official repository to your system to ensure you get the latest and trusted Docker packages.
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/debian bullseye stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
#### 2. Download and Save Docker GPG Key
This command fetches the official Docker GPG key and securely stores it for package verification.
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
#### 3. Update System
Update your system's package index to ensure all repositories are refreshed.
```bash
sudo apt update
```
#### 4. Install Docker
Installs Docker and its required components for container management.
```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```
#### 5. Start and Enable Docker
Start the Docker service and enable it to automatically launch at system startup.
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
#### 6. Download MobSF
Download the latest MobSF Docker image to prepare for the analysis environment.
```bash
sudo docker pull opensecurity/mobile-security-framework-mobsf:latest
```
#### 7. Run MobSF
Run the MobSF container on port 8000, accessible from your browser.
```bash
sudo docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

## 🌐 Access MobSF

Once the installation is complete, you can access MobSF by visiting:  
🔗 **[http://localhost:8000](http://localhost:8000)**  

### 🧑‍💻 Login Credentials
| **Username** | **Password** |
|:--------------|:-------------|
| `mobsf`        | `mobsf`      |

---

🎯 *This script ensures a smooth and secure MobSF installation. Happy testing!*

© 2025
