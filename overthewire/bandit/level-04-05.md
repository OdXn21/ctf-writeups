# Bandit Level 4 → Level 5

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 4 → 5 |
| Difficulty | Easy |
| Tags | `file`, `human-readable`, `ASCII`, `binary-files` |

---

## Objective

There are multiple files inside the `inhere` directory named `-file00` through `-file09`. Only one of them contains human-readable (ASCII) text — that file holds the password. Identify which one it is and read it.

---

## Concepts Involved

**Human-readable vs binary files:** Not all files contain plain text. Many files (executables, images, compressed archives, encrypted data) contain binary data — arbitrary bytes that do not form readable characters. A human-readable file contains ASCII or UTF-8 text that can be meaningfully displayed in a terminal.

**The `file` command:** Determines the type of a file by inspecting its content (magic bytes and internal structure), not just its extension. It is one of the most useful commands during forensic triage — you cannot trust file extensions in a security investigation.

**Wildcards (`*`):** The `*` character in a shell command matches any sequence of characters. Using `./-file0*` matches all files starting with `-file0` in the current directory.

---

## Solution

```bash
cd inhere
```

First approach — using `file` to identify the type of each file:

```bash
file ./-file0*
```

Output (example):
```
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

The only human-readable file is `-file07`:

```bash
cat ./-file07
```

---

## Commands Breakdown

### `file ./-file0*`

| Part | Meaning |
|---|---|
| `file` | Determine the type of each file by inspecting its content |
| `./-file0*` | Matches all files in the current directory whose name starts with `-file0`; `./` is needed because the filenames start with `-` |

### `cat ./-file07`

| Part | Meaning |
|---|---|
| `cat` | Read and print the contents of a file |
| `./-file07` | Explicit path to the target file, using `./` to avoid the dash being interpreted as a flag |

---

## Key Takeaways

- **Never trust file extensions.** In a real incident, attackers frequently rename malicious files with innocent-looking extensions (`.txt`, `.log`, `.jpg`) to avoid detection. The `file` command reads the actual content structure to determine the real type — this is a fundamental forensic technique.

- **`file` is a triage tool.** When you land on a compromised machine and find a directory full of unknown files, running `file *` is one of the fastest ways to understand what you are looking at before deciding what to investigate further.

- **`file ./*` vs `file *`:** When filenames start with `-`, always use `./*` or `./-file*` to prevent the shell from interpreting them as command flags. This pattern comes up constantly when dealing with adversarially crafted directories.

---

## Password

```
4oQYVPkxZ0OE005pTW81FB8j8lxXGUQw
```
