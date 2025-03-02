# Week 2: Linux System Administration & Automation
## Task 3: Log File Analysis with AWK, Grep & Sed
---
Logs are crucial for monitoring and troubleshooting.

## 📌 Steps to Perform Log File Analysis

### Download the Log File

If the log file is hosted on a repository, download it using `wget` or `curl`:

```bash
wget https://<repository_url>/Linux_2k.log
```

### Find All Occurrences of "error" using `grep`

```bash
grep -i "error" Linux_2k.log
```

- `-i`: Makes the search case-insensitive.
- this command will list all log lines containing "error".

### Extract Timestamps and Log Levels using `awk`
```bash
awk '{print $1, $2, $3}' Linux_2k.log
```

Explanation:

- `$1` = First column (Timestamp)
- `$2` = Second column (Time)
- `$3` = Log Level (ERROR, INFO, WARN)


### Replace IP Addresses with `[REDACTED]` using `sed`

```bash
sed -E 's/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/[REDACTED]/g' Linux_2k.log
```

This will:

- Replace all IP addresses with `[REDACTED]`.

### Find the Most Frequent Log Entries using `awk` or `sort`

```bash
awk '{print $0}' Linux_2k.log | sort | uniq -c | sort -nr | head -10
```

Explanation:

- `sort`: Sorts the log entries.
- `uniq -c`: Counts unique log entries.
- `sort -nr`: Sorts them in descending order by frequency.
- `head -10`: Displays the top 10 frequent logs.


