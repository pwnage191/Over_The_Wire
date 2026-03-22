### Level Info
- **Level:** Bandit Level 26 - Level 27.
- **Category:** Privilege Escalation / SUID / Command Execution.

### Goal
Good job getting a shell. Now hurry and grab the password for bandit27.

### Walkthrough
- Log in to bandit26 using the password.
- We already know that bandit26 uses `/usr/bin/showtext`.
- Minimize the terminal window and press `v` to open the interactive text editor (vim).
- Inside vim, set the shell: `:set shell=/bin/bash`
- Then execute: `:shell`
- This spawns a bash shell as bandit26.
- Check available files: `ls -l`
- <img width="700" height="144" alt="image" src="https://github.com/user-attachments/assets/4bc17679-9677-4549-8312-5f5911b4c3b2" />
- Found:  `bandit27-do`  , `text.txt`
- Observed:
	  - `bandit27-do` has SUID permission.
	  - The file owner is bandit27.
	  - It is a binary file.
- Execute command to read password: `./bandit27-do cat /etc/bandit_pass/bandit27`
- This returns the password for bandit27.

### What I Learned
- SUID binaries run with the permissions of the file owner.  
- Programs can be designed to execute commands as another user.  
- Identifying SUID files is important for privilege escalation.  

### Security Insight
- Misconfigured SUID binaries can allow users to execute commands with higher privileges.  
- Allowing arbitrary command execution in privileged binaries is a security flaw.  
