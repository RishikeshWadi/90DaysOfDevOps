# Day 10 – File Permissions & File Operations Challenge

## Task
Master file permissions and basic file operations in Linux.

- Create and read files using `touch`, `cat`, `vim`
- Understand and modify permissions using `chmod`

---

## ✅ Task 1: Create Files

### 1️⃣ Create empty file `devops.txt`
```bash
touch devops.txt
```
**Explanation:**  
`touch` creates an empty file if it doesn’t exist.

---

### 2️⃣ Create `notes.txt` with content
```bash
echo "This is my DevOps notes file" > notes.txt
```
**Explanation:**  
- `echo` prints text  
- `>` writes output into the file (overwrites if file exists)

---

### 3️⃣ Create `script.sh` using vim
```bash
vim script.sh
```
Inside vim, type:
```bash
echo "Hello DevOps"
```
Save and exit:
```
ESC → :wq → Enter
```

---

### 4️⃣ Verify files & permissions
```bash
ls -l
```

**Sample Output:**
```text
-rw-r--r-- devops.txt
-rw-r--r-- notes.txt
-rw-r--r-- script.sh
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-10/2026/day-10/day10Snaps/task1.jpg)

---

## ✅ Task 2: Read Files

### 1️⃣ Read `notes.txt`
```bash
cat notes.txt
```
**Explanation:**  
`cat` displays file content.

---

### 2️⃣ View `script.sh` in read-only mode
```bash
vim -R script.sh
```
**Explanation:**  
`-R` opens file in read-only mode.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-10/2026/day-10/day10Snaps/vim-content.jpg)

---

### 3️⃣ Display first 5 lines of `/etc/passwd`
```bash
head -n 5 /etc/passwd
```

---

### 4️⃣ Display last 5 lines of `/etc/passwd`
```bash
tail -n 5 /etc/passwd
```

---

## ✅ Task 3: Understand Permissions
### Check current permissions
```bash
ls -l devops.txt notes.txt script.sh
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-10/2026/day-10/day10Snaps/task3.jpg)

---

## ✅ Task 4: Modify Permissions (20 minutes)

### 1️⃣ Make `script.sh` executable
```bash
chmod +x script.sh
./script.sh
```

---

### 2️⃣ Set `devops.txt` to read-only
```bash
chmod a-w devops.txt
```

---

### 3️⃣ Set `notes.txt` to `640`
```bash
chmod 640 notes.txt
```

---

### 4️⃣ Create directory `project/` with `755`
```bash
mkdir project
chmod 755 project
```

---

### 5️⃣ Verify permissions
```bash
ls -l
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-10/2026/day-10/day10Snaps/task4.jpg)

---

## ✅ Task 5: Test Permissions
### 1️⃣ Try writing to read-only file
```bash
echo "test" >> devops.txt
```
**Error:**
```text
Permission denied
```

---

### 2️⃣ Try executing without execute permission
```bash
chmod -x script.sh
./script.sh
```
**Error:**
```text
Permission denied
```

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-10/2026/day-10/day10Snaps/task5.jpg)

---

```
#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
```

Happy Learning