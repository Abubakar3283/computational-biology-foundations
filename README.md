# 🐧 Linux Fundamentals & High-Performance Computing (HPC) Guide

Welcome to the lab! This repository is a structured, practical, and hands-on guide designed for new graduate researchers to quickly master the Linux environment, command-line operations, shell scripting, and data processing.

---

## 📑 Table of Contents
1. [Computer Architecture & OS Layers](#1-computer-architecture--os-layers)
2. [Anatomy of the Terminal Prompt](#2-anatomy-of-the-terminal-prompt)
3. [Linux Filesystem Hierarchy (FHS)](#3-linux-filesystem-hierarchy-fhs)
4. [Essential Navigation & File Operations](#4-essential-navigation--file-operations)
5. [Data Processing & Text Wrangling (grep, sed, awk)](#5-data-processing--text-wrangling)
6. [Process Control & Job Management](#6-process-control--job-management)
7. [Archiving & Compression](#7-archiving--compression)
8. [Best Practices for Research Computing](#8-best-practices-for-research-computing)

---

## 1. Computer Architecture & OS Layers

Understanding what happens under the hood when a command is executed:

```text
[ User ]
   │
   ▼
[ Software Interface (CLI / GUI) ]
   │
   ▼
[ System Calls / API Interface ]
   │
   ▼
[ Operating System Kernel ]
   │
   ▼
[ Hardware (CPU, RAM, Storage, Network) ]


/ (System Root)
├── bin/          # Essential system command binaries (ls, cp, bash)
├── dev/          # Hardware device representations (disks, terminals)
├── etc/          # System-wide configuration files (networking, apps)
├── home/         # User personal workspaces (/home/username)
├── mnt/          # Mount points for external drives (e.g., Windows C: drive in WSL)
├── tmp/          # Temporary scratchpad files (cleared on reboot)
└── usr/bin/      # User-installed applications (python3, git, gcc)

whoami          # Prints current logged-in username
uname -a        # Displays Linux kernel version and system architecture
date            # Prints current system timestamp
clear           # Clears the terminal screen

pwd             # Print Working Directory (shows your exact location)
cd ~            # Jump to user home directory
cd ..           # Move one directory up (to parent)
cd -            # Toggle back to the previous directory
cd /            # Jump directly to the system root

mkdir -p a/b/c  # Create nested directories in a single command
touch file.txt  # Create an empty file or update timestamp
ls -lh          # List files in detailed, human-readable format
cp src.txt dst/ # Copy a file to target directory
mv old.txt new/ # Move or rename a file
rm -rf folder/  # Recursively delete a directory (use with caution!)

cat << 'EOF' > script.sh
echo "Automating tasks..."
echo "Done!"
EOF

grep "ERROR" server.log             # Search and print matching lines
grep -c "Taiwan" customers.csv      # Count occurrences of a keyword
grep -E "pattern1|pattern2" log.txt # Extended regular expression matching

grep "CRITICAL" app.log > errors.txt       # Overwrite
grep "WARNING" app.log >> errors.txt       # Append
cat data.csv | grep "Active" | wc -l       # Pipeline chaining

# Substitute word in stream (e.g., replace Taiwan with TW)
sed 's/Taiwan/TW/g' input.csv > output.csv

# Convert comma-delimited (CSV) to tab-delimited (TSV)
tr ',' '\t' < data.csv > data.tsv

# Print column 2 and 4 from a tab-separated file
awk -F'\t' '{print $2, $4}' data.tsv

# Filter rows where column 3 is "TW" and calculate sum of column 5
awk -F',' '$3 == "TW" {sum += $5} END {print "Total Spending: ", sum}' data.csv

sleep 100 &     # Run a process in the background using '&'
jobs            # List active background jobs in the current shell
fg %1           # Bring background job 1 back to foreground
bg %1           # Resume a paused job (Ctrl + Z) in the background
top             # Interactive real-time process monitor (press 'q' to quit)
watch -n 2 ls   # Monitor directory changes every 2 seconds

# Create a Bzip2 compressed archive
tar -cjvf project_backup.tar.bz2 project/

# Create a Gzip compressed archive
tar -czvf project_backup.tar.gz project/

# Extract an archive
tar -xvf project_backup.tar.bz2















































































## 1. Operating System Architecture & Computing Foundations
* **Layered System Model:** User -> Shell/GUI -> System Calls (API) -> Linux Kernel -> Hardware (CPU, RAM, Disk, Network).
* **Kernel Responsibilities:** Process scheduling, virtual memory management, virtual filesystem (VFS), and hardware peripheral abstraction.
* **Distributions vs. Vanilla Kernel:** Linus Torvalds kernel core vs. complete distributions (Ubuntu, Debian, Arch, Fedora) bundled with GNU coreutils, glibc, and package systems (apt).
* **Shell Anatomy:** Interaction between terminal emulator, shell interpreter (Bash/Zsh), environment variables, and the prompt (user@host:pwd$).
* **Inspection Commands:** whoami, uname -a, which, date, clear, history, man.

---

## 2. Linux Filesystem Structure & Navigation
* **Filesystem Hierarchy Standard (FHS):**
  * / : Universal root directory.
  * /bin, /usr/bin : Executable user binaries and system tools.
  * /etc : System-wide daemon and service configurations.
  * /home : User home environments and workspaces.
  * /mnt : External mount points and WSL Windows drives (/mnt/c/).
  * /tmp : Ephemeral/scratch storage.
* **Path Traversal Syntax:**
  * Absolute paths (/home/user/...) vs. Relative paths (./, ../).
  * Shorthands: Current (.), Parent (..), Home (~), Previous (cd -).
  * Nested directory tree generation: mkdir -p dir1/dir2/dir3.

---

## 3. File Operations, Archiving & Compression
* **File Management:** Creation and modification using touch, cp, mv, and recursive deletion rm -rf.
* **Archiving vs. Compression Engines:**
  * Archiving packs multi-file trees without size reduction (tar).
  * Compression shrinks data streams (gzip, bzip2, zip).
  * Standard archive builds: tar -czvf archive.tar.gz and tar -cjvf archive.tar.bz2.
  * Streaming inspection without uncompressing: zcat file.gz | head.
* **I/O Redirection & Heredoc Construction:**
  * Standard output overwriting (>) vs. appending (>>).
  * Multiline heredoc automation: cat << "EOF" > file.txt.

---

## 4. Text Processing, Stream Wrangling & Regex
* **Tabular Standards:** TSV (Tab-Separated Values) vs. CSV, and why TSV prevents delimiter collision during bioinformatics streaming pipelines.
* **Stream Filtering & Regular Expressions:**
  * Matching patterns and counting lines: grep -c "pattern" file.
  * Extended Regular Expressions (grep -E) for alternation, domain extraction, and alphanumeric boundaries.
* **Stream Transformation Utilities:**
  * In-place token substitution: sed "s/old/new/g".
  * Character translations and field conversions: tr "," "\\t".
* **Column-Oriented Parsing & AWK Processing:**
  * Extracting columns via cut -f 1,3 and computing unique line frequencies via sort | uniq -c | sort -nr.
  * Field parsing with awk: Delimiters (-F"\\t"), condition logic ($3 == "gene"), and inline accumulator mathematics (sum += $5).

---

## 5. Process Lifecycle, System Monitoring & Terminal Multiplexing
* **Process & Job Control:**
  * Suspending processes with sleep or Ctrl + Z.
  * Moving jobs between background (bg, &) and foreground (fg).
  * Process monitoring: top, htop, and scheduled command polling with watch.
* **Terminal Multiplexing with Tmux:**
  * Decoupling long compute jobs from terminal sessions to prevent disconnections.
  * Creating named sessions: tmux new -s <session_name>.
  * Keybindings: Detaching (Ctrl+B, D), reattaching (tmux attach -t <name>), and listing (tmux ls).

---

## 6. Permissions, Shell Scripting & Server Basics
* **Linux Security Triad:** Read (r=4), Write (w=2), Execute (x=1) across User, Group, and Others.
* **Executable Bits:** Enabling execution via chmod +x script.sh.
* **Automated Bash Scripting:** Utilizing #!/bin/bash shebangs, parameters, conditional evaluation, and automated data cleaning loops.
* **Server daemons:** Service state control via systemctl start|stop|status|restart.

---

## 7. Python & Scientific Environment Management (Conda)
* **Isolated Environment Architecture:** Preventing package version collisions and dependency rot across bioinformatics libraries.
* **Conda Lifecycle:**
  * Creating environments: conda create -n bio_project python=3.10.
  * Activation & Deactivation: conda activate bio_project / conda deactivate.
  * Inspecting binary paths: which python and conda list.
* **Scripted Data Pipelines:** Reading multi-gigabyte coordinate files line-by-line, dictionary lookups, and building lookup tables without RAM overload.

---

## 8. Version Control with Git & GitHub
* **Local Operations:** Repository setup (git init), state verification (git status), staging (git add), and semantic commits (git commit -m "...").
* **Remote Synchronization:** Linking remotes (git remote add origin), branch configuration (git branch -M main), and upstream pushing (git push -u origin main).
* **Branch Conflict & Rebase Resolution:**
  * Diagnosing non-fast-forward push rejections.
  * Resolving merge conflicts resulting from simultaneous edits across web editors and local workstations.
  * Managing rebase flows: git pull --rebase origin main, aborting via git rebase --abort, and synchronized updates.

---

## 9. Modern AI-Assisted Tooling & Editor Integration
* **Terminal Coding Agents (OpenCode):**
  * Launching context-aware agent sessions (opencode) in the local repository tree.
  * Prompting agents to parse file trees, apply targeted code patches, and close unclosed markdown blocks without copy-paste truncation.
* **VS Code Workflow:** CLI invocation (code .) and syntax visualization to catch malformed code fences and unclosed backticks.

---

## 10. Computational Genomics & Coordinate Systems (Ensembl GFF3)
* **GFF3 9-Column Specification:**

| Col | Field | Biological Interpretation |
| :---: | :--- | :--- |
| **1** | `seqid` | Chromosome or unplaced scaffold identifier (`1-19`, `X`, `Y`, `MT`, `GL...`) |
| **2** | `source` | Annotation authority or pipeline (`ensembl_havana`) |
| **3** | `type` | Sequence Ontology term (`gene`, `mRNA`, `CDS`, `exon`) |
| **4** | `start` | 1-based start genomic base position |
| **5** | `end` | Inclusive end genomic base position |
| **6** | `score` | Alignment confidence score |
| **7** | `strand` | Directionality of transcription (`+` forward, `-` reverse) |
| **8** | `phase` | Codon reading frame offset for CDS (`0`, `1`, `2`) |
| **9** | `attributes` | Semicolon-delimited ancestry metadata (`ID=...;Parent=...`) |

* **Hierarchical Central Dogma Representation:**
  Gene (ID=gene:...) -> mRNA (Parent=gene:...) -> CDS / Exon (Parent=transcript:...)
* **Exon vs. CDS Divergence:**
  * **Exons:** Genomic regions retained in mature RNA (including non-coding 5 and 3 UTRs).
  * **CDS:** Strictly protein-coding segments translated into amino acid chains.
* **Alternative Splicing Ratio:** Mouse transcriptome reveals ~2.60 transcripts per protein-coding gene locus.
* **Chromosomal Diversity:** 22 canonical chromosomes vs. unplaced assembly scaffolds (GL..., JH...).

---

## 11. Interactome Biology & Probabilistic Network Modeling (STRING)
* **Biological Context of PPI:** Proteins function within macromolecular machines, multimeric complexes, and metabolic cascades.
* **Pairwise Data Graph:** STRING strictly represents pairwise relations (A <-> B). Complex multiprotein assemblies decompose into sets of pairwise edges.
* **The 7 Biological Evidence Channels:**
  * Experiments, Databases, Text-mining, Co-expression, Neighborhood, Gene Fusion, and Co-occurrence.
* **Probabilistic Scoring Model:**
  Combining independent channel error probabilities (1 - S_i):
  * S_combined = 1 - product(1 - S_i)
  * Final_Score = round(S_combined * 1000)
* **Confidence Tiers:** Low (>= 150), Medium (>= 400), High (>= 700), and Highest Confidence (>= 900).

---

## 12. Technical Writing & Markdown Engineering
* Constructing executive-grade documentation with dashboard status tables, LaTeX mathematical expressions, and systematic schemas.
* Eliminating broken terminal buffer truncations and ensuring strict compliance with open/close backtick markers.
"""

with open("README.md", "w", encoding="utf-8") as f:
    f.write(content)
print("SUCCESS: README.md created cleanly with all 12 modules!")
'
