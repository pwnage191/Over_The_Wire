### Level
- Leviathan 01 -> Leviathan 02
- Category: SUID Binary Analysis / Library Function Tracing

### Discovery Path
- Logged in as `leviathan1` using the password obtained from the previous level.
- Started by enumerating the home directory and checking for hidden files and unusual permissions.
- Used `ls -la` and discovered a file named `check`.
- Noticed that `check` had the SUID permission bit set, indicating it would run with the privileges of its owner.
- Executed the binary using `./check`.
- The program prompted for a password.
- Entered a random password and received the message:
  ```
  Wrong password, Good Bye ...
  ``` 
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/3e6848cf-9237-48e1-87ff-5d51da305d96" />
- Considered using `grep` and `strings`, but suspected the password validation might occur dynamically.
- Decided to analyze the program's behavior using `ltrace`.
- Observed that the program used the `strcmp()` library function to compare the supplied password against a hardcoded value.
- The password was revealed in the `ltrace` output.
- Entered the correct password and gained access as `leviathan2`.
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/0eaa909d-732e-43c2-bdd6-f7826d5a2feb" />
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/2bb109ea-4c8d-4025-9cdd-1221da5aadab" />
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/83395c40-7905-4d2c-a5d3-b9dc2d27c96a" />
- Read the next level's password from:
  ```bash
  cat /etc/leviathan_pass/leviathan2
  ```
- <img width="700" alt="image" src="https://github.com/user-attachments/assets/0358ebce-7a89-4f46-b060-3360e07e1db3" />

### Learning Drops
- SUID binaries execute with the permissions of the file owner rather than the current user.
- `ltrace` traces library function calls and can reveal sensitive information such as hardcoded credentials.
- `strcmp()` is commonly used to compare two strings and is frequently encountered during binary analysis.
- Dynamic analysis can reveal information that may not be visible through static methods such as `strings`.
