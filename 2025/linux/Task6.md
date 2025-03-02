# Week 2: Linux System Administration & Automation
## Task 6: Automate Backups with Shell Scripting
---

- Write a shell script to back up /devops_workspace as backup_$(date +%F).tar.gz.
- Save it in /backups and schedule it using cron.
- Make the script display a success message in green text using echo -e.

---

1. **Create the Script file and directory**

```bash
cd ~  #home directory
mkdir -p scripts
vim scripts/automate_backup_script.sh
```
- `i` to insert mode

## create the shell script based on the requirement and automate task
```bash

#!/bin/bash


















```

- paste with `Ctrl+v`
- then `Esc` (to escape from Insert mode)
- Save and quit with `:wq`

2. **Make the Script file executable**

```bash
chmod 700 automate_backup_script.sh
```

3. **Test the Script**

```bash
# Assuming you have a folder `devops_workspace` in your home directory
./automate_backup_script.sh /home/devops_user/devops_workspace /home/devops_user/backups
```

4. **Schedule with Cron**
- Open the cron job editor
```bash
crontab -e
```

- Add this line to run daily at midnight:

```bash
0 0 * * * /home/devops_user/scripts/automate_backup_script.sh /home/devops_user/devops_workspace /home/devops_user/backups
```

- Add this line to test for each minute:

```bash
* * * * * /home/devops_user/scripts/automate_backup_script.sh /home/devops_user/devops_workspace /home/devops_user/backups
```
