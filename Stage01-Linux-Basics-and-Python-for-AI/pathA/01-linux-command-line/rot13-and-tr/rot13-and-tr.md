# ROT13 & the `tr` Command

## What is `tr`?
`tr` = **translate** — replaces characters from one set with another set.

**Structure:**
```bash
tr 'list1' 'list2'
```
Every character from list1 gets replaced by the character in the same position in list2.

**Simple example:**
```bash
echo "cat" | tr 'cat' 'dog'
# c→d, a→o, t→g
# Output: dog
```

---

## What is ROT13?
ROT13 = **Rotate by 13** — each letter is shifted 13 positions in the alphabet.

```
A → N    (A is position 1, +13 = position 14 = N)
B → O
C → P
...
N → A    (wraps back around)
```

**Why 13 is special:**
The alphabet has 26 letters. 13 = exactly half.
So ROT13 is **self-reversing** — encode and decode use the same command.

```
A → N → A  (shift 13, then shift 13 again = back to start)
```

---

## ROT13 with `tr`

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Breaking it down:
```
First list:  A-Za-z          = full alphabet (A to Z, then a to z)
Second list: N-ZA-Mn-za-m    = alphabet cut in half and swapped
```

Why `N-ZA-M` and not just `N-Z`:
```
N-Z  = letters N through Z = 13 letters (only half)
A-Z  = letters A through Z = 26 letters (full alphabet)

Need A-M after N-Z to complete the mapping:
N-Z  covers positions 1-13  (A through M become N through Z)
A-M  covers positions 14-26 (N through Z become A through M)
```

Visual:
```
Original:  A B C D E F G H I J K L M | N O P Q R S T U V W X Y Z
Rotated:   N O P Q R S T U V W X Y Z | A B C D E F G H I J K L M
```

---

## Important: `tr` Doesn't Know ROT13
`tr` is just a character replacement tool.
ROT13 is just ONE way to use `tr`.
The intelligence is in the mapping you provide — not in `tr` itself.

---

## Other `tr` Uses
```bash
# Convert uppercase to lowercase
echo "HELLO" | tr 'A-Z' 'a-z'

# Remove specific characters
echo "hello world" | tr -d 'l'
# Output: heo word

# Squeeze repeated characters
echo "heeello" | tr -s 'e'
# Output: hello
```

---

## Red Team Significance
ROT13 is a classic **encoding** technique (not encryption):
- No key required — anyone who knows the pattern can decode it
- Used to obfuscate data, not secure it
- Common in CTFs as a first layer of encoding
- Real attackers use it to obscure malicious strings in scripts
