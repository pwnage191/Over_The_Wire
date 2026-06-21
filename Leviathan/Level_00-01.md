### Level
- Level 00 to 01
- Category: Hidden files

### Discovery Path
- Connected to the target using:
  ```bash
  ssh leviathan0@leviathan.labs.overthewire.org
  ```
- Logged in with the provided credentials for Level 0.
- Began by enumerating the file system and checking the contents of the home directory.
- Used `ls -la` to identify hidden files.
- <img width="700"  alt="image" src="https://github.com/user-attachments/assets/ee887709-d843-4a36-80a8-db8b6c4206c7" />
- Inspected the discovered files for useful information.
- Used `grep -i "password" <filename>` to perform a case-insensitive search for password-related strings.
- Found the password for the next level and used it to progress to Level 1.
- <img width="700"  alt="image" src="https://github.com/user-attachments/assets/a9078fd3-d231-4cd6-a91f-2792cd2b887e" />

### Learning Drops
- Hidden files can contain sensitive information and should always be checked during enumeration.
- `ls -la` is essential for discovering hidden files and viewing file permissions.
