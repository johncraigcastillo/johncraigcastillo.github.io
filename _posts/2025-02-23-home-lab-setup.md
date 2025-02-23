---
created: 2025-02-23T16:49
updated: 2025-02-23T16:54
tags:
  - homelab
  - cybersecurity
  - virtualization
layout: post
title: Building a Cybersecurity Home Lab with KVM/QEMU
date: 2025-02-23 17:51:00
description: Overview of my home lab setup
categories: cybersecurity journey
---
---
## 💻 Setting Up a Home Lab for Cybersecurity

I am beginning my journey into **cybersecurity**, and setting up a **home lab** is my first step toward hands-on learning. While I am not sure if this is the **definitive** setup, I am confident that it is enough to get me started. This guide is simply a **general breakdown of the steps I took** to set up my lab using **KVM/QEMU** for virtualization.

---

## 🛠️ Step 1 - Installing KVM/QEMU on Pop!_OS 22.04

To ensure efficient virtualization, I opted for **KVM/QEMU** over VirtualBox. Here’s how I set it up:

### 1️⃣ Check CPU Virtualization Support

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```

If the output is **1 or higher**, your CPU supports virtualization.

### 2️⃣ Install KVM/QEMU & Virt-Manager

```bash
sudo apt update && sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager
```

### 3️⃣ Enable and Start Libvirt Service

```bash
sudo systemctl enable --now libvirtd
```

### 4️⃣ Add User to Libvirt Group & Reboot

```bash
sudo usermod -aG libvirt $(whoami)
sudo reboot
```

### ✅ Verification Checklist

- [ ]  Verified CPU supports virtualization.
- [ ]  Installed KVM/QEMU and Virt-Manager.
- [ ]  Confirmed libvirt service is running (`sudo systemctl status libvirtd`).
- [ ]  Added user to `libvirt` group and rebooted.
- [ ]  Successfully launched `virt-manager`.

---

## 📌 Step 2 - Creating Virtual Machines

I set up two essential virtual machines for cybersecurity practice:

### 🖥️ Windows 10/11 VM (For Security Analysis & Active Directory)

✅ **Purpose:** Windows event logging, Active Directory, security monitoring. ✅ **Download:** [Windows 10 Enterprise Evaluation](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)

### 📖 Installation Steps

1. Open **Virt-Manager** and create a new VM.
2. Select **Local install media** and browse for the Windows 10 ISO.
3. Assign **4+ GB RAM, 2+ CPU cores**.
4. Create a **40GB+ virtual disk**.

### ✅ Verification Checklist

- [ ]  Windows VM installed successfully.
- [ ]  Splunk and Wireshark installed.
- [ ]  VirtIO drivers installed.
- [ ]  Active Directory simulation ready (if needed).

---

### 🐧 Kali Linux VM (For Penetration Testing & Offensive Security)

✅ **Purpose:** Ethical hacking, penetration testing, security research. ✅ **Download:** [Kali Linux](https://www.kali.org/get-kali/)

### 📖 Installation Steps

1. Create a new VM in **Virt-Manager**.
2. Select **Local install media** and choose the Kali Linux ISO.
3. Assign **4+ GB RAM, 2+ CPU cores**.
4. Create a **40GB+ virtual disk**.

### ✅ Verification Checklist

- [ ]  Kali Linux VM installed and updated.
- [ ]  Installed essential penetration testing tools (Metasploit, Nmap, etc.).
- [ ]  Verified network connectivity for security testing.

---

## 📌 Step 3: Test Your Home Lab Setup

### ✅ **Networking & Connectivity**

- [ ]  Windows and Linux VMs can **ping each other** (Test using `ping <IP Address>` in CMD or Terminal).
- [ ]  Both VMs have **internet access** (Check using `ping 8.8.8.8`).

_I am not doing the rest of step 3 because I have decided to learn more before I get into more testing. I can ping between the two VMs and I am happy with that at the moment. I'm still at step one when it comes to my knowledge. But I at least have the VMs set up._

---

## 🔹 Expanding the Home Lab

- **Active Directory Simulation**: Set up a Windows Server VM to practice attacks.
- **SIEM Expansion**: Install ELK Stack for deeper log analysis.
- **Pivoting/Networking**: Add a vulnerable Linux server for penetration testing exercises.

With this setup, my **home lab is ready** for hands-on cybersecurity training! 🚀 Stay tuned for more security research and learning experiences.