## What is Cron Job?

A **Cron Job** is a scheduled task in Linux/Unix that runs automatically at a specific time or interval.

Think of it as an **alarm clock for commands and scripts**.

### Real-Time Examples

* Take a database backup every day at 2 AM.
* Delete old log files every Sunday.
* Restart a service every night.
* Run a monitoring script every 5 minutes.

---

## What is Crontab?

**Crontab** stands for **Cron Table**.

It is a file that stores all scheduled cron jobs for a user.

```bash
# To view your cron jobs:
crontab -l

#To edit cron jobs:
crontab -e

# To remove all cron jobs:
crontab -r
```
## Cron Job Format

```bash
* * * * * command
| | | | |
| | | | +---- Day of Week (0-7)
| | | +------ Month (1-12)
| | +-------- Day of Month (1-31)
| +---------- Hour (0-23)
+------------ Minute (0-59)
```

```bash
# Syntax
Minute Hour Day Month DayOfWeek Command
# Examples
* * * * * echo "Hello"
# Every day at 2:00 AM
0 2 * * * /home/priyanka/backup.sh
Meaning:
0   = Minute
2   = Hour
*   = Every day
*   = Every month
*   = Every weekday
# Every Sunday at 5 AM
0 5 * * 0 /home/priyanka/cleanup.sh
# Comma (,): Multiple values: Runs at 9 AM and 6 PM.
0 9,18 * * *
# # Hyphen (-): Runs every hour from 9 AM to 5 PM.
0 9-17 * * *
# Slash (/): Runs every 10 minutes. Interval.
*/10 * * * *
```

## Practical DevOps Examples

### Backup Database Daily

```bash
0 2 * * * /scripts/db_backup.sh
```

---

### Clean Logs Every Sunday

```bash
0 0 * * 0 find /var/log -name "*.log" -mtime +30 -delete
```

---

### Monitor Disk Usage Every 5 Minutes

```bash
*/5 * * * * /scripts/disk_monitor.sh
```

---

### Restart Application Daily

```bash
0 3 * * * systemctl restart nginx
```

---

## How to Create a Cron Job

### Step 1: Create Script

```bash
vim test.sh
```

```bash
#!/bin/bash
echo "Cron Job Running" >> /tmp/output.log
```

---

### Step 2: Give Permission

```bash
chmod +x test.sh
```

---

### Step 3: Open Crontab

```bash
crontab -e
```

Add:

```bash
*/1 * * * * /home/priyanka/test.sh
```

---

### Step 4: Verify

```bash
crontab -l
```

---

### Step 5: Check Output

```bash
cat /tmp/output.log
```

---

## Interview Question

### What is Cron?

Cron is a Linux scheduler service used to run commands or scripts automatically at specified times and intervals.

### What is Crontab?

Crontab is a configuration file that stores cron job schedules for a user.

### Difference Between Cron and Crontab

| Cron                      | Crontab            |
| ------------------------- | ------------------ |
| Background service/daemon | Configuration file |
| Executes scheduled tasks  | Stores schedules   |
| Runs continuously         | Edited by users    |

### One-Line Interview Answer

> Cron is a Linux scheduling daemon that executes tasks automatically, while Crontab is the file where we define the schedule and commands to be executed.
