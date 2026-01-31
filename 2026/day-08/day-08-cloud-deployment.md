# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## 🎯 Today’s Goal  
Today's goal is to **deploy a real web server on the cloud** and learn practical server management.

You will:
- Launch a cloud instance (AWS EC2 or Utho)
- Connect via SSH
- Install Nginx
- Configure security groups for web access (port 80 by default for nginx)
- Extract and save logs to a file
- Verify your webpage is accessible from the internet

This is real DevOps work - exactly what you'll do in production.

---

## Part 1: Launch Cloud Instance & SSH Access

### Step 1: Create a Cloud Instance (AWS EC2)

**High-level steps (AWS Console):**
1. Go to **EC2 → Launch Instance**
2. Choose **Ubuntu Server 22.04 LTS**
3. Instance type: `t2.micro` (Free Tier)
4. Create or select a **key pair (.pem)**
5. Configure **Security Group**:
   - SSH → Port `22` → Your IP
   - HTTP → Port `80` → Anywhere (`0.0.0.0/0`)
6. Storage
7. Review and launch your instance

**Post Launch **
Wait for your instance to launch successfully

---

### Step 2: Connect via SSH

```bash
ssh -i your-key.pem ubuntu@<your-instance-ip>
```

**Explanation:**
- `ssh` → Secure Shell for remote login
- `-i your-key.pem` → Identity file (private key)
- `ubuntu` → Default user for Ubuntu AMI
- `<your-instance-ip>` → Public IP of EC2 or using its Public DNS.

**Usage:**
Used to securely access your cloud server from your local machine.

If successful, you’ll be logged into your EC2 instance terminal.

---

## Part 2: Install Nginx

### Step 1: Update System Packages

```bash
sudo apt update 

sudo apt upgrade

or

sudo apt update && sudo apt upgrade
```

**Explanation:**
- `apt update` → Refreshes package index
- `apt upgrade` → Install latest updates

**Usage:**
Always run this before installing new software on a fresh server.

---

### Step 2: Install Nginx

```bash
sudo apt install nginx
```

**Explanation:**
- Install the **Nginx web server**

**Usage:**
Nginx is a lightweight, high-performance web server commonly used in production.

---

### Step 3: Verify Nginx Is Running

```bash
systemctl status nginx
```

**Explanation:**
- `systemctl` → Controls system services
- `status nginx` → Checks Nginx service state

**Output:**
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-08/2026/day-08/day08Snaps/NginxStatus.jpg)

---

## Part 3: Security Group Configuration

Ensure your **EC2 Security Group** allows:

| Type | Protocol | Port | Source |
|----|----|----|----|
| SSH | TCP | 22 | Your IP |
| HTTP | TCP | 80 | 0.0.0.0/0 |

---

### Test Web Access

Open your browser and visit:
You should see the **Nginx Welcome Page**

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-08/2026/day-08/day08Snaps/welcomeToNginx.jpg)

## Part 4: Extract Nginx Logs

### Step 1: View Nginx Logs

```bash
sudo tail /var/log/nginx/access.log
```

**Explanation:**
- `tail` → Shows last lines of a file
- `access.log` → Records all HTTP requests

**Usage:**
Used to verify incoming traffic and debug web access issues.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-08/2026/day-08/day08Snaps/NginxLogs.jpg)

---

### Step 2: Save Logs to a File

```bash
sudo cat /var/log/nginx/access.log > ~/nginx-logs.txt
```

**Explanation:**
- `cat` → Reads file content
- `>` → Redirects output to a file
- `~/nginx-logs.txt` → Saved in home directory

**Usage:**
Creates a portable log file for analysis or submission.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-08/2026/day-08/day08Snaps/NginxLogsToFiles.jpg)

---

### Step 3: Download Log File to Local Machine

#### From your local machine (new terminal window)

**For AWS:**
```bash
scp -i your-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

**For Utho:**
```bash
scp root@<your-instance-ip>:~/nginx-logs.txt .
```

**Explanation:**
- `scp` → Secure Copy
- Copies file from remote server to local system

**Usage:**
Used to download logs, backups, or artifacts from servers.

---

## Outcome Checklist

✔ EC2 instance launched  
✔ SSH access working  
✔ Nginx installed and running  
✔ Webpage accessible via public IP  
✔ Logs extracted and downloaded  

---

## Why This Matters for DevOps

This exercise teaches you:
- **Cloud infrastructure provisioning** - launching and configuring servers
- **Remote server management** - SSH, security, access control
- **Service deployment** - installing and running applications
- **Log management** - accessing and analyzing logs
- **Security** - configuring firewalls and security groups

These are core skills for any DevOps engineer working in production.

---

```
#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
```

Happy Learning