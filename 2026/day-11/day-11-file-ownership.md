# Day 11 Challenge – File Ownership (chown & chgrp)

## Objective

Learn how Linux file ownership works by changing file owners and groups using `chown` and `chgrp`, including recursive ownership changes.

---

# Task 1: Understanding Ownership

## Check File Ownership

```bash
ls -l
```

Sample Output:

```text
-rw-r--r-- 1 bimal bimal  120 Jun 11 10:00 notes.txt
-rwxr-xr-x 1 bimal bimal   25 Jun 11 10:05 script.sh
```

### Ownership Format

```text
-rw-r--r-- 1 owner group size date filename
```

Example:

```text
-rw-r--r-- 1 bimal developers 120 Jun 11 notes.txt
```

- **Owner:** User who owns the file.
- **Group:** Group associated with the file.

### Difference Between Owner and Group

- Owner has primary control over the file.
- Group permissions allow multiple users in the same group to access the file according to assigned permissions.

---

# Task 2: Basic chown Operations

## Create File

```bash
touch devops-file.txt
```

## Check Current Ownership

```bash
ls -l devops-file.txt
```

Output:

```text
-rw-r--r-- 1 bimal bimal 0 Jun 11 10:10 devops-file.txt
```

## Create Users (if not already present)

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
```

## Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

Verify:

```bash
ls -l devops-file.txt
```

Output:

```text
-rw-r--r-- 1 tokyo bimal 0 Jun 11 10:10 devops-file.txt
```

## Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

Verify:

```bash
ls -l devops-file.txt
```

Output:

```text
-rw-r--r-- 1 berlin bimal 0 Jun 11 10:10 devops-file.txt
```

---

# Task 3: Basic chgrp Operations

## Create File

```bash
touch team-notes.txt
```

## Create Group

```bash
sudo groupadd heist-team
```

## Check Current Group

```bash
ls -l team-notes.txt
```

Output:

```text
-rw-r--r-- 1 bimal bimal 0 Jun 11 10:15 team-notes.txt
```

## Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

Verify:

```bash
ls -l team-notes.txt
```

Output:

```text
-rw-r--r-- 1 bimal heist-team 0 Jun 11 10:15 team-notes.txt
```

---

# Task 4: Combined Owner & Group Change

## Create File

```bash
touch project-config.yaml
```

## Create User professor

```bash
sudo useradd -m professor
```

## Change Owner and Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

Verify:

```bash
ls -l project-config.yaml
```

Output:

```text
-rw-r--r-- 1 professor heist-team 0 Jun 11 10:20 project-config.yaml
```

---

## Create Directory

```bash
mkdir app-logs
```

## Change Directory Ownership

```bash
sudo chown berlin:heist-team app-logs
```

Verify:

```bash
ls -ld app-logs
```

Output:

```text
drwxr-xr-x 2 berlin heist-team 4096 Jun 11 10:21 app-logs
```

---

# Task 5: Recursive Ownership

## Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

## Create Group

```bash
sudo groupadd planners
```

## Recursive Ownership Change

```bash
sudo chown -R professor:planners heist-project
```

## Verify

```bash
ls -lR heist-project
```

Sample Output:

```text
heist-project:
drwxr-xr-x professor planners plans
drwxr-xr-x professor planners vault

heist-project/plans:
-rw-r--r-- professor planners strategy.conf

heist-project/vault:
-rw-r--r-- professor planners gold.txt
```

Observation:

All files and subdirectories inherited the new ownership recursively.

---

# Task 6: Practice Challenge

## Create Users

```bash
sudo useradd -m nairobi
```

## Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

## Create Directory

```bash
mkdir bank-heist
```

## Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

## Set Ownership

### access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

### blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

### escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

## Verify

```bash
ls -l bank-heist
```

Sample Output:

```text
-rw-r--r-- 1 tokyo   vault-team access-codes.txt
-rw-r--r-- 1 berlin  tech-team  blueprints.pdf
-rw-r--r-- 1 nairobi vault-team escape-plan.txt
```

---

# Files & Directories Created

### Files

- devops-file.txt
- team-notes.txt
- project-config.yaml
- gold.txt
- strategy.conf
- access-codes.txt
- blueprints.pdf
- escape-plan.txt

### Directories

- app-logs
- heist-project
- heist-project/vault
- heist-project/plans
- bank-heist

---

# Ownership Changes Summary

| File/Directory | Before | After |
|---------------|---------|---------|
| devops-file.txt | bimal:bimal | berlin:bimal |
| team-notes.txt | bimal:bimal | bimal:heist-team |
| project-config.yaml | bimal:bimal | professor:heist-team |
| app-logs | bimal:bimal | berlin:heist-team |
| heist-project/* | bimal:bimal | professor:planners |
| access-codes.txt | bimal:bimal | tokyo:vault-team |
| blueprints.pdf | bimal:bimal | berlin:tech-team |
| escape-plan.txt | bimal:bimal | nairobi:vault-team |

---

# Commands Used

```bash
ls -l
ls -ld
ls -lR

touch
mkdir
mkdir -p

useradd -m
groupadd

chown
chown -R
chgrp
```

---

# What I Learned

1. Every Linux file has an owner and a group associated with it.
2. `chown` can change both owner and group simultaneously using `owner:group`.
3. `chgrp` changes only the group ownership.
4. Recursive ownership changes (`chown -R`) are useful for application directories and deployments.
5. Proper ownership management is critical for security, application access, and DevOps automation.

---

# Conclusion

Successfully practiced Linux ownership management by creating users, groups, files, and directories, then modifying ownership using `chown` and `chgrp`. Learned how recursive ownership works and why proper ownership is important for real-world DevOps operations.
