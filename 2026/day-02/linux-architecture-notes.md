# Day 02 – Linux Architecture, Processes, and systemd

## Task
Today’s goal is to **understand how Linux works under the hood**.

### Boot Flow
Hardware → Kernel → systemd (PID 1) → Services → Users

---

## The Core Components of Linux (kernel, user space, init/systemd)

Linux is not just the kernel — it’s a layered system.

### Kernel (The Heart of Linux)
The Linux kernel is the core program.  
It directly talks to hardware.

**Key responsibilities:**
- Process management – CPU scheduling, context switching
- Memory management – virtual memory, paging, swapping
- File systems – ext4, xfs, procfs, sysfs
- Device drivers – keyboard, disk, network
- System calls – interface between user space and kernel

Applications cannot access hardware directly. They must request the kernel using system calls.

---

### User Space
User space is where applications run.

**Includes:**
- Shells (bash, zsh)
- System utilities (ls, ps, top, grep)
- Libraries (glibc – provides APIs like `malloc()`, `printf()`)
- Services & Daemons (nginx, sshd, cron)

User space is isolated from the kernel. If an app crashes, the kernel stays safe.

---

### Init System (systemd)
The init system is the first user-space process started by the kernel.

**Responsible for:**
- Starting services
- Managing system startup
- Handling service failures
- System shutdown/reboot

On modern Linux systems, this is **systemd**.

---

## How Processes Are Created and Managed

### What Is a Process?
A process is a running instance of a program.

A process contains:
- Program code
- Memory (heap, stack)
- File descriptors
- Process ID (PID)
- User and permissions

---

### Process Creation Flow
1. A user runs a command (e.g., `nginx`)
2. Shell requests the kernel to create a process
3. Kernel:
   - Allocates memory
   - Assigns a PID
   - Schedules it on the CPU
4. Process runs in user space

---

### Key Concepts
- **PID**: Unique process ID  
- **Parent / Child processes**
- **States:**
  - Running
  - Sleeping
  - Stopped
  - Zombie

The kernel scheduler decides which process runs when.  
Every running program is just a process managed by the kernel.

---

## What systemd Does and Why It Matters

### What Is systemd?
systemd is a service manager and system initializer.

It replaced older init systems like:
- SysVinit
- Upstart

---

### systemd Units
Everything in systemd is a unit.

**Common unit types:**
- `.service` → background services
- `.socket` → socket activation
- `.timer` → cron replacement
- `.mount` → mount points
- `.target` → group of units (runlevels)

**Example:** `nginx.service`

---

### Why systemd Matters
systemd matters because:
- Predictable service management
- Automatic recovery (self-healing)
- Better observability (logs + status)
- Dependency-based startup

---

## System Startup Flow
Power On → Bootloader (GRUB) → Linux Kernel → [init → systemd (PID 1)] → Start Services → User Applications

---

## Explain Process States (running, sleeping, zombie, etc.)

### Process States

**Running (R)**
- The process is currently using the CPU or is ready to run.
- Example: A script actively executing.

---

**Sleeping (S / D)**

- **Sleeping (S – Interruptible sleep):**
  - Waiting for an event like user input or I/O
  - Can be interrupted
  - Most normal background processes stay here

- **Disk sleep (D – Uninterruptible sleep):**
  - Waiting for disk or network I/O
  - Cannot be interrupted easily
  - Cannot be killed until the operation completes

---

**Stopped (T)**
- The process is paused, usually by a signal (e.g., Ctrl + Z)
- It can be resumed later

---

**Zombie (Z)**
- The process has finished execution, but its parent hasn’t collected its exit status
- Uses no CPU or memory—only an entry in the process table
- Indicates poor process handling by the parent

---

**Idle / Waiting**
- The process is waiting for CPU scheduling or resources

---

## List 5 Commands You Would Use Daily

1. **ps**  
   View running processes and their states.  
   Example: `ps aux`  
   Use `ps aux` to quickly identify zombie (Z) or stuck (D) processes.

2. **top / htop**  
   Real-time monitoring of CPU, memory, and process states.  
   Real-time system and process monitoring.

3. **ls**  
   List files and directories.  
   Example: `ls -l`

4. **systemctl**  
   Manage services.  
   Example: `systemctl status nginx`

5. **df**  
   Check disk usage.  
   Example: `df -h`

6. **cd**  
   Navigate between directories.

7. **grep**  
   Search text inside files or command output.  
   Example: `grep "ERROR" app.log`

---

## Resources
You may refer to:

- Linux `man` pages (`ps`, `top`, `systemctl`)
- Official systemd docs
- Your class notes

Avoid copying/pasting AI Generated content.
Focus on understanding.

---

## Why This Matters for DevOps
Linux is the base OS for almost every production system.

If you know how processes and systemd work, you can:
- Debug crashed services faster
- Fix CPU/memory issues
- Understand logs and service restarts confidently
- This knowledge saves hours during incidents.



Happy Learning
