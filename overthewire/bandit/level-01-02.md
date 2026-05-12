# Bandit Level 1 → Level 2

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 1 → 2 |
| Difficulty | Easy |
| Tags | `cat`, `special-filenames`, `dash-files`, `path-notation` |

---

## Objective

The password for level 2 is stored in a file called `-` in the home directory. Read it.

---

## Concepts Involved

**Files with special names:** Linux filenames can contain almost any character, including characters that have special meaning in the shell (like `-`, `*`, `~`, or spaces). When a filename conflicts with shell syntax, you need to use specific techniques to reference it unambiguously.

**The dash (`-`) as a special argument:** In most Unix tools, `-` is a convention that means "read from standard input" rather than from a file. If you run `cat -`, the shell interprets it as "read from stdin" and waits for keyboard input — it does not read the file named `-`.

**Path notation (`./`):** Prefixing a filename with `./` explicitly tells the shell: "this is a file in the current directory." It bypasses the special meaning of `-` because the argument is now clearly a path, not a flag or stdin indicator.

---

## Solution

```bash
ls
```

Output:
```
-
```

```bash
cat ./-
```

---

## Commands Breakdown

### `cat ./-`

| Part | Meaning |
|---|---|
| `cat` | Read and print the contents of a file |
| `./` | Explicitly refers to the current directory — turns `-` into a path |
| `-` | The filename |

Without `./`, the shell would interpret `-` as "read from standard input" and the command would hang waiting for keyboard input.

---

## Key Takeaways

- **Never assume filenames are clean.** In real-world incident response and forensics, attackers sometimes name files or directories with special characters specifically to make them harder to interact with and easier to hide. Knowing how to handle unusual filenames is a practical skill.

- **`./` is your escape hatch for ambiguous filenames.** Any time a filename starts with `-` or another character that might confuse the shell, prefix it with `./` to treat it as an explicit path.

- **Understanding stdin vs file arguments matters.** Many Unix tools accept `-` as a synonym for stdin. This is useful in pipelines but can trip you up when a file happens to share that name. Being aware of this dual behavior is important when writing scripts or automating tasks in a security context.

---

## Password

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```
