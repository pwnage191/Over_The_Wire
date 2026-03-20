### Level Info
- **Level:** Bandit Level 1  - Level 2
- **Category:**  File Read

### Goal
The password for the next level is stored in a file called - located in the home directory

### Walkthrough
- Log into bandit1 using the obtained password  
- Enumerate the files using `ls`  
- A file named `-` is displayed  
- If the filename starts with `-`, using `cat -` treats it as standard input instead of a filename  
- To treat it as a file:  
- Use `cat ./-` to specify the current directory  
- Use `cat -- -` so that `-` is treated as a filename, not an option  
- Read the file contents to obtain the password for the next level

### What I Learned
- Understood how to read the file contents that starts with '-'
- Learned how special characters in filenames can cause unexpected shell behaviour

### Security Insight
- A filename is just text, and text can be weaponized  
- A file named `; rm -rf /` passed to a shell command, won't just read a file, it'll wipe your server
- This type of vulnerability is called command injection  
- Never trust user input  
- Always sanitize filenames before passing them to any command
