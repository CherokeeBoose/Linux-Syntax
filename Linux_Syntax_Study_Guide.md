# 🧭 Linux Syntax Study Guide

## 🪶 Overview

This document serves as a comprehensive guide to understanding **Linux command syntax**, **file and directory management**, and key text-display utilities. It combines conceptual overviews with hands-on examples for practical learning.

---

## ⚙️ Basic Command Syntax & Conventions

| Concept | Description | Example |
|----------|--------------|----------|
| **Case Sensitivity** | Linux is case-sensitive. Commands and file names must be typed exactly as they appear. | `cd Documents` ≠ `cd documents` |
| **Command Structure** | Most commands follow the structure:<br>`command [options] [arguments]` | `ls -l /home` |
| **Options (Flags)** | Modify the behavior of a command. Short options use a single `-`, long options use `--`. | `ls -a`, `ls --all` |
| **Arguments** | Specify the target file, directory, or value for the command. | `cat week1.txt` |
| **Chaining Commands** | Combine commands with logical operators. | `cd notes && ls` |
| **Pipes (`|`)** | Send output of one command as input to another. | `ls | grep week` |
| **Redirectors (`>`, `>>`, `<`)** | Direct input/output streams to files. | `echo "Hello" > greeting.txt` |
| **Wildcards** | `*` matches multiple characters, `?` matches a single character. | `cat week*.txt` |
| **Manual Pages** | Get help for commands. | `man ls` or `ls --help` |

---

## 🧮 Understanding Shell Environments

| Shell | Description | Common Use |
|--------|--------------|------------|
| **Bash** | Default Linux shell (Bourne Again SHell). Uses `~/.bashrc` for customization. | Most Linux systems. |
| **Zsh** | Advanced interactive shell with autosuggestions. | macOS, developers. |
| **Fish** | User-friendly shell with smart completion. | Interactive scripting. |
| **PowerShell** | Object-based shell for Windows, can run on Linux via `pwsh`. | Cross-platform automation. |

🔹 **Tip:** To check which shell you are using:
```bash
echo $SHELL
```

---

## 📦 Data Formats: JSON & YAML

### **JSON (JavaScript Object Notation)**
- Structured data in key–value pairs.  
- Commonly used for APIs and configuration files.

Example:
```json
{
  "name": "student",
  "week": 2,
  "topics": ["Linux", "CLI", "File Management"]
}
```

Validate JSON syntax using:
```bash
cat config.json | jq .
```
(Install `jq` using `sudo apt install jq` if not available.)

### **YAML (YAML Ain’t Markup Language)**
- More human-readable than JSON.
- Uses indentation instead of braces.

Example:
```yaml
name: student
week: 2
topics:
  - Linux
  - CLI
  - File Management
```

---

## 🌲 Installing and Using the `tree` Command

The `tree` command displays directory structures in a visual hierarchy.

### **Installation**

| OS | Command |
|----|----------|
| Ubuntu/Debian | `sudo apt install tree` |
| Fedora/RHEL | `sudo dnf install tree` |
| macOS (Homebrew) | `brew install tree` |
| Windows (via Git Bash) | Preinstalled or install manually from Git. |

### **Usage**
```bash
tree notes
```
Output:
```
notes/
├── week1.txt
├── week2.txt
└── week3.txt
```

**Common Options:**
| Option | Description |
|---------|--------------|
| `-L <n>` | Limit display to `<n>` directory levels. |
| `-a` | Show hidden files. |
| `-d` | Display directories only. |
| `-f` | Show full path for each file. |

Example:
```bash
tree -L 2 -a
```

---

## 🗂️ Directory & File Management

### **Creating Directories**
```bash
mkdir notes
cd notes
```
- `mkdir` creates a directory.
- `cd` navigates into it.

Create multiple folders:
```bash
mkdir finance hr management
```

### **Creating Files**
```bash
touch week1.txt week2.txt week3.txt
```
- `touch` creates empty files.  
- Confirm with `ls`.

### **Viewing Directory Structure**
```bash
ls -l
```
- `-l` shows detailed info (permissions, size, date).

---

## 📝 Adding and Editing Content

### **Add Text to Files**
```bash
echo "Week 1: Introduction to Linux" > week1.txt
echo "Week 2: Understanding File Systems" > week2.txt
```
- `>` overwrites file content.
- `>>` appends to a file.

### **Open with Nano Editor**
```bash
nano week1.txt
```
Inside Nano:
- Type text.
- `CTRL + O` → Save.
- `CTRL + X` → Exit.

---

## 🧭 Viewing File Contents

### **`cat` — Concatenate & Display**
```bash
cat week1.txt
```
Displays entire file at once. Great for short files.

### **`more` — View One Page at a Time**
```bash
more week1.txt
```
Press **Space** for next page, **q** to quit.

### **`less` — Scroll and Search**
```bash
less week2.txt
```
- Arrow keys to navigate.
- `/keyword` to search.
- `n` to jump to next match.

### **`head` — Show Beginning of File**
```bash
head -n 5 week3.txt
```
Shows first 5 lines (default = 10).

### **`tail` — Show End of File**
```bash
tail -n 5 week3.txt
```
Shows last 5 lines (default = 10).

---

## 🧪 Lab Exercise: Investigating Files

1. Create notes:
   ```bash
   mkdir notes
   cd notes
   touch week1.txt week2.txt week3.txt
   ```
2. Add text:
   ```bash
   echo "Week 1: Introduction to Linux" > week1.txt
   echo "Week 2: File System Basics" > week2.txt
   echo "Week 3: Text Utilities" > week3.txt
   ```
3. Duplicate:
   ```bash
   cp week2.txt week1_copy.txt
   ```
4. Inspect with `cat`, `more`, `less`, `head`, `tail`.

**Reflection:** When would you use each?

| Command | Purpose | Best Use |
|----------|----------|----------|
| `cat` | Display full file | Small files |
| `more` | Scroll forward | Medium files |
| `less` | Scroll + search | Large files |
| `head` | View start | Headers |
| `tail` | View end | Logs or summaries |

---

## 🧩 Departmental Example

### Creating a Company Structure
```bash
mkdir finance hr management
touch finance/budget.txt hr/employees.txt management/notes.txt
```
Add content:
```bash
echo "Budget Planning" > finance/budget.txt
echo "Employee Onboarding" > hr/employees.txt
echo "Meeting Notes" > management/notes.txt
```

Display hierarchy:
```bash
tree
```

---

## 🧩 Bonus Challenge

Combine the first lines of all notes:
```bash
head -n 1 week*.txt > summary.txt
cat summary.txt
```

---

## 🏁 Key Takeaways

- **Commands are case-sensitive.**
- **`mkdir` creates directories**, **`touch` creates files**.  
- **Use `cat`, `more`, `less`, `head`, `tail` to view text.**
- **`tree` provides visual structure.**
- **Always use `man <command>` for documentation.**

---

## 🔒 Security & Good Practices

- Avoid using `sudo` unless necessary.
- Use `chmod` carefully to set permissions.
- Use relative paths (`./file`) for local references.
- Keep backups using `cp` before overwriting files.

---

© 2025 AWS Cloud Learning — Linux Fundamentals Week 2 Study Notes
