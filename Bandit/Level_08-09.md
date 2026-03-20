### Level Info
- **Level:** Bandit Level 8 - Level 9
- **Category:** Search word

### Goal
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs exactly once.

### Walkthrough
- Log into bandit8 using the obtained password  
- Enumerate the files using `ls -l`, which shows `data.txt`  
- Use `sort data.txt | uniq -u` to identify the unique line  
- The `sort` command arranges lines so duplicates become adjacent  
- Sorting is necessary because `uniq` only compares adjacent lines, so unsorted duplicates would be missed  
- The `uniq -u` command displays only lines that appear exactly once  
- This reveals the password  

### What I Learned
- Learned how to combine `sort` and `uniq` to identify unique lines  
- Understood that `uniq` requires sorted input to work correctly  

### Security Insight
- Storing sensitive data in plain text is insecure  
- Sensitive data should be encrypted at rest  
