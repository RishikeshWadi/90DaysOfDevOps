# Day 12 – Breather & Revision (Days 01–11)

## Goal
Take a **one-day pause** to consolidate everything from Days 01–11 so you don’t forget the fundamentals you just built.

---

## What I Reviewed

### 1) Mindset & Plan
- Revisited Day 01 learning plan
- Goal still aligned: **Strong Linux fundamentals for DevOps + hands-on confidence**
- Tweak: Spend more time on **troubleshooting workflows** (logs → process → service)

---

### 2) Processes & Services (Day 04/05)
**Commands Re-run:**
```bash
ps aux | head
systemctl status ssh
journalctl -u ssh -n 10
```
**Observations:**
- `ps` gives quick visibility into running processes and resource usage
- `systemctl status` immediately shows service state and recent logs
- `journalctl -u` is fastest way to diagnose service issues

---

### 3) File Skills Practice (Days 06–11)
**Operations Practiced:**
```bash
echo "Revision Day" >> notes.txt
chmod 644 notes.txt
ls -l notes.txt
mkdir revision-test
cp notes.txt revision-test/
```
**Outcome:**
- Clear understanding of permissions and file ownership impact
- Confident with basic file and directory operations

---

### 4) Cheat Sheet Refresh (Day 03)
**Top 5 Commands I’d Use First in an Incident:**
1. `ls -l` – verify permissions quickly
2. `df -h` – check disk space issues
3. `free -m` – validate memory availability
4. `ps aux` – identify problematic processes
5. `journalctl -xe` – immediate log visibility

---

### 5) User / Group Sanity Check (Day 09 / 11)
**Scenario Recreated:**
```bash
sudo useradd testrev
id testrev
sudo chown testrev:testrev notes.txt
ls -l notes.txt
```
**Verification:**
- User created successfully
- Ownership change verified using `ls -l`

---

## Mini Self-Check

### Q1. Which 3 commands save you the most time right now, and why?
- `ls -l` – instant permission and ownership clarity
- `systemctl status` – quick service health check
- `journalctl -u <service>` – fastest way to debug failures

### Q2. How do you check if a service is healthy?
```bash
systemctl status <service>
journalctl -u <service> -n 20
ps aux | grep <service>
```

### Q3. How do you safely change ownership and permissions without breaking access?
```bash
sudo chown user:group file.txt
sudo chmod 644 file.txt
```
(Change ownership first, then adjust permissions conservatively)

### Q4. What will you focus on improving in the next 3 days?
- Faster troubleshooting using logs
- Stronger understanding of networking basics
- More real-world incident-style practice

---

```
#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
```

Happy Learning 
