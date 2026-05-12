# Bandit Level 0 → Level 1

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 0 → 1 |
| Difficulty | Easy |
| Tags | `ssh`, `ls`, `cat`, `file-reading` |

---

## Objective

Connect to the Bandit server via SSH using the credentials for `bandit0`, find the password for the next level stored in a file called `readme` in the home directory, and use it to log in as `bandit1`.

---

## Concepts Involved

**SSH (Secure Shell):** A cryptographic network protocol used to securely connect to remote systems over an unsecured network. It is the standard method for remote administration of Linux servers. In professional environments, SSH access is one of the most audited and monitored entry points — knowing how it works at a fundamental level is essential for both system administration and security analysis.

**`ls` — List directory contents:** Displays the files and directories in the current location. One of the most frequently used commands in Linux. Without arguments, it shows non-hidden files in the current working directory.

**`cat` — Concatenate and print:** Reads a file and outputs its contents to the terminal. Despite its simplicity, `cat` is used extensively in scripting, log analysis, and forensic investigation to quickly inspect file contents.

---

## Solution

### Connecting to the server

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

When prompted for a password, enter: `bandit0`

### Finding and reading the file

```bash
ls
```

Output:
```
readme
```

```bash
cat readme
```

---

## Commands Breakdown

### `ssh bandit0@bandit.labs.overthewire.org -p 2220`

| Part | Meaning |
|---|---|
| `ssh` | Invoke the SSH client |
| `bandit0@...` | Connect as user `bandit0` on the specified host |
| `-p 2220` | Connect on port 2220 (non-standard; default SSH port is 22) |

### `cat readme`

| Part | Meaning |
|---|---|
| `cat` | Read and print the contents of a file |
| `readme` | The target file in the current directory |

---

## Key Takeaways

- **SSH is the backbone of remote Linux administration.** Every server interaction in a real SOC environment — whether investigating a compromised machine or pulling logs — starts with an SSH connection. Understanding flags like `-p` (port), `-i` (identity file), and `-v` (verbose) is fundamental.

- **`ls` before `cat` is a habit worth building.** Always enumerate what's in a directory before acting. In a real investigation, jumping to read files without first understanding the directory structure can lead to missing important artifacts.

- **Port numbers matter.** The default SSH port is 22. Non-standard ports (like 2220 here) are a common technique used to reduce automated scanning noise. In a SOC context, seeing SSH traffic on unusual ports is a detection signal worth investigating.

---

## Password

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```
