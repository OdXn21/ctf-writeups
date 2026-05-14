# Bandit Level 7 → Level 8

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 7 → 8 |
| Difficulty | Easy |
| Tags | `grep`, `text-search`, `large-files`, `pattern-matching` |

---

## Objective

The password is stored in the file `data.txt` next to the word "millionth". The file is very large. Find the line containing that word and extract the password.

---

## Concepts Involved

**`grep` — Global Regular Expression Print:** Searches through text (files or piped input) for lines matching a given pattern and prints those lines. It is one of the most essential tools in Linux for log analysis, pattern searching, and text filtering.

**Searching large files:** In a production environment, log files can be gigabytes in size. Opening them with `cat` or a text editor is impractical. `grep` reads the file line by line and only outputs matches, making it efficient regardless of file size.

**Fixed string search vs regex:** `grep "millionth"` searches for the literal string. `grep` also supports regular expressions for more complex patterns — essential for log parsing in a SOC context.

---

## Solution

```bash
grep millionth data.txt
```

Output:
```
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

## Commands Breakdown

### `grep millionth data.txt`

| Part | Meaning |
|---|---|
| `grep` | Search for lines matching a pattern |
| `millionth` | The literal string to search for |
| `data.txt` | The file to search in |

---

## Key Takeaways

- **`grep` is a daily-use tool in a SOC.** Log analysis is one of the core activities of a Security Operations Centre. Whether you are looking for a specific IP address, a username, an error code, or a suspicious string in thousands of log lines, `grep` is the starting point. Knowing it deeply — including flags like `-i` (case-insensitive), `-r` (recursive), `-n` (line numbers), `-v` (invert match), and `-E` (extended regex) — is essential.

- **Combining `grep` with other tools creates powerful pipelines.** In practice you rarely use `grep` alone. Common patterns: `grep "error" syslog | sort | uniq -c | sort -rn` to count error occurrences, or `grep -r "password" /etc/` to search config files for exposed credentials.

- **`grep` for threat hunting.** In a real investigation, `grep`-based searches across log files are often the first step before escalating to a full SIEM query. Being comfortable constructing these searches quickly is a practical skill interviewers will test.

---

## Password

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
