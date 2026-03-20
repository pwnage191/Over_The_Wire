### Level Info
- **Level:** Bandit Level 2  - Level 3
- **Category:**  File Read

### Goal
The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory

### Walkthrough
- Log into bandit2 using the obtained password  
- Enumerate the files using `ls`  
- A file named `cat --spaces in this filename--` is displayed  
- If the filename starts with `--` & contains spaces, when i tested with `cat --spaces in this filename` treats it as standard
  input and showed `cat: unrecognized option '--spaces'`
- To treat it as a file:  
- Use `cat ./` to specify the current directory  
- Use `"` , so that spaces are also treated as a filename, instead of broken.
- `cat ./"--spaces in this filename--"`
- `cat ./--spaces\ in\ this\ filename--` ( use backslash as escape character to skip spaces )
- Read the file contents to obtain the password for the next level

### What I Learned
- Understood how to read the file contents that starts with '--' and has spaces.
- Spaces are separators in linux command, it allows the users to give multiple arguments.
- It leads to control the command parser behavior

### Security Insight
- Spaces are separators in the shell, a filename with spaces looks like multiple arguments. Attackers can exploit this to
  manipulate how commands are parsed. Always quote or escape filenames when passing them to shell commands.
