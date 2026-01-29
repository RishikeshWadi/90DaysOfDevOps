# Day 06 – Linux Fundamentals: Read and Write Text Files

## Task
This is a **continuation of Day 05**, but much simpler.

Today’s goal is to **practice basic file read/write** using only fundamental commands.

You will create a small text file and practice:
- Creating a file
- Writing text to a file
- Appending new lines
- Reading the file back

---

# Linux File Read/Write Practice (Basics)

Practice creating, writing, appending, and reading files using fundamental Linux commands.

---

## 1️⃣ Create an empty file
```bash
touch notes.txt
```

**Explanation:  touch <filename>**
Creates an empty file named notes.txt if it does not already exist.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/touch_cmd.jpg)

---

## 2️⃣ Write the first line (overwrite mode)
```bash
echo "Learning Linux file operations" > notes.txt
```

**Explanation: echo "text" > filename**
Writes text to the file using > redirection.
This will overwrite existing content.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/echo_cmd_Line1.jpg)

---

## 3️⃣ Append a second line
```bash
echo "Using redirection and basic commands" >> notes.txt
```

**Explanation: echo "text" >> filename**
Appends text to the file without deleting existing content.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/echo_cmd_Line2.jpg)

---

## 4️⃣ Append and display using tee
```bash
echo "tee helps write and display output" | tee -a notes.txt
```

**Explanation: command | tee -a filename**
tee displays output on the terminal and appends it to the file using -a.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/echo_cmd_Line3.jpg)

---

## 5️⃣ Read the full file
```bash
cat notes.txt
```

**Explanation: cat filename**
Displays the entire content of the file.

---

## 6️⃣ Read the first 2 lines
```bash
head -n 2 notes.txt
```

**Explanation: head -n <number> filename**
Displays the first two lines of the file.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/head_tail_cmd.jpg)

---

## 7️⃣ Read the last 2 lines
```bash 
tail -n 2 notes.txt
```

**Explanation: tail -n <number> filename**
Displays the last two lines of the file.

![Verify ](https://github.com/RishikeshWadi/90DaysOfDevOps/blob/Day-06/2026/day-06/day06snaps/head_tail_cmd.jpg)

---

## Resources
Use these docs to understand the commands:

- `touch` (create an empty file) 
- `cat` (read full file) 
- `head` and `tail` (read parts of a file) 
- `tee` (write and display at the same time)

---

## Why This Matters for DevOps
Reading and writing files is a daily task in DevOps.

Logs, configs, and scripts are all text files.  
If you can handle files quickly, you can debug and automate faster.

---

## ✅ Summary

Practiced basic file creation and editing.
Used >, >>, tee, cat, head, and tail
Strengthened understanding of Linux file read/write fundamentals.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham

Happy Learning  