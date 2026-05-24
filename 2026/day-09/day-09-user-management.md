# Day 09 Challenge – Linux User & Group Management

## Objective

Practice Linux user management, group administration, and shared directory permissions.

---

# Users & Groups Created

## Users

- tokyo
- berlin
- professor
- nairobi

## Groups

- developers
- admins
- project-team

---

# Task 1: Create Users

## Commands Used

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

## Verification

```bash
grep -E "tokyo|berlin|professor" /etc/passwd
```

Sample Output:

```text
tokyo:x:1001:1001::/home/tokyo:/bin/bash
berlin:x:1002:1002::/home/berlin:/bin/bash
professor:x:1003:1003::/home/professor:/bin/bash
```

Check home directories:

```bash
ls -l /home
```

---

# Task 2: Create Groups

## Commands Used

```bash
sudo groupadd developers
sudo groupadd admins
```

## Verification

```bash
grep -E "developers|admins" /etc/group
```

Sample Output:

```text
developers:x:1004:
admins:x:1005:
```

---

# Task 3: Assign Users to Groups

## Commands Used

### tokyo → developers

```bash
sudo usermod -aG developers tokyo
```

### berlin → developers + admins

```bash
sudo usermod -aG developers,admins berlin
```

### professor → admins

```bash
sudo usermod -aG admins professor
```

## Verification

```bash
groups tokyo
groups berlin
groups professor
```

Sample Output:

```text
tokyo : tokyo developers
berlin : berlin developers admins
professor : professor admins
```

---

# Task 4: Shared Directory

## Create Directory

```bash
sudo mkdir -p /opt/dev-project
```

## Set Group Owner

```bash
sudo chgrp developers /opt/dev-project
```

## Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

## Verification

```bash
ls -ld /opt/dev-project
```

Sample Output:

```text
drwxrwxr-x 2 root developers 4096 Jun 1 10:00 /opt/dev-project
```

## Test File Creation

Create file as tokyo:

```bash
sudo -u tokyo touch /opt/dev-project/tokyo-file.txt
```

Create file as berlin:

```bash
sudo -u berlin touch /opt/dev-project/berlin-file.txt
```

Verify:

```bash
ls -l /opt/dev-project
```

Sample Output:

```text
-rw-r--r-- 1 tokyo  tokyo  0 tokyo-file.txt
-rw-r--r-- 1 berlin berlin 0 berlin-file.txt
```

---

# Task 5: Team Workspace

## Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

## Create Group

```bash
sudo groupadd project-team
```

## Add Users

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

## Create Workspace

```bash
sudo mkdir -p /opt/team-workspace
```

## Set Group Ownership

```bash
sudo chgrp project-team /opt/team-workspace
```

## Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

## Verification

```bash
ls -ld /opt/team-workspace
```

Sample Output:

```text
drwxrwxr-x 2 root project-team 4096 Jun 1 10:15 /opt/team-workspace
```

## Test Access

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi-test.txt
```

Verify:

```bash
ls -l /opt/team-workspace
```

Sample Output:

```text
-rw-r--r-- 1 nairobi nairobi 0 nairobi-test.txt
```

---

# Group Assignments Summary

| User | Groups |
|--------|---------|
| tokyo | developers, project-team |
| berlin | developers, admins |
| professor | admins |
| nairobi | project-team |

---

# Commands Used

```bash
useradd -m
passwd
groupadd
usermod -aG
groups
mkdir
chgrp
chmod
ls -ld
touch
grep
```

---

# What I Learned

1. Users can belong to multiple groups using `usermod -aG`.
2. Group ownership and directory permissions control shared access.
3. `chmod 775` allows owner and group members full access while others get read and execute permissions.
4. `groups username` helps verify group membership quickly.
5. Shared directories are commonly used in DevOps teams for collaboration.

---

# Conclusion

Successfully created users, groups, assigned memberships, configured shared directories, and verified permissions. This exercise demonstrated how Linux access control works in real-world DevOps environments where multiple teams share resources securely.
