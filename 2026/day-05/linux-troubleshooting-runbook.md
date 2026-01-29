# Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs

## Task
Today’s goal is to **run a focused troubleshooting drill**.

pick a running process/service on your system and:
- Capture a quick health snapshot (CPU, memory, disk, network)
- Trace logs for that service
- Write a **mini runbook** describing what you did and what you’d do next if things were worse

This turns yesterday’s practice into a repeatable troubleshooting routine.

### What’s a runbook?
A **runbook** is a short, repeatable checklist you follow during an incident: the exact commands you run, what you observed, and the next actions if the issue persists. Keep it concise so you can reuse it under pressure.

---

## Environment Basics

**`uname` prints system information.**

**Command:**
```bash
uname -a
```
`uname` prints system information.  
`-a` displays all details including kernel name, version, architecture, and build.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/uname_cat_command.jpg)

This command is used to confirm kernel version and CPU architecture when:
- correlating issues with kernel bugs
- checking driver compatibility
- validating OS consistency across servers

---

**Displays Linux distribution name, version, and release metadata**  

**Command:**
```bash
cat /etc/os-release
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/uname_cat_command.jpg)

This command is used to :
- confirm OS version and vendor
- check compatibility with packages and services
- match issues with distro‑specific documentation or bugs

---

## Filesystem Sanity

**Creates a temporary directory and copies a file into it to test disk write and read operations.** 

**Command:**
```bash
mkdir /tmp/runbook-demo
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/mkdir_tmp_command.jpg)

This command is used to verify:
- filesystem is writable
- permissions are working correctly
- disk is not mounted read‑only during incidents

---

**Shows disk space usage for all mounted filesystems in human‑readable format.**  

**Command:**
```bash
df -h
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/df-h_commad.jpg)

This command is used to: 
- detect disk‑full conditions
- identify filesystems nearing capacity
- explain service failures caused by lack of disk space

---

## CPU & Memory

**Displays process ID, CPU usage, memory usage, and command name for the `sshd` process.**  

**Command:**
```bash
ps -o pid,pcpu,pmem,comm -C sshd
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/ps-o_command.jpg)

This command is used to:
- detect high CPU consumption
- identify memory leaks
- confirm whether sshd is actively running or stuck

---

**Shows total, used, and free system memory and swap usage.**

**Command:**
```bash
free -h
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/free-h_command.jpg)

This command is used to:
- identify memory pressure
- check if swap is being heavily used
- explain performance degradation

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/top_command.jpg)
---

## Disk & IO

**Calculates the total disk usage of the `/var/log` directory.**  

**Command:**
```bash
du -sh /var/log
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/du-sh_directory_command.jpg)

This command is used to: 
- detect excessive log growth
- prevent disk exhaustion
- identify logging misconfigurations

---

**Reports CPU, memory, swap, and I/O statistics at regular intervals.**  

**Command:**
```bash
vmstat 1 3
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/vmstat_start_end_cmd.jpg)

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/vmstat.jpg)

This command is used to: 
Used to:
- detect high I/O wait
- identify swapping activity
- spot CPU contention under load

---

## Network

**Lists listening TCP/UDP sockets along with the processes that own them.**  

**Command:**
```bash
ss -tulpn | grep ssh
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/du-sh_tulpn_cmd.jpg)

This command is used to:
- confirm sshd is listening on port 22
- verify correct network binding
- troubleshoot connection failures

---

**Sends an HTTP HEAD request and returns response headers only.**  

**Command:**
```bash
curl -I http://localhost
```

This command is used to: 
- quickly check HTTP service reachability
- validate response codes
- avoid downloading full content during checks

---

## Logs Reviewed

**Check service logs via journalctl**

**Command:**
```bash
journalctl -u ssh -n 5
```
`journalctl` is a systemd log viewer.  
`-u ssh` filters logs only for the SSH service.  
`-n 5` shows the last 5 log entries.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/journalctl-u_cmd.jpg)

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/journalctl-u_cmd2.jpg)

This command is used to quickly check recent SSH service logs to identify:
- startup failures
- crashes
- authentication errors
- configuration issues

This helps confirm whether the service itself is failing or behaving normally.

---

**Inspect application logs (tail)**

**Command:**
```bash
tail -n 50 /var/log/auth.log
```
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-05/2026/day-05/day5/tail%20-n%20command.jpg)

Displays the last 50 lines of the authentication log file.

This command is used to: 
- inspect recent login attempts
- detect failed authentications
- identify suspicious access patterns

---

## Quick Findings
- sshd is running normally
- No resource or disk pressure observed
- Logs show expected authentication activity

---

## If This Worsens (Next Steps)
1. Restart SSH service: `systemctl restart ssh`
2. Increase logging verbosity using `LogLevel DEBUG`
3. Attach live diagnostics using `strace -p <pid>`

---

**Purpose:** Service‑focused, on‑call‑ready Linux troubleshooting runbook.

---

## Resources
You may refer to:

- Notes from Day 02–04
- Linux `man` pages (`top`, `ps`, `df`, `journalctl`, `ss/netstat`)
- class notes

---

## Why This Matters for DevOps
Incidents rarely come with perfect clues. A fast, repeatable checklist saves minutes when services misbehave.

This drill builds:
- Habit of capturing evidence before acting
- Confidence reading resource signals (CPU, memory, disk, network)
- Log-first mindset before restarts or escalations

These habits reduce downtime and prevent guesswork in production.

---

Use hashtags:  
#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham

Happy Learning  