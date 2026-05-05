# Operating System (OS)
An **Operating System (OS)** is system software that acts as a bridge between: User, Applications and Hardware. It manages all computer resources and allows applications to run.
```text id="os1"
OS = Software that manages hardware and software resources
OS helps applications communicate with hardware.
```
**Real Architecture:**
```text id="os2"
User --> Applications --> Operating System --> Hardware
```
### Why OS is Required
| Reason              | Explanation                          |
| ------------------- | ------------------------------------ |
| Hardware Management | Controls CPU, RAM, disk, network     |
| Run Applications    | Executes software/programs           |
| User Interface      | Allows users to interact with system |
| Resource Management | Allocates system resources           |
| File Management     | Stores/manages files                 |
| Security            | User authentication & permissions    |
| Networking          | Internet/network communication       |

#### Without OS
- Applications cannot access hardware directly
- No memory management, No process scheduling, No file handling, No user interface.
- System becomes very difficult to use.
### Main Components of OS

```
1. Kernel: Core of OS      
2. File System: Manages files/folders  
3. Process Manager: Runs applications/processes   / Manages running programs
4. Memory Manager: Allocates RAM / Handles RAM               
5. Device Drivers:  Controls keyboard, disk, printer / Controls hardware         
6. Network Manager: Internet communication / Handles networking       
7. Security Manager: Authentication and permissions / User permissions/security
8. File Management: Stores/retrieves files
9. Resource Scheduling:CPU scheduling 

#  Example
When opening Chrome browser:
Chrome Request --> Operating System --> CPU + RAM + Disk + Network
OS allocates resources to Chrome.
```
## concepts
#### 1. Kernel: The Linux kernel is the core part of the operating system that manages hardware, memory, processes, and communication between software and hardware.
#### 2. Linux File System: The Linux file system is the structure used to organize, store, and manage files and directories in Linux.
#### 3. Shell: The shell is a command interpreter that takes user commands and sends them to the Linux kernel for execution.
#### 4.Terminal: The terminal is the interface or application used to interact with the shell and execute Linux commands.
#### 5. Service/Daemon: A service or daemon is a background process that runs continuously to perform system or application tasks automatically.
#### 6. Process management: Process management in Linux means monitoring, controlling, and managing running programs and tasks in the system.
#### 7. Memory Management: Memory management in Linux means allocating, using, and freeing RAM memory for running processes and applications.
#### 8. Linux Networking: Linux networking means managing network connections, communication, IP addresses, ports, and internet connectivity in Linux systems.
#### 9. Package Management: Package management in Linux means installing, updating, removing, and managing software packages using tools like `apt`, `yum`, or `dnf`.
#### 10. Linux Security: Linux security means protecting the Linux system, users, files, processes, and network from unauthorized access and attacks.
#### 11. Cache: Cache is a temporary high-speed storage area used to store frequently accessed data so the system can access it faster later.
#### 12. Host Operating System: The host operating system is the main operating system installed directly on the physical machine that manages hardware and runs applications, virtual machines, or containers.
#### 13. System Resources: System resources are the hardware and software components used by the operating system and applications, such as CPU, memory (RAM), disk space, network, and processes.

## Kernel 
Kernel is the core part of an Operating System, it acts as a bridge between hardware and software. It allows applications to communicate with hardware, without directly accessing the hardware components.

Kernel **manages system resources:** such as CPU, memory, storage. **file systems:** it helps in reading, writing, and storing files on storage devices. **memory allocation:** it decides how much memory each program can use. **CPU scheduling:** it decides which process should use the CPU first.

Kernel **controls process management:** such as creating, scheduling, and terminating processes. **multitasking:** it allows multiple applications to run at the same time.

Kernel **handles device management:** such as keyboard, mouse, printer, disk, and network devices and **system calls:** applications use system calls to request services from the operating system. **interrupt management:** it responds when hardware devices send signals to the system.

Kernel **provides security and access control**, it prevents unauthorized access to system resources. It improves system stability, it prevents applications from directly damaging hardware or memory.

