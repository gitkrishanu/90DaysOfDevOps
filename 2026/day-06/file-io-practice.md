# Day 06 – Linux Fundamentals: Read and Write Text Files

## Objective
Practice basic file creation, writing, appending, and reading using Linux commands.

---

## Commands Executed

### 1. Create an empty file
```bash
touch notes.txt
```
Creates an empty file named `notes.txt`.

### 2. Write the first line
```bash
echo "Learning Linux file operations" > notes.txt
```
Writes text to the file and overwrites existing content.

### 3. Append a second line
```bash
echo "Using redirection operators > and >>" >> notes.txt
```
Appends text to the existing file.

### 4. Append a third line using tee
```bash
echo "tee can write and display output simultaneously" | tee -a notes.txt
```
Displays the text and appends it to the file.

### 5. Add more lines
```bash
echo "cat displays complete file content" >> notes.txt
echo "head shows beginning of file" >> notes.txt
echo "tail shows end of file" >> notes.txt
echo "File handling is important for DevOps" >> notes.txt
echo "Practice improves command-line skills" >> notes.txt
```

### 6. Read the entire file
```bash
cat notes.txt
```

### Output
```text
Learning Linux file operations
Using redirection operators > and >>
tee can write and display output simultaneously
cat displays complete file content
head shows beginning of file
tail shows end of file
File handling is important for DevOps
Practice improves command-line skills
```

### 7. Read first two lines
```bash
head -n 2 notes.txt
```

### Output
```text
Learning Linux file operations
Using redirection operators > and >>
```

### 8. Read last two lines
```bash
tail -n 2 notes.txt
```

### Output
```text
File handling is important for DevOps
Practice improves command-line skills
```

---

## Key Learnings

- `touch` creates a file.
- `>` writes and overwrites file content.
- `>>` appends content to an existing file.
- `tee -a` writes and displays output simultaneously.
- `cat` displays the entire file.
- `head` and `tail` help read specific sections of a file.

---

## Conclusion

Today's practice helped me understand basic Linux file operations that are commonly used while managing logs, configuration files, and scripts in DevOps environments.
