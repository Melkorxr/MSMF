# 🚀 MobSF Dynamic Analyzer for Android on Kali Linux

## Overview

MobSF Dynamic Analyzer is a feature of the Mobile Security Framework that enables runtime analysis of Android applications by executing them on an emulator or a physical device. Unlike static analysis, it observes the app’s behavior in real-time, capturing network traffic, monitoring system logs, tracking file system changes, and detecting suspicious activities such as permission abuse or use of sensitive APIs. It relies on ADB communication and may use tools like Frida for function hooking. This helps security testers uncover runtime vulnerabilities, hidden behaviors, and malicious operations that wouldn't be visible through code analysis alone.

## Tools

1. MobSF 
2. Genymotion
3. Socat

## Steps

#### 1. Download & Login Genymotion Dekstop for Kali Linux
You can read the installation guide on link below:

🔗 **https://docs.genymotion.com/desktop/Get_started/013_Linux_install/** 

After the installation you can run Genymotion on terminal with this command below.
```bash
cd /genymotion/

LIBGL_ALWAYS_SOFTWARE=1 ./genymotion
```
The command is used to launch Genymotion (an Android emulator) while forcing it to use software rendering instead of hardware (GPU) acceleration. This can be useful in environments where GPU drivers are incompatible, missing, or when running inside a virtual machine that doesn't support proper hardware acceleration.

#### 2. Create Device on Genymotion
This command fetches the official Docker GPG key and securely stores it for package verification.
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
#### 3. Run Socat & MobSF
Socat is used to create a TCP proxy that forwards traffic from a chosen port to port 6555 on localhost (This is crucial because, for some reason, my MobSF Analyzer consistently fails to connect to the ADB device—it always returns a "connection refused" error). The command I use to set up this TCP proxy with socat is as follows:
```bash
socat TCP-LISTEN:7555,fork TCP:127.0.0.1:6555

#For TCP-LISTEN, you can use any available port.
```
Now that Socat has been set up, we can run MobSF using the following command:
```bash
sudo docker run -it --rm --add-host=host.docker.internal:host-gateway -p 8000:8000 \
  -e MOBSF_ANALYZER_IDENTIFIER=host.docker.internal:7555 \
  opensecurity/mobile-security-framework-mobsf:latest
```
This Docker command is used to run the Mobile Security Framework (MobSF) for dynamic analysis. It launches the MobSF container in interactive mode and automatically removes it after use. The command maps the host machine's host.docker.internal to allow the container to communicate with services running outside of Docker, such as an Android emulator. It exposes port 8000 to provide access to the MobSF web interface and sets the MOBSF_ANALYZER_IDENTIFIER environment variable to direct MobSF to the ADB connection of the emulator (in this case, via Socat)

#### 4. Start Booting Emulator Device

```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```
#### 5. llll
Start the Docker service and enable it to automatically launch at system startup.
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
#### 6. Start Dynamic Analyzer for Android
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

### 🧑‍💻 Login Credentials Default
| **Username** | **Password** |
|:--------------|:-------------|
| `mobsf`        | `mobsf`      |

---

🎯 *This script ensures a smooth and secure MobSF installation. Happy testing!*

© Melkorxr 2025