- There are different types of kernels, such as Monolithic Kernel, Microkernel, Hybrid Kernel, and Exokernel.

Monolithic Kernel contains all services inside the kernel space, it provides high performance. Microkernel contains only essential services in kernel space, other services run in user space. Hybrid Kernel combines features of Monolithic and Microkernel, it balances performance and flexibility.

## Linux File System
Linux File System is the method used by Linux Operating System to organize, store, and manage files and directories. In Linux, everything is treated as a file, such as documents, devices, processes, and directories.

Linux File System follows a hierarchical structure, everything starts from the root directory called `/`. The root directory `/` is the top-level directory, all other directories exist under it.

- `/bin`:  contains essential user commands, such as ls, cp, mv, and cat.

- `/sbin`:  contains system administration commands, such as fdisk, reboot, and iptables.

- `/etc`:  stores system configuration files, such as network configuration and user settings.

- `/home`: contains personal directories of users, each user gets a separate folder inside `/home`.

- `/root`:  is the home directory of the root user, it is different from `/home`.

- `/dev`:  contains device files, such as hard disks, USB devices, and terminals.

- `/proc`:  contains process and kernel information, it provides real-time system details.

- `/var`:  stores variable data, such as logs, cache files, and mail files.

- `/tmp`:  stores temporary files, files in this directory may be deleted after reboot.

- `/usr`:  contains user applications and software packages, such as programs and libraries.

- `/lib`:  contains shared libraries required by system programs and commands.

- `/boot`:  contains boot loader files and Linux kernel files required during system startup.

- `/mnt`:  is used to temporarily mount storage devices, such as USB drives and external disks.

- `/media`:  is used for automatic mounting of removable devices, such as CDs and USB drives.

- `/opt`:  contains optional third-party software packages and applications.

- `/srv`:  stores data related to services provided by the system, such as web server files.

- `/run`:  stores runtime process information, it exists only while the system is running.

A file system manages file permissions, it controls who can read, write, or execute files. Linux file permissions are divided into User, Group, and Others, each having read, write, and execute permissions.

Linux uses inode structure to store file metadata, such as file size, permissions, and ownership. Mounting is the process of attaching a file system to a directory structure, so users can access the storage device. Unmounting removes the attached file system safely from the directory structure.

- The `df` command shows disk space usage, the `du` command shows directory file size usage.

- The `ls` command lists files and directories, the `pwd` command shows the current directory path.

- The `cd` command changes the current directory, the `mkdir` command creates a new directory.

- The `rm` command removes files or directories, the `cp` command copies files and directories.

- The `mv` command moves or renames files and directories.

Linux File System is important because it helps organize data efficiently, securely, and systematically in the operating system.

## Shell
Shell is a command-line interpreter in Linux, it allows users to communicate with the Operating System using commands. Shell scripting is used to automate repetitive tasks, such as backups, deployments, and monitoring. **The shell provides features like command history, tab completion, variables, loops, and conditions.** Environment variables in the shell store system information, such as user path and home directory.

Shell acts as a bridge between the user and the Linux kernel, it takes user commands and sends them to the kernel for execution. It reads commands entered by the user, processes them, and displays the output in the terminal. It can execute Linux commands, shell scripts, and automation tasks.

Common Linux shells are Bash, Sh, Zsh, and Korn Shell. Bash stands for Bourne Again Shell, it is the default shell in many Linux distributions.

- The `echo` command displays text or variable values in the shell.

- The `export` command creates environment variables in the shell session.

- The `history` command shows previously executed commands in the shell.

- The `alias` command creates shortcut names for long commands.

## Terminal
Terminal is the interface used to access the shell, it provides a window where users type commands. Terminal is also called a command-line interface called CLI.

The terminal allows users to interact with Linux systems without using a graphical interface. The terminal sends user commands to the shell, the shell processes the commands and returns the output to the terminal.

Examples of Linux terminal applications are GNOME Terminal, Konsole, and Xterm.

The terminal supports multiple tabs and sessions, users can work on multiple tasks simultaneously.

