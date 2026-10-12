# 💻 Linux, Shell & Scientific Computing Toolkit

> A foundational, hands-on engineering guide covering Linux system architecture, terminal navigation, text stream wrangling, environment management, scientific Python pipelines, and version control workflows.

![Linux](https://img.shields.io/badge/Platform-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Conda](https://img.shields.io/badge/Package_Manager-Conda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)
![Git](https://img.shields.io/badge/Version_Control-Git-F05032?style=for-the-badge&logo=git&logoColor=white)

---

## 📑 Table of Contents

| # | Section |
|---|---------|
| 1 | [Operating System Architecture & Terminal Prompt](#1-operating-system-architecture--terminal-prompt) |
| 2 | [Filesystem Hierarchy Standard (FHS) & Navigation](#2-filesystem-hierarchy-standard-fhs--navigation) |
| 3 | [File Management & Core Utilities](#3-file-management--core-utilities) |
| 4 | [Text Wrangling & Data Streaming](#4-text-wrangling--data-streaming-grep-sed-awk-tr) |
| 5 | [Process Lifecycle & Job Monitoring](#5-process-lifecycle--job-monitoring) |
| 6 | [Terminal Multiplexing with Tmux](#6-terminal-multiplexing-with-tmux) |
| 7 | [Archiving & Data Compression](#7-archiving--data-compression) |
| 8 | [File Permissions & Shell Automation](#8-file-permissions--shell-automation-sh) |
| 9 | [Virtual Environments & Package Management (Conda)](#9-virtual-environments--package-management-conda) |
| 10 | [Scientific Python & Tabular Data Processing](#10-scientific-python--tabular-data-processing) |
| 11 | [Version Control with Git & GitHub](#11-version-control-with-git--github) |
| 12 | [Terminal Coding Best Practices](#12-terminal-coding-best-practices) |

---

## 1. Operating System Architecture & Terminal Prompt

### 🏗️ System Architecture Layers

Understanding how your commands travel from your fingertips down to the hardware:

```
[ User / Developer ]
         │
         ▼
[ Command Line Interface (CLI) / Shell (Bash) ]
         │
         ▼
[ System Calls (POSIX API) ]
         │
         ▼
[ Linux Kernel (Process Scheduling, Memory, Hardware Access) ]
         │
         ▼
[ Hardware (CPU, RAM, Disks, Network) ]
```

### 🖥️ Understanding the Terminal Prompt

Every part of the terminal prompt tells you something important:

```
(base) pumath3283@hostname:~/practice$
  │        │          │        │      │
  │        │          │        │      └─ Privilege: $ (Normal User) | # (Root/Superuser)
  │        │          │        └─ Current Directory (~ = /home/username)
  │        │          └─ Computer / Server Hostname
  │        └─ Active Username
  └─ Active Conda Environment
```

> **💡 Tip:** When you see `#` instead of `$`, you are operating as the **root (superuser)**. Be extra careful — root can delete or overwrite anything on the system.

---

## 2. Filesystem Hierarchy Standard (FHS) & Navigation

### 🌳 Linux Directory Tree

Unlike Windows drive letters (`C:\`, `D:\`), Linux uses a **single unified tree** starting at the root `/`:

| Directory | Purpose |
|-----------|---------|
| `/` | Universal root — everything starts here |
| `/bin` & `/usr/bin` | Executable program binaries (`ls`, `cp`, `python3`) |
| `/etc` | System-wide configuration files |
| `/home` | Personal workspaces for each user (`/home/username`) |
| `/mnt` | External storage mounts (and Windows drives inside WSL) |
| `/tmp` | Temporary scratch directory — **cleared on every reboot** |

### 🧭 Directory Navigation Commands

| Command | Description |
|---------|-------------|
| `pwd` | Print working directory — shows your full absolute path |
| `cd /path/to/folder` | Change to an absolute or relative directory path |
| `cd ~` or `cd` | Jump directly to your home directory |
| `cd ..` | Step up one level to the parent directory |
| `cd -` | Toggle back to the previous directory you were in |

---

## 3. File Management & Core Utilities

### 🔍 Basic Identity & Inspection

| Command | Description |
|---------|-------------|
| `whoami` | Display the current active username |
| `uname -a` | Show OS details, kernel version, and hardware architecture |
| `date` | Display system date and time |
| `clear` or `Ctrl + L` | Clear the terminal screen |
| `history` | View list of previously executed commands |

### 📁 Creating, Copying & Deleting

| Command | Description |
|---------|-------------|
| `ls` | List directory contents |
| `ls -lh` | List files with details — permissions, owner, size (MB/GB), modification date |
| `mkdir folder_name` | Create a single directory |
| `mkdir -p a/b/c` | Create deeply nested folders in one command |
| `touch file.txt` | Create an empty file or update its timestamp |
| `cp source.txt destination/` | Copy a file to another location |
| `cp -r source_dir/ target_dir/` | Copy an entire directory recursively |
| `mv old_name.txt new_name.txt` | Rename a file or move it to another folder |
| `rm file.txt` | Delete a file permanently |
| `rm -rf target_folder/` | Delete a folder and **all** its contents recursively |

> ⚠️ **Warning:** `rm -rf` is **irreversible**. There is no recycle bin in Linux. Double-check your path before running this command.

### 👁️ Viewing File Contents

| Command | Description |
|---------|-------------|
| `cat file.txt` | Output the entire file to the screen |
| `head -n 20 file.txt` | View the first 20 lines |
| `tail -n 20 file.txt` | View the last 20 lines |
| `less file.txt` | Interactively scroll through a large file (`q` to exit) |
| `wc -l file.txt` | Count the total number of lines in a file |

---

## 4. Text Wrangling & Data Streaming (grep, sed, awk, tr)

Linux **pipes** (`|`) stream the output of one tool into another — processing data **without loading full files into memory**. This is incredibly powerful for large datasets.

### 🔎 Pattern Matching with `grep`

| Command | Description |
|---------|-------------|
| `grep "keyword" data.tsv` | Find and print lines matching keyword |
| `grep -i "keyword" data.tsv` | Case-insensitive search |
| `grep -v "keyword" data.tsv` | Invert match — exclude lines containing keyword |
| `grep -c "keyword" data.tsv` | Count the total number of matching lines |
| `grep -E "(word1\|word2)" data.tsv` | Extended regular expression search |

### ➡️ I/O Redirection

| Symbol | Behavior |
|--------|----------|
| `>` | **Overwrite** output into a file: `command > out.txt` |
| `>>` | **Append** output to end of a file: `command >> out.txt` |
| `\|` | **Pipe** output of one command into the next: `cat file.txt \| grep "test" \| wc -l` |

### ✂️ Stream Editing with `sed` & `tr`

```bash
# Replace all occurrences of a word across a file
sed 's/old_text/new_text/g' input.txt > output.txt

# Convert comma-delimited CSV into tab-delimited TSV
tr ',' '\t' < file.csv > file.tsv
```

### 📊 Field Parsing with `awk`

```bash
# Print columns 1 and 3 from a tab-separated file
awk -F'\t' '{print $1, $3}' file.tsv

# Filter rows where column 3 is >= 100
awk -F',' '$3 >= 100 {print $1, $3}' data.csv

# Accumulate and print the sum of column 2
awk '{sum += $2} END {print "Sum =", sum}' data.txt
```

---

## 5. Process Lifecycle & Job Monitoring

### ⚙️ Job Execution & Background Tasks

| Command | Description |
|---------|-------------|
| `command &` | Execute a command directly in the background |
| `Ctrl + Z` | Pause a running foreground command |
| `jobs -l` | List background jobs and their Process IDs (PID) |
| `bg %1` | Resume job #1 in the background |
| `fg %1` | Bring job #1 back to the foreground |
| `kill -9 <PID>` | Force terminate a running process |

### 📈 System Resource Monitoring

| Command | Description |
|---------|-------------|
| `top` / `htop` | Interactive real-time CPU, RAM, and thread monitor |
| `watch -n 2 "ls -lh"` | Re-run a command every 2 seconds to observe live changes |

---

## 6. Terminal Multiplexing with Tmux

`tmux` is essential for **remote server work** — it keeps your programs running even if your SSH connection drops.

```
┌──────────────────────────────────────┐
│  tmux Session (survives disconnects) │
│  ┌───────────┐  ┌───────────┐        │
│  │ Window 1  │  │ Window 2  │  ...   │
│  │ (train.py)│  │ (monitor) │        │
│  └───────────┘  └───────────┘        │
└──────────────────────────────────────┘
```

| Command | Description |
|---------|-------------|
| `tmux new -s work` | Create a new named tmux session |
| `Ctrl + B`, then `D` | Safely **detach** from the session (it keeps running) |
| `tmux ls` | List all active sessions |
| `tmux attach -t work` | **Reattach** to a running session |
| `tmux kill-session -t work` | Terminate a specific session |

---

## 7. Archiving & Data Compression

> **Key Concept:** Archiving (grouping files together) and compression (shrinking size) are **two separate operations** — `tar` combines both.

| Command | Description |
|---------|-------------|
| `tar -cvf archive.tar folder/` | Archive only (no compression) |
| `tar -czvf archive.tar.gz folder/` | Archive + **Gzip** compression |
| `tar -cjvf archive.tar.bz2 folder/` | Archive + **Bzip2** compression (smaller, slower) |
| `tar -xvf archive.tar.gz` | Extract any tar archive |

### Inspecting Compressed Files Without Extracting

```bash
# View the first 10 lines of a compressed file directly
zcat file.tsv.gz | head -n 10

# Count lines in a compressed file without extracting
zcat file.tsv.gz | wc -l
```

---

## 8. File Permissions & Shell Automation (.sh)

### 🔐 Linux Security Triad

Every file has three layers of permissions across three user categories:

```
-rwxr-xr-x  1  owner  group  size  date  filename
 │││││││││
 │└┤└┤└┤└┤── Others: r-x (read + execute only)
 │ │ └─┤── Group: r-x (read + execute only)
 │ └───┤── Owner: rwx (full: read + write + execute)
 └─────── File type (- = file, d = directory)
```

| Permission | Symbol | Numeric Value |
|------------|--------|---------------|
| Read | `r` | `4` |
| Write | `w` | `2` |
| Execute | `x` | `1` |

```bash
chmod +x script.sh      # Grant execute permission to all
chmod 755 script.sh     # Full for owner; read+execute for group & others
```

### 🤖 Writing Automated Bash Scripts

A professional, fault-tolerant shell script template:

```bash
#!/bin/bash
set -euo pipefail

INPUT_DIR="data"
OUTPUT_DIR="results"

mkdir -p "${OUTPUT_DIR}"

echo "[INFO] Starting automated workflow..."
# Your commands go here — they execute sequentially
echo "[SUCCESS] Workflow finished cleanly."
```

| Flag | Behavior |
|------|----------|
| `set -e` | Stop **immediately** if any command returns an error |
| `set -u` | Disallow undefined/unset variables |
| `set -o pipefail` | Prevent errors inside pipelines from being silently ignored |

---

## 9. Virtual Environments & Package Management (Conda)

Virtual environments **isolate software tools** per project, completely avoiding package version conflicts between different workflows.

### ⚙️ Channel Configuration (Run Once)

```bash
conda config --add channels conda-forge
conda config --add channels bioconda
conda config --set channel_priority strict
```

### 🔧 Environment Operations

| Command | Description |
|---------|-------------|
| `conda create -n my_env python=3.10 -y` | Create a new Python 3.10 environment |
| `conda activate my_env` | Enter (activate) the virtual environment |
| `conda deactivate` | Exit back to the base system |
| `conda list` | List all installed packages and their versions |
| `conda install -y package_name` | Install a package into the active environment |
| `conda env remove -n my_env` | Permanently delete an entire environment |

---

## 10. Scientific Python & Tabular Data Processing

### 🧮 High-Performance Chunk Reading

When working with files too large to load into RAM all at once, process them in **chunks**:

```python
import pandas as pd

def process_large_file(filepath):
    """Read and filter a massive TSV file in memory-safe chunks."""
    chunk_size = 50_000  # Rows processed per iteration

    for chunk in pd.read_csv(filepath, sep='\t', chunksize=chunk_size):
        filtered = chunk[chunk['score'] > 80]
        # Perform your analysis on each filtered chunk here
        print(f"  → Processed {len(chunk):,} rows, kept {len(filtered):,}")
```

### 📝 Writing Python Files via Terminal (Heredoc)

Write and run a Python script entirely from the terminal without opening a text editor:

```bash
cat << 'EOF' > test.py
print("Environment and Python are functioning properly.")
EOF

python3 test.py
```

---

## 11. Version Control with Git & GitHub

### 🔄 The Git Workflow

```
Working Directory  →  Staging Area  →  Local Repo  →  Remote Repo (GitHub)
   (edit files)       (git add)       (git commit)     (git push)
```

### 🏁 Initializing & Committing Locally

| Command | Description |
|---------|-------------|
| `git init` | Initialize an empty Git repository in current folder |
| `git status` | Check tracked, modified, and untracked files |
| `git add filename` | Stage a specific file for commit |
| `git add .` | Stage **all** changed files at once |
| `git commit -m "feat: descriptive message"` | Save staged changes with a message |

### 🌐 Remote Synchronization (GitHub)

```bash
# Link your local repo to a remote GitHub repository
git remote add origin https://github.com/Username/Repo.git

# Rename the primary branch to 'main' (modern standard)
git branch -M main

# Push your local commits to GitHub for the first time
git push -u origin main

# Pull remote updates and cleanly rebase your local work on top
git pull --rebase origin main
```

### 🚫 Preventing Bloat with `.gitignore`

Create a `.gitignore` file to stop large or temporary files from ever entering your Git history:

```gitignore
# Compressed data files
*.gz
*.tar
*.tar.gz

# Results and output directories
results/
output/

# Python bytecode cache
*.pyc
__pycache__/
```

> **💡 Tip:** Always create your `.gitignore` **before** your first `git add .` to avoid accidentally committing large binary files.

---

## 12. Terminal Coding Best Practices

### ✅ Golden Rules

| # | Rule | Why It Matters |
|---|------|----------------|
| 1 | **Always use `Tab` for auto-completion** | Prevents typos in file and directory names |
| 2 | **Linux is case-sensitive** | `file.txt`, `File.txt`, `FILE.TXT` are three completely separate files |
| 3 | **`Ctrl + C` to cancel anything** | Immediately stops any stuck or runaway terminal process |
| 4 | **Wrap paths with spaces in quotes** | `"my folder/data.txt"` — prevents the shell from misreading the path |

### 🛡️ Defensive Scripting Checklist

- [ ] Add `set -euo pipefail` at the top of every `.sh` script
- [ ] Use `mkdir -p` before writing output files
- [ ] Quote all variables: `"${VAR}"` not `$VAR`
- [ ] Test scripts on small sample data before running on full datasets
- [ ] Commit your scripts to Git before running them on production data

---

## 📜 License

This toolkit is shared for **educational and personal reference purposes**.

---

## 🙌 Acknowledgements

Built as a personal engineering reference for mastering the Linux terminal, scientific computing workflows, and reproducible research practices.

---

<div align="center">

**⭐ If this reference helped you, consider starring the repository! ⭐**

![Made with Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)
![Maintained](https://img.shields.io/badge/Maintained-Yes-green.svg)

</div>
