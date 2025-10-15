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

## 1. Essential Commands

### Getting Help
```bash
# View manual for any command
man command_name
# Example:
man ls

# Quick help for command
command_name --help
# Example:
ls --help

# What these commands teach you:
# - How to use commands properly
# - What options are available
# - Examples of command usage
```

### Checking Your Identity
```bash
# Show current user
whoami

# Expected Output:
ec2-user

# Show system name
hostname

# Expected Output:
ip-172-31-0-100.ec2.internal

# Why this matters:
# - Confirms your user permissions
# - Verifies which system you're on
# - Important for AWS EC2 management
```

### Viewing System Information
```bash
# Show operating system information
uname -a

# Expected Output:
Linux ip-172-31-0-100 4.14.133-113.105.amzn2.x86_64 #1 SMP x86_64 x86_64 x86_64 GNU/Linux

# Show system uptime
uptime

# Expected Output:
14:23:45 up 7 days, 2:34, 1 user, load average: 0.00, 0.01, 0.05
```

## 2. File System Navigation

### Understanding Your Location
```bash
# Print working directory
pwd

# Expected Output:
/home/ec2-user

# List files and directories
ls

# Common ls options:
ls -l    # Long format
ls -a    # Show hidden files
ls -h    # Human-readable sizes

# Expected Output:
total 32
drwxr-xr-x 2 ec2-user ec2-user 4096 Oct 15 14:23 Documents
-rw-r--r-- 1 ec2-user ec2-user  123 Oct 15 14:22 file.txt
```

### Moving Around
```bash
# Change directory
cd directory_name

# Common cd shortcuts:
cd ~         # Go to home directory
cd ..        # Go up one directory
cd -         # Go to previous directory

# Examples:
cd /var/log  # Go to logs directory
cd ~/projects # Go to projects in home directory
```

### Using Tree Command
```bash
# First, install tree if not present
sudo yum install -y tree   # Amazon Linux
sudo apt install -y tree   # Ubuntu

# View directory structure
tree

# Expected Output:
.
├── Documents
│   └── project.txt
├── Downloads
└── scripts
    └── backup.sh

# Limit directory depth
tree -L 2

# Show only directories
tree -d
```
[Continuing with the guide...]

## 3. File Operations

### Creating Files and Directories
```bash
# Create directory
mkdir my_project

# Create multiple directories
mkdir -p project/src/main

# The -p flag:
# - Creates parent directories if they don't exist
# - Prevents errors if directory exists
# - Useful for scripting

# Create empty file
touch file.txt

# Expected Output:
$ ls -l
total 4
drwxr-xr-x 3 ec2-user ec2-user 4096 Oct 15 14:23 my_project
-rw-r--r-- 1 ec2-user ec2-user    0 Oct 15 14:23 file.txt
```

### Copying Files
```bash
# Copy file
cp source.txt destination.txt

# Copy directory and its contents
cp -r source_dir destination_dir

# Common cp options:
# -r : Copy directories recursively
# -p : Preserve permissions
# -v : Verbose (show what's being copied)

# Examples:
cp -v config.json backup/config.json
cp -r ~/logs /var/tmp/logs_backup

# Expected Output:
'config.json' -> 'backup/config.json'
```

### Moving and Renaming
```bash
# Move file
mv source.txt destination/

# Rename file
mv oldname.txt newname.txt

# Move and rename
mv ~/temp/file.txt ~/documents/newfile.txt

# Tips:
# - mv can move and rename in one command
# - Use with caution to avoid overwriting files
# - Use -i flag for interactive mode (asks before overwrite)
```

### Removing Files and Directories
```bash
# Remove file
rm filename.txt

# Remove empty directory
rmdir empty_directory

# Remove directory and contents
rm -r directory_name

# Safety tips:
# -i : Interactive (asks before removal)
# -f : Force removal (be careful!)

# WARNING: Always double-check before using rm -rf
# There's no recovery from deletion!
```

## 4. Text Processing

### Viewing File Contents
```bash
# Display entire file
cat filename.txt

# View file page by page
less filename.txt
# less commands:
# Space : Next page
# b     : Previous page
# q     : Quit
# /word : Search for "word"

# Show first 10 lines
head filename.txt

# Show last 10 lines
tail filename.txt

# Monitor file in real-time (useful for logs)
tail -f /var/log/syslog
```

