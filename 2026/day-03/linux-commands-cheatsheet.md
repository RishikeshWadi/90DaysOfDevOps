# Day 03 – Linux Commands Practice

## Task
Today’s goal is to **build Linux command confidence**.

*I've created a Linux Commands Cheat Sheet focused on:*

---

## Process Management
- `ps aux` 
    – Displays all running processes with detailed information  
- `top` 
    – Shows real-time CPU and memory usage  
- `htop` 
    – Interactive and user-friendly process monitor  
- `atop` 
    – Advanced process monitor with disk and network stats  
- `kill <PID>` 
    – Sends a signal to stop a process  
- `kill -9 <PID>` 
    – Forcefully terminates a process  
- `pkill <name>` 
    – Kills processes by name  
- `pgrep <name>` 
    – Finds process IDs by name  
- `jobs` 
    – Lists background jobs  
- `nice` 
    – Starts a process with a given priority  
- `renice` 
    – Changes priority of a running process  
- `uptime` 
    – Shows system running time and load  
- `watch <cmd>` 
    – Repeats a command at regular intervals  

---

## File System & File Operations
- `ls -la` 
    – Lists files with permissions and hidden files  
- `pwd` 
    – Prints the current working directory  
- `cd <dir>` 
    – Changes the current directory  
- `tree` 
    – Displays directory structure in tree format  
- `mkdir <dir>` 
    – Creates a new directory  
- `rmdir <dir>` 
    – Deletes an empty directory  
- `rm -rf <dir>` 
    – Deletes files or directories recursively  
- `cp -r <source> <destination>` 
    – Copies files or directories  
- `mv <source> <destination>` 
    – Moves or renames files  
- `stat <file>` 
    – Displays detailed file information  
- `find /path -name file` 
    – Searches files by name  
- `locate <fileName>` 
    – Quickly finds files using index  
- `du -sh <dir>` 
    – Shows directory size  
- `df -h` 
    – Displays disk usage  
- `chmod 755 <fileName>` 
    – Changes file permissions  
- `chown user:group <fileName>`
    – Changes file ownership  

---

## Networking & Troubleshooting
- `ping <host>` 
    – Tests network connectivity  
- `ip addr` 
    – Displays IP addresses and interfaces  
- `ip link` 
    – Shows network interface status  
- `ip route` 
    – Displays routing table  
- `ifconfig` 
    – Shows network configuration (legacy)  
- `ss -tuln` 
    – Lists listening ports  
- `netstat -tuln` 
    – Shows open ports and connections  
- `curl <url>` 
    – Sends HTTP requests to test APIs  
- `wget <url>` 
    – Downloads files from the internet  
- `dig <domain>` 
    – Performs DNS lookup  
- `nslookup <domain>` 
    – Queries DNS records  
- `traceroute <host>` 
    – Traces network path  
- `nc -zv host port` 
    – Tests port connectivity  
- `tcpdump` 
    – Captures network packets  
- `hostname -I` 
    – Displays system IP address  

---

## Resources
You may refer to:

- Linux `man` pages
- Your class notes
- Reliable Linux command references

---

## Why This Matters for DevOps
Real production issues are solved at the command line.

The faster you can inspect logs and network issues, the faster you can:
- Restore service
- Reduce downtime
- Gain trust as an operator

---

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham

Happy Learning