- The shortcut `Ctrl + C` stops a running command in the terminal.
- `Ctrl + Z` pauses a running process temporarily.
- `Ctrl + L` clears the terminal screen.
- `clear` command also clears the terminal display.

## Service/Deamon
Service in Linux is a background program that performs specific tasks for the system or applications. Services run in the background without direct user interaction, they provide continuous functionality to the system. Services are also called daemons in Linux systems. Services usually start automatically during system boot, they continue running in the background. 

Examples of services are Nginx, Apache, Docker, SSH, Jenkins, and MySQL. The Docker service manages containers running on the system. The Nginx service handles web server requests from users.

The SSH service allows remote login access to Linux systems.

Linux uses `systemd` to manage services in modern distributions.

Example : The `systemctl` command is used to manage services.
- `systemctl start nginx` starts the Nginx service.
- `systemctl stop nginx` stops
- `systemctl restart nginx` restarts
- `systemctl status nginx` checks the current service status.
- `systemctl enable nginx` enables the service to start automatically during boot.
- `systemctl disable nginx` prevents the service from starting during boot.

The `service` command is also used in some Linux distributions to manage services.

Logs related to services can be checked using the `journalctl` command.
- Example `journalctl -u nginx` displays logs for the Nginx service.

## Host Operating System
Host Operating System is the main operating system installed directly on a physical computer or server, it manages hardware and system resources.

The Host Operating System acts as the base system, other applications, virtual machines, and containers run on top of it. The host operating system communicates directly with hardware components, such as CPU, memory, storage, and network devices. Examples of Host Operating Systems are Linux, Windows, and macOS.

In virtualization, the host operating system runs virtualization software, such as VMware, VirtualBox, or Hyper-V.

The virtualization software creates and manages virtual machines on the host operating system. A virtual machine runs a Guest Operating System, while the actual physical system runs the Host Operating System. The host operating system allocates CPU, RAM, storage, and network resources to virtual machines.

**In Docker, the host operating system provides the kernel required for running containers.** Containers share the host operating system kernel, they do not require separate full operating systems like virtual machines. Linux containers require a Linux kernel from the host operating system to run properly.

The host operating system handles process management, memory management, networking, and device management for all running applications. The host operating system controls security policies, user access, and file permissions on the system. System services and background processes run on the host operating system. The host operating system manages software installation, package updates, and hardware drivers.

In cloud computing, cloud servers also run a host operating system to manage virtual machines and containers. **If the host operating system crashes, all running applications, containers, and virtual machines may stop working.** The performance of applications and virtual machines depends on the stability and resource management of the host operating system.

The host operating system is important because it provides the environment required for running software, virtual machines, and containers efficiently.
## Linux Users & Permissions
Linux Users are accounts created in the Linux Operating System, they allow people or services to access the system securely. it controls who can access files and system resources. Each user in Linux has a unique username and User ID called UID.

There are mainly three types of users in Linux, Root User, Regular User, and Service/System User. Root User is the administrator account, it has full control over the entire system. Regular User is a normal user account, it has limited permissions for security purposes. System Users are used by applications and services, they usually do not log in manually.

Linux stores user information in the `/etc/passwd` file, it contains usernames and user details. Encrypted user passwords are stored in the `/etc/shadow` file, only privileged users can access it.

Groups in Linux are used to manage permissions for multiple users together. Each group has a unique Group ID called GID. Linux stores group information in the `/etc/group` file. A user can belong to one primary group and multiple secondary groups.

- The `whoami` command shows the currently logged-in user.

- The `id` command displays user ID, group ID, and group information.

- The `adduser` or `useradd` command is used to create a new user.

- The `passwd` command is used to set or change a user password.

- The `usermod` command is used to modify user account details.

- The `userdel` command is used to delete a user account.

- The `groupadd` command is used to create a new group.

- The `groupdel` command is used to delete a group.

- The `su` command switches from one user to another user.

- The `sudo` command allows a regular user to execute administrative commands temporarily.

