# Bandit Level 9 → Level 10

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 9 → 10 |
| Difficulty | Easy–Medium |
| Tags | `strings`, `grep`, `binary-files`, `text-extraction` |

---

## Objective

The password is stored in `data.txt` among binary data. It is one of the few human-readable strings in the file, and it is preceded by several `=` characters.

---

## Concepts Involved

**Binary files and embedded strings:** Many files contain a mix of binary data and readable text. Executables, compiled libraries, firmware images, and memory dumps all contain printable ASCII strings embedded within non-printable binary content. `cat` on such a file produces garbage output.

**`strings`:** Extracts printable character sequences from a binary file, outputting only the human-readable text. By default, it reports sequences of 4 or more printable characters. It is a standard first-step tool in malware analysis and binary forensics.

**Chaining `strings` with `grep`:** `strings` extracts all readable text from a file; `grep` then filters for the specific pattern you are looking for. The combination is extremely useful for rapidly locating specific content in binary files.

---

## Solution

```bash
strings data.txt | grep =====
```

Output (example):
```
========== the
========== password
========== is
========== FGUW5illVJrxX9kMYMmlN4MgbpfMiqey
```

---

## Commands Breakdown

### `strings data.txt | grep =====`

| Part | Meaning |
|---|---|
| `strings` | Extract printable character sequences from the file |
| `data.txt` | The input file (contains binary data mixed with text) |
| `\|` | Pipe the output of `strings` into `grep` |
| `grep =====` | Filter for lines containing five or more `=` characters — the pattern hinting at the password location |

---

## Key Takeaways

- **`strings` is a core malware analysis tool.** When you receive a suspicious binary file — whether from a phishing email attachment, a compromised machine, or a malware sample — running `strings` on it is one of the first steps. It can reveal hardcoded URLs, IP addresses, registry keys, API function names, and even embedded credentials, without requiring you to reverse engineer the binary.

- **`strings | grep` is a pattern you will use repeatedly.** Combining these two tools to search for IPs, URLs, credentials, or specific keywords inside binary blobs is a technique used in incident response, malware analysis, and CTF challenges alike.

- **Applying `grep` to `strings` output is not just for CTFs.** In real investigations: `strings malware.exe | grep -E "http|https"` to find C2 URLs, `strings firmware.bin | grep -E "[0-9]{1,3}\.[0-9]{1,3}"` to find IP addresses, or `strings memory.dmp | grep "password"` during a memory forensics investigation.

---

## Password

```
FGUW5illVJrxX9kMYMmlN4MgbpfMiqey
```
