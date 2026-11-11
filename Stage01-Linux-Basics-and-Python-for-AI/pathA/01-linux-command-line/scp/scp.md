# SCP — Secure Copy

## What is SCP?
SCP = **Secure Copy** — like `cp` but between two different machines over SSH.

**Analogy:** `cp` moves files inside your house. `scp` moves files between houses — securely.

---

## Basic Structure
```bash
scp [flags] [source] [destination]
```

---

## Remote File Format
When the source or destination is on a remote machine, use this format:
```
user@host:filepath
```
The `:` separates the machine from the file path.

**Examples:**
```
bandit13@bandit.labs.overthewire.org:sshkey.private   ← remote file
bandit13@bandit.labs.overthewire.org:/home/bandit13/  ← remote directory
```

---

## Common Usage

### Copy FROM remote server TO your local machine
```bash
scp -P 2220 user@host:remotefile .
# . means current local directory
```

### Copy FROM your local machine TO remote server
```bash
scp -P 2220 localfile user@host:/remote/path/
```

### Copy entire folder
```bash
scp -r -P 2220 user@host:remotefolder/ .
# -r = recursive (copy everything inside)
```

---

## Important: Port Flag Difference
```bash
ssh  → lowercase -p 2220   (small p)
scp  → UPPERCASE -P 2220   (capital P)
```
This trips everyone up. Capital P for SCP — always.

---

## Example from Bandit Level 13
```bash
# Copy private key from Bandit server to Kali machine
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

# What each part means:
# scp           = secure copy command
# -P 2220       = use port 2220
# bandit13@...  = connect as bandit13 to this server
# :sshkey.private = copy this specific file
# .             = save it here in current directory
```

---

## Red Team Use Cases
- Exfiltrate files from a compromised server
- Transfer tools to a target machine
- Copy SSH keys found during reconnaissance
