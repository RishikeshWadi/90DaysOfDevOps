# Day 09 – Linux User & Group Management Challenge

## Task
Today's goal is to **practice user and group management** by completing hands-on challenges.

Figure out how to:
- Create users and set passwords
- Create groups and assign users
- Set up shared directories with group permissions

---

## Task 1: Create Users

### Users Created
- tokyo
- berlin
- professor

### Commands Used
```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

### Explanation
- `useradd` creates a new user.
- `-m` creates the home directory under `/home`.
- `passwd` sets the user password.

### Verification
```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor"
ls /home
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/userTokyo.jpg)
![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/userBerlin.jpg)

---

## Task 2: Create Groups

### Groups Created
- developers
- admins

### Commands Used
```bash
sudo groupadd developers
sudo groupadd admins
```

### Explanation
- `groupadd` creates a new Linux group.

### Verification
```bash
cat /etc/group | grep -E "developers|admins"
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/groupadd_cmd.jpg)

---

## Task 3: Assign Users to Groups

### Group Assignments
- tokyo → developers
- berlin → developers, admins
- professor → admins

### Commands Used
```bash
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
sudo usermod -aG admins professor
```

### Explanation
- `usermod` modifies user properties.
- `-aG` appends the user to groups without removing existing memberships.

### Verification
```bash
groups tokyo
groups berlin
groups professor
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/assignUsersToGroup.jpg)

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/groups_cmd.jpg)

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/checkCreatedGroups.jpg)

---

## Task 4: Shared Directory – /opt/dev-project

### Commands Used
```bash
sudo mkdir /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project
```

### Explanation
- `mkdir` creates the directory.
- `chgrp` changes group ownership.
- `chmod 775` allows full access to owner & group, read/execute for others.

### Verification
```bash
ls -ld /opt/dev-project
```

### Testing Access
```bash
sudo -u tokyo touch /opt/dev-project/tokyo.txt
sudo -u berlin touch /opt/dev-project/berlin.txt
ls -l /opt/dev-project
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/Task4.jpg)

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/Task4_2.jpg)

---

## Task 5: Team Workspace

### User & Group Created
- User: nairobi
- Group: project-team

### Commands Used
```bash
sudo useradd -m nairobi
sudo passwd nairobi
sudo groupadd project-team
```

### Add Users to Group
```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

### Create Workspace Directory
```bash
sudo mkdir /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

### Verification
```bash
groups nairobi
ls -ld /opt/team-workspace
```

### Testing Access
```bash
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
ls -l /opt/team-workspace
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-09/2026/day-09/day09Snaps/Task5.jpg)

---

## What I Learned
- Practical user and group management in Linux
- Using group-based permissions for team collaboration
- Safely validating access using `sudo -u`
- How shared directories are configured in real-world DevOps environments


```
#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
```

Happy Learning