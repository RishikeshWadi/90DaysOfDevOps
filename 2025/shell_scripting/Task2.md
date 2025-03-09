# Week 3 Challenge 2: Automated Backup & Recovery using Cron

---
This Bash script automates the backup process for a specified directory. It creates timestamped backup folders and implements a rotation mechanism to retain only the last 3 backups.

## Features
- Creates a timestamped backup folder inside the specified directory.
- Copies all files from the target directory into the backup folder.
- Retains only the last 3 backups by removing the oldest ones.

## Usage
```bash
./backup_with_rotation.sh <directory_path>
```
Example:
```bash
./backup_with_rotation.sh /home/user/documents
```

## Step-by-Step Explanation

### **Check if a Directory Path is Provided**
```bash
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <directory_path>"
    exit 1
fi
```
- The script requires a directory path as an argument.
- If no argument is provided, it prints a usage message and exits.

---

### **Initialize Variables**
```bash
DIR="$1"
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_DIR="$DIR/backup_$TIMESTAMP"
```
- `DIR="$1"` → Stores the directory path from the command-line argument.
- `TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")` → Generates a timestamp in `YYYY-MM-DD_HH-MM-SS` format.
- `BACKUP_DIR="$DIR/backup_$TIMESTAMP"` → Defines the backup folder’s name with a timestamp.

---

### **Create a Backup Directory**
```bash
mkdir -p "$BACKUP_DIR"
```
- Creates the backup folder if it doesn’t already exist.
- `-p` ensures no error occurs if the parent directory already exists.

---

### **Copy Files to the Backup Folder**
```bash
cp -r "$DIR"/* "$BACKUP_DIR" 2>/dev/null
```
- Copies all files from the target directory (`$DIR`) into the new backup folder (`$BACKUP_DIR`).
- `-r` ensures directories are copied recursively.
- `2>/dev/null` suppresses error messages (e.g., if there are no files to copy).

---

### **Check If Backup Was Successful**
```bash
if [ $? -eq 0 ]; then
    echo "Backup created: $BACKUP_DIR"
else
    echo "Error creating backup"
    exit 1
fi
```
- `$?` stores the exit status of the last command (`cp` in this case).
- If successful (`0`), it prints the backup location.
- Otherwise, it prints an error message and exits.

---

### **Implement Backup Rotation**
```bash
BACKUPS=($(ls -d $DIR/backup_* 2>/dev/null | sort -r))
```
- Lists all existing backup folders (`backup_*`) in the directory.
- `ls -d $DIR/backup_*` lists only directories (not files).
- `sort -r` sorts them in **reverse order** (newest first).

---

### **Remove Oldest Backups (Keep Only the Last 3)**
```bash
if [ ${#BACKUPS[@]} -gt 3 ]; then
    REMOVE_COUNT=$((${#BACKUPS[@]} - 3))
    for ((i=${#BACKUPS[@]}-1; i>=3; i--)); do
        rm -rf "${BACKUPS[i]}"
        echo "Removed old backup: ${BACKUPS[i]}"
    done
fi
```
- **Check if there are more than 3 backups**:
  - `if [ ${#BACKUPS[@]} -gt 3 ];` → If the number of backups is more than 3, proceed.
- **Remove the oldest backups**:
  - The script calculates how many extra backups exist.
  - It loops through the extra backups and deletes them using `rm -rf`.

## Summary
1. The script takes a directory path as input.
2. It creates a timestamped backup folder inside that directory.
3. It copies all files from the target directory to the backup folder.
4. It ensures that only the last 3 backups are retained by deleting the oldest ones.
