# Day 12 – Revision (Days 01–11)

## Objective

Today was a revision day focused on reinforcing Linux fundamentals learned during Days 01–11, including process management, services, file operations, permissions, ownership, and user/group administration.

---

# Mindset & Plan Review

## Original Goal

- Build strong Linux fundamentals for DevOps.
- Become comfortable with command-line operations.
- Learn troubleshooting techniques used in production environments.

## Progress Check

### Completed Topics

- Linux navigation and basic commands
- Users and groups
- File operations
- File permissions
- File ownership
- Process monitoring
- Service management
- Log analysis
- Basic troubleshooting

### Areas to Improve

- More practice with `journalctl`
- Better understanding of process signals and process management
- More real-world troubleshooting scenarios

---

# Processes & Services Review

## Command 1

```bash
ps aux | head
```

### Observation

Displayed currently running processes along with CPU and memory usage information.

### Learning

Useful for identifying resource-consuming processes and verifying application execution.

---

## Command 2

```bash
systemctl status ssh
```

### Observation

SSH service was active and running.

### Learning

Quick way to verify whether a service is healthy and operational.

---

## Command 3

```bash
journalctl -u ssh -n 10
```

### Observation

Recent SSH login and authentication events were displayed.

### Learning

Logs provide valuable information for troubleshooting service-related issues.

---

# File Skills Practice

## Append Text to File

```bash
echo "Revision Day Notes" >> notes.txt
```

### Result

Successfully added a new line to the file.

---

## Change Permissions

```bash
chmod 640 notes.txt
```

### Result

Owner has read/write permissions, group has read permission, others have no access.

---

## Check Permissions

```bash
ls -l notes.txt
```

### Result

Verified permission changes successfully.

---

## Create Directory

```bash
mkdir revision-test
```

### Result

Created a test directory for practice.

---

## Copy File

```bash
cp notes.txt revision-test/
```

### Result

Successfully copied file to another location.

---

# Cheat Sheet Refresh

## Five Commands I Would Use First During an Incident

### 1. ps aux

```bash
ps aux
```

Reason:
Check running processes and resource usage.

---

### 2. top

```bash
top
```

Reason:
Monitor CPU and memory usage in real time.

---

### 3. systemctl status

```bash
systemctl status nginx
```

Reason:
Check service health and status.

---

### 4. journalctl

```bash
journalctl -u nginx -n 50
```

Reason:
Review recent service logs.

---

### 5. ls -l

```bash
ls -l
```

Reason:
Verify file permissions and ownership quickly.

---

# User & Group Review

## Create User

```bash
sudo useradd -m revisionuser
```

## Verify User

```bash
id revisionuser
```

Output Example:

```text
uid=1002(revisionuser) gid=1002(revisionuser)
```

---

## Create Test File

```bash
touch revision.txt
```

## Change Ownership

```bash
sudo chown revisionuser revision.txt
```

## Verify Ownership

```bash
ls -l revision.txt
```

Output Example:

```text
-rw-r--r-- 1 revisionuser revisionuser 0 Jun 12 10:00 revision.txt
```

### Learning

Ownership determines who controls a file, while permissions determine what actions can be performed.

---

# Mini Self-Check

## 1. Which 3 commands save you the most time right now, and why?

### ps aux

Quickly shows running processes and resource usage.

### systemctl status

Immediately reveals whether a service is running or failed.

### ls -l

Displays file permissions and ownership for troubleshooting access issues.

---

## 2. How do you check if a service is healthy?

Commands:

```bash
systemctl status nginx

journalctl -u nginx -n 50

ss -tulpn
```

Purpose:

- Verify service state.
- Review recent logs.
- Confirm the service is listening on the expected port.

---

## 3. How do you safely change ownership and permissions?

Example:

```bash
sudo chown appuser:developers app.log
chmod 640 app.log
```

Explanation:

- Change ownership first.
- Apply only the minimum required permissions.
- Verify using `ls -l`.

---

## 4. What will you focus on improving in the next 3 days?

- Service troubleshooting using systemd tools.
- Log analysis using journalctl and log files.
- Linux networking basics and port verification.
- More hands-on practice with permissions and ownership.

---

# Key Takeaways

- Logs should be checked before restarting services.
- Understanding permissions prevents many access issues.
- Ownership and permissions work together for security.
- Process and service monitoring are essential troubleshooting skills.
- Small daily practice improves command-line confidence significantly.

---

# Conclusion

Day 12 was a valuable revision session that reinforced Linux fundamentals learned during Days 01–11. Repeating key commands and reviewing troubleshooting workflows helped strengthen retention and improve confidence in daily Linux administration tasks.
