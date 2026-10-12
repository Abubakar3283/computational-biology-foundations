# 💻 Linux, Shell & Scientific Computing Toolkit

A foundational, hands-on engineering guide covering Linux system architecture, terminal navigation, text stream wrangling, environment management, scientific Python pipelines, and version control.

---

## 📑 Table of Contents
1. [Operating System Architecture & Terminal Prompt](#1-operating-system-architecture--terminal-prompt)
2. [Filesystem Hierarchy Standard (FHS) & Navigation](#2-filesystem-hierarchy-standard-fhs--navigation)
3. [File Management & Core Utilities](#3-file-management--core-utilities)
4. [Text Wrangling & Data Streaming (grep, sed, awk, tr)](#4-text-wrangling--data-streaming-grep-sed-awk-tr)
5. [Process Lifecycle & Job Monitoring](#5-process-lifecycle--job-monitoring)
6. [Terminal Multiplexing with Tmux](#6-terminal-multiplexing-with-tmux)
7. [Archiving & Data Compression](#7-archiving--data-compression)
8. [File Permissions & Shell Automation (.sh)](#8-file-permissions--shell-automation-sh)
9. [Virtual Environments & Package Management (Conda)](#9-virtual-environments--package-management-conda)
10. [Scientific Python & Tabular Data Processing](#10-scientific-python--tabular-data-processing)
11. [Version Control with Git & GitHub](#11-version-control-with-git--github)
12. [Terminal Coding Best Practices](#12-terminal-coding-best-practices)

---

## 1. Operating System Architecture & Terminal Prompt

### System Architecture Layers
```text
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

(base) pumath3283@hostname:~/practice$ 
  │        │          │        │      │
  │        │          │        │      └─ Privilege: $ (Normal User), # (Root / Superuser)
  │        │          │        └─ Current Directory (~ represents /home/username)
  │        │          └─ Computer / Server Hostname
  │        └─ Active Username
  └─ Active Conda Environment



# 💻 Linux, Shell & Scientific Computing Toolkit

A foundational, hands-on engineering guide covering Linux system architecture, terminal navigation, text stream wrangling, environment management, scientific Python pipelines, and version control.

---

## 📑 Table of Contents
1. [Operating System Architecture & Terminal Prompt](#1-operating-system-architecture--terminal-prompt)
2. [Filesystem Hierarchy Standard (FHS) & Navigation](#2-filesystem-hierarchy-standard-fhs--navigation)
3. [File Management & Core Utilities](#3-file-management--core-utilities)
4. [Text Wrangling & Data Streaming (grep, sed, awk, tr)](#4-text-wrangling--data-streaming-grep-sed-awk-tr)
5. [Process Lifecycle & Job Monitoring](#5-process-lifecycle--job-monitoring)
6. [Terminal Multiplexing with Tmux](#6-terminal-multiplexing-with-tmux)
7. [Archiving & Data Compression](#7-archiving--data-compression)
8. [File Permissions & Shell Automation (.sh)](#8-file-permissions--shell-automation-sh)
9. [Virtual Environments & Package Management (Conda)](#9-virtual-environments--package-management-conda)
10. [Scientific Python & Tabular Data Processing](#10-scientific-python--tabular-data-processing)
11. [Version Control with Git & GitHub](#11-version-control-with-git--github)
12. [Terminal Coding Best Practices](#12-terminal-coding-best-practices)

---

## 1. Operating System Architecture & Terminal Prompt

### System Architecture Layers
- User / Developer: Human operator executing analytical pipelines.
- CLI / Shell: Command interpreter translating user text instructions into system calls.
- System Calls (POSIX API): Standard programmatic interface communicating with kernel space.
- Linux Kernel: Operating system engine managing CPU scheduling, memory allocation, and hardware abstractions.
- Hardware: Physical infrastructure (x86_64 CPU, RAM, NVMe/SSD, Network controllers).

### Understanding the Terminal Prompt
A standard interactive shell prompt displays contextual system identity:
`pumath3283@hostname:~/practice$`

- `pumath3283` : Current logged-in user account.
- `@` : Connective delimiter meaning "at".
- `hostname` : Network name of the computer or remote server node.
- `:` : Separator between host identity and current directory location.
- `~/practice` : Working directory path (`~` represents user home workspace `/home/pumath3283`).
- `$` : Privilege marker indicating standard user privileges (`#` indicates administrative root access).

---

## 2. Filesystem Hierarchy Standard (FHS) & Navigation

Linux organizes all mounted storage devices under a single root directory (`/`):
- `/` : Root of the entire filesystem hierarchy.
- `/bin` & `/usr/bin` : Standard user executable command binaries (`ls`, `cp`, `python3`, `bash`).
- `/etc` : System-wide daemon and application configuration files.
- `/home` : Personal workspaces assigned to individual user accounts (`/home/username`).
- `/mnt` : Mount points for external filesystems (including Windows drives on WSL e.g. `/mnt/c/`).
- `/tmp` : Temporary scratch storage flushed on operating system reboot.

### Directory Navigation Syntax
- `pwd` : Print Working Directory (outputs current absolute path).
- `cd /path/to/folder` : Change directory using an absolute or relative path.
- `cd ~` or `cd` : Jump directly to user home directory (`$HOME`).
- `cd ..` : Move one step upward to the immediate parent directory.
- `cd -` : Toggle back to the previously active working directory.

---

## 3. File Management & Core Utilities

### Basic Identity & Diagnostic Inspection
- `whoami` : Output currently authenticated user identity.
- `uname -a` : Display Linux kernel build, release architecture, and system information.
- `date` : Print formatted system clock and timezone timestamp.
- `clear` : Flush visible terminal viewport buffer (shortcut: `Ctrl + L`).
- `history` : Display numbered list of previously executed shell commands.

### Creating, Moving, Copying & Deleting
- `ls` : List contents of current directory.
- `ls -lh` : List files in long format showing file size in human-readable units (K, M, G).
- `mkdir folder_name` : Create a single directory.
- `mkdir -p dir1/dir2/dir3` : Create nested directory trees without returning missing-parent errors.
- `touch file.txt` : Create a zero-byte empty file or refresh existing file access timestamps.
- `cp source.txt target/` : Copy a file to target directory.
- `cp -r source_dir/ target_dir/` : Recursively copy directories and their contents.
- `mv old_path.txt new_path.txt` : Move or rename files and directories.
- `rm file.txt` : Permanently unlink/delete a file.
- `rm -rf folder/` : Forcefully delete a directory tree recursively (irreversible operation).

### Inspection & Text Reading
- `cat file.txt` : Print entire file content to standard output.
- `head -n 20 file.txt` : Output the top 20 lines of a file.
- `tail -n 20 file.txt` : Output the final 20 lines of a file.
- `less file.txt` : Interactive file viewer for large files (`q` to exit, `/` to search).
- `wc -l file.txt` : Count total newline delimiters in a file.

---

## 4. Text Wrangling & Data Streaming (grep, sed, awk, tr)

Linux pipelines pass standard output (`stdout`) to standard input (`stdin`) using the pipe operator (`|`), allowing continuous processing without disk intermediate saves.

### Stream Filtering with `grep`
- `grep "pattern" data.tsv` : Extract rows matching exact string or regex pattern.
- `grep -i "pattern" data.tsv` : Perform case-insensitive search.
- `grep -v "pattern" data.tsv` : Invert filter to return lines that do not match.
- `grep -c "pattern" data.tsv` : Count total occurrences of matching lines.
- `grep -E "pattern1|pattern2" data.tsv` : Extended regex search for alternative patterns.

### Standard I/O Redirection
- `>` : Overwrite command stdout into a file (`command > file.txt`).
- `>>` : Append command stdout to the end of a file (`command >> file.txt`).
- `|` : Chain output of preceding command directly as input into the following command.

### Stream Editing with `sed` & `tr`
- `sed 's/old_value/new_value/g' file.txt > updated.txt` : Replace string occurrences across lines.
- `tr ',' '\t' < input.csv > output.tsv` : Fast stream translation converting CSV to tab-separated TSV.

### Column-Oriented Processing with `awk`
- `awk -F'\t' '{print $1, $3}' data.tsv` : Extract and print designated columns.
- `awk -F',' '$3 >= 100 {print $1, $3}' table.csv` : Conditional evaluation on numeric fields.
- `awk '{sum += $2} END {print "Total Sum: ", sum}' data.txt` : Accumulator operations across rows.

---

## 5. Process Lifecycle & Job Monitoring

### Job Control
- `command &` : Execute command directly in the background.
- `Ctrl + Z` : Suspend currently running foreground task.
- `jobs -l` : List background tasks running in current shell session with PIDs.
- `bg %1` : Resume suspended task #1 in the background.
- `fg %1` : Bring background job #1 back into foreground interactive mode.
- `kill -9 <PID>` : Send SIGKILL signal to forcefully terminate process ID.

### Real-Time Monitoring
- `top` : Interactive terminal task manager displaying memory, CPU, and process states (`q` to quit).
- `watch -n 2 "ls -lh"` : Execute command repeatedly at 2-second intervals to track real-time changes.

---

## 6. Terminal Multiplexing with Tmux

Tmux maintains terminal sessions independently from network connections, preventing process interruption during connection loss.

- `tmux new -s project_session` : Create a named tmux workspace.
- `Ctrl + B`, release and press `D` : Detach from session cleanly while background computations continue.
- `tmux ls` : List active sessions running on the machine.
- `tmux attach -t project_session` : Reconnect to detached workspace.
- `tmux kill-session -t project_session` : Destroy and close specified session.

---

## 7. Archiving & Data Compression

Archiving aggregates files into a single bundle, while compression reduces physical byte size.

- `tar -cvf archive.tar directory/` : Archive directory without compression.
- `tar -czvf archive.tar.gz directory/` : Archive and compress using gzip engine.
- `tar -cjvf archive.tar.bz2 directory/` : Archive and compress using bzip2 engine (higher compression ratio).
- `tar -xvf archive.tar.gz` : Decompress and unbundle archive into working directory.
- `zcat file.txt.gz | head -n 10` : Inspect gzip-compressed text files without unpacking to disk.
- `zcat file.txt.gz | wc -l` : Count lines within compressed file streams.

---

## 8. File Permissions & Shell Automation (.sh)

### Linux Security Matrix
Permissions are categorized into Owner (u), Group (g), and Others (o) across Read (`r=4`), Write (`w=2`), and Execute (`x=1`).
- `chmod +x pipeline.sh` : Assign executable permission bit to a script.
- `chmod 755 pipeline.sh` : Grant full permissions to owner; read and execute permissions to group and others.

### Defensive Shell Scripting Architecture
Scripts must enforce predictable execution parameters:
- `#!/bin/bash` : Shebang specifying the Bash interpreter.
- `set -e` : Immediately terminate execution if any command yields a non-zero exit code.
- `set -u` : Treat uninitialized variables as syntax errors.
- `set -o pipefail` : Propagate pipeline exit codes correctly from failing sub-commands.

---

## 9. Virtual Environments & Package Management (Conda)

Package management isolates software binaries and libraries, preventing version collisions.

### Channel Priorities
Configuring channels in `.condarc`:
- `conda config --add channels conda-forge`
- `conda config --add channels bioconda`
- `conda config --set channel_priority strict`

### Environment Lifecycle Operations
- `conda create -n dev_env python=3.10 -y` : Create a standalone environment pinned to Python 3.10.
- `conda activate dev_env` : Enter target environment.
- `conda deactivate` : Exit active environment back to base system.
- `conda list` : Display installed software packages and build versions.
- `conda install -y package_name` : Install a package into currently active environment.
- `conda env remove -n dev_env` : Completely purge an environment and its local dependencies.

---

## 10. Scientific Python & Tabular Data Processing

### Chunk-Based Stream Parsing
Loading massive files into memory causes system memory exhaustion. Processing files via chunks ensures bounded memory usage:
```python
import pandas as pd

def stream_tabular_dataset(filepath, chunk_size=50000):
    for chunk in pd.read_csv(filepath, sep='\t', chunksize=chunk_size):
        filtered_records = chunk[chunk['score'] >= 100]
        # Perform downstream vectorized processing
