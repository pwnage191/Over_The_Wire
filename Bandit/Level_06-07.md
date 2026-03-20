### Level Info
- **Level:** Bandit Level 6 - Level 7
- **Category:** File Read

### Goal
The password for the next level is stored somewhere on the server and has all of the following properties:
- owned by user bandit7  
- owned by group bandit6  
- 33 bytes in size  

### Walkthrough
- Log into bandit 6 using the obtained password  
- Enumerate the files using `ls`, nothing is shown  
- Use the `find` command to filter by the given properties  
- `find / -type f -user bandit7 -group bandit6 -size 33c`  
- Permission denied occurs because `find /` searches the entire filesystem, including directories that your user does not have
  permission to access  
- Alternate: use `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`  
- The alternate works because `2>/dev/null` redirects error messages (permission denied) to `/dev/null`, hiding them while still
  allowing valid results to be displayed
- <img width="600" height="480" alt="image" src="https://github.com/user-attachments/assets/3850dbca-504e-42a9-8b17-563bd328cefe" />
- Read the content of the file using the `cat` command and obtain the password for the next level  

### What I Learned
- Learned how to use the `find` command effectively with multiple filters simultaneously, which is more efficient than manually
  checking files across nested directories  
- Learned about standard streams:
  - `0` -> standard input (stdin)  
  - `1` -> standard output (stdout)  
  - `2` -> standard error (stderr)  

### Security Insight
- Filtering files based on user, group, and size helps identify sensitive data efficiently in large directory structures
- Always enforce strict file permissions (e.g., chmod 600) to ensure that even discoverable files cannot be read by
  unauthorized users. 
