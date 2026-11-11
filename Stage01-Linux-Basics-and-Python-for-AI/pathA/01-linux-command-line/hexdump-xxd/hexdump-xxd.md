# Hexdump & xxd

## What is a Hexdump?
A hexdump = all the raw data of a file displayed as **hexadecimal numbers** instead of readable text.

**Why hex?**
Computers store everything as binary (0s and 1s).
Hexadecimal (base 16) is a compact way to represent binary data.
1 hex digit = 4 bits. 2 hex digits = 1 byte.

**Analogy:**
Normal text file → open it → see: `Hello`
Hexdump of same file → open it → see:
```
48 65 6c 6c 6f
```
Same data — just displayed differently.
`H` = 0x48, `e` = 0x65, `l` = 0x6c, `l` = 0x6c, `o` = 0x6f

---

## What a Hexdump Looks Like
```
00000000: 1f8b 0808 dfcd eb66 0203 6461 7461 322e  .......f..data2.
00000010: 6269 6e00 013e 02c1 fd42 5a68 3931 4159  bin..>...BZh91AY
```
- Left column: memory address (position in file)
- Middle: hex values (the actual data)
- Right: ASCII representation (dots = non-printable characters)

---

## xxd — The Hexdump Tool

```bash
xxd filename          # create hexdump of file
xxd -r hexfile > bin  # REVERSE hexdump back to binary
```

`-r` = reverse (convert hex back to binary)

**Example:**
```bash
# Convert hexdump data.txt back to binary file.bin
xxd -r data.txt > file.bin

# Then check what type it is
file file.bin
```

---

## Why Hexdumps Are Used
1. **Storing binary data as text** — binary files can't be stored in plain text files
2. **Forensics** — examining raw file data
3. **CTFs** — hiding data in encoded form
4. **Debugging** — seeing exact bytes in a file

---

## Red Team Significance
- Identifying file types from raw bytes (magic bytes)
- Analyzing malware at binary level
- Bypassing file extension filters (rename .exe to .txt — `file` still reveals the truth)
- Forensic analysis of captured data
