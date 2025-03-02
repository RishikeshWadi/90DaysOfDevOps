# Week 2: Linux System Administration & Automation
## Task 5 : Process Management & Monitoring
---

## 1. Start a Background Process
Run the following command to start the `ping` process in the background and log its output:

```bash
ping google.com > ping_test.log &
```

- `&` sends the process to the background.
- The output is redirected to `ping_test.log`.

---

## 2. Monitor the Process

### Using `ps`
```bash
ps aux | grep ping
```
OR
```bash
ps -ef | grep ping
```
This will list all running processes and filter for `ping`.

### Using `top`
```bash
top
```
Press **Shift + F**, type **COMMAND**, then press **Enter**, and look for `ping`.

### Using `htop`
```bash
htop
```
-  Once inside `htop`, press **F3**, type `ping`, and press **Enter** to search

---

## 3. Kill the Process
Find the **PID (Process ID)** from the `ps` command and terminate it using:

```bash
kill <PID>
```

If the process doesn’t stop, force kill it:

```bash
kill -9 <PID>
```

---

## 4. Verify the Process is Terminated
Run:

```bash
ps aux | grep ping
```

If no output appears (except for the `grep` command itself), the process has been successfully terminated.