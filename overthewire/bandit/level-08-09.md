# Bandit Level 8 → Level 9

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 8 → 9 |
| Difficulty | Easy–Medium |
| Tags | `sort`, `uniq`, `pipes`, `deduplication`, `text-processing` |

---

## Objective

The password is stored in `data.txt` and is the only line that appears exactly once in the file. All other lines are duplicates.

---

## Concepts Involved

**`sort`:** Sorts the lines of a file alphabetically (or numerically). It is a prerequisite for `uniq` because `uniq` only detects consecutive duplicates — if identical lines are not adjacent, it will miss them.

**`uniq`:** Filters or reports duplicate adjacent lines. With the `-u` flag, it outputs only the lines that are unique (appear exactly once). Without `-u`, it simply removes consecutive duplicates but keeps one copy of each.

**Pipes (`|`):** The pipe operator sends the standard output of one command directly as the standard input of the next. This allows chaining commands together into a pipeline without needing intermediate files. Pipelines are fundamental to how Unix tools are designed to work.

**Why `sort` before `uniq`?** `uniq` only compares adjacent lines. If a value appears on lines 1, 5, and 100, `uniq` will not recognise them as duplicates unless they are sorted to be consecutive first.

---

## Solution

```bash
sort data.txt | uniq -u
```

Output:
```
McfCopsVMkSjH0RczhUpMNz3wj8lByZU
```

---

## Commands Breakdown

### `sort data.txt | uniq -u`

| Part | Meaning |
|---|---|
| `sort` | Sort all lines in the file alphabetically, making duplicates adjacent |
| `data.txt` | The input file |
| `\|` | Pipe — passes the sorted output as input to the next command |
| `uniq` | Filter adjacent duplicate lines |
| `-u` | Output only lines that are unique (appear exactly once) |

---

## Key Takeaways

- **The `sort | uniq` pipeline is a classic.** It appears constantly in log analysis, data normalisation, and security investigations. Common real-world uses: finding unique IP addresses in an access log, identifying unique user agents, or deduplicating event lists.

- **`uniq -c` is equally useful.** Adding `-c` counts the occurrences of each line: `sort data.txt | uniq -c | sort -rn` gives you a frequency-sorted list — extremely useful for identifying the most common events in a log file, which is a standard SOC technique for spotting anomalies.

- **Pipelines are the Unix philosophy in action.** Each tool does one thing well; you chain them together to solve complex problems without writing any custom code. Understanding how to build effective pipelines is a core skill for security automation and rapid triage.

---

## Password

```
McfCopsVMkSjH0RczhUpMNz3wj8lByZU
```
