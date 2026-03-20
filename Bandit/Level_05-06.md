### Level Info
- **Level:** Bandit Level 5  - Level 6
- **Category:**  File Read

### Goal
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

### Walkthrough
- Log into bandit5 using the obtained password  
- Enumerate the files using `ls`  
- It shows a directory named `inhere`  
- Navigate to the directory and list the files using `ls`  
- It showed 20 folders, like  `maybehere00` and so on.
- Use the `find` command to filter by the given properties.
- ` find . -type f -size 1033c ! -executable` , It displays the path of the matching file
- `f` refers to the file, `1033c refers to 1033 bytes`
- Read the content of the file by using cat command and obtained the password for the next level.
- 
### What I Learned
- Learned how to use the `find` command with multiple filters simultaneously, this is more efficient than manually checking files
- across nested directories.

### Security Insight
- Filtering files based on size, type, and permissions helps identify sensitive data efficiently in large directory structures
