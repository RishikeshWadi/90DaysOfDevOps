# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

## Task
Today's goal is to **understand where things live in Linux** and **practice troubleshooting like a DevOps engineer**.

Created notes covering:
- Linux File System Hierarchy (the most important directories)
- Practice solving real-world scenarios step by step

This consolidates Linux fundamentals and prepares for real-world troubleshooting.

---

## gi Part 1: Linux File System Hierarchy

Understanding the Linux filesystem is important because **logs, configs, binaries, and user data live in predictable places**.

---

## Core Directories

### `/` (root) 
The top-level directory. Everything in Linux starts here.
The starting point of everything.

```bash
ls -l /
```

Directories like /bin, /etc, /home, /var, /usr

**I would use to understand the overall system structure or navigate anywhere in Linux.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/root_dir.jpg)

---

### `/home`
Home directories for all regular users.
User home directories

```bash
ls -l /home
```

User folders such as user, ubuntu

**I would use this when accessing user files, scripts, SSH keys, or application data.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/home_dir.jpg)

---

### `/root`
Home directory of the root (admin) user.
Root user's home directory

```bash
ls -l /root
```

**I would use this while performing system-level administration tasks.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/root_dir2.jpg)

---

### `/etc`
System-wide configuration files.
Configuration files

```bash
ls -l /etc
```

Files like hostname, hosts, ssh/, systemd/

**I would use this to Configure services, networking, users, or system behavior.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/etc_dir1.jpg)
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/etc_dir2.jpg)

---

### `/var/log`
System and application logs (very important for DevOps).
Log files

```bash
ls -l /var/log
```

syslog, auth.log, journal/

**I would use this to troubleshoot failures, crashes, or performance issues.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/var_logs_dir.jpg)

---

### `/tmp`
Temporary files created by applications.
Temporary files

Commands like ls, cp, mv

```bash
ls -l /tmp
```

**I would use this to store short-lived or temporary data.**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/tmp_dir.jpg)

---

## Additional Directories (Good to Know)

### `/bin`
Essential system command binaries.

```bash
ls -l /bin
```

Commands like ls, cp, mv

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/bin_dir.jpg)


### `/usr/bin`
Most user-level command binaries.

Commands like git, python, curl

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/usr_bin_dir.jpg)


### `/opt`
Optional or third‑party applications.

---

## Hands-On Tasks

**Identify logs consuming the most disk space.**
```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/find_largest_log.jpg)


***Confirm system identity.**
```bash
cat /etc/hostname
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/hotname_view.jpg
)

**Review permissions, hidden files, and user data.**
```bash
ls -la ~
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/la_-la_cmd.jpg)

---

### Part 2: Scenario-Based Practice

**Important:** Focus on understanding the **troubleshooting flow**, not memorizing commands. Use the hints!

---

#### SOLVED EXAMPLE: Understanding How to Approach Scenarios

**Example Scenario: Check if a service is running**
```
Question: How do you check if the 'nginx' service is running?
```

**My Solution (Step by step):**

**Step 1:** Check service status
```bash
systemctl status nginx
```
**Why this command?** It shows if the service is active, failed, or stopped

**Step 2:** If service is not found, list all services
```bash
systemctl list-units --type=service
```
**Why this command?** To see what services exist on the system

**Step 3:** Check if service is enabled on boot
```bash
systemctl is-enabled nginx
```
**Why this command?** To know if it will start automatically after reboot

**What I learned:** Always check status first, then investigate based on what you see.

---

**Scenario 1: Service Not Starting** 
```
A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.
```

**Hint:**
- First check: Is the service running or failed?
- Then check: What do the logs say?
- Finally check: Is it enabled to start on boot?

**Commands to explore:** `systemctl status myapp`, `systemctl is-enabled myapp`, `journalctl -u myapp -n 50`

**Resource:** Review Day 04 (Process and Services practice)

```
Step 1: 
```bash
systemctl status myapp
```
Why:It shows if the service is active, failed, or stopped

Step 2:
```bash
systemctl is-enabled myapp
```
Why: To know if it will start automatically after reboot

Step 3:
```bash
journalctl -u myapp -n 50
```
Why: View recent logs to find error messages.

Step 4:
```bash
systemctl restart myapp
```
Why: Attempt a restart after reviewing logs.

---

### 🔥 Scenario 2: High CPU Usage

**Scenario 2: High CPU Usage** 
```
Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?
```

**Hint:**
- Use a command that shows **live** CPU usage
- Look for processes sorted by CPU percentage
- Note the PID (Process ID) of the top process

**Commands to explore:** `top` (press 'q' to quit), `htop`, `ps aux --sort=-%cpu | head -10`

**Resource:** Review Day 05 (Troubleshooting Drill - CPU & Memory section)

Step 1:
```bash
top
```
Why: View live CPU usage and running processes.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/top_cmd.jpg)


Step 2:
```bash
ps aux --sort=-%cpu | head -10
```
Why: Identify top CPU-consuming processes.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/pa_aux_cmd.jpg)


Step 3:
```bash
ps -fp <PID>
```
Why: Get details of the problematic process.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/ps-fp_cmd.jpg)

---

**Scenario 3: Finding Service Logs** 
```
A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?
```

**Hint:**
- systemd services → logs are in journald
- Command pattern: `journalctl -u <service-name>`
- Use -n flag to limit number of lines
- Use -f flag to follow logs in real-time (like tail -f)

Step 1:
```bash
systemctl status docker
```
Why: Confirm service status and basic log info.

Step 2:
```bash
journalctl -u docker -n 50
```
Why: View recent logs.

Step 3:
```bash
journalctl -u docker -f
```
Why: Follow logs in real time.


**Commands to explore:**
```bash
# Check service status first
systemctl status ssh
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/systemctl_status_ssh.jpg)

# View last 50 lines of logs
```bash
journalctl -u ssh -n 50
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/journalctl-u_cmd.jpg)

# Follow logs in real-time
```bash
journalctl -u ssh -f
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/journalctl-ussh_cmd.jpg)


**Resource:** Review Day 04 (Process and Services - Log checks section)

---


**Scenario 4: File Permissions Issue** 
```
A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?
```

**Hint:**
- First: Check what permissions the file has
- Understand: Files need 'x' (execute) permission to run
- Fix: Add execute permission with chmod

**Step-by-step solution structure:**

Step 1: Check current permissions
Command: 

```bash
ls -l /home/user/startup.sh
```
Look for: -rw-r--r-- (notice no 'x' = not executable)

Step 2: Add execute permission
Command: 
```bash
chmod +x /home/user/startup.sh
```

Step 3: Verify it worked
Command: 
```bash
ls -l /home/user/startup.sh
```
Look for: -rwxr-xr-x (notice 'x' = executable)

Step 4: Try running it
Command: 
```bash
./startup.sh
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-07/2026/day-07/day07snap/check_file_permission.jpg
)

**Resource:** Review Day 02 (File Permissions and Users Management)

---

## 🎯 Key Takeaways

- Linux directories tell you **where to look**
- Logs explain **what went wrong**
- Permissions decide **what can run**
- DevOps troubleshooting is about **process, not panic**

---

## Why This Matters for DevOps
Understanding the file system is critical for:
- Knowing where to find logs, configs, and binaries
- Troubleshooting deployment issues
- Writing automation scripts that work across systems

Scenario-based practice prepares you for:
- Real production incidents
- DevOps interviews
- On-call troubleshooting under pressure

These are questions you **will** face in interviews and during real incidents.

----

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
```

Happy Learning