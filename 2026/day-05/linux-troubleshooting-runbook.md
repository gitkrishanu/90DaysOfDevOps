# Linux Troubleshooting Runbook

## Target Service / Process

**Service:** sshd (OpenSSH Server)

**Objective:** Verify system health, network connectivity, and service logs to ensure SSH access is functioning normally.

---

# Environment Basics

## 1. System Information

### Command
```bash
uname -a
```

### Sample Output
```text
Linux ubuntu 6.8.0-60-generic x86_64 GNU/Linux
```

### Observation
Kernel and architecture identified successfully. System is running a modern Linux kernel.

---

## 2. OS Information

### Command
```bash
cat /etc/os-release
```

### Sample Output
```text
NAME="Ubuntu"
VERSION="24.04 LTS"
```

### Observation
Confirmed operating system version and distribution.

---

# Filesystem Sanity Checks

## 3. Create Test Directory

### Command
```bash
mkdir -p /tmp/runbook-demo
```

### Observation
Temporary directory created successfully.

---

## 4. Copy and Verify File

### Command
```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

### Sample Output
```text
-rw-r--r-- 1 user user 245 hosts-copy
```

### Observation
Filesystem write operations working correctly.

---

# Snapshot: CPU & Memory

## 5. Memory Usage

### Command
```bash
free -h
```

### Sample Output
```text
Mem: 7.6Gi total, 3.2Gi used, 3.8Gi free
```

### Observation
Memory utilization is healthy with sufficient free memory available.

---

## 6. SSH Process Resource Usage

### Command
```bash
ps -C sshd -o pid,pcpu,pmem,comm
```

### Sample Output
```text
PID %CPU %MEM COMMAND
834 0.0 0.1 sshd
```

### Observation
SSH service consuming minimal CPU and memory resources.

---

# Snapshot: Disk & IO

## 7. Disk Space Usage

### Command
```bash
df -h
```

### Sample Output
```text
Filesystem Size Used Avail Use%
/dev/sda1 50G 18G 30G 38%
```

### Observation
Root filesystem has adequate free space.

---

## 8. Log Directory Size

### Command
```bash
du -sh /var/log
```

### Sample Output
```text
180M /var/log
```

### Observation
Log directory size is reasonable and not consuming excessive disk space.

---

# Snapshot: Network

## 9. Listening Ports

### Command
```bash
ss -tulpn | grep sshd
```

### Sample Output
```text
LISTEN 0 128 *:22 *:* users:(("sshd",pid=834))
```

### Observation
SSH daemon is listening on TCP port 22.

---

## 10. Service Connectivity Test

### Command
```bash
curl -I http://localhost
```

### Sample Output
```text
HTTP/1.1 200 OK
```

### Observation
Local web service responds successfully. Network stack functioning normally.

---

# Logs Reviewed

## 11. Recent SSH Logs

### Command
```bash
sudo journalctl -u ssh -n 50
```

### Sample Output
```text
Accepted publickey for user from 192.168.1.10
```

### Observation
Recent successful SSH logins observed. No authentication failures detected.

---

## 12. System Log Review

### Command
```bash
sudo tail -n 50 /var/log/syslog
```

### Observation
No critical errors or repeated warnings found in recent log entries.

---

# Quick Findings

- System resources are healthy.
- No CPU or memory pressure detected.
- Disk utilization within acceptable limits.
- SSH daemon is active and listening on port 22.
- Recent logs show successful connections.
- No critical errors identified during investigation.

---

# If This Worsens (Next Steps)

1. Collect extended diagnostics:
   ```bash
   top
   vmstat 1 10
   iostat -xz 1 10
   ```

2. Increase logging and trace service behavior:
   ```bash
   sudo journalctl -fu ssh
   sudo strace -p <sshd-pid>
   ```

3. Validate connectivity and restart service if required:
   ```bash
   ssh localhost
   sudo systemctl restart ssh
   sudo systemctl status ssh
   ```

---

# Conclusion

The SSH service is operating normally. System resources, network connectivity, and logs show no immediate signs of instability. Continue routine monitoring and escalate only if error frequency or resource utilization increases.
