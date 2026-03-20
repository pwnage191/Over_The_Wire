### Level Info
- **Level:** Bandit Level 4 - Level 5
- **Category:** File Read

### Goal
The password for the next level is stored in the only human-readable file in the **inhere** directory.

### Walkthrough
- Log into bandit4 using the obtained password  
- Enumerate the files using `ls`  
- It shows a directory named `inhere`  
- Navigate to the directory and list the files using `ls`  
- It shows 10 files starting with `-file0` and so on  
- To identify the human-readable file, determine the file type  
- Use `file ./*` (`./*` refers to all files in the current directory)  
- One of the files shows `ASCII text`, read the content of that file to obtain the password
- <img width="775" height="411" alt="image" src="https://github.com/user-attachments/assets/ce4ffd99-1cad-43e4-917e-7f997cadb409" />

### What I Learned
- Understood how to identify file types and find human-readable files  

### Security Insight
- Identifying file types before opening them helps avoid interacting with unexpected or binary files  
