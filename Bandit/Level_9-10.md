### Level Info
- **Level:** Bandit Level 9 - Level 10
- **Category:** Search word

### Goal
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several '=' characters.

### Walkthrough
- Log into bandit9 using the obtained password  
- Enumerate the files using `ls -l`, which shows `data.txt`  
- Use `strings data.txt | grep "="` to extract the password  
- `strings data.txt` extracts human-readable text from the file (since it contains mostly binary data)  
- `grep "="` filters lines containing '=' as indicated in the clue  
- This reveals the password  

### What I Learned
- Learned how to extract readable content from binary files using `strings`  
- Understood how to combine `strings` with `grep` to filter specific patterns  

### Security Insight
- Storing sensitive data in readable form within binary files is insecure  
- Attackers can extract hidden information using simple tools like `strings`  
- Sensitive data should be encrypted at rest  
