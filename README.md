# 🔐 Remote SSH and File Transfer: Windows 11 to Linux Server (VirtualBox Lab)

## 📘 Overview

This project demonstrates how to:
- Connect from a Windows 11 client to a Linux server via SSH
- Authenticate using both password and SSH key-pair methods
- Transfer files securely using `scp` (CLI) and `WinSCP` (GUI)

---

## 🎯 Objectives

- Set up OpenSSH on Ubuntu Server
- Connect from Windows 11 terminal using `ssh`
- Generate and use key-pair authentication to eliminate password prompts
- Perform file transfers between systems using SSH

---

## 🧰 Tools & Technologies

| Tool | Purpose |
|------|---------|
| VirtualBox | Virtual environment for Windows and Linux VMs |
| Windows 11 | SSH client host |
| Ubuntu Server 22.04+ | SSH server |
| OpenSSH | Secure remote shell & file transfer |

---

## 🧱 Lab Setup

### 🖥️ VM Network Configuration
- Get Linux VM's IP using:
  Terminal ==> ip add
<img width="741" alt="01-Get Linux Passworrd" src="https://github.com/user-attachments/assets/95d05c83-ada3-4d10-b6d5-8c24b66aafca" />




---

## 🔧 Step-by-Step Implementation

### ✅ Step 1: Enable and Start SSH on Ubuntu Server

- bash
    - sudo apt update
    - sudo apt install openssh-server -y
    - sudo systemctl enable ssh
    - sudo systemctl start ssh

- sudo ufw allow ssh  # if UFW is active
<img width="904" alt="03-Firewall allow" src="https://github.com/user-attachments/assets/83f060a9-14dd-4570-9863-2ca2d64189b3" />


- Verify SSH is running: 

  - sudo systemctl status ssh
<img width="901" alt="02-SSH Status" src="https://github.com/user-attachments/assets/e83d99b2-fe28-40c0-b2ea-bf4ef7d269f3" />

---

### ✅ Step 2: Connect from Windows 11 Using Password

Open PowerShell or CMD:

ssh username@linux_ip

Example: 
ssh adegboye@192.168.0.123

Login using your Linux account password.
<img width="1064" alt="01-Passowrd login successful" src="https://github.com/user-attachments/assets/56085f46-deeb-4147-a8fe-321775e2ff50" />

---

### ✅ Step 3: Set Up Key-Based Authentication

#### 📍 Step 3.1: Generate SSH Key Pair on Windows 11

```powershell
ssh-keygen
```

* Accept default location (`C:\Users\<YourName>\.ssh\id_rsa`)
* Press Enter for no passphrase (or enter one if preferred)

#### 📍 Step 3.2: Copy Public Key to Linux Server

```powershell
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh username@linux_ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys"
```

#### 📍 Step 3.3: Test Passwordless SSH

```cmd
ssh adegboye@192.168.0.123
```

You should log in without entering your password.

<img width="697" alt="05-login without password" src="https://github.com/user-attachments/assets/7360d760-7104-442b-b2bd-04b89d781175" />

---

## 📁 Step 4: File Transfer with SCP

### ⬆️ Copy from Windows to Linux

```powershell
scp C:\Users\YourName\Documents\report.txt username@linux_ip:/home/username/
```

### ⬇️ Copy from Linux to Windows

```powershell
scp username@linux_ip:/home/username/file.txt C:\Users\YourName\Downloads\
```

<img width="946" alt="06-file from Windows" src="https://github.com/user-attachments/assets/1e8a8127-86be-44e1-8211-1878df16f950" />

<img width="898" alt="07-File moved to Linux" src="https://github.com/user-attachments/assets/32d4e546-40a0-48e3-983c-ef1f969d881a" />

<img width="1027" alt="08-Copy Folder" src="https://github.com/user-attachments/assets/9f4da751-f074-4f7d-9c0e-55e816ca935f" />

<img width="894" alt="09-Folder in Linux" src="https://github.com/user-attachments/assets/5de59e1d-2db9-4dec-9678-17ba45857ad6" />

---

## 🧠 Skills Demonstrated

* SSH client/server setup
* Key-pair authentication and security best practices
* Secure file transfer using SCP
* Windows/Linux interoperability using native tools

---

## ✅ Final Outcome

A working remote shell and secure file transfer setup between Windows 11 and Ubuntu Server, enabling you to:

* Connect and manage Linux VMs without typing a password
* Transfer files quickly using secure protocols
* Simulate real-world remote support using different operating systems
---

## 🚀 Next Steps (Optional)

* Disable password authentication in `/etc/ssh/sshd_config` for stronger security:

  ```
  PasswordAuthentication no
  ```
* Install `fail2ban` for brute-force protection

---

## 📌 Notes

* Ensure both VMs are on the same network segment.
* Test connectivity with `ping linux_ip` from Windows.
* Adjust firewall settings if needed.

---

