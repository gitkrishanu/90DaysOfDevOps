# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

# Part 1: Linux File System Hierarchy

## 1. / (Root Directory)

**Purpose:**
The root directory is the top-level directory in Linux. Every file and directory starts from here.

**Command:**
```bash
ls -l /
```

**Sample Observation:**
```text
bin
boot
dev
etc
home
opt
tmp
usr
var
```

**I would use this when:**
I need to navigate the Linux filesystem or locate major system directories.

---

## 2. /home

**Purpose:**
Contains personal directories for normal users.

**Command:**
```bash
ls -l /home
```

**Sample Observation:**
```text
bimal
ubuntu
developer
```

**I would use this when:**
Managing user files, SSH keys, scripts, and personal configurations.

---

## 3. /root

**Purpose:**
Home directory of the root (administrator) user.

**Command:**
```bash
sudo ls -la /root
```

**Sample Observation:**
```text
.bashrc
.ssh
```

**I would use this when:**
Performing administrative tasks as root.

---

## 4. /etc

**Purpose:**
Stores system-wide configuration files.

**Command:**
```bash
ls -l /etc | head
```

**Sample Observation:**
```text
hostname
hosts
passwd
group
ssh
```

**I would use this when:**
Troubleshooting services, networking, authentication, and application configurations.

---

## 5. /var/log

**Purpose:**
Stores system and application log files.

**Command:**
```bash
ls -l /var/log | head
```

**Sample Observation:**
```text
syslog
messages
auth.log
journal
```

**I would use this when:**
Investigating application failures, login issues, and server incidents.

---

## 6. /tmp

**Purpose:**
Temporary files used by applications and users.

**Command:**
```bash
ls -la /tmp | head
```

**Sample Observation:**
```text
systemd-private
tmpfile.txt
```

**I would use this when:**
Testing scripts and storing temporary files.

---

## 7. /bin

**Purpose:**
Contains essential Linux commands required for booting and recovery.

**Command:**
```bash
ls -l /bin | head
```

**Sample Observation:**
```text
bash
cat
cp
ls
mv
```

**I would use this when:**
Running core Linux commands.

---

## 8. /usr/bin

**Purpose:**
Contains user-level executable programs.

**Command:**
```bash
ls -l /usr/bin | head
```

**Sample Observation:**
```text
python3
git
curl
vim
```

**I would use this when:**
Locating installed software binaries.

---

## 9. /opt

**Purpose:**
Used for optional and third-party applications.

**Command:**
```bash
ls -l /opt
```

**Sample Observation:**
```text
google
custom-app
```

**I would use this when:**
Managing manually installed software packages.

---

# Hands-on Practice

## Find Largest Log Files

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

**Observation:**
Journal and application logs consume the most disk space.

---

## View Hostname Configuration

```bash
cat /etc/hostname
```

**Observation:**
Displays the configured hostname of the system.

---

## Check Home Directory Contents

```bash
ls -la ~
```

**Observation:**
Contains user configuration files such as `.bashrc`, `.profile`, and `.ssh`.

---

# Part 2: Scenario-Based Practice

## Scenario 1: Service Not Starting

### Step 1
```bash
systemctl status myapp
```

**Why:**
Check whether the service is running, failed, or inactive.

### Step 2
```bash
journalctl -u myapp -n 50
```

**Why:**
Review recent logs to identify startup errors.

### Step 3
```bash
systemctl is-enabled myapp
```

**Why:**
Verify whether the service starts automatically after reboot.

### Step 4
```bash
journalctl -xe
```

**Why:**
Inspect detailed system-wide errors related to service startup.

### What I Learned
Always check service status first, then investigate logs before attempting a restart.

---

## Scenario 2: High CPU Usage

### Step 1
```bash
top
```

**Why:**
Monitor CPU and memory usage in real time.

### Step 2
```bash
ps aux --sort=-%cpu | head -10
```

**Why:**
Identify the top CPU-consuming processes.

### Step 3
```bash
ps -fp <PID>
```

**Why:**
View detailed information about the problematic process.

### Step 4
```bash
vmstat 1 5
```

**Why:**
Check CPU wait time and overall system performance.

### What I Learned
Use `top` for quick visibility and `ps` for detailed process investigation.

---

## Scenario 3: Finding Service Logs

### Step 1
```bash
systemctl status docker
```

**Why:**
Confirm service status and identify basic issues.

### Step 2
```bash
journalctl -u docker -n 50
```

**Why:**
View recent Docker logs.

### Step 3
```bash
journalctl -u docker -f
```

**Why:**
Follow logs in real time while reproducing the issue.

### Step 4
```bash
journalctl --since "1 hour ago" -u docker
```

**Why:**
Investigate recent events within a specific timeframe.

### What I Learned
Systemd services store logs in journald, accessible using `journalctl`.

---

## Scenario 4: File Permissions Issue

### Step 1
```bash
ls -l /home/user/backup.sh
```

**Why:**
Check current file permissions.

### Step 2
```bash
chmod +x /home/user/backup.sh
```

**Why:**
Grant execute permission.

### Step 3
```bash
ls -l /home/user/backup.sh
```

**Why:**
Verify execute permission has been applied.

### Step 4
```bash
./backup.sh
```

**Why:**
Run the script and verify successful execution.

### What I Learned
Scripts require execute permission (`x`) before they can be run.

---

# Key Takeaways

- `/etc` stores configuration files.
- `/var/log` is the primary location for troubleshooting logs.
- `systemctl` and `journalctl` are essential for service management.
- `top` and `ps` help diagnose performance issues.
- File permissions directly affect script execution.
- A structured troubleshooting process prevents guesswork during incidents.

# Conclusion

Today I learned the Linux file system hierarchy and practiced real-world troubleshooting scenarios involving services, CPU usage, logs, and file permissions. These skills are essential for DevOps engineers handling production systems.
