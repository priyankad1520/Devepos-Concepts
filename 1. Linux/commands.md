# Linux 

## What is Linux?
Linux is an **open-source operating system** 

used in:

* Servers
* Cloud computing
* DevOps
* Networking
* Cybersecurity
* Embedded systems
* Android phones

Most companies use Linux servers because it is: Fast, Secure, Stable, Free, Highly customizable

---

# Linux Architecture
![Image](https://images.openai.com/static-rsc-4/EiL1vXNJH3cD7rOCTPQTKC-6sbXAQEdMRQpuppUTEr_6SoSRgLONKbEQMuxy-li6BmMW1j_oDbowSNHo1jcgDDEKGQdouh2ioEV5ogyAoVadJ9JTPi-aWisprUyv8PAhuI4Uykek6bxK_-E5rsdZjQQryrdPm62gcWSaEOwevHBVSfTKg679qMqT9diXByLt?purpose=fullsize)


### Components

| Component        | Purpose                     |
| ---------------- | --------------------------- |
| Kernel           | Core of Linux OS            |
| Shell            | Command interpreter         |
| File System      | Organizes files/directories |
| Terminal         | Interface to run commands   |
| Services/Daemons | Background processes        |

---

# Important Linux Directories

```text
/        → Root directory
/home    → User files
/etc     → Configuration files
/var     → Logs and variable data
/tmp     → Temporary files
/bin     → Basic commands
/sbin    → System commands
/usr     → User applications
/opt     → Optional software
/dev     → Device files
/proc    → Process information
```

---

## Basic Linux Commands 

### **1. `pwd` — Print Working Directory**
Shows the current directory you are in.

```sh
$ pwd
/home/username
```

---

### **2. `ls` — List Directory Contents**
Lists files and folders in the current directory.

```sh
$ ls
Documents  downloads  pictures

$ ls -l    # Long listing with permissions, size, etc.
```

---

### **3. `cd` — Change Directory**
Navigates between directories.

```sh
$ cd Documents
$ cd /home/username/pictures
$ cd ..    # Go up one level
```

---

### **4. `cp` — Copy Files or Directories**
Copies files or directories.

```sh
$ cp file.txt /home/username/Documents/
$ cp -r dir1/ dir2/     # Copy entire directory
```

---

### **5. `mv` — Move or Rename Files/Directories**
Moves or renames files and directories.

```sh
$ mv oldname.txt newname.txt   # Rename file
$ mv file.txt /home/username/Desktop/   # Move file
```

---

### **6. `rm` — Remove Files or Directories**
Deletes files or directories.

```sh
$ rm file.txt
$ rm -r foldername    # Remove directory and contents
```

---

### **7. `touch` — Create Empty File or Update Timestamp**
Creates a new empty file.

```sh
$ touch newfile.txt
```

---

### **8. `cat` — Concatenate and Display File Content**
Displays content of a file.

```sh
$ cat file.txt
```

---

### **9. `echo` — Print to Screen**
Displays a line of text or variables.

```sh
$ echo "Hello, Linux!"
$ echo $HOME    # Print value of HOME variable
```

---

### **10. `mkdir` — Make Directory**
Creates a new folder.

```sh
$ mkdir newfolder
```

---

### **11. `rmdir` — Remove Empty Directory**
Deletes an empty directory.

```sh
$ rmdir emptyfolder
```

---

### **12. `man` — Manual Pages**
Shows the manual (help) for a command.

```sh
$ man ls
```

---

### **13. `sudo` — Run as Superuser (Administrator)**
Runs commands with superuser privileges.

```sh
$ sudo apt update
```

---

### **14. `grep` — Search Text in File**
Looks for text in files.

```sh
$ grep "hello" file.txt   # Finds "hello" in file.txt
```

---

### **15. `find` — Locate Files or Directories**
Searches for files and directories.

```sh
$ find /home/username -name "*.jpg"
```

---

**💡 Pro Tip:** For more information about any command, run:
```sh
man commandname
```
Example: `man grep`

These commands form the foundation of Linux usage. Once you master these basics, you can combine them to perform more complex tasks!
# Complete Linux Commands Reference Guide

Here's a comprehensive guide covering all the major Linux command categories with detailed explanations and examples:

---

## 1. **File & Directory Management**

| Command | Purpose | Example |
|---------|---------|---------|
| `pwd` | Print working directory | `pwd` |
| `ls` | List files and directories | `ls -la` (detailed listing) |
| `cd` | Change directory | `cd /home/user/Documents` |
| `mkdir` | Create directory | `mkdir newfolder` |
| `rmdir` | Remove empty directory | `rmdir emptyfolder` |
| `cp` | Copy files/directories | `cp file.txt backup.txt` or `cp -r dir1/ dir2/` |
| `mv` | Move/rename files | `mv oldname.txt newname.txt` |
| `rm` | Remove files/directories | `rm file.txt` or `rm -r folder/` |
| `touch` | Create empty file | `touch newfile.txt` |
| `cat` | Display file contents | `cat file.txt` |
| `less`/`more` | View file page by page | `less large_file.txt` |
| `find` | Search files | `find /home -name "*.txt"` |

---

## 2. **User Management**

| Command | Purpose | Example |
|---------|---------|---------|
| `useradd` | Add new user | `sudo useradd john` |
| `usermod` | Modify user info | `sudo usermod -aG sudo john` (add to sudo group) |
| `userdel` | Delete user | `sudo userdel john` |
| `passwd` | Set/change password | `passwd username` |
| `groupadd` | Create new group | `sudo groupadd developers` |
| `usermod -aG` | Add user to group | `sudo usermod -aG developers john` |
| `groups` | Show user groups | `groups username` |
| `id` | Display user ID info | `id username` |
| `whoami` | Current logged-in user | `whoami` |
| `who` | All logged-in users | `who` |
| `su` | Switch user | `su - username` |
| `sudo` | Run as superuser | `sudo apt update` |

---

## 3. **File Permissions**

### **Understanding Permissions**

Permissions consist of **three types** for **three categories** of users:

**Permission Types:**
| Symbol | Meaning | Octal Value |
|--------|---------|-------------|
| r | Read | 4 |
| w | Write | 2 |
| x | Execute | 1 |

**User Categories:**
- **u** = Owner (User)
- **g** = Group
- **o** = Others (Everyone else)

### **Octal Notation Explained**

Each digit (0-7) represents a combination of permissions:

| Number | Binary | Permissions | Meaning |
|--------|--------|-------------|---------|
| 0 | 000 | --- | No permissions |
| 1 | 001 | --x | Execute only |
| 2 | 010 | -w- | Write only |
| 3 | 011 | -wx | Write + Execute |
| 4 | 100 | r-- | Read only |
| 5 | 101 | r-x | Read + Execute |
| 6 | 110 | rw- | Read + Write |
| 7 | 111 | rwx | Read + Write + Execute |

**⚠️ Important:** Octal uses digits 0-7 only. The number **8 is invalid** in octal notation.

### **chmod Examples**

```bash
# chmod [3-digit number] [file]
chmod 755 script.sh     # Owner: rwx, Group: r-x, Others: r-x
chmod 644 file.txt      # Owner: rw-, Group: r--, Others: r--
chmod 700 private.txt   # Owner: rwx, Group: ---, Others: ---
chmod 600 secrets.txt   # Owner: rw-, Group: ---, Others: ---
chmod 777 everyone.txt  # Owner: rwx, Group: rwx, Others: rwx (AVOID)
```

### **Permission Examples Table**

| Chmod | Owner | Group | Others | Use Case |
|-------|-------|-------|--------|----------|
| 600 | rw- | --- | --- | Private file (only owner can read/write) |
| 644 | rw- | r-- | r-- | Public read file (owner writes, others read) |
| 700 | rwx | --- | --- | Owner-only executable (private script) |
| 755 | rwx | r-x | r-x | Public executable (everyone can run) |
| 777 | rwx | rwx | rwx | Full access (dangerous, avoid) |

### **Symbolic Notation (Alternative)**

```bash
chmod u+x file.sh       # Add execute permission to owner
chmod g+r file.txt      # Add read permission to group
chmod o-r file.txt      # Remove read permission from others
chmod a+r file.txt      # Add read permission to all
chmod u=rwx,g=rx,o=r file.txt  # Set specific permissions
```

### **Change Ownership**

```bash
chown username file.txt                 # Change owner
chown username:groupname file.txt       # Change owner and group
chown -R username directory/            # Recursive (for directories)
```

---

## 4. **Process Management**

| Command | Purpose | Example |
|---------|---------|---------|
| `ps` | List processes | `ps aux` (all processes with details) |
| `ps -ef` | Tree format | `ps -ef --forest` |
| `ps -u` | User's processes | `ps -u username` |
| `top` | Real-time processes | `top` (live monitoring) |
| `htop` | Enhanced top | `htop` (colorized, interactive) |
| `kill` | Terminate process | `kill 1234` (graceful) or `kill -9 1234` (force) |
| `killall` | Kill by name | `killall firefox` |
| `bg` | Run in background | `bg %1` |
| `fg` | Bring to foreground | `fg %1` |
| `jobs` | List background jobs | `jobs` |
| `pgrep` | Find process by name | `pgrep firefox` |
| `systemctl` | Service control | `systemctl status nginx` |

### **Kill Signal Types**

```bash
kill -15 PID    # SIGTERM (graceful shutdown)
kill -9 PID     # SIGKILL (force kill)
kill -1 PID     # SIGHUP (reload config)
kill -0 PID     # Check if process exists (no signal)
```

---

## 5. **Networking**

| Command | Purpose | Example |
|---------|---------|---------|
| `ip addr` | Show IP addresses | `ip addr show` |
| `ip route` | Show routing table | `ip route show` |
| `ifconfig` | Display network interfaces | `ifconfig` (legacy) |
| `ping` | Test connectivity | `ping google.com` |
| `netstat` | Network statistics | `netstat -tuln` (show open ports) |
| `ss` | Socket statistics | `ss -tuln` (modern replacement) |
| `nslookup` | DNS lookup | `nslookup google.com` |
| `dig` | Advanced DNS lookup | `dig google.com` |
| `traceroute` | Trace route to host | `traceroute google.com` |
| `wget` | Download file | `wget https://example.com/file.zip` |
| `curl` | Transfer data | `curl https://example.com` |
| `nmcli` | Network Manager CLI | `nmcli con show` |
| `hostname` | Show hostname | `hostname` or `hostnamectl` |
| `whois` | Domain info | `whois example.com` |

### **Common Networking Examples**

```bash
# Check if host is reachable
ping -c 4 8.8.8.8

# Show listening ports and connections
netstat -tuln

# Show all active connections
ss -tunap

# DNS lookup
nslookup github.com

# Get website content
curl https://example.com

# Download file
wget https://example.com/file.zip
```

---

## 6. **Disk & Memory**

| Command | Purpose | Example |
|---------|---------|---------|
| `df` | Disk space usage | `df -h` (human-readable) |
| `df -i` | Inode usage | `df -i` |
| `du` | Directory size | `du -sh /home/user` |
| `du -sh *` | Size of all items | `du -sh *` (in current directory) |
| `free` | Memory usage | `free -h` (human-readable) |
| `free -m` | Memory in MB | `free -m` |
| `vmstat` | Virtual memory stats | `vmstat 1 5` (5 samples, 1 sec apart) |
| `iostat` | I/O statistics | `iostat -x 1` |
| `lsblk` | Block device info | `lsblk` |
| `fdisk` | Partition management | `sudo fdisk -l` |
| `parted` | Partition editor | `sudo parted /dev/sda print` |

### **Memory and Disk Examples**

```bash
# Show disk space (human-readable)
df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   30G  40% /

# Show memory usage
free -h
              total        used        free
Mem:           15Gi       8.5Gi       6.5Gi
Swap:          2.0Gi          0       2.0Gi

# Find largest files/folders
du -sh /home/user/* | sort -hr | head -10
```

---

## 7. **Service Management (systemctl)**

| Command | Purpose | Example |
|---------|---------|---------|
| `systemctl start` | Start service | `sudo systemctl start nginx` |
| `systemctl stop` | Stop service | `sudo systemctl stop nginx` |
| `systemctl restart` | Restart service | `sudo systemctl restart nginx` |
| `systemctl reload` | Reload config | `sudo systemctl reload nginx` |
| `systemctl status` | Check status | `systemctl status nginx` |
| `systemctl enable` | Auto-start at boot | `sudo systemctl enable nginx` |
| `systemctl disable` | Disable auto-start | `sudo systemctl disable nginx` |
| `systemctl list-units` | List all services | `systemctl list-units --type=service` |
| `systemctl is-active` | Check if running | `systemctl is-active nginx` |
| `systemctl is-enabled` | Check if enabled | `systemctl is-enabled nginx` |

### **Service Management Examples**

```bash
# Start and enable a service
sudo systemctl start ssh
sudo systemctl enable ssh

# Check status
systemctl status ssh

# View service logs
journalctl -u ssh -n 50

# Stop and disable
sudo systemctl stop apache2
sudo systemctl disable apache2
```

---

## 8. **Package Management (apt)**

| Command | Purpose | Example |
|---------|---------|---------|
| `apt update` | Refresh package list | `sudo apt update` |
| `apt upgrade` | Upgrade packages | `sudo apt upgrade` |
| `apt install` | Install package | `sudo apt install git` |
| `apt remove` | Remove package | `sudo apt remove nano` |
| `apt purge` | Remove + config | `sudo apt purge nano` |
| `apt search` | Search package | `apt search nodejs` |
| `apt show` | Package info | `apt show git` |
| `apt list` | List packages | `apt list --installed` |
| `apt autoremove` | Remove unused deps | `sudo apt autoremove` |
| `apt clean` | Clean cache | `sudo apt clean` |
| `dpkg -l` | List installed | `dpkg -l` |
| `dpkg -i` | Install .deb file | `sudo dpkg -i package.deb` |

### **Package Management Examples**

```bash
# Update system
sudo apt update
sudo apt upgrade

# Install packages
sudo apt install git nodejs npm

# Search for package
apt search nginx

# Remove package (keep config)
sudo apt remove firefox

# Remove package (delete config too)
sudo apt purge firefox

# Clean up unused packages
sudo apt autoremove
sudo apt clean
```

---

## 9. **Log Monitoring**

| Command | Purpose | Example |
|---------|---------|---------|
| `tail` | View end of file | `tail -f /var/log/syslog` |
| `tail -n` | Last N lines | `tail -20 /var/log/auth.log` |
| `tail -f` | Follow in real-time | `tail -f /var/log/nginx/access.log` |
| `grep` | Search in logs | `grep "ERROR" /var/log/syslog` |
| `tail -f` + `grep` | Real-time filter | `tail -f /var/log/syslog \| grep "ERROR"` |
| `journalctl` | View systemd logs | `journalctl -u nginx` |
| `journalctl -f` | Follow systemd logs | `journalctl -f` |
| `journalctl --since` | Logs since time | `journalctl --since "2024-04-27 12:00"` |
| `less` | Page through logs | `less /var/log/syslog` |
| `cat` | Display entire log | `cat /var/log/messages` |
| `head` | View start of file | `head -50 /var/log/syslog` |
| `awk`/`sed` | Parse logs | `grep "404" access.log \| awk '{print $1}'` |

### **Log Monitoring Examples**

```bash
# View last 50 lines of syslog
tail -50 /var/log/syslog

# Monitor logs in real-time
tail -f /var/log/nginx/error.log

# Search for errors
grep "ERROR" /var/log/syslog

# Real-time filter (show only errors)
tail -f /var/log/syslog | grep "ERROR"

# View logs from specific service
journalctl -u nginx -n 100

# View logs since specific time
journalctl --since "2024-04-27 10:00" --until "2024-04-27 11:00"

# View kernel logs
journalctl -k

# Show failed services
systemctl --failed
```

### **Common Log Locations**

```
/var/log/syslog        - General system logs
/var/log/auth.log      - Authentication logs
/var/log/kern.log      - Kernel logs
/var/log/nginx/        - Nginx logs
/var/log/apache2/      - Apache logs
/var/log/mysql/        - MySQL logs
/var/log/messages      - System messages (RedHat/CentOS)
```

---

## **Quick Reference Cheat Sheet**

```bash
# File Operations
ls -la          # List all with details
cp -r src dst   # Copy recursively
mv old new      # Move/rename
rm -rf folder   # Remove recursively

# User & Permissions
useradd user    # Add user
chmod 755 file  # Change permissions
chown user:group file   # Change owner

# Processes
ps aux          # List all processes
kill -9 PID     # Force kill process
top             # Real-time monitoring

# Networking
ping host       # Test connectivity
netstat -tuln   # Show open ports
curl url        # Fetch web content

# Disk/Memory
df -h           # Disk usage
free -h         # Memory usage
du -sh folder   # Folder size

# Services
systemctl start service     # Start service
systemctl enable service    # Enable at boot

# Packages
apt update      # Update repository
apt install pkg # Install package

# Logs
tail -f /var/log/syslog     # Real-time logs
journalctl -u service       # Service logs
```
---
# Important Linux Concepts for DevOps

## SSH

Secure remote login.

```bash
ssh user@server-ip
```

---

## Cron Jobs

Schedule tasks.

```bash
crontab -e
```

Example:

```text
0 2 * * * backup.sh
```

Runs at 2 AM daily.

---

## Environment Variables

```bash
echo $PATH
export JAVA_HOME=/opt/java
```

---

# Linux Boot Process

```text
BIOS/UEFI
   ↓
GRUB Bootloader
   ↓
Kernel
   ↓
systemd/init
   ↓
Services
   ↓
Login
```

---

# Linux for DevOps Engineers

Common tools used on Linux:

* Docker
* Kubernetes
* Jenkins
* Ansible
* Terraform
* Git
* Prometheus
* Grafana

---

# Most Important Daily Linux Commands for DevOps

```bash
ls
cd
pwd
grep
find
cat
tail -f
top
ps -ef
systemctl
journalctl
curl
wget
ssh
scp
chmod
chown
df -h
free -m
netstat
ss
docker ps
kubectl get pods
```

---

# Simple Example Workflow

## Check server issue

```bash
top
df -h
free -m
systemctl status nginx
tail -f /var/log/nginx/error.log
```

Purpose:

* Check CPU
* Check disk
* Check memory
* Check service
* Check logs

---
