### Level
- Leviathan 05 -> Leviathan 06
- Category: Symlink (Symbolic Link) Exploitation

### Discovery path
- I started by exploring the file system and found a binary file (`leviathan5`) with the **SetUID** permission.
- I ran the binary program, and it displayed the message: `Cannot find /tmp/file.log`.
- I used `ltrace` to identify which library functions were called by the binary.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/69bfc7e3-6a8a-475b-bd2f-68d7bac0ee85" />
- I observed that the program attempted to open `/tmp/file.log` using `fopen()`, but the file did not exist.
- I verified that `/tmp/file.log` was missing.
- I created a symbolic link named `/tmp/file.log` pointing to `/etc/leviathan_pass/leviathan6`.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/319e1c72-1fd9-4bfb-bcc4-b5641d5380e1" />
- Since the binary has the **SetUID** permission, it runs with the effective UID of `leviathan6`.
- Therefore, when `fopen()` opens `/tmp/file.log`, it follows the symbolic link and successfully reads `/etc/leviathan_pass/leviathan6`.
- The program printed the password for the next level.

### Learning Drops
- `ltrace` can be used to identify which library functions are called by a binary program.
- `fopen()` is a C library function used to open a file. Internally, it calls the `open()` system call.
- A symbolic link (symlink) acts as a pointer to another file. When a program opens the symlink, the kernel follows it and opens the target file instead.
- In a SetUID program, file operations such as `open()` are performed using the **effective UID (EUID)**, not the real UID (RUID).
