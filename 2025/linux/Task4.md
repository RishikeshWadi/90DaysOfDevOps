# Week 2: Linux System Administration & Automation
## Task 4: Volume Management & Disk Usage
---

### Step 1: Create a Directory
```bash
sudo mkdir -p /mnt/devops_data
```

### Step 2: Create a Loop Device (For Local Practice)
If an additional volume is not available, create a loop device using a file:
```bash
sudo dd if=/dev/zero of=/devops_volume.img bs=1M count=1000
sudo losetup /dev/loop0 /devops_volume.img
sudo mkfs.ext4 /dev/loop0
```
This creates a 1GB file and sets up a loop device.

### Step 3: Mount the Volume
```bash
sudo mount /dev/loop0 /mnt/devops_data
```

### Step 4: Verify the Mount
Run the following commands to confirm the mount:
```bash
df -h | grep devops_data
mount | grep devops_data
```

---

- If using an actual volume instead of a loop device, replace `/dev/loop0` with the appropriate device name (e.g., `/dev/xvdf`).
- To unmount and detach the loop device:
  ```bash
  sudo umount /mnt/devops_data
  sudo losetup -d /dev/loop0
  ```
