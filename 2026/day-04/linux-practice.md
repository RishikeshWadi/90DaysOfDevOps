# Day 04 – Linux Practice: Processes and Services

## Task
Today’s goal is to **practice Linux fundamentals with real commands**.

Create a short practice note by actually running basic commands and capturing the output:
- Check running processes
- Inspect one systemd service
- Capture a small troubleshooting flow

---

# Linux Practice Note (Hands-on)

## Process checks

### List running processes

```bash
ps aux | head -n 5
```

**Output:**
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-04/2026/day-04/screenshots/ps%20aux%20comand.jpg)

**Explanation & Usage:**
`ps` shows running processes.

* `a` → processes from all users
* `u` → user-oriented format (CPU, MEM, user)
* `x` → include processes without a terminal
  Use this when you want a snapshot of what is running on the system.

---

### Find processes by name

```bash
pgrep -l ssh
```

```bash
pgrep -l python
```

```bash
pgrep -a ssh
```

**Output:**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-04/2026/day-04/screenshots/pgrep%20command.jpg)

**Explanation & Usage:**
`pgrep` searches process IDs by name.

* `-l` → also prints the process name
  Useful for quickly checking **whether a specific application is running** and how many instances exist.

* `-a` → (or --list-full) 
  flag is used to list the full command line of matching processes along with their process IDs (PIDs). 

---

## Service checks (systemd)

> Target service for inspection : **ssh**

### Check service status

```bash
systemctl status ssh
```

**Output:**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-04/2026/day-04/screenshots/systemctl%20status%20command.jpg)

**Explanation & Usage:**
`systemctl status` shows whether a service is active, inactive, or failed, along with recent logs.

---

### List running services

```bash
systemctl list-units --type=service | head
```

**Output:**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-04/2026/day-04/screenshots/systemctl%20list-units%20command.jpg)

**Explanation & Usage:**
This command lists all currently loaded services.
Commonly used to **verify whether a service is running** on a VM or bare-metal Linux system.

---

## Log checks

### Check service logs via journalctl

```bash
journalctl -u ssh --no-pager | head
```

**Output:**
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-04/2026/day-04/screenshots/journalctl%20command.jpg)

**Explanation & Usage:**
`journalctl` queries logs collected by systemd.

* `-u ssh` → logs only for the ssh service
* `--no-pager` → prints output directly
  If systemd is unavailable, journal logs will not exist.

---

### Inspect application logs (tail)

```bash
tail -n 10 /var/log/chrome.supervisord.log
```

**Output:**

```
2026-01-27 09:15:42,570 INFO exited: apply_patch (exit status 42; expected)
2026-01-27 09:15:42,571 INFO exited: chromium (exit status 42; expected)
2026-01-27 09:15:42,572 INFO exited: notebook_server (exit status 42; expected)
2026-01-27 09:15:42,573 INFO success: logrotate entered RUNNING state
2026-01-27 09:15:42,573 INFO success: python_tool entered RUNNING state
```

**Explanation & Usage:**
`tail` displays the last lines of a file.

* `-n 10` → show last 10 lines
  Used during troubleshooting to see the most recent errors or status messages.

---

## Mini troubleshooting steps

1. **Is the process running?**

   * Use `ps aux` or `pgrep -l <process>` to confirm.

2. **Is the service manager available?**

   * If `systemctl` fails, check if the system is a container or minimal OS.

3. **Check relevant logs**

   * Use `journalctl` on systemd systems or `tail` for application logs.

4. **Restart correctly**

   * VMs: `systemctl restart <service>`
   * Containers: restart via supervisor or container runtime.

5. **Validate again**

   * Re-check process list and logs to confirm recovery.

---

## Resources
You may refer to:

- Your notes from Day 02 and Day 03
- Linux `man` pages
- Your class notes

---

## Why This Matters for DevOps
Hands‑on practice builds speed and confidence.

When issues happen in production, you won’t have time to search for basic commands.  
This day helps you build muscle memory with Linux fundamentals.

---

Use hashtags:
#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham

Happy Learning