#### There are three permission types in Linux, Read, Write, and Execute.
Linux permissions control access to files and directories, they improve security and prevent unauthorized access.

- Read permission allows viewing file contents or listing directory contents.

- Write permission allows modifying files or creating and deleting files inside directories.

- Execute permission allows running a file as a program or entering a directory.

- Numeric permission values are Read = 4, Write = 2, Execute = 1.

- Permission `7` means read, write, and execute together because `4+2+1=7`. Permission `6` means read and write because `4+2=6`. Permission `5` means read and execute because `4+1=5`. Permission `4` means only read permission.
- The `ls -l` command displays file permissions in long format.
- Example permission format is `-rwxr-xr--`, it represents permissions for user, group, and others. `r` means read permission, `w` means write permission, `x` means execute permission. A dash `-` means that permission is not granted.

#### Permissions are assigned to three categories, User, Group, and Others.
- The `chmod` command changes file permissions. Example `chmod 765 file.sh` gives full permissions to 7 to owner and read-write permissions to 6 to Group and read-execute permissions to 5 to others.

- User permissions apply to the file owner, group permissions apply to users in the same group, others permissions apply to all remaining users.

- The `chown` command changes file ownership. Example `chown user1 file.txt` changes the owner of the file.

- The `chgrp` command changes group ownership of a file or directory.

File ownership and permissions are important in Linux, they protect system files and user data from unauthorized access.

## Process Management
Process management in Linux means monitoring, controlling, and managing running programs and tasks in the system.

Process Management is the activity of managing running programs/applications in the Operating System, it controls how processes are created, executed, and terminated. Linux Process Management helps in multitasking, it allows multiple programs to run simultaneously.

The kernel manages all processes, it decides how system resources are allocated to each process. A process is a program that is currently running in memory

Each process has a unique PID, the system uses this ID to identify and manage processes. each process has its own Process ID called PID.

The first process started in Linux is called `init` or `systemd`, it usually has PID 1.

#### Types of Processes
- A parent process can create child processes, this process creation is called forking.

- Foreground processes run directly in the terminal, users can interact with them.

- Background processes run without user interaction, they continue running after terminal commands are executed.

- Daemon processes are background service processes, such as web servers and database services.

- Linux process states describe the current condition of a process, such as Running, Sleeping, Stopped, or Zombie.

#### Types of processes status
- Running state means the process is actively using the CPU.

- Sleeping state means the process is waiting for an event or resource.

- Stopped state means the process execution is paused temporarily.

- Zombie state means the process has completed execution but still exists in the process table.

#### commands
- The `ps` command displays currently running processes. Example `ps -ef` shows detailed information about all running processes.

- The `top` command displays real-time process and system resource usage.  `htop` command provides an interactive view of processes with better visualization.

- The `pidof` command shows the PID of a specific process.

- The `pstree` command displays processes in a tree structure.

- The `jobs` command lists background jobs running in the current shell.

- The `bg` command moves a stopped process to the background.

- The `fg` command brings a background process to the foreground.

- The `kill` command terminates a process using its PID. Example `kill 1234` stops the process with PID 1234.

- The `killall` command terminates processes by process name instead of PID.

- The `pkill` command kills processes based on name or other attributes.

Signals are used to control processes, the system sends signals to start, stop, or terminate processes.

- `SIGTERM` is a graceful termination signal, it allows the process to clean up before exiting.

- `SIGKILL` forcefully terminates a process immediately.

- `SIGSTOP` pauses a running process temporarily.

- `SIGCONT` resumes a stopped process.

- The `nice` command starts a process with a specific priority level. # Lower nice values give higher CPU priority, higher nice values give lower CPU priority.

- The `renice` command changes the priority of a running process.

Process Management is important because it ensures efficient CPU usage, multitasking, resource allocation, and system stability.

The scheduler in Linux decides which process gets CPU time, it helps in efficient multitasking.

Context switching is the process of saving one process state and loading another process state into the CPU.

Memory management works closely with process management, each process gets its own memory space.

