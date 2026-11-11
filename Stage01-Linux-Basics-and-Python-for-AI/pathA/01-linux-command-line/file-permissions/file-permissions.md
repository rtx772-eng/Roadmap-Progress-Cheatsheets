# File Permissions in Linux

## The Three Permission Types
```
r = read    = 4
w = write   = 2
x = execute = 1
```

## The Three User Groups
```
Owner   = the user who owns the file
Group   = a group of users
Others  = everyone else
```

## Reading Permission Output
```bash
ls -lah
-rw-r----- 1 bandit5 bandit4 33 Apr 3 15:17 -file07
```

Breaking it down:
```
- rw- r-- ---
│  │   │   │
│  │   │   └── Others:  no permission
│  │   └────── Group:   read only
│  └────────── Owner:   read + write
└───────────── file type (- = regular file, d = directory)
```

## Octal Notation
Each group gets a number:
```
rwx = 4+2+1 = 7   (all permissions)
rw- = 4+2+0 = 6   (read + write)
r-x = 4+0+1 = 5   (read + execute)
r-- = 4+0+0 = 4   (read only)
-wx = 0+2+1 = 3   (write + execute)
-w- = 0+2+0 = 2   (write only)
--x = 0+0+1 = 1   (execute only)
--- = 0+0+0 = 0   (no permission)
```

## chmod — Change Permissions
```bash
chmod [owner][group][others] filename

chmod 755 file   # rwxr-xr-x (owner all, group r+x, others r+x)
chmod 644 file   # rw-r--r-- (owner r+w, group r, others r)
chmod 400 file   # r-------- (owner read only, nobody else)
chmod 600 file   # rw------- (owner r+w, nobody else)
chmod 700 file   # rwx------ (owner all, nobody else)
```

## Common Permission Examples
```
755 = rwxr-xr-x  → typical for directories and executables
644 = rw-r--r--  → typical for regular files
400 = r--------  → private key files (SSH requirement)
600 = rw-------  → private files (SSH keys also acceptable)
```

## SSH Private Key Rules
```bash
chmod 400 sshkey.private   # ✅ correct
chmod 600 sshkey.private   # ✅ acceptable
chmod 640 sshkey.private   # ❌ SSH REFUSES (group can read)
chmod 644 sshkey.private   # ❌ SSH REFUSES (others can read)
```
SSH enforces strict permissions on private keys for security.
If too open → SSH prints WARNING and refuses to use the key.

## Principle of Least Privilege
> Give any user, system, or process ONLY the minimum access needed — nothing more.

Applied to files:
- Don't give execute if only read is needed
- Don't give write if only read is needed
- Don't give group access if only owner needs access

## Red Team Significance
File permissions are critical in:
- **Privilege escalation:** finding files with weak permissions
- **SUID files:** files that run as owner regardless of who runs them
- **SSH key exposure:** poorly protected keys = unauthorized access
- **Log files:** if writable by others = logs can be tampered with
