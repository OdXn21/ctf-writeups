# OverTheWire — Bandit

> Bandit is a wargame designed for absolute beginners. It teaches the fundamentals of Linux, the command line, file permissions, and basic security concepts through a series of increasingly complex challenges.  
> Each level gives you SSH credentials to connect to a remote server, find a password, and use it to advance to the next level.

**Host:** `bandit.labs.overthewire.org` | **Port:** `2220`

---

## Progress

| Level | Main Concept | Writeup |
|---|---|---|
| 0 → 1 | SSH connection, basic file reading | [level-00-01.md](./level-00-01.md) |
| 1 → 2 | Reading files with special names (`-`) | [level-01-02.md](./level-01-02.md) |
| 2 → 3 | Files with spaces in the name | [level-02-03.md](./level-02-03.md) |
| 3 → 4 | Hidden files, directory navigation | [level-03-04.md](./level-03-04.md) |
| 4 → 5 | Identifying human-readable files | [level-04-05.md](./level-04-05.md) |
| 5 → 6 | `find` by size and executable bit | [level-05-06.md](./level-05-06.md) |
| 6 → 7 | `find` by user, group and size across the filesystem | [level-06-07.md](./level-06-07.md) |
| 7 → 8 | `grep` to search inside large files | [level-07-08.md](./level-07-08.md) |
| 8 → 9 | Finding unique lines with `sort` and `uniq` | [level-08-09.md](./level-08-09.md) |
| 9 → 10 | Extracting strings from binary files | [level-09-10.md](./level-09-10.md) |
| 10 → 11 | Base64 decoding | [level-10-11.md](./level-10-11.md) |

---

## Connecting to Each Level

```bash
ssh bandit<LEVEL>@bandit.labs.overthewire.org -p 2220
```

Replace `<LEVEL>` with the level number (e.g., `bandit0`, `bandit1`, etc.).

---

## Notes

- Passwords change periodically on the OverTheWire servers. The passwords in these writeups may not be current — the methodology is what matters.
- Each level builds on skills from previous ones. If you're stuck, the answer is usually a `man` page away.