- The `free` command shows memory usage details related to processes.

- The `uptime` command shows system running time and load average.

- The `nohup` command allows a process to continue running even after logging out from the terminal. Example `nohup python app.py &` runs the application in the background permanently.

- The `systemctl` command manages system services and daemon processes in modern Linux systems. Example `systemctl status nginx` checks the status of the Nginx service.

## Memory Management
Memory management in Linux means allocating, using, and freeing RAM memory for running processes and applications.

Memory Management is the process of managing system memory in the Operating System, it controls how memory is allocated and released for programs.It allows multiple processes to run simultaneously, each process gets its own memory space.

The Linux kernel handles memory management, it ensures efficient usage of RAM and system resources. The kernel allocates memory to processes when applications start running. The kernel releases memory when a process is terminated, this prevents memory wastage. The kernel uses memory optimization techniques, such as caching and swapping, to improve system performance. The kernel isolates process memory spaces, one process cannot directly access another process memory.

#### RAM and Swap
- RAM stands for Random Access Memory, it stores data and programs currently being used by the CPU.

- Virtual Memory is a memory management technique, it uses disk space as additional memory when RAM becomes full.

- Swap Space is a reserved disk area used as virtual memory, it helps the system handle low memory conditions.

- When RAM usage becomes high, inactive data is moved from RAM to swap space.

- Swap memory is slower than RAM, because disk storage is slower than physical memory.

- The kernel moves pages between RAM and swap space based on memory usage.

Paging is the process of dividing memory into fixed-size blocks called pages. Linux uses demand paging, pages are loaded into memory only when required by the process.

Segmentation divides memory into logical sections, such as code segment, data segment, and stack segment. Memory fragmentation happens when free memory becomes scattered into small blocks, it reduces memory efficiency.

- The stack stores function calls and local variables during program execution.

- The heap stores dynamically allocated memory used by applications.

- Cache memory is high-speed memory used to improve CPU performance, it stores frequently accessed data temporarily.

- Buffer memory temporarily stores data during data transfer operations, such as disk and network communication.

- Shared Memory allows multiple processes to access the same memory area, it improves communication speed between processes.

- Memory leaks happen when a program does not release unused memory, this can reduce system performance over time.

- Out Of Memory called OOM occurs when the system does not have enough free memory to allocate for processes.

The OOM Killer in Linux automatically terminates processes when the system runs out of memory completely.

- The `free` command displays RAM and swap memory usage. Example `free -h` shows memory usage in human-readable format.

- The `vmstat` command displays virtual memory statistics and system performance information.

- The `ps aux` command shows memory usage details of running processes.

- The `/proc/meminfo` file contains detailed memory information about the Linux system.

- The `cat /proc/meminfo` command displays complete memory details.

- The `swapon` command enables swap space in Linux.

- The `swapoff` command disables swap space.

- The `df -h` command checks disk space usage, it helps monitor swap partition storage.

- The `sync` command writes cached data from memory to disk storage safely.

Memory protection improves system security and stability, it prevents unauthorized memory access. Efficient memory management improves multitasking, application performance, and overall system stability.

## Linux Networking
Linux networking means managing network connections, communication, IP addresses, ports, and internet connectivity in Linux systems.

Linux Networking is the process of connecting Linux systems to communicate with other systems and devices over a network. Linux networking allows systems to share data, access internet services, and communicate with servers.

- An IP Address is a unique address assigned to a device in a network, it helps identify the device. IPv4 uses 32-bit addresses, example `192.168.1.1`. IPv6 uses 128-bit addresses, it provides a larger address range.

- A subnet mask defines the network and host portion of an IP address.

- A gateway is a device that connects one network to another network, usually used to access the internet.

- DNS stands for Domain Name System, it converts domain names into IP addresses.

- MAC Address is a physical hardware address assigned to a network interface card.

- TCP is a connection-oriented protocol, it provides reliable communication and data delivery.

- UDP is a connectionless protocol, it provides faster communication with less reliability.

