### Level
- Leviathan 02 -> Leviathan 03
- Category: Command Injection / Unquoted User Input

### Discovery Path
- Logged in as `leviathan2` using the password obtained from the previous level.
- Enumerated the home directory using `ls -la` and found a SUID binary named `printfile`.
- Executed the binary and observed the usage message:
- <img width="700"  alt="image" src="https://github.com/user-attachments/assets/5e382210-9836-475d-9c7a-0347b32613cf" />
- Created a test file in `/tmp/leviathan_test/test.txt` containing the text:
  ```text
  Hello all
  ```
- Verified that the binary could print the contents of the file:
  ```bash
  ~/printfile test.txt
  ```
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/88567cc0-93f2-484d-800f-63427cf76da7" />
- Observed that the program performs an `access()` check before executing a command through `system()`.
- Since `leviathan2` could not directly read `/etc/leviathan_pass/leviathan3`, I created a symbolic link to the password file and tested whether the
  SUID binary would follow the link.
- Created a symbolic link to the password file:
  ```bash
  ln -s /etc/leviathan_pass/leviathan3 lev_3
  ```
- Used `ltrace` to analyze the program and identify the library functions it uses.
- Attempted to read the password through the symbolic link:
  ```bash
  ~/printfile lev_3
  ```
- The attempt failed because `access()` follows the symbolic link and checks whether the current user (`leviathan2`) has permission to read the target file.
- Since `leviathan2` cannot read `/etc/leviathan_pass/leviathan3`, the access check failed.
- Created an empty file with a space in its name:
  ```bash
  touch "test.txt lev_3"
  ```
- Executed:
  ```bash
  ~/printfile "test.txt lev_3"
  ```
- The password was displayed because:
  - `access()` treated `"test.txt lev_3"` as a single filename and verified that `leviathan2` had permission to access that file.
  - The filename was later passed to `system()` without proper quoting.
  - The shell split the filename into two arguments:
    ```bash
    cat test.txt lev_3
    ```
  - The command executed with the privileges of `leviathan3` because the binary is SUID.
  - `cat` followed the symbolic link `lev_3` and read `/etc/leviathan_pass/leviathan3`.
  - <img width="700" alt="image" src="https://github.com/user-attachments/assets/66c00c3d-6814-40be-bf4b-2714e98f31b4" />

### Learning Drops
- `access()` checks permissions using the real user ID rather than the effective user ID.
- User input should never be passed directly to `system()` without proper quoting or sanitization.
- Symbolic links can be used to redirect file access during exploitation.
- Security checks can fail when validation and execution interpret the same input differently.
