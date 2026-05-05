# Ultimate Linux Guide

This repository is created to serve as a revision notes for the YouTube course created by **Abhishek Veeramalla**(`iam-veeramalla` on GitHub) on his youtube channel - `Abhishek.Veeramalla`.

Following topics are covered as part of the course and documentation.

- Fundamentals of Linux
- Linux vs Windows
- Core components of Linux
- Setup Linux on Windows & MacOS
- Linux folder structure
- Linux user management
- Linux file management
- VI Editor shortcuts (commonly used)
- File permissions
- Process management
- Linux system monitoring
- Basic Networking in Linux
- Disk and Storage management in Linux

Please refer to the folders at the root level of this repository to go through the documentation. 
# Linux Commands with Definition, Why We Use, and Example

| Command             | Definition                             | Why We Use / Uses                                  | Example                         |
| ------------------- | -------------------------------------- | -------------------------------------------------- | ------------------------------- |
| `pwd`               | Shows present working directory        | Used to know current location in Linux file system | `pwd`                           |
| `ls`                | Lists files and directories            | Used to view files and folders                     | `ls`                            |
| `ls -l`             | Lists files with detailed information  | Used to check permissions, owner, size, and date   | `ls -l`                         |
| `ls -la`            | Lists all files including hidden files | Used to view hidden configuration files            | `ls -la`                        |
| `cd`                | Changes directory                      | Used to move between directories                   | `cd /home/user`                 |
| `mkdir`             | Creates directory                      | Used to create folders                             | `mkdir devops`                  |
| `rmdir`             | Removes empty directory                | Used to delete empty folders                       | `rmdir test`                    |
| `touch`             | Creates empty file                     | Used to create files quickly                       | `touch file.txt`                |
| `cat`               | Displays file content                  | Used to read small files                           | `cat file.txt`                  |
| `less`              | Displays file content page by page     | Used for large files and logs                      | `less logfile.txt`              |
| `head`              | Shows first lines of file              | Used to check beginning of file                    | `head file.txt`                 |
| `tail`              | Shows last lines of file               | Used for monitoring logs                           | `tail logfile.txt`              |
| `tail -f`           | Displays live log updates              | Used for real-time monitoring                      | `tail -f /var/log/syslog`       |
| `cp`                | Copies files or directories            | Used for backup and duplication                    | `cp file.txt backup.txt`        |
| `mv`                | Moves or renames files                 | Used to rename or move files                       | `mv old.txt new.txt`            |
| `rm`                | Removes files                          | Used to delete files                               | `rm file.txt`                   |
| `rm -r`             | Removes directories recursively        | Used to delete folders with content                | `rm -r testdir`                 |
| `rm -rf`            | Force removes files/directories        | Used to delete without confirmation                | `rm -rf olddir`                 |
| `find`              | Searches files and directories         | Used to locate files in system                     | `find / -name file.txt`         |
| `grep`              | Searches text patterns                 | Used to find words in files/logs                   | `grep error logfile.txt`        |
| `echo`              | Displays text or variables             | Used for output and scripting                      | `echo Hello`                    |
| `nano`              | Simple text editor                     | Used to edit files easily                          | `nano file.txt`                 |
| `vim`               | Advanced text editor                   | Used for editing configuration files               | `vim file.txt`                  |
| `clear`             | Clears terminal screen                 | Used to clean terminal output                      | `clear`                         |
| `history`           | Shows command history                  | Used to review previous commands                   | `history`                       |
| `whoami`            | Shows current logged-in user           | Used to identify active user                       | `whoami`                        |
| `id`                | Displays user and group IDs            | Used for permission and identity checking          | `id`                            |
| `hostname`          | Shows system hostname                  | Used to identify server name                       | `hostname`                      |
| `uname -a`          | Shows system information               | Used to check Linux kernel and OS details          | `uname -a`                      |
| `date`              | Shows current date and time            | Used for time verification                         | `date`                          |
| `cal`               | Displays calendar                      | Used to check dates quickly                        | `cal`                           |
| `free -h`           | Shows memory usage                     | Used to monitor RAM usage                          | `free -h`                       |
| `df -h`             | Shows disk space usage                 | Used to check storage usage                        | `df -h`                         |
| `du -sh`            | Shows directory size                   | Used to identify large folders                     | `du -sh /var/log`               |
| `top`               | Displays running processes live        | Used for monitoring CPU and memory usage           | `top`                           |
| `htop`              | Interactive process viewer             | Used for advanced monitoring                       | `htop`                          |
| `ps -ef`            | Lists running processes                | Used to view active processes                      | `ps -ef`                        |
| `kill`              | Terminates process                     | Used to stop unwanted processes                    | `kill 1234`                     |
| `kill -9`           | Force kills process                    | Used when normal kill fails                        | `kill -9 1234`                  |
| `jobs`              | Shows background jobs                  | Used to monitor background tasks                   | `jobs`                          |
| `bg`                | Runs process in background             | Used to continue stopped jobs                      | `bg`                            |
| `fg`                | Brings background job to foreground    | Used to interact with background process           | `fg`                            |
| `chmod`             | Changes file permissions               | Used for access control                            | `chmod 755 script.sh`           |
| `chown`             | Changes file ownership                 | Used to assign file owner                          | `chown user:user file.txt`      |
| `useradd`           | Creates user                           | Used for user management                           | `sudo useradd devops`           |
| `passwd`            | Sets user password                     | Used to secure user accounts                       | `sudo passwd devops`            |
| `userdel`           | Deletes user                           | Used to remove users                               | `sudo userdel devops`           |
| `groupadd`          | Creates group                          | Used for permission grouping                       | `sudo groupadd admins`          |
| `su`                | Switches user                          | Used to login as another user                      | `su root`                       |
| `sudo`              | Executes command as root               | Used for administrative tasks                      | `sudo apt update`               |
| `ip addr`           | Shows IP addresses                     | Used for networking checks                         | `ip addr`                       |
| `ping`              | Checks network connectivity            | Used to test internet/server reachability          | `ping google.com`               |
| `curl`              | Transfers data from URLs               | Used for API testing and downloads                 | `curl https://example.com`      |
| `wget`              | Downloads files                        | Used to download packages/files                    | `wget file_url`                 |
| `ssh`               | Remote server login                    | Used to connect remote Linux servers               | `ssh user@server-ip`            |
| `scp`               | Securely copies files                  | Used for remote file transfer                      | `scp file.txt user@server:/tmp` |
| `netstat`           | Shows network connections              | Used for port and connection monitoring            | `netstat -tulnp`                |
| `ss`                | Modern network socket tool             | Used to check listening ports                      | `ss -tulnp`                     |
| `nslookup`          | DNS lookup tool                        | Used to resolve domain names                       | `nslookup google.com`           |
| `traceroute`        | Tracks packet route                    | Used for network troubleshooting                   | `traceroute google.com`         |
| `tar`               | Archives files/directories             | Used for backup and packaging                      | `tar -cvf backup.tar dir`       |
| `gzip`              | Compresses files                       | Used to reduce file size                           | `gzip file.txt`                 |
| `gunzip`            | Uncompresses gzip files                | Used to extract compressed files                   | `gunzip file.txt.gz`            |
| `zip`               | Creates zip archive                    | Used for compression and sharing                   | `zip files.zip file.txt`        |
| `unzip`             | Extracts zip archive                   | Used to extract zip files                          | `unzip files.zip`               |
| `apt update`        | Updates package list                   | Used before package installation                   | `sudo apt update`               |
| `apt install`       | Installs packages                      | Used to install software                           | `sudo apt install nginx`        |
| `apt remove`        | Removes packages                       | Used to uninstall software                         | `sudo apt remove nginx`         |
| `systemctl start`   | Starts service                         | Used to start applications/services                | `sudo systemctl start nginx`    |
| `systemctl stop`    | Stops service                          | Used to stop running services                      | `sudo systemctl stop nginx`     |
| `systemctl restart` | Restarts service                       | Used after configuration changes                   | `sudo systemctl restart nginx`  |
| `systemctl status`  | Shows service status                   | Used for troubleshooting services                  | `systemctl status nginx`        |
| `systemctl enable`  | Enables service at boot                | Used for automatic startup                         | `sudo systemctl enable nginx`   |
| `journalctl`        | Displays system logs                   | Used for troubleshooting                           | `journalctl -xe`                |
| `env`               | Shows environment variables            | Used for configuration checks                      | `env`                           |
| `export`            | Creates environment variable           | Used for temporary variables                       | `export NAME=Priyanka`          |
| `alias`             | Creates command shortcut               | Used for faster command execution                  | `alias ll='ls -la'`             |
| `crontab -e`        | Edits cron jobs                        | Used for task scheduling                           | `crontab -e`                    |
| `reboot`            | Restarts system                        | Used after updates/config changes                  | `sudo reboot`                   |
| `shutdown`          | Powers off system                      | Used to safely stop server                         | `sudo shutdown now`             |
| `uptime`            | Shows system running time              | Used for server monitoring                         | `uptime`                        |
| `man`               | Displays command manual                | Used to learn command details                      | `man ls`                        |
| `which`             | Shows command location                 | Used to locate binaries                            | `which python`                  |
| `whereis`           | Finds command files                    | Used to locate binaries/man pages                  | `whereis nginx`                 |
| `locate`            | Quickly searches files                 | Used for fast file searching                       | `locate file.txt`               |
