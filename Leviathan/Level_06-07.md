### Level
- Leviathan 06 -> Leviathan 07
- Category: Brute Force Attack

### Discovery path
- I started by exploring the file system and found a binary file (`leviathan6`) with the SetUID permission.
- I ran the binary program, and it prompted me to enter a 4-digit code.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/04586f90-e096-4133-94df-7db7425d426f" />
- I used `ltrace` to analyze the program and observed that it called `atoi()` to convert the input string into an integer.
- Since the code was only four digits (0000–9999), I wrote a simple brute-force script to test every possible value.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/3e5dbd95-2638-45d6-be0c-0e4a2fad939c" />
- After finding the correct code, the program spawned a shell running as `leviathan7`.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/b33177ed-e04e-4fa7-a05f-784df9ae8b2e" />
- I verified the current user using `whoami` and then read the password from `/etc/leviathan_pass/leviathan7`.

### Learning Drops
- `atoi()` converts a string into an integer.
- `ltrace` can be used to identify which library functions are called by a binary program.
- A SetUID binary runs with the effective UID of the file owner. After the correct code is entered, the program spawns
   a shell with the privileges of `leviathan7`.