### Searching File Contents
```bash
# Search for pattern in file
grep "search_term" filename.txt

# Common grep options:
grep -i "search"  # Case-insensitive
grep -n "search"  # Show line numbers
grep -r "search"  # Search recursively

# Example: Find errors in log file
grep -i "error" /var/log/syslog

# Expected Output:
Oct 15 14:23:45 ip-172-31-0-100 ERROR: Connection failed
```

### Basic Text Editing
```bash
# Open nano editor (beginner-friendly)
nano filename.txt

# Nano commands (shown at bottom of screen):
# Ctrl + O : Save file
# Ctrl + X : Exit
# Ctrl + W : Search for text

# Open vim editor (more powerful but complex)
vim filename.txt

# Vim basic commands:
# i     : Enter insert mode
# Esc   : Exit insert mode
# :w    : Save file
# :q    : Quit
# :wq   : Save and quit
```

## 5. System Information

### System Resources
```bash
# Show memory usage
free -h

# Expected Output:
              total        used        free      shared  buff/cache   available
Mem:           15Gi       1.5Gi        10Gi       0.0Gi       3.5Gi        13Gi
Swap:           0B          0B          0B

# Show disk space
df -h

# Expected Output:
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1      30G   15G   15G  50% /
```

## 1. Understanding File Permissions

In Linux, every file and folder has permissions that control who can read, write, or execute them. This is crucial for security in cloud environments.

```bash
# View file permissions
ls -l myfile.txt

# Expected Output:
-rw-r--r-- 1 ec2-user ec2-user 123 Oct 15 14:23 myfile.txt
```

Breaking down the permissions:
```
-    rw-    r--    r--
↑     ↑      ↑      ↑
type  owner  group  others
```

* First character indicates:
  - `-` : Regular file
  - `d` : Directory
  - `l` : Symbolic link

* Permission groups:
  - Owner (your user)
  - Group (users in the same group)
  - Others (everyone else)

* Permission types:
  - `r` : Read
  - `w` : Write
  - `x` : Execute

## 2. Changing File Permissions

Use the `chmod` command to change permissions.

```bash
# Make a file readable and writable by owner, readable by others
chmod 644 myfile.txt

# Make a script executable
chmod 755 myscript.sh

# Common permission patterns:
# 644 (-rw-r--r--) : Regular files
# 755 (rwxr-xr-x)  : Scripts or directories
# 600 (-rw-------)  : Sensitive files
```

Understanding numeric permissions:
* 4 = Read
* 2 = Write
* 1 = Execute
* Add them together for each group (owner/group/others)

## 3. Users and Groups

Managing users and groups is essential for controlling access.

```bash
# Check your username
whoami

# Check your groups
groups

# Expected Output:
ec2-user wheel docker
```

View user information:
```bash
# Show current user and groups
id

# Expected Output:
uid=1000(ec2-user) gid=1000(ec2-user) groups=1000(ec2-user),10(wheel)
```

## 4. Password Security

Best practices for password management:

```bash
# Change your password
passwd

# View password status
passwd -S

# Lock an account
sudo passwd -l username

# Unlock an account
sudo passwd -u username
```

Password Safety Rules:
* Use strong passwords (mix of letters, numbers, symbols)
* Don't reuse passwords
* Change passwords regularly
* Never share passwords

## 5. SSH Security

Basic SSH security for AWS EC2:

```bash
# Set correct permissions for SSH key
chmod 400 mykey.pem

# Safe connection using SSH key
ssh -i mykey.pem ec2-user@your-instance-ip

# Common SSH errors and fixes:
# "Permissions too open" → chmod 400 mykey.pem
# "Connection timed out" → Check security group rules
```

SSH Key Protection:
* Keep private keys secure
* Never share private keys
* One key per person/purpose
* Regular key rotation

## 6. System Updates

Keeping your system updated is crucial for security:

```bash
# Check for updates
sudo yum check-update

# Install all updates
sudo yum update -y

# Show installed packages
yum list installed
```

Update Best Practices:
* Regular updates
* Schedule maintenance windows
* Test updates in non-production first
* Keep system logs for tracking

## 7. Service Management

Managing running services:

```bash
# List running services
sudo systemctl list-units --type=service --state=running

# Check specific service status
sudo systemctl status servicename

# Example: Check SSH service
sudo systemctl status sshd
```

Security Tips:
* Only run necessary services
* Regular service audits
* Monitor service logs
* Keep services updated

---

