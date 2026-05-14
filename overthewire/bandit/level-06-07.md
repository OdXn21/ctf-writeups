# Bandit Level 6 → Level 7

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 6 → 7 |
| Difficulty | Easy–Medium |
| Tags | `find`, `user`, `group`, `ownership`, `stderr-redirection` |

---

## Objective

The password is stored somewhere on the server (not just in the home directory). The file has three attributes: it is owned by user `bandit7`, belongs to group `bandit6`, and is exactly 33 bytes in size.

---

## Concepts Involved

**File ownership in Linux:** Every file in Linux has both an owner (a user) and a group. These determine who has access to the file based on the permission bits. The `find` command can filter by both `-user` and `-group`.

**Searching the entire filesystem:** Searching from `/` (root) rather than a specific directory means `find` will traverse the whole system. This will produce many "Permission denied" errors for directories the current user cannot access.

**Redirecting stderr to `/dev/null`:** When running `find` system-wide, it generates a large number of `Permission denied` error messages which clutter the output and make it hard to see the actual results. Redirecting standard error (`2>`) to `/dev/null` discards these errors, leaving only the useful output.

**`/dev/null`:** A special file in Linux that discards everything written to it. It is often called the "black hole" of the filesystem. Redirecting unwanted output here is a standard technique in scripting and command-line work.

---

## Solution

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Output:
```
/var/lib/dpkg/info/bandit7.password
```

```bash
cat /var/lib/dpkg/info/bandit7.password
```

---

## Commands Breakdown

### `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

| Part | Meaning |
|---|---|
| `find` | Search for files in a directory hierarchy |
| `/` | Start from the filesystem root — search everywhere |
| `-user bandit7` | Match only files owned by the user `bandit7` |
| `-group bandit6` | Match only files belonging to the group `bandit6` |
| `-size 33c` | Match files of exactly 33 bytes |
| `2>/dev/null` | Redirect standard error (file descriptor 2) to `/dev/null`, suppressing "Permission denied" messages |

---

## Key Takeaways

- **File ownership is a core Linux security mechanism.** Understanding user and group ownership is fundamental to Linux privilege escalation — a key topic in both penetration testing and CTF challenges. Many privilege escalation paths involve finding files with unusual ownership or world-writable permissions.

- **`2>/dev/null` is a professional habit.** In real-world scripts and forensic queries, suppressing irrelevant error messages makes output clean and actionable. A script that floods the terminal with permission errors is harder to use and easier to miss results in.

- **System-wide `find` queries are a post-compromise technique.** After gaining initial access to a system, attackers run queries like this to find credential files, configuration files with passwords, or other sensitive data owned by specific users. Defenders need to understand this to anticipate attacker behaviour.

- **`/var/lib/dpkg/info/`** is a location that stores package metadata for Debian-based systems. Finding a password file there is unusual — in a real environment, that would be a significant indicator of tampering.

---

## Password

```
morbNTDkSW6jiLUc0ymOdMaLnOLFVAaj
```
