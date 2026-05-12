# Bandit Level 3 → Level 4

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 3 → 4 |
| Difficulty | Easy |
| Tags | `hidden-files`, `dot-files`, `cd`, `find`, `ls -la` |

---

## Objective

The password is stored in a hidden file inside the `inhere` directory. Find and read it.

---

## Concepts Involved

**Hidden files in Linux (dot-files):** In Linux, any file or directory whose name begins with a dot (`.`) is considered hidden. It does not appear in a standard `ls` listing. This convention exists primarily to keep configuration files out of normal directory views, but it is also commonly abused to hide malicious files on compromised systems.

**`ls -la`:** The `-a` flag shows all files including hidden ones. The `-l` flag shows them in a long-form listing with permissions, ownership, size, and modification date. Together, `ls -la` is one of the first commands you run when investigating a directory.

**`find` for locating files:** The `find` command searches the filesystem for files matching specified criteria. It is far more powerful than `ls` for locating files, especially when you don't know the exact name or location.

**`cd` — Change directory:** Navigates to a different directory in the filesystem. Essential for any terminal workflow.

---

## Solution

```bash
cd inhere
```

```bash
find . -name ".*"
```

Output:
```
./.hidden
```

```bash
cat ./.hidden
```

Alternatively, from the home directory without `cd`:

```bash
ls -la inhere/
cat inhere/.hidden
```

---

## Commands Breakdown

### `cd inhere`

| Part | Meaning |
|---|---|
| `cd` | Change the current working directory |
| `inhere` | The target directory name |

### `find . -name ".*"`

| Part | Meaning |
|---|---|
| `find` | Search for files in a directory hierarchy |
| `.` | Start the search in the current directory |
| `-name ".*"` | Match files whose name starts with a dot (hidden files) |

### `cat ./.hidden`

| Part | Meaning |
|---|---|
| `cat` | Read and print the contents of a file |
| `./.hidden` | Explicitly references the hidden file in the current directory |

---

## Key Takeaways

- **Hidden files are a real attacker technique.** When an attacker gains access to a Linux system, one of their first actions is often to plant persistence mechanisms (backdoors, cron jobs, modified configs) in hidden files or dot-directories. During a forensic investigation, `ls -la` and `find / -name ".*"` are among the first commands run to hunt for anomalies.

- **`ls` without flags hides information.** Standard `ls` will miss hidden files entirely. In a security context, this means you should always use `ls -la` when enumerating a directory — or better yet, use `find` to search recursively.

- **`find` is more reliable than `ls` for enumeration.** `find` can search recursively, filter by name patterns, ownership, permissions, modification time, and more. It is an essential tool in both penetration testing and incident response.

---

## Password

```
2WmrDFRmJIq3IPxneAaMGhapOpFhF3NJ
```
