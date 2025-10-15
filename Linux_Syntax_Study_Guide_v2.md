# Linux Syntax

> **Purpose:** A comprehensive, copy‑pasteable study guide + lab that **keeps everything you already had** (notes/week1–week11 scenario; `cat`, `more`, `less`, `head`, `tail`; `mkdir` vs `touch`; departmental example; editing with `nano`/`echo`; JSON/YAML basics) and **enhances** it with deeper context, a detailed **permissions** section, and an install + usage guide for the **`tree`** command.  
> **Scope:** Bash-focused. No PowerShell comparisons (kept separate per your preference).

---

## Table of Contents
1. [CLI Conventions & Syntax Basics](#cli-conventions--syntax-basics)  
2. [Shells at a Glance (Bash-first)](#shells-at-a-glance-bash-first)  
3. [Paths, Globbing, Quoting & Redirection](#paths-globbing-quoting--redirection)  
4. [Core Scenario: 11-Week `notes` Directory](#core-scenario-11-week-notes-directory)  
5. [Viewing Text: `cat`, `more`, `less`, `head`, `tail`](#viewing-text-cat-more-less-head-tail)  
6. [Create/Organize: `mkdir`, `touch`, `cp`, `mv`, `rm` (safe use)](#createorganize-mkdir-touch-cp-mv-rm-safe-use)  
7. [Editing: `nano` plus quick adds with `echo`/redirection](#editing-nano-plus-quick-adds-with-echoredirection)  
8. [`tree`: install, verify, and use](#tree-install-verify-and-use)  
9. [JSON & YAML quick basics](#json--yaml-quick-basics)  
10. [Permissions (Deep Dive): `ls -l`, `chmod`, `chown`, `umask`, setuid/setgid/sticky](#permissions-deep-dive-ls--l-chmod-chown-umask-setuidsetgidsticky)  
11. [Hands‑On Labs](#hands-on-labs)  
12. [Key Takeaways](#key-takeaways)

---

## CLI Conventions & Syntax Basics

| Concept | What it means | Micro‑example |
|---|---|---|
| **Case sensitivity** | Linux treats file/dir names and commands as case‑sensitive. | `notes` ≠ `Notes`; `ls` works, `LS` doesn’t. |
| **Command form** | `command [options] [arguments]` | `ls -l /var/log` |
| **Short vs long options** | Short: `-l` (single hyphen). Long: `--all` (double). May combine short flags: `-lah`. | `ls -la` = show hidden + long format |
| **Arguments** | Targets the command acts on (files, dirs, patterns). | `cat week1.txt` |
| **Exit status** | `0` = success; non‑zero = error. | Immediately check: `echo $?` |
| **Pipes** | Send output of one command to another. | `ls | grep week` |
| **Redirection** | `>` overwrite; `>>` append; `<` stdin from file. | `echo "hi" > a.txt` |
| **Wildcards (globbing)** | `*` = many chars, `?` = single char, `[]` class. | `cat week?.txt` |
| **Help** | Built‑in help or manpages. | `ls --help`, `man ls` |
| **Tab completion** | Press **Tab** to auto-complete names. | `cd no<Tab>` → `cd notes/` |

> **Tip:** Commands run in the current working directory. Show it with `pwd` and change it with `cd`.

---

## Shells at a Glance (Bash-first)

- **Bash** (Bourne Again SHell) — default on many distros. Config in `~/.bashrc` (interactive) and `~/.bash_profile` (login).  
- **Zsh** — friendly completion and prompts; popular on macOS.  
- **Fish** — out-of-the-box suggestions, not POSIX‑sh compatible.  
- **Check your shell:**  
  ```bash
  echo $SHELL
  ```

---

## Paths, Globbing, Quoting & Redirection

**Paths**
- **Absolute:** start with `/` (e.g., `/home/user/notes`).  
- **Relative:** from current directory (e.g., `notes/week1.txt`).  
- `~` = home; `.` = current; `..` = parent.

**Globbing**
- `week*.txt` → week files (any suffix).  
- `week?.txt` → `week1.txt` … `week9.txt` (single char).

**Quoting**
- `"double quotes"`: expands variables & globs (unless escaped).  
- `'single quotes'`: literal text (no expansion).  
- Escape a space with `\ ` or quote the whole path.

**Redirection & Pipes**
```bash
echo "Intro" > week1.txt   # overwrite
echo "More"  >> week1.txt  # append
cat week1.txt | wc -l      # count lines via pipe
```

---

## Core Scenario: 11-Week `notes` Directory

> You maintain weekly notes for an 11‑week program inside `notes/`.

**Visual structure**
```
notes/
├── week1.txt
├── week2.txt
├── week3.txt
├── week4.txt
├── week5.txt
├── week6.txt
├── week7.txt
├── week8.txt
├── week9.txt
├── week10.txt
└── week11.txt
```

**Create it (idempotent from scratch):**
```bash
mkdir -p notes
cd notes
touch week1.txt week2.txt week3.txt week4.txt week5.txt week6.txt week7.txt week8.txt week9.txt week10.txt week11.txt
```
- `-p` creates parents if needed; does nothing if they already exist.  
- `touch` ensures files exist (creates empty if missing, updates mtime if present).

**Populate some content:**
```bash
echo "Week 1: Introduction to Linux and the CLI" > week1.txt
echo "Week 2: Understanding the File System"    > week2.txt
echo "Week 3: Working with Text Files"          > week3.txt
```

**Duplicate a file (possible mistake to investigate):**
```bash
cp week2.txt week1_copy.txt
```

---

## Viewing Text: `cat`, `more`, `less`, `head`, `tail`

### `cat` — Concatenate & display entire file
```bash
cat week1.txt
cat week1_copy.txt
```
- Fast, simple view for **small** files.  
- Use side‑by‑side with shell features to compare quickly.

### `more` — Page through forward
```bash
more week1.txt   # Space = next page, q = quit
```
- Minimal paging; forward‑only reading.

### `less` — Best pager (scroll & search)
```bash
less week2.txt   # ↑/↓ to scroll; /keyword to search; n for next; q to quit
```
- Efficient for large files; does not read entire file at once.

### `head` — First lines
```bash
head week3.txt         # default 10 lines
head -n 5 week3.txt    # first 5 lines
```

### `tail` — Last lines
```bash
tail week3.txt         # default 10 lines
tail -n 5 week3.txt    # last 5 lines
```
> **Pro move:** `tail -f logfile` to follow growth in real time (use `Ctrl+C` to stop).

---

## Create/Organize: `mkdir`, `touch`, `cp`, `mv`, `rm` (safe use)

```bash
mkdir finance hr management          # create 3 directories
touch finance/budget.txt hr/employees.txt management/notes.txt
ls -l                                # verify
```
**Safe habits**
- `cp -i` prompts before overwrite; `cp -r` for directories.  
- `mv -i` prompts on overwrite; useful for renames.  
- `rm -i` prompts; `rm -r` removes directories; **avoid** `rm -rf /` (danger).  
- Prefer moving to a “trash” folder if nervous; or use `gio trash`/`trash-cli` where available.

---

## Editing: `nano` plus quick adds with `echo`/redirection

```bash
nano week1.txt
# In nano: type text → Ctrl+O (write) → Enter (confirm) → Ctrl+X (exit)
```
Quick one‑liners:
```bash
echo "Additional topic on commands" >> week1.txt
```

---

## `tree`: install, verify, and use

The **`tree`** command prints a directory tree in ASCII.

### Install
| Platform | Command |
|---|---|
| Debian/Ubuntu | `sudo apt update && sudo apt install -y tree` |
| Fedora/RHEL/CentOS (dnf) | `sudo dnf install -y tree` |
| openSUSE | `sudo zypper install -y tree` |
| Arch/Manjaro | `sudo pacman -S tree` |
| macOS (Homebrew) | `brew update && brew install tree` |
| Windows (MSYS2/Git Bash) | Provided with some Git Bash installs; otherwise use MSYS2 `pacman -S tree` |

**Verify install & version:**
```bash
which tree && tree --version
```

### Use
```bash
tree notes
tree -L 2 -a       # depth 2, include hidden
tree -d            # directories only
tree -f            # print full paths
```
**Sample output**
```
notes/
├── week1.txt
├── week2.txt
└── week3.txt
```

**Troubleshooting**
- `tree: command not found` → install it (see table above).  
- On macOS, ensure Homebrew is in PATH: `echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile && source ~/.zprofile` (Apple Silicon path).

---

## JSON & YAML quick basics

**JSON**
```json
{
  "name": "student",
  "week": 2,
  "topics": ["Linux", "CLI", "File Management"]
}
```
Validate/pretty‑print with `jq`:
```bash
cat config.json | jq .
# Install jq (Debian/Ubuntu): sudo apt install -y jq
```

**YAML**
```yaml
name: student
week: 2
topics:
  - Linux
  - CLI
  - File Management
```
- Indentation matters (spaces, not tabs).  
- Keys end with `:`; lists use `-`.

---

## Permissions (Deep Dive): `ls -l`, `chmod`, `chown`, `umask`, setuid/setgid/sticky

### Read file metadata
```bash
ls -l notes/week1.txt
```
Example output:
```
-rw-r--r-- 1 user user 41 Oct 15 12:00 notes/week1.txt
```
Breakdown:
- `-` = regular file (directory would be `d`).
- `rw-` (owner), `r--` (group), `r--` (others).
- Owner = `user`; group = `user`.
- Size = 41 bytes; modified Oct 15 12:00.

**Permission bits**
- `r` = read, `w` = write, `x` = execute.  
- For **directories**, `x` means *enter/search*; `r` means *listable*; `w` allows creating/removing entries.

### Change permissions: `chmod`

**Symbolic mode**
```bash
chmod u+x script.sh     # give execute to user
chmod g-w file.txt      # remove write from group
chmod a+r notes/*.txt   # everyone gets read
chmod u=rw,go=r file    # set exactly
```

**Octal mode**
- `r=4`, `w=2`, `x=1` → sum per role.  
- `chmod 644 file` → `rw-r--r--`  
- `chmod 600 secrets.txt` → `rw-------`  
- `chmod 755 bin/` → `rwxr-xr-x` (common for dirs & executables)

### Ownership: `chown` & `chgrp`
```bash
sudo chown alice:developers project/ -R   # recursive
chgrp instructors notes/*.txt
```

### Default masks: `umask`
Show current:
```bash
umask
```
Common values:
- `022` → files default to `644`, dirs `755`.  
- `077` → private: files `600`, dirs `700`.

**How it works:** default mode (files 666, dirs 777) **minus** the mask.  
E.g., `666 - 022 = 644` for files.

### Special bits: setuid, setgid, sticky
- **setuid (4xxx)**: run program with file owner’s UID (mostly on executables like `/usr/bin/passwd`).  
- **setgid (2xxx)**: on **dirs**, new files inherit the directory’s group (useful for shared folders).  
- **sticky (1xxx)**: on **dirs**, only owner (or root) can delete files there (e.g., `/tmp`).

Examples:
```bash
chmod 2755 shared/       # setgid on directory + rwxr-xr-x
chmod 1755 /srv/dropbox  # sticky + rwxr-xr-x
```

### Audit / find by permission
```bash
find . -type f -perm 0777
find shared -type d -perm -2000   # directories with setgid
```

> **Security tips**  
> • Give the **least** permissions needed.  
> • For scripts: `chmod 700 myscript.sh` while developing.  
> • For shared dirs: use group + setgid on the directory instead of world‑writable flags.  
> • Avoid `chmod -R 777`.

---

## Hands‑On Labs

### Lab 1 — Inspect potential duplicate notes

1) Create & populate
```bash
mkdir -p notes && cd notes
touch week1.txt week2.txt week3.txt
echo "Week 1: Introduction to Linux" > week1.txt
echo "Week 2: File System Basics"    > week2.txt
echo "Week 3: Text Utilities"        > week3.txt
cp week2.txt week1_copy.txt
```

2) Investigate with viewers
```bash
cat week1.txt
cat week1_copy.txt
more week1.txt
less week2.txt     # /File to search the word 'File'
head -n 3 week3.txt
tail -n 2 week3.txt
```

3) Decide action (rename/remove if duplicate)
```bash
mv -i week1_copy.txt week2_notes_backup.txt   # -i prompts before overwrite
```

### Lab 2 — Departmental structure + `tree`
```bash
cd ..
mkdir finance hr management
touch finance/budget.txt hr/employees.txt management/notes.txt
echo "Q1 Budget Planning" > finance/budget.txt
echo "Employee Onboarding" > hr/employees.txt
echo "Leadership Notes"    > management/notes.txt
tree -L 2 -a
```

### Lab 3 — Permissions round‑trip
```bash
ls -ld finance hr management
chmod 2775 finance           # setgid so new files inherit group
chmod 750  hr                # restrict HR dir
chmod 755  management        # readable by all
ls -ld finance hr management
umask 077                    # private defaults for this shell
touch finance/private.txt
ls -l finance/private.txt
```

### Lab 4 — Summary file
```bash
cd notes
head -n 1 week*.txt > summary.txt
cat summary.txt
```

---

## Key Takeaways
- Keep **case sensitivity** and **command structure** in mind: `command [options] [args]`.
- Use the right **viewer** for the job: `cat` (small), `less` (large/search), `head`/`tail` (spot checks).
- Distinguish **files vs directories**: `touch` creates files; `mkdir` creates directories.
- `tree` gives a fast visual of structure; install it if missing.
- Master **permissions**: read `ls -l`, set with `chmod`, manage owners with `chown`, set collaborative behavior with setgid, and choose defaults with `umask`.
