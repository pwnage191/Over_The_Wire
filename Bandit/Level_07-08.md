### Level Info
- **Level:** Bandit Level 7 - Level 8
- **Category:** Search Word

### Goal
The password for the next level is stored in the file **data.txt** next to the word **millionth**

### Walkthrough
- Log into bandit7 using the obtained password  
- Enumerate the files using `ls -l`, it shows `data.txt` and the file size is large  
- Use `grep millionth data.txt` to search for the word  
- It displays the matching line, which contains the password  

### What I Learned
- Learned how to search for a specific word inside a file using `grep`  

### Security Insight
- Searching large files efficiently helps identify sensitive information quickly without manually reviewing the entire content  
