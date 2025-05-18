---
layout: default
title: "Unix/Linux Command Reference"
---

# 🧾 Unix/Linux Command Reference

## 📁 File Commands

```bash
ls                  # list directory contents
ls -al              # detailed list including hidden files
cd dir              # change directory to 'dir'
cd                  # go to home directory
pwd                 # show current directory
mkdir dir           # create a new directory named 'dir'
rm file             # delete file
rm -r dir           # delete directory recursively
rm -f file          # force delete file
rm -rf dir          # force delete directory recursively
cp file1 file2      # copy file1 to file2
cp -r dir1 dir2     # copy dir1 to dir2 (recursively)
mv file1 file2      # move or rename file1 to file2
ln -s file link     # create symbolic link 'link' to 'file'
touch file          # create or update file
cat > file          # write standard input into file
more file           # display file contents page by page
head file           # display first 10 lines of file
tail file           # display last 10 lines of file
tail -f file        # display content as it grows (log files)
````

---

## 🧠 Process Management

```bash
ps                  # list current processes
top                 # show all running processes
kill pid            # kill process with ID 'pid'
killall proc        # kill all processes named 'proc'
bg                  # resume job in background
fg                  # bring most recent job to foreground
fg n                # bring job number n to foreground
```

---

## 🔐 File Permissions

```bash
chmod 777 file      # read/write/execute for all
chmod 755 file      # rwx for owner, rx for group and others
```

* **Permission values:**

  * `4` – read (r)
  * `2` – write (w)
  * `1` – execute (x)

For more, run: `man chmod`

---

## 🔗 SSH

```bash
ssh user@host           # connect to remote host
ssh -p port user@host   # connect using specific port
ssh-copy-id user@host   # copy SSH key for passwordless login
```

---

## 🔍 Searching

```bash
grep pattern file           # search for pattern in file
grep -r pattern dir         # recursive search in directory
command | grep pattern      # filter command output
locate file                 # find file by name
```

---

## 🖥️ System Information

```bash
date                        # show date/time
cal                         # show calendar
uptime                      # system uptime
w                           # who is online
whoami                      # current username
finger user                 # user info
uname -a                    # kernel info
cat /proc/cpuinfo           # CPU details
cat /proc/meminfo           # memory details
man command                 # manual for command
df                          # disk usage
du                          # directory space usage
free                        # memory and swap usage
whereis app                 # app location
which app                   # shows which app will run
```

---

## 📦 Compression

```bash
tar cf file.tar files       # create tar archive
tar xf file.tar             # extract tar archive
tar czf file.tar.gz files   # create gzip compressed tar
tar xzf file.tar.gz         # extract gzip tar
tar cjf file.tar.bz2 files  # create bzip2 compressed tar
tar xjf file.tar.bz2        # extract bzip2 tar
gzip file                   # compress file to .gz
gzip -d file.gz             # decompress .gz file
```

---

## 🌐 Networking

```bash
ping host                   # check connectivity
whois domain                # domain info
dig domain                  # DNS info
dig -x host                 # reverse DNS lookup
wget file                   # download file
wget -c file                # resume download
```

---

## 📥 Installation

```bash
./configure                 # configure from source
make                        # compile
make install                # install compiled app

dpkg -i pkg.deb             # install .deb package (Debian)
rpm -Uvh pkg.rpm            # install .rpm package (RPM)
```

---

## ⌨️ Keyboard Shortcuts

```bash
Ctrl+C      # cancel current command
Ctrl+Z      # suspend command
Ctrl+D      # logout / end session
Ctrl+W      # delete one word
Ctrl+U      # delete whole line
Ctrl+R      # reverse search in history
!!          # repeat last command
exit        # exit session
```

> ⚠️ Use commands like `rm -rf` and `killall` with **extreme caution**!

---

