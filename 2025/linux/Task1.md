# Week 2: Linux System Administration & Automation
## Task 1: User & Group Management 
---

# Linux Users, Groups, and Permissions

Linux is a multi-user operating system that allows multiple users to access the system with different permission levels. Understanding user and group management is essential for security and access control.

## 1. Users in Linux
A **user** is an entity that can log in and execute commands on the system.

### Types of Users:
1. **Root User (Superuser)**
   - Has **full control** over the system.
   - Can execute any command, modify system files, and manage other users.
   - Identified by `UID 0`.

2. **Regular Users**
   - Created by the administrator.
   - Have limited access based on permissions.
   - Each user has a **unique user ID (UID)**.

3. **System Users**
   - Used by system services and processes (e.g., `www-data`, `nobody`).
   - Usually **don’t have login access**.

### `/etc/passwd` – User Account Information
The `/etc/passwd` file contains user account details. Each line follows this format:
```
username:x:UID:GID:comment:home_directory:shell
```
Example:
```
devops_user:x:1001:1001:DevOps User:/home/devops_user:/bin/bash
```
- `username` → Login name.
- `x` → Password is stored in `/etc/shadow`.
- `UID` → Unique User ID.
- `GID` → Group ID (primary group).
- `comment` → Description (optional).
- `home_directory` → User’s home folder.
- `shell` → Default shell (e.g., `/bin/bash`).

---

## 2. Groups in Linux
A **group** is a collection of users with shared permissions.

### Types of Groups:
1. **Primary Group**
   - Assigned when the user is created.
   - Every file the user creates belongs to this group.

2. **Secondary (Supplementary) Groups**
   - Users can belong to multiple secondary groups for additional permissions.

### `/etc/group` – Group Information
The `/etc/group` file stores group details. Format:
```
group_name:x:GID:user1,user2
```
Example:
```
devops_team:x:1002:devops_user,admin_user
```
- `group_name` → Group name.
- `x` → Password field (rarely used, typically in `/etc/gshadow`).
- `GID` → Group ID.
- `user1,user2` → Members of the group.

---

## 3. File Permissions in Linux
Each file and directory in Linux has associated **permissions** and **ownership**.

### Understanding File Permissions
Run `ls -l` to see permissions:
```
-rw-r--r--  1 devops_user devops_team  2048 Feb 26 12:00 example.txt
```
#### Breakdown of `-rw-r--r--`
| Symbol | Meaning  |
|---------|-----------|
| `-` | File type (`-` = file, `d` = directory, `l` = symlink) |
| `rw-` | **Owner** (read, write) |
| `r--` | **Group** (read only) |
| `r--` | **Others** (read only) |


## **Important System Files**  

### **`/etc/passwd` (User Database)**  
Stores user information, including username, UID, GID, home directory, and default shell.  
Example entry:  
```
devops_user:x:1001:1001::/home/devops_user:/bin/bash
```

### **`/etc/group` (Group Database)**  
Defines groups and their members.  
Example entry:  
```
devops_team:x:1002:devops_user
```

### **`/etc/shadow` (Password File - Encrypted)**  
Contains user passwords in an encrypted format.  

### **`/etc/sudoers` (Sudo Configuration)**  
Controls administrative privileges.  

### **`/etc/ssh/sshd_config` (SSH Configuration)**  
Manages SSH login permissions.  

### Changing Permissions
- Change **file owner**:
  ```bash
  sudo chown devops_user:devops_team example.txt
  ```
- Change **permissions** (e.g., allow the owner to execute):
  ```bash
  chmod u+x example.txt
  ```
- Numeric method (`r=4, w=2, x=1`):
  ```bash
  chmod 755 example.txt
  ```
  - **7** → Owner: Read(4) + Write(2) + Execute(1)  
  - **5** → Group: Read(4) + Execute(1)  
  - **5** → Others: Read(4) + Execute(1)  

---
# **3. Step-by-Step Task Execution**  

### **Step 1: Create a User `devops_user`**
```bash
sudo useradd -m devops_user
```
or
```bash
sudo useradd -m -s /bin/bash devops_user
```
- `-m` → Creates a home directory (`/home/devops_user`).  
- `-s /bin/bash` → Assigns Bash as the default shell.

![Verify ](https://github.com/RishikeshWadi/DevOps_Project/blob/main/CloudSecurityWithIAM/projectImages/EC2InstanceNameandTags.png)

### **Step 2: Create a Group `devops_team`**  
```bash
sudo groupadd devops_team
```
- Creates a new group named `devops_team`.

### **Step 3: Add `devops_user` to `devops_team` Group**  
```bash
sudo usermod -aG devops_team devops_user
```
- `-aG` → Appends the user to the specified group.  

### **Step 4: Set a Password for `devops_user`**  
```bash
sudo passwd devops_user
```
- Enter a password when prompted.  

### **Step 5: Grant Sudo Access to `devops_user`**  
#### **Method 1: Add User to `sudo` Group**  
```bash
sudo usermod -aG sudo devops_user
```
- This gives `devops_user` default sudo access.  

#### **Method 2: Grant Specific sudo Privileges - Edit `/etc/sudoers` File**  
```bash
sudo visudo
```
Add the following line at the end:  
```
devops_user  ALL=(ALL:ALL) ALL
```
- This allows `devops_user` to execute any command.  

### **Step 6: Restrict SSH Login for Certain Users**  
Edit the SSH configuration file:  
```bash
sudo nano /etc/ssh/sshd_config
```
#### **To deny specific users from logging in via SSH, add:**  
Add the following line:  
```
DenyUsers test_user user1
```
- This prevents `test_user` and `user1` from logging in via SSH.  

#### **To allow only specific users**    
```
AllowUsers devops_user root
```
- To allow only `devops_user` and `root` to log in via SSH.

- Save and exit (CTRL+X, then Y, then Enter).

### **Step 7: Restart SSH Service to Apply Changes**  
```bash
sudo systemctl restart sshd
```
- This applies the SSH restrictions.

- If you face any failure, while restarting ssh service, check the following:

### Install SSH if Not Installed
ensure SSH is installed by running:
```bash
sudo apt update && sudo apt install openssh-server -y
```

### Check the Exact Service Name
Run the following command to check if SSH is installed and its exact service name:
```bash
systemctl list-unit-files | grep ssh
```

### Enable and Start SSH Service
Use the correct service name to enable and start SSH:
```bash
sudo systemctl enable --now ssh
```
or
```bash
sudo systemctl enable --now sshd
```
---



## **Verification**  
### **Check User Information**  
```bash
id devops_user
```
- This displays the UID, GID, and group memberships.  

![Verify ](https://github.com/RishikeshWadi/DevOps_Project/blob/main/CloudSecurityWithIAM/projectImages/EC2InstanceNameandTags.png)
### **Check Group Membership**  
```bash
groups devops_user
```

### **Verify Sudo Access**  
```bash
sudo whoami
```
- Expected output: `root`  
or
```bash
sudo -l -U devops_user
```

![Verify ](https://github.com/RishikeshWadi/DevOps_Project/blob/main/CloudSecurityWithIAM/projectImages/EC2InstanceNameandTags.png)


### **Test SSH Login Restriction**  
Try logging in as a restricted user to confirm access is denied.

---

## **Summary**
✔ **Created a user (`devops_user`) and group (`devops_team`).**  
✔ **Added `devops_user` to `devops_team`.**  
✔ **Set a password and granted sudo access.**  
✔ **Restricted SSH login for certain users.**  
