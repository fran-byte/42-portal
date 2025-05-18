---
layout: default
title: "fran-byte 42 Madrid"
---

# 🔐 Born2beroot — A Guide to Tackle the Project with Confidence

## 🔹 1. Prerequisites (Before You Begin)

### 📌 Objective:

To gain a clear understanding of **how a Linux system works**, its basic security configurations, and how to document and defend your work during the evaluation.

---

### 🧰 Essential Tools

#### ✅ VirtualBox or UTM

* **Create a virtual machine** with Debian (or Rocky Linux).
* Make sure to use the **official configurations** (RAM, CPU, disk size).

#### ✅ Debian (recommended)

* Familiarize yourself with commands like: `apt`, `sudo`, `adduser`, `passwd`, `ufw`, `hostname`, `crontab`, `systemctl`, `auditd`.

#### ✅ Markdown and Word

* You’ll need to **document everything** in a `.md` or `.pdf` file.
* You must explain **what you did and why** (this is crucial for your defense).

---

## 🔹 2. Project Requirements Checklist

### 🖥️ 1. VM Configuration

* Debian or Rocky Linux (depending on what's allowed at your campus).
* The hostname must follow this pattern: `login42`.
* User: `login`, correctly added to the `sudo` group.

---

### 🔒 2. Password Security

* Passwords must include:

  * At least 10 characters
  * 1 uppercase, 1 lowercase, 1 digit
* Expiration policy: max 30 days
* 3 failed login attempts → temporary account lock

You achieve this by configuring:

* `/etc/login.defs`
* `/etc/pam.d/common-password` (using `pam_pwquality.so`)
* The `chage` command

---

### 🧑‍💻 3. Sudo

* You must install and configure `sudo`.
* Only users in the `sudo` group can use it.
* You must **audit every use of `sudo`**.

---

### 🧾 4. Cron Jobs

* Create a **cron job** to:

  * Send a disk usage report every 10 minutes to a file in `/var/log/`
* Use `crontab -e` or edit `/etc/crontab`.

---

### 📜 5. Hostname and UFW

* Change the hostname using: `hostnamectl set-hostname login42`
* Configure **UFW** (the firewall) to allow only SSH (port 22) and optionally HTTP (port 80).

---

### 🧠 6. Custom Scripts

* Create a script called `monitoring.sh`:

  * It should display: disk usage, memory, CPU, number of users, IP addresses, etc.
  * It must be executed at system startup using a cron job or systemd.

---

### 📦 7. Active Services

* `ssh` must be active and working.
* Other services must be **kept to a minimum and controlled** (`systemctl` and `ss` help verify this).

---

## 🔹 3. Step-by-Step Action Plan

### Step 1: Properly Set Up the VM

* Choose the OS allowed by your campus
* Allocate the required RAM and disk space
* Set up the user and password correctly

### Step 2: Apply Security Policies

* Use `passwd`, `chage`, `login.defs`, and `pam` to harden access
* Test with wrong passwords to ensure account locking works

### Step 3: Install and Configure `sudo`

* Ensure only your user has permissions
* Check logs in `/var/log/auth.log`

### Step 4: Create and Test the Monitoring Cron Job

* Ensure the script runs and logs are correctly saved

### Step 5: Document Everything

* Use Markdown or Word
* For each step: **explain what, how, and why**
* Include screenshots if possible

---

## 🔹 4. Defense Tips

* The evaluator may ask you to explain **how you configured each part**.
* They might break or alter something to see if you can fix it.
* They may ask you to:

  * Add a new user with proper security policies
  * Show `sudo` logs
  * Edit cron jobs live

---

## 🧠 Extra Advice

* **Take VM snapshots** before making major changes.
* **Test everything from scratch** at least once before submitting.
* Practice using `man`, `vim`, and `grep`.
* Use `bash -x script.sh` to debug your scripts.

---
