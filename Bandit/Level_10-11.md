### Level Info
- **Level:** Bandit Level 10 - Level 11
- **Category:** Encoding

### Goal
The password for the next level is stored in the file **data.txt**, which contains Base64 encoded data.

### Walkthrough
- Log into bandit10 using the obtained password  
- Enumerate the files using `ls -l`, which shows `data.txt`  
- View the file using `cat data.txt` (output appears as Base64-encoded text ending with `=`)  
- Use `base64 -d data.txt` to decode the content  
- The decoded output reveals the password  

### What I Learned
- Learned how to identify Base64-encoded data (commonly ends with `=` or `==`)   
- Learned the difference between encoding and encryption:  
  - Encoding is reversible and used for data formatting or transmission  
  - Encryption is used for security and requires a key to decode  

### Security Insight
- Encoded data can be easily decoded by unauthorized users  
- Sensitive information should be encrypted, not just encoded  
