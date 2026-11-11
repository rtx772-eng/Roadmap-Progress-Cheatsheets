# SSH — Secure Shell

## What is SSH?
SSH creates an **encrypted tunnel** between your machine and a remote server,
giving you a command line (shell) on that remote machine — as if you were sitting in front of it.

**SSH = Secure + Shell**
- Secure = everything is encrypted — nobody can intercept what you type
- Shell = you get a command line on the remote machine

---

## Two Ways to Authenticate

### 1. Password Authentication (basic)
```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
# Then type password when prompted
```
- Simple but less secure
- Password can be guessed or brute-forced

### 2. Key Authentication (professional)
```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
# No password needed — key file proves identity
```
- More secure — can't be guessed
- Only person with the key FILE can log in

---

## SSH Key Pair — How it Works

```
YOUR MACHINE          |          SERVER
------------------    |    ------------------
Private Key 🔑        |    Public Key 🔒
(keep secret)         |    (the lock)
                      |
Your private key + server's public key = MATCH = ACCESS ✅
```

**Analogy:** Private key = physical key. Public key = the lock on the door.
If your key fits the lock — you're in. No password needed.

---

## SSH Flags
```bash
ssh user@host           # basic connection
ssh user@host -p 2220   # specify port (lowercase -p)
ssh -i keyfile user@host -p 2220  # use private key file (-i = identity)
```

---

## Private Key Security Rules
```bash
chmod 400 sshkey.private  # ✅ correct — read only, owner only
chmod 600 sshkey.private  # ✅ acceptable — read+write, owner only
chmod 640 sshkey.private  # ❌ too open — group can read — SSH REFUSES
chmod 644 sshkey.private  # ❌ too open — others can read — SSH REFUSES
```

**Why SSH enforces this:**
If your private key is readable by others — it's not private anymore.
SSH protects you by refusing to use an insecure key.

---

## Red Team Significance
> Finding a private key file on a compromised system = master key access
> No password needed — just copy the file and SSH in as that user
> This is why private keys must NEVER be left exposed on a system

---

## Example — Full Connection Flow
```bash
# 1. Copy key from remote server to local machine
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

# 2. Fix permissions
chmod 400 sshkey.private

# 3. Connect using the key
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

# 4. You're in — no password needed ✅
```
