# File Compression & Decompression

## What is Compression?
Compression = making a file smaller by encoding its data more efficiently.
Decompression = reversing that — restoring the original file.

**Analogy:** Compression is like vacuum-packing clothes — same content, less space.

---

## The Golden Rule of Decompression
```
1. file [filename]      → identify the compression type
2. mv file file.ext     → rename with correct extension
3. decompress           → run the right tool
4. repeat               → until you reach the original file
```

> **"The filename means nothing. The `file` command tells the truth."**

---

## Compression Tools

### gzip — Most Common
```bash
gzip file           # compress → creates file.gz
gzip -d file.gz     # decompress
```
Extension: `.gz`
`-d` = decompress (same logic as `base64 -d`)

### bzip2 — Better Compression
```bash
bzip2 file          # compress → creates file.bz2
bzip2 -d file.bz2   # decompress
```
Extension: `.bz2`

### tar — Archive (bundles multiple files)
```bash
tar -xf file.tar          # extract archive
tar -czf out.tar.gz dir/  # create compressed archive
```
Extension: `.tar`, `.tar.gz`, `.tgz`
`x` = extract, `f` = from this file
**Important:** tar REQUIRES the `-f` flag — without it, refuses to read

---

## Identifying File Types
```bash
file filename
```

Common outputs:
```
gzip compressed data      → rename to .gz  → gzip -d
bzip2 compressed data     → rename to .bz2 → bzip2 -d
POSIX tar archive         → rename to .tar → tar -xf
ASCII text                → cat it → done ✅
```

---

## Why Rename Before Decompressing?
```bash
gzip -d file      # ❌ gzip doesn't recognize it
gzip -d file.gz   # ✅ gzip knows what to do
```
Each tool recognizes files by their extension.
Without the correct extension → tool refuses or fails.

---

## The `-d` Flag Pattern
Almost every decompression tool uses `-d`:
```
gzip -d    = decompress gzip
bzip2 -d   = decompress bzip2
base64 -d  = decode base64
xxd -r     = reverse hexdump (uses -r not -d but same idea)
```

---

## Hexdump Conversion (Level 12 Special)
```bash
# A hexdump = binary data displayed as hex numbers
# xxd -r converts it back to real binary

xxd -r data.txt > file.bin
# Then start the decompression cycle on file.bin
```

---

## Level 12 Full Example
```bash
# Setup workspace
mktemp -d                    # create temp dir → /tmp/tmp.ABC123
cd /tmp/tmp.ABC123
cp /home/bandit12/data.txt .

# Step 1: Convert hexdump to binary
xxd -r data.txt > file.bin

# Step 2-9: Decompression cycle (repeated)
file file.bin                # → gzip
mv file.bin file.gz
gzip -d file.gz              # → produces: file

file file                    # → bzip2
mv file file.bz2
bzip2 -d file.bz2            # → produces: file

file file                    # → gzip again
mv file file.gz
gzip -d file.gz              # → produces: file

file file                    # → tar
mv file file.tar
tar -xf file.tar             # → produces: data5.bin

# ...continue cycle until...
file finalfile               # → ASCII text ✅
cat finalfile                # → PASSWORD
```
