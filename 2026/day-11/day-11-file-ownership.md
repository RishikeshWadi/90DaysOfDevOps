# Day 11 – File Ownership Challenge (chown & chgrp)

## Task
Master file and directory ownership in Linux.

- Understand file ownership (user and group)
- Change file owner using `chown`
- Change file group using `chgrp`
- Apply ownership changes recursively

---

## Task 1: Understanding Ownership

I started by listing files in my home directory to understand file ownership.

### Command Used
```bash
ls -l
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task1.jpg)

### Explanation
- **Owner**: The user who owns the file (usually the creator).
- **Group**: A collection of users who share access permissions to the file.

### Difference Between Owner and Group
- **Owner** has primary control over the file (read/write/execute).
- **Group** allows shared access among multiple users without changing ownership.

---

## Task 2: Basic `chown` Operations

### Files Created
```bash
touch devops-file.txt
```

### Check Current Owner
```bash
ls -l devops-file.txt
```

### Ownership Changes
```bash
sudo chown tokyo devops-file.txt
sudo chown berlin devops-file.txt
```

### Verification
```bash
ls -l devops-file.txt
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task2.jpg)

---

## Task 3: Basic `chgrp` Operations

### File Created
```bash
touch team-notes.txt
```

### Group Created
```bash
sudo groupadd heist-team
```

### Change Group
```bash
sudo chgrp heist-team team-notes.txt
```

### Verification
```bash
ls -l team-notes.txt
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task3.jpg)

---

## Task 4: Combined Owner & Group Change

### File and Directory Created
```bash
touch project-config.yaml
mkdir app-logs
```

### Change Owner & Group Together
```bash
sudo chown professor:heist-team project-config.yaml
sudo chown berlin:heist-team app-logs
```

### Verification
```bash
ls -l project-config.yaml
ls -ld app-logs
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task4.jpg)

---

## Task 5: Recursive Ownership

### Directory Structure Created
```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

### Group Created
```bash
sudo groupadd planners
```

### Recursive Ownership Change
```bash
sudo chown -R professor:planners heist-project/
```

### Verification
```bash
ls -lR heist-project/
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task5.jpg)

---

## Task 6: Practice Challenge

### Users Created
```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

### Groups Created
```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

### Directory & Files Created
```bash
mkdir bank-heist
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

### Ownership Assigned
```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

### Verification
```bash
ls -l bank-heist/
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-11/2026/day-11/day11Snaps/Task6.jpg)

---

## Files & Directories Created
- devops-file.txt
- team-notes.txt
- project-config.yaml
- app-logs/
- heist-project/
- bank-heist/

---

## Changes

- devops-file.txt: user → tokyo → berlin
- team-notes.txt: group → heist-team
- project-config.yaml: professor:heist-team
- app-logs/: berlin:heist-team
- heist-project/: professor:planners (recursive)
- access-codes.txt: tokyo:vault-team
- blueprints.pdf: berlin:tech-team
- escape-plan.txt: nairobi:vault-team

---

## Key Commands

```bash
ls -l filename
sudo chown newowner filename
sudo chgrp newgroup filename
sudo chown owner:group filename
sudo chown -R owner:group directory/
sudo chown :groupname filename
```

---

## What I Learned:

1. Linux file ownership is divided into owner and group for controlled access.
2. chown can modify both user and group, while chgrp is group-specific.
3. Recursive ownership changes are critical for managing large directory structures efficiently.

---

```
#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
```

Happy Learning