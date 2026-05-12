# Bandit Level 2 → Level 3

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 2 → 3 |
| Difficulty | Easy |
| Tags | `cat`, `special-filenames`, `spaces`, `quoting` |

---

## Objective

The password is stored in a file called `spaces in this filename` in the home directory. Read it.

---

## Concepts Involved

**Spaces in filenames:** The space character is used by the shell as a delimiter between arguments. A filename like `spaces in this filename` is interpreted by the shell as four separate arguments: `spaces`, `in`, `this`, and `filename`. To treat it as a single argument, you need to either quote it or escape each space.

**Quoting in bash:** Surrounding an argument with double quotes (`"..."`) or single quotes (`'...'`) tells the shell to treat everything inside as a single token, including spaces. This is essential knowledge for scripting, log parsing, and handling paths with special characters.

**Escape characters (`\`):** An alternative to quoting — placing a backslash before a space (`\ `) tells the shell to treat that specific space as a literal character rather than a delimiter. Both approaches achieve the same result.

---

## Solution

```bash
ls
```

Output:
```
spaces in this filename
```

```bash
cat "./spaces in this filename"
```

Alternatively, using backslash escaping:

```bash
cat spaces\ in\ this\ filename
```

---

## Commands Breakdown

### `cat "./spaces in this filename"`

| Part | Meaning |
|---|---|
| `cat` | Read and print the contents of a file |
| `"./spaces in this filename"` | The full filename wrapped in quotes so the shell treats it as one argument; `./` makes the path explicit |

### Alternative: `cat spaces\ in\ this\ filename`

| Part | Meaning |
|---|---|
| `\ ` | Backslash-escaped space — tells the shell this space is part of the filename, not a separator |

---

## Key Takeaways

- **Spaces in paths are a common real-world issue.** When writing bash scripts that process files (logs, evidence files, exported reports), paths with spaces will break your script unless you quote your variables properly. The correct habit is always `"$variable"` with double quotes.

- **Quoting is fundamental to safe scripting.** In security automation — writing parsers, SIEM correlation rules, or forensic scripts — unquoted variables are a frequent source of bugs and vulnerabilities. This level reinforces why quoting is non-negotiable.

- **Tab completion is your ally.** In a real shell, pressing Tab after typing the first few characters of a filename with spaces will auto-complete it with proper escaping. A small but useful workflow detail.

---

## Password

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```
