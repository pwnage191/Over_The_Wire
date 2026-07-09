### Level
- Leviathan 03 -> Leviathan 04
- Category: SetUID Password Recovery

### Discovery path
- I started exploring the file system and found a binary file with the **SetUID** permission.
- I ran the binary program, and it prompted me to enter a password.
- I entered a random password, and it displayed "Wrong password". Next, I checked which library functions were used by the binary program.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/4aa9cc3b-f0b3-4453-ad28-b88e64eac6f0" />
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/8d1c336b-794e-462e-9813-a0c250a9855f" />
- It used `strcmp()` to compare the password. In C, `strcmp()` compares two strings lexicographically.
- I used the discovered password to run the binary program.
- I checked the current username, and it displayed `leviathan4`.
- Then, I read the password from `/etc/leviathan_pass/leviathan4`.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/0422fc0c-67f9-46c4-9012-ed2c7242c063" />

### Learning Drops
- `ltrace` is a tool used to identify which library functions are called by a binary program.
- `strcmp()` is used to compare two strings (such as a password) lexicographically.
- The binary has the SetUID permission. When it is executed, the process runs with the effective UID of the file owner (`leviathan4`), allowing it to 
  access resources that `leviathan3` normally cannot.
