# CTF Writeups & Security Research

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Platform](https://img.shields.io/badge/platform-OverTheWire%20%7C%20HackTheBox%20%7C%20TryHackMe-blue)
![Language](https://img.shields.io/badge/language-English-lightgrey)

> A structured collection of writeups documenting my hands-on journey through CTF platforms, wargames, and cybersecurity challenges.  
> Each writeup goes beyond the solution — it explains the methodology, the tools, and the real-world relevance of each concept.

---

## About Me

I'm studying **ASIR** (Network and Computer Systems Administration) and focusing on a career in **cybersecurity**, specifically in Blue Team / SOC analysis.

These writeups serve as both a learning journal and a technical portfolio. Every challenge is approached with a structured methodology: reconnaissance → enumeration → exploitation → documentation. I write these as if I were writing an incident report — because that's the skill that actually matters on the job.

---

## Platforms

| Platform | Category | Status |
|---|---|---|
| [OverTheWire — Bandit](./overthewire/bandit/) | Linux fundamentals, file permissions, privilege escalation | Levels 0–10 ✅ |
| HackTheBox | Penetration testing, CTF | Coming soon |
| TryHackMe | Blue Team, SOC, Penetration testing | Coming soon |
| PortSwigger Web Academy | Web Application Security | Coming soon |

---

## Skills Demonstrated

- **Linux command line** — navigation, file permissions, process management, I/O redirection
- **Data manipulation** — grep, sort, uniq, strings, base64 encoding/decoding
- **Enumeration methodology** — finding files by attributes (owner, group, size, type)
- **Privilege escalation concepts** — SUID bits, credential files, user/group ownership
- **Structured technical writing** — documenting methodology in a reproducible format

---

## Repository Structure

```
ctf-writeups/
├── README.md                            ← This file
└── overthewire/
    └── bandit/
        ├── README.md                    ← Bandit index and overview
        ├── level-00-01.md
        ├── level-01-02.md
        └── ...
```

---

## Methodology

Every writeup follows the same structure:

1. **Metadata** — platform, difficulty, relevant tags
2. **Objective** — what the level asks you to do, in plain language
3. **Concepts Involved** — the technical concepts behind the challenge, explained
4. **Solution** — step-by-step with exact commands
5. **Commands Breakdown** — every flag and argument explained
6. **Key Takeaways** — what I learned and how it connects to real security work

---

## Disclaimer

All challenges documented here are performed on legal, authorized platforms specifically designed for security learning and skill development. No unauthorized systems were accessed.
