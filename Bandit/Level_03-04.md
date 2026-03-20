### Level Info
- **Level:** Bandit Level 3  - Level 4
- **Category:**  File Read

### Goal
The password for the next level is stored in a hidden file in the **inhere** directory.

### Walkthrough
- Log into bandit3 using the obtained password  
- Enumerate the files using `ls`  
- It shows a directory named `inhere`  
- Navigate to the directory and list the files using `ls`  
- No files are visible in this directory  
- Use `ls -a`, where `-a` shows all files including hidden files  
- One of the file names is `...Hide-From_you`, open the file  
- Read the file contents to obtain the password for the next level

### What I Learned
- Understood how to read the hidden files in the linux.

### Security Insight
- Hidden does not mean safe, the attackers also able to read that file.
- Never rely on hiding files as a security measure; use proper file permissions instead.
