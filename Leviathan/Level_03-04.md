### Level
- Leviathan 03 -> Leviathan 04
- Category: SetUID Password Recovery

### Discovery path
- I started exploring the file system and found a binary file with the **SetUID** permission.
- I ran the binary program, and it prompted me to enter a password.
- I entered a random password, and it displayed **"Wrong password."** Next, I checked which library functions were used by the binary program.
- It used `strcmp()` to compare the password. In C, `strcmp()` compares two strings lexicographically.
- I used the discovered password to run the binary program.
- I checked the current username, and it displayed `leviathan4`.
- Then, I read the password from `/etc/leviathan_pass/leviathan4`.

### Learning Drops
- `ltrace` is a tool used to identify which library functions are called by a binary program.
- `strcmp()` is used to compare two strings (such as a password) lexicographically.
- The binary has the SetUID permission. When it is executed, the process runs with the **effective UID of the file owner (`leviathan4`)**, allowing it to 
  access resources that `leviathan3` normally cannot.
