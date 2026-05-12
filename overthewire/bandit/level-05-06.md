# Bandit Level 5 → Level 6

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 5 → 6 |
| Difficulty | Easy–Medium |
| Tags | `find`, `size`, `executable-bit`, `file-attributes` |

---

## Objective

The password is stored somewhere inside the `inhere` directory, which contains many subdirectories and files. The target file has three specific properties: it is human-readable, exactly 1033 bytes in size, and not executable.

---

## Concepts Involved

**`find` with multiple criteria:** The `find` command supports combining multiple filters in a single query using flags like `-type`, `-size`, and `!` (negation). This allows precise targeting of files matching all specified attributes simultaneously.

**File size notation in `find`:** The `-size` flag accepts units: `c` for bytes, `k` for kilobytes, `M` for megabytes. Using `-size 1033c` matches files of exactly 1033 bytes.

**Executable bit:** Linux file permissions include an executable bit (`x`). A file with this bit set can be run as a program. Using `! -executable` in `find` filters for files where this bit is not set — i.e., plain data or text files.

**`-type f`:** Restricts results to regular files only, excluding directories, symbolic links, device files, and other special file types.

---

## Solution

```bash
cd inhere
```

Initial approach — trying to identify the file manually (too slow with many files):

```bash
file ./*
```

This quickly becomes impractical with nested subdirectories. The correct approach is using `find` with all three criteria at once:

```bash
find . -type f -size 1033c ! -executable
```

Output:
```
./maybehere07/.file2
```

```bash
cat ./maybehere07/.file2
```

> **Note:** My first instinct was to use `file ./*` to check each file individually, which would have worked on a flat directory but is far too inefficient when there are multiple nested subdirectories. Using `find` with combined filters was the right tool for this scale.

---

## Commands Breakdown

### `find . -type f -size 1033c ! -executable`

| Part | Meaning |
|---|---|
| `find` | Search for files in a directory hierarchy |
| `.` | Start the search from the current directory (recursive by default) |
| `-type f` | Match only regular files (excludes directories, symlinks, etc.) |
| `-size 1033c` | Match files of exactly 1033 bytes (`c` = bytes/characters) |
| `! -executable` | Negate the executable bit — only match files that are NOT executable |

---

## Key Takeaways

- **`find` is a precision instrument.** When you have a large, unknown filesystem to search through — as you do in post-compromise forensic analysis — being able to filter by type, size, ownership, permissions, and modification time simultaneously is essential. A single well-constructed `find` command can save hours of manual investigation.

- **Combining filters is more efficient than sequential filtering.** My initial instinct to use `file ./*` was not wrong for a small directory, but it does not scale. The correct habit is to think upfront about all the attributes you know and combine them in one `find` query.

- **The `! -executable` filter matters in real investigations.** During a post-compromise analysis, attackers often leave behind executable files (backdoors, reverse shells, privilege escalation binaries). Being able to filter specifically for executables — or exclude them — is a useful triage technique.

- **File size can be a fingerprint.** Known good files (system binaries, config files, log files) have expected sizes. A file with an unusual size in an expected location is an anomaly worth investigating.

---

## Password

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```
