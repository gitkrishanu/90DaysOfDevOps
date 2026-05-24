# Day 10 Challenge – File Permissions & File Operations

## Objective

Practice creating files, reading file contents, understanding Linux permissions, modifying permissions, and testing access control.

---

# Task 1: Create Files

## Create Empty File

```bash
touch devops.txt
```

## Create notes.txt with Content

```bash
echo "Linux file permissions are important." > notes.txt
echo "DevOps engineers work with files daily." >> notes.txt
```

## Create script.sh

```bash
vim script.sh
```

Contents:

```bash
echo "Hello DevOps"
```

## Verify Files

```bash
ls -l
```

Sample Output:

```text
-rw-rw-r-- 1 user user 0 devops.txt
-rw-rw-r-- 1 user user 67 notes.txt
-rw-rw-r-- 1 user user 19 script.sh
```

---

# Task 2: Read Files

## Read notes.txt

```bash
cat notes.txt
```

Output:

```text
Linux file permissions are important.
DevOps engineers work with files daily.
```

---

## Open script.sh in Read-Only Mode

```bash
vim -R script.sh
```

Observation:

File opens in read-only mode and cannot be modified accidentally.

---

## Display First 5 Lines of /etc/passwd

```bash
head -n 5 /etc/passwd
```

Sample Output:

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

---

## Display Last 5 Lines of /etc/passwd

```bash
tail -n 5 /etc/passwd
```

Sample Output:

```text
mysql:x:110:115::/nonexistent:/bin/false
sshd:x:111:65534::/run/sshd:/usr/sbin/nologin
user:x:1000:1000::/home/user:/bin/bash
```

---

# Task 3: Understand Permissions

## Check Permissions

```bash
ls -l devops.txt notes.txt script.sh
```

Sample Output:

```text
-rw-rw-r-- devops.txt
-rw-rw-r-- notes.txt
-rw-rw-r-- script.sh
```

### Permission Breakdown

| Permission | Meaning |
|------------|---------|
| rw- | Owner can read and write |
| rw- | Group can read and write |
| r-- | Others can only read |

### Who Can Access?

#### devops.txt

Owner:
- Read ✅
- Write ✅
- Execute ❌

Group:
- Read ✅
- Write ✅
- Execute ❌

Others:
- Read ✅
- Write ❌
- Execute ❌

Same permissions apply to notes.txt and script.sh before modification.

---

# Task 4: Modify Permissions

## Make script.sh Executable

```bash
chmod +x script.sh
```

Verify:

```bash
ls -l script.sh
```

Output:

```text
-rwxrwxr-x script.sh
```

Run Script:

```bash
./script.sh
```

Output:

```text
Hello DevOps
```

---

## Make devops.txt Read-Only

```bash
chmod a-w devops.txt
```

Verify:

```bash
ls -l devops.txt
```

Output:

```text
-r--r--r-- devops.txt
```

---

## Set notes.txt to 640

```bash
chmod 640 notes.txt
```

Verify:

```bash
ls -l notes.txt
```

Output:

```text
-rw-r----- notes.txt
```

Meaning:

Owner:
- Read ✅
- Write ✅

Group:
- Read ✅

Others:
- No access ❌

---

## Create Directory project

```bash
mkdir project
```

Set Permissions:

```bash
chmod 755 project
```

Verify:

```bash
ls -ld project
```

Output:

```text
drwxr-xr-x project
```

Meaning:

Owner:
- Read, Write, Execute

Group:
- Read, Execute

Others:
- Read, Execute

---

# Task 5: Test Permissions

## Attempt to Write to Read-Only File

```bash
echo "test" >> devops.txt
```

Output:

```text
Permission denied
```

Observation:

Write access removed successfully.

---

## Attempt to Execute Non-Executable File

```bash
chmod -x script.sh
./script.sh
```

Output:

```text
Permission denied
```

Observation:

Linux requires execute permission to run a script.

Restore:

```bash
chmod +x script.sh
```

---

# Permission Changes Summary

| File | Before | After |
|--------|---------|---------|
| script.sh | rw-rw-r-- | rwxrwxr-x |
| devops.txt | rw-rw-r-- | r--r--r-- |
| notes.txt | rw-rw-r-- | rw-r----- |
| project/ | default | rwxr-xr-x |

---

# Commands Used

```bash
touch
echo
cat
vim
vim -R
head
tail
ls -l
ls -ld
chmod +x
chmod -x
chmod a-w
chmod 640
chmod 755
mkdir
```

---

# What I Learned

1. Linux permissions are controlled using read (r), write (w), and execute (x) bits.
2. chmod can modify permissions using symbolic and numeric methods.
3. Scripts require execute permission before they can run.
4. Read-only files prevent accidental modification.
5. Directories require execute permission for users to access their contents.

---

# Conclusion

Successfully created files, viewed file contents, modified permissions, executed scripts, and tested Linux access controls. Understanding permissions is critical for securing systems and managing access in DevOps environments.
