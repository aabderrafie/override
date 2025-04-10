
# Level00 Challenge Solution

## Overview
The goal of the Level00 challenge is to authenticate by providing the correct password. After decompiling the binary, we saw that the program compares our input to a specific value and runs a shell upon successful authentication. 

## Steps to Solve

1. **SSH into the Server**:
   First, SSH into the provided server:
   ```bash
   ssh level00@10.11.247.251 -p 4242
   ```
   Use the password `level00` to log in.

2. **Run the Program**:
   Once logged in, run the following command to execute the program:
   ```bash
   ./level00
   ```
   The program prompts for a password:
   ```
   ***********************************
   * 	     -Level00 -		  *
   ***********************************
   Password:
   ```

3. **Decompiling the Program**:
   After decompiling the binary, we observed the following critical code:
   ```asm
   cmp eax, 0x149   ; eax contains the result of scanf(%d)
   jne 0x0804850d   ; jumps to an error if input is not 5276 (0x149)
   ```
   This indicates that the program compares the input (which is read as an integer) with `0x149`, the hexadecimal representation of `5276`. If the input is correct, it will proceed to run the command `system("/bin/sh")` and authenticate the user.

4. **Enter the Correct Password**:
   We identified that the correct password is `5276` (decimal), which is `0x149` in hexadecimal. When prompted for the password, input `5276`:
   ```
   Password: 5276
   ```
   Upon successful authentication, the program will output:
   ```
   Authenticated!
   ```

5. **Accessing the Next Level**:
   After authentication, we gained access to the shell. We then checked the `.pass` file for the next level's password:
   ```bash
   cat /home/users/level01/.pass
   ```
   The password for the next level is:
   ```
   uSq2ehEGT6c9S24zbshexZQBXUGrncxn5sD5QfGL
   ```

---
