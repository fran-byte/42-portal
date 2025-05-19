---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Preliminary Fundamentals (before tackling Born2BeRoot)

### 📌 Objective:

Have **all the technical and conceptual tools** necessary to configure and secure a Debian virtual machine **with confidence**, avoiding common mistakes and understanding **what you are doing and why**.

---

### 🛠️ Creation and Configuration of the Virtual Machine

#### ✅ Download Debian ISO and Install VirtualBox

1. **Download Debian ISO**: Click here
2. **Download VirtualBox**: Click here

#### 🔧 Creating the Virtual Machine

1. Open VirtualBox and create a new virtual machine.
2. Configure the virtual machine in the **sgoinfre** directory.
3. Select the amount of RAM.
4. Create a dynamically allocated virtual hard disk (VDI).
5. Select the Debian ISO and start the installation.

---

### 🧱 Installing Debian on the VM

1. Select language, time zone, and country.
2. Create a hostname and password for the machine.
3. Create a first user and their password.
4. Configure the machine's partitions using LVM (Logical Volume Manager).

#### 🧪 What is LVM?

LVM allows you to create, resize, or delete partitions dynamically from the command line while the system is running, without needing to reboot.

---

### 📦 Configuration of the Virtual Machine

#### 🛠️ Package Management

1. **aptitude**: Remembers which packages were explicitly requested and automatically uninstalls packages that are no longer needed.
2. **apt**: Executes exactly what is indicated in the command line.

#### 🔒 Security

1. **APPArmor**: Security system that provides mandatory access control.
2. **SSH (Secure Shell)**: Allows secure management of Linux servers.
3. **UFW (Uncomplicated Firewall)**: Firewall configuration to protect the network, leaving only port 4242 open.
4. **Password Policy**: Rules to improve password security, including expiration every 30 days and complexity requirements.

---

### 📚 Groups and Users

1. **root and sudo**: Use `sudo` to grant temporary administrator permissions without logging in as root.
2. **Crontab**: Use `cron` to automatically execute scripts at predefined intervals.

---

### 🧬 Monitoring Script

#### ✅ Script Description

A Bash script that collects system information, such as architecture, physical and virtual cores, memory and disk usage, CPU usage percentage, last reboot, LVM usage, TCP connections, logged-in users, IP and MAC address, and the number of commands executed with `sudo`.

#### 🧪 Script Example

```bash
#!/bin/bash
# O.S. ARCHITECTURE
architecture=$(uname -a)
# PHYSICAL CPU identifier
cpu_phy=$(grep "physical id" /proc/cpuinfo | wc -l)
# Number of virtual processors (vCPUs)
vcpus=$(grep "processor" /proc/cpuinfo | wc -l)
# MEMORY RAM
total_memory=$(free --mega | awk '$1 == "Mem:" {print $2}')
used_memory=$(free --mega | awk '$1 == "Mem:" {print $3}')
memory_usage_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
# DISK
total_disk_space=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')
used_disk_space=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
disk_usage_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t += $2} END {printf("%d"), disk_u/disk_t*100}')
# CPU load
inactive_cpu=$(vmstat 1 2 | tail -1 | awk '{printf $15}')
cpu_usage=$(expr 100 - $inactive_cpu)
formatted_cpu=$(printf "%.1f" $cpu_usage)
# LAST BOOT
last_boot=$(who -b | awk '$1 == "system" {print $3 " " $4}')
# LVM USE
lvm_use=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)
# TCP CONNECTIONS
tcp_connections=$(ss -ta | grep ESTAB | wc -l)
# USER LOG
user_log=$(users | wc -w)
# NETWORK
ip_net=$(hostname -I)
mac=$(ip link | grep "link/ether" | awk '{print $2}')
# SUDO COMMANDS
sudo_commands=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
# Wall message
wall "\t# Architecture: $architecture\n\t# CPU physical: $cpu_phy\n\t# vCPU: $vcpus\n\t# Memory Usage: $used_memory/${total_memory}MB ($memory_usage_percent%)\n\t# Disk Usage: $used_disk_space/${total_disk_space} ($disk_usage_percent%)\n\t# CPU load: $formatted_cpu%\n\t# Last boot: $last_boot\n\t# LVM use: $lvm_use\n\t# TCP Connections: $tcp_connections ESTABLISHED\n\t# User log: $user_log\n\t# Network: IP $ip_net ($mac)\n\t# Sudo: $sudo_commands cmd"
```

---

### 🧾 Crontab

#### ✅ Crontab Configuration

Publish a message every 10 minutes using `cron`.

```bash
sudo crontab -u root -e
```

Crontab Format:

- **m** Minute of execution (0-59).
- **h** Hour of execution (0-23).
- **dom** Day of the month (you can specify a day, like 15).
- **dow** Day of the week (0-7, where 0 and 7 are Sunday) or the first three letters of the day in English: mon, tue, wed, thu, fri, sat, sun.
- **user** User executing the command (root or another with permissions).
- **command** Command or absolute path of the script to execute.

---

### 📜 Signature.txt

#### ✅ Generating the Signature

Use `shasum` to obtain the signature of the virtual machine and upload it to the repository.

```bash
shasum nombremaquina.vdi
```

---

### 🧠 Evaluation

#### ✅ Evaluation Questions

1. **What is a virtual machine?**
2. **Why did you choose Debian?**
3. **Basic differences between Rocky and Debian**
4. **Purpose of virtual machines**
5. **Differences between apt and aptitude**
6. **What is APPArmor?**
7. **What is LVM?**

#### ✅ Evaluation Commands

1. **Verify graphical interfaces in use:** `ls /usr/bin/*session`
2. **Check UFW service status:** `sudo ufw status`
3. **Check SSH service status:** `sudo service ssh status`
4. **Verify operating system (Debian or CentOS):** `uname -v` or `uname --kernel-version`
5. **Verify membership in "sudo" and "user42" groups:** `getent group sudo` and `getent group user42`
6. **Create new user with password policy:** `sudo adduser name_user`
7. **Create "evaluating" group:** `sudo addgroup evaluating`
8. **Add user to the group:** `sudo adduser name_user evaluating`
9. **Check hostname:** `hostname`
10. **Change hostname:** Edit `/etc/hostname` and `/etc/hosts`
11. **Check partitions:** `lsblk`
12. **Verify if sudo is installed:** `which sudo` or `dpkg -s sudo`
13. **Add new user to sudo group:** `sudo adduser name_user sudo`
14. **Show application of sudo rules.**
15. **Verify existence of /var/log/sudo/:** Check that it contains at least one file of command history used with sudo.
16. **Verify installation and status of UFW:** `dpkg -s ufw` and `sudo service ufw status`
17. **List active rules in UFW:** `sudo ufw status numbered`
18. **Create and delete rule for port 8080:** `sudo ufw allow 8080` and `sudo ufw delete num_rule`
19. **Check SSH status and port 4242:** `which ssh` and `sudo service ssh status`
20. **Log in with the new user via SSH:** `ssh newuser@localhost -p 4242`

---