- Ports are logical communication endpoints, services use ports to communicate over the network. Example port `22` is used for SSH, port `80` is used for HTTP, port `443` is used for HTTPS.

- SSH stands for Secure Shell, it is used for secure remote login and server management.

- Ping command checks network connectivity between systems. Example `ping google.com` tests internet connectivity.
- Firewall controls incoming and outgoing network traffic, it improves system security.

- `iptables` and `firewalld` are commonly used firewall management tools in Linux.
#### commands
- The `ifconfig` command displays or configures network interfaces in older Linux systems.

- The `ip addr` command displays IP address information in modern Linux systems.

- The `netstat` command shows network connections and listening ports.

- The `ss` command is a modern replacement for `netstat`, it displays socket and connection information.

- The `traceroute` command shows the path packets travel to reach a destination.

- The `nslookup` command checks DNS resolution information.

- The `curl` command transfers data from servers, it is commonly used to test APIs and websites.

- The `wget` command downloads files from the internet.

- The `scp` command securely copies files between systems using SSH.

- The `rsync` command synchronizes files between systems efficiently.


## Package Management
Package management in Linux means installing, updating, removing, and managing software packages in Linux using tools like apt, yum, or dnf.

A package contains application files, libraries, configuration files, and dependencies required for software installation. Package management helps maintain system stability, security, and software updates efficiently. Package managers automatically handle software dependencies, they simplify software management.

Different Linux distributions use different package managers.

APT is used in Debian and Ubuntu based systems. YUM and DNF are used in Red Hat and CentOS based systems. RPM is a package format used in Red Hat based systems.

- The `apt update` command refreshes package repository information.

- The `apt upgrade` command upgrades installed packages to newer versions.

- The `apt install nginx` command installs the Nginx package.

- The `apt remove nginx` command removes the installed package.

- The `yum install httpd` command installs Apache HTTP Server in Red Hat systems.

- The `dnf update` command updates installed packages in modern Red Hat systems.

Repositories are online storage locations containing software packages. Linux package managers download packages from repositories automatically.

- The `dpkg` command manages `.deb` packages manually in Debian based systems.

- The `rpm` command manages `.rpm` packages manually in Red Hat based systems.

## Linux Security
Linux security means protecting the Linux system, users, files, processes, and network from unauthorized access and attacks.

Linux Security is the practice of protecting Linux systems from unauthorized access, attacks, and data loss. Linux security controls users, permissions, processes, network access, and system resources. Linux security is important because it protects systems, applications, networks, and sensitive data from threats and unauthorized access.

Authentication verifies user identity using usernames and passwords. Authorization controls what actions a user is allowed to perform in the system. File permissions protect files and directories from unauthorized access.

The root user has full system access, misuse of root privileges can create security risks. The `sudo` command provides temporary administrative privileges securely.

SSH security is important for remote server access, strong passwords and SSH keys improve security. Firewall protects the system by filtering network traffic based on rules. 

Encryption protects sensitive data by converting it into unreadable format. HTTPS uses SSL/TLS encryption to secure web communication.

SELinux stands for Security-Enhanced Linux, it provides mandatory access control for system security. AppArmor is another Linux security framework, it restricts application capabilities.

Regular software updates are important for fixing security vulnerabilities.

- The `chmod` command changes file permissions for security management.

- The `chown` command changes file ownership to control access.

- The `passwd` command changes user passwords.

- The `fail2ban` tool blocks suspicious login attempts automatically.

Logs help monitor security events and suspicious activities in the system.

- The `/var/log` directory stores important system and security log files.

- The `journalctl` command displays system logs managed by systemd.

Antivirus and malware scanning tools can also be used in Linux systems for additional protection. Backup is an important security practice, it helps recover data after failures or attacks.

Q1: What is OS? --> Software that manages hardware and software resources.
Q2: What are main functions of OS? --> Process, memory, file, device, networking, security management.
Q3: Why Linux OS is preferred in DevOps? --> Stable, lightweight, automation-friendly, and container support.

👉 OS acts as manager/controller of the entire system.
