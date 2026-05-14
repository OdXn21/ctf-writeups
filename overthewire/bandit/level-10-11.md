# Bandit Level 10 → Level 11

## Metadata

| Field | Value |
|---|---|
| Platform | OverTheWire — Bandit |
| Level | 10 → 11 |
| Difficulty | Easy |
| Tags | `base64`, `encoding`, `decoding`, `data-encoding` |

---

## Objective

The password is stored in `data.txt`, which contains data encoded in Base64. Decode it to retrieve the password.

---

## Concepts Involved

**Base64 encoding:** A binary-to-text encoding scheme that represents binary data using 64 printable ASCII characters (A–Z, a–z, 0–9, `+`, `/`). It is not encryption — it provides no confidentiality whatsoever. Its purpose is to safely transmit binary data over channels that only support text (such as email, JSON payloads, or HTTP headers).

**Why Base64 matters in security:** Attackers frequently use Base64 to obfuscate payloads in phishing emails, malicious scripts, and command-and-control traffic. A PowerShell command encoded in Base64, an email attachment, a suspicious cookie value — recognising and decoding Base64 on sight is a fundamental skill for a SOC analyst or malware investigator.

**`base64 -d`:** The `-d` (or `--decode`) flag tells the `base64` utility to decode rather than encode. Without any flag, `base64` encodes its input.

---

## Solution

```bash
base64 -d data.txt
```

Output:
```
The password is dtR173fZKb0RRsDFSgsg2RWnpNVj3qRr
```

---

## Commands Breakdown

### `base64 -d data.txt`

| Part | Meaning |
|---|---|
| `base64` | Encode or decode data using Base64 |
| `-d` | Decode mode — interpret the input as Base64 and output the original data |
| `data.txt` | The file containing the Base64-encoded data |

---

## Key Takeaways

- **Base64 ≠ encryption.** This is one of the most important distinctions in security. Base64-encoded data is trivially reversible by anyone. A common mistake — especially among non-technical stakeholders — is to confuse encoding with encryption. Encoding transforms the format; encryption protects the content. Always clarify this distinction.

- **SOC analysts decode Base64 constantly.** Malicious PowerShell commands are routinely Base64-encoded to bypass simple keyword filters: `powershell.exe -EncodedCommand <base64string>`. Email phishing payloads, obfuscated JavaScript, and suspicious API calls often contain Base64 segments. Being able to decode them quickly — in a terminal, in CyberChef, or in a SIEM — is a core analyst skill.

- **CyberChef is the GUI equivalent for investigations.** For complex real-world cases involving chained encodings (Base64 → XOR → gzip → Base64 again), the web tool CyberChef provides a visual pipeline for decoding. But understanding the underlying `base64` command is the foundation.

- **Recognising Base64 by eye:** Base64 strings typically end with one or two `=` padding characters and consist only of alphanumeric characters plus `+` and `/`. Seeing this pattern in a log or network capture is an immediate signal to decode and inspect.

---

## Password

```
dtR173fZKb0RRsDFSgsg2RWnpNVj3qRr
```
