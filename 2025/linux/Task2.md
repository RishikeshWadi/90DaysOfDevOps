# Week 2: Linux System Administration & Automation
## Task 2: File & Directory Permissions
---
- This task involves creating a directory and a file, setting specific permissions, and verifying them using the `ls -l` command.

### 1. Create a Directory and a File
```bash
mkdir /devops_workspace
```

```bash
touch /devops_workspace/project_notes.txt
```

### 2. Set Permissions
- Set permissions:
    - Owner can edit, group can read, others have no access.
The required permissions are:
- **Owner**: Read and Write (`rw-`)
- **Group**: Read-only (`r--`)
- **Others**: No access (`---`)

```bash
chmod 640 /devops_workspace/project_notes.txt
```

### 3. Verify Permissions
Use the `ls -l` command to check if the permissions are set correctly:
```bash
ls -l /devops_workspace/
```

### 4. Expected Output

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/week2-linux/2025/linux/screenshots/Task2_Output.jpg)

---

- File and directory permissions in Linux determine who can read, write, or execute files and directories. These permissions help maintain security and control over system files and user data.

---

## Types of Users in Linux Permissions
Each file and directory has three types of users:
- **Owner (User)** – The creator of the file or directory.
- **Group** – A set of users who share the same group permissions.
- **Others** – Any user who is not the owner or part of the group.

---

## Types of Permissions
| Permission | Symbol | File Meaning | Directory Meaning |
|------------|--------|--------------|------------------|
| **Read** | `r` (4) | Can view file contents | Can list files in the directory |
| **Write** | `w` (2) | Can modify the file | Can add, delete, or rename files in the directory |
| **Execute** | `x` (1) | Can run the file as a program/script | Can enter (`cd`) the directory |

---

## Viewing File Permissions
Use the `ls -l` command to view permissions:
```bash
ls -l
```
Example Output:
```
-rw-r--r-- 1 user group 1234 Mar 2 10:00 example.txt
```
Breaking down `-rw-r--r--`:
- `-`   → File type: -=file,d=directory
- `rw-` → Owner: Read & Write
- `r--` → Group: Read-only
- `r--` → Others: Read-only

---

## Changing File Permissions
### Using `chmod`
- The chmod command is used to modify permissions.
**Symbolic Method:**
```bash
chmod u=rwx,g=rx,o=r file.txt
```

**Numeric Method:**
- Each permission has a numeric value:
  - r = 4
  - w = 2
  - x = 1
Combine the values to set permissions:
```bash
chmod 754 file.txt
```
- **7 (Owner)** → `rwx`
- **5 (Group)** → `r-x`
- **4 (Others)** → `r--`

---

## Changing Ownership and Group
- Change owner:
  ```bash
  chown new_user file.txt
  ```
- Change group:
  ```bash
  chgrp new_group file.txt
  ```
- Change both owner and group:
  ```bash
  chown new_user:new_group file.txt
  ```
---

## Directory Permissions
Permissions for directories work slightly differently:
- **Read (`r`)** → Allows listing files (`ls`).
- **Write (`w`)** → Allows adding/deleting files.
- **Execute (`x`)** → Allows entering the directory (`cd`).

Example:
```bash
ls -ld mydir
```
Output:
```
drwxr-x--- 2 user group 4096 Mar 2 10:00 mydir
```

### Changing Directory Permissions
```bash
chmod 755 mydir
```
- `7 (rwx)` → Owner can do everything.
- `5 (r-x)` → Group can read & enter.
- `5 (r-x)` → Others can read & enter.

---

manage security and access control effectively. Using `chmod`, `chown`, and `ls -l`, you can configure permissions to protect sensitive data.

---

# File Permissions - Numeric (Octal) Method

- file permissions determine who can **read, write, and execute** a file or directory. These permissions are represented numerically using the **octal (base 8) system**.

## Numeric Representation of Permissions
Each permission type is assigned a numeric value:

| Permission | Symbol | Numeric Value |
|------------|--------|--------------|
| No permission | `---` | `0` |
| Execute (`x`) | `--x` | `1` |
| Write (`w`) | `-w-` | `2` |
| Write & Execute (`wx`) | `-wx` | `3` |
| Read (`r`) | `r--` | `4` |
| Read & Execute (`rx`) | `r-x` | `5` |
| Read & Write (`rw-`) | `rw-` | `6` |
| Read, Write & Execute (`rwx`) | `rwx` | `7` |

A Linux file or directory has three types of users:
1. **Owner**
2. **Group**
3. **Others**

Each user type gets an octal number representing their permissions, written as three digits.

## Examples

### 1. Full Permissions for Everyone
```bash
chmod 777 file.txt
```
**Explanation:** `777` → `(rwx rwx rwx)` → Owner, group, and others have full permissions.

### 2. Owner Full, Group and Others Read & Execute
```bash
chmod 755 file.txt
```
**Explanation:** `755` → `(rwx r-x r-x)` → Owner has full permissions, group and others can read & execute.

### 3. Owner Read & Write, Group and Others Read Only
```bash
chmod 644 file.txt
```
**Explanation:** `644` → `(rw- r-- r--)` → Owner can read & write, others can only read.

## Viewing File Permissions
To check current file permissions:
```bash
ls -l file.txt
```
