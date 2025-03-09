# Week 3 Challenge 1: User Account Management
---
This Bash script provides user account management functionalities on a Linux system. It allows administrators to create, delete, reset passwords, and list users efficiently.

## Features
- **Create a User (-c | --create)**: Add a new user with a username and password.
- **Delete a User (-d | --delete)**: Remove an existing user account.
- **Reset Password (-r | --reset)**: Change the password for an existing user.
- **List Users (-l | --list)**: Display all system users along with their User IDs (UIDs).
- **Help Menu (-h | --help)**: Shows usage instructions.
- **Error Handling**: Ensures usernames are checked before performing actions and provides meaningful messages.

## Usage
Run the script with one of the following options:

### 1. Display Help Information
```bash
./user_management.sh -h
```
This command displays the available options and their usage.

---

### 2. Create a New User

```bash
create_user() {
    read -p "Enter new username: " username
    if id "$username" &>/dev/null; then
        echo "Error: Username '$username' already exists."
        exit 1
    fi
    read -s -p "Enter password: " password
    echo ""
    sudo useradd -m "$username"
    echo "$username:$password" | sudo chpasswd
    echo "User '$username' created successfully."
}
```
```bash
./user_management.sh -c
```

- Prompts for a username.
- Checks if the username already exists using id "$username" &>/dev/null.
- If the username exists, it exits with an error.
- If not, Prompts for a password (-s hides input for security).
- Uses sudo useradd -m "$username" to create the user with a home directory.
- Uses sudo chpasswd to set the password.
- Displays a success message.

---

### 3. Delete an Existing User
```bash
delete_user() {
    read -p "Enter username to delete: " username
    if ! id "$username" &>/dev/null; then
        echo "Error: Username '$username' does not exist."
        exit 1
    fi
    sudo userdel -r "$username"
    echo "User '$username' deleted successfully."
}

```
```bash
./user_management.sh -d
```

- Prompts for a username to delete.
- Checks if the username exists; if not, it exits with an error.
- If found, Uses sudo userdel -r "$username" to delete the user and their home directory.
- Displays a success message.

---

### 4. Reset Password for a User
```bash
reset_password() {
    read -p "Enter username: " username
    if ! id "$username" &>/dev/null; then
        echo "Error: Username '$username' does not exist."
        exit 1
    fi
    read -s -p "Enter new password: " password
    echo ""
    echo "$username:$password" | sudo chpasswd
    echo "Password for user '$username' has been reset successfully."
}

```
```bash
./user_management.sh -r
```

- Prompts for a username and checks if it exists.
- If the user exists, it asks for a new password (input hidden).
- Uses sudo chpasswd to reset the password.
- Displays a success message.

---

### 5. List All Users
```bash
list_users() {
    echo "User Accounts:"
    awk -F: '{print $1 " (UID: "$3")"}' /etc/passwd
}

```
```bash
./user_management.sh -l
```
- Displays all user accounts along with their **User IDs (UIDs)**.

---

## Script Breakdown

### **Shebang and Function Definitions**
The script begins with `#!/bin/bash`, specifying Bash as the interpreter.

### **Help Menu (`usage()`)**
- Displays available options and usage instructions.

### **User Creation (`create_user()`)**
- Prompts for a username and checks if it exists.
- If available, prompts for a password and creates the user using:
  ```bash
  sudo useradd -m "$username"
  echo "$username:$password" | sudo chpasswd
  ```

### **User Deletion (`delete_user()`)**
- Checks if the user exists.
- If found, deletes the user with:
  ```bash
  sudo userdel -r "$username"
  ```

### **Password Reset (`reset_password()`)**
- Checks if the user exists.
- If found, prompts for a new password and updates it using:
  ```bash
  echo "$username:$password" | sudo chpasswd
  ```

### **List Users (`list_users()`)**
- Extracts user details from `/etc/passwd` and displays usernames with UIDs:
  ```bash
  awk -F: '{print $1 " (UID: "$3")"}' /etc/passwd
  ```


## Example Output
![Verify ]()

