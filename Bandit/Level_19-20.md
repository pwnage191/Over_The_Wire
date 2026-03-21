### Level Info
- **Level:** Bandit Level 19 - Level 20.
- **Category:** Privilege Escalation / Setuid.

### Goal
To gain access to the next level, use the setuid binary in the home directory. Execute it without arguments to understand its usage. The
password can be found in `/etc/bandit_pass` after using the setuid binary.

### Walkthrough
- Observed a setuid binary in the home directory: ( ls -l )
  - `bandit20-do` 
  - <img width="600" height="105" alt="image" src="https://github.com/user-attachments/assets/a129fbe1-2175-473d-a1fa-acbc5b1d1186" />
- Understood that:
  - Setuid means the program runs with the permissions of the file owner, not the user who executes it.  
  - `./binary_file <command>` passes a command as an argument, which is executed with the owner’s privileges.  
- Tested the binary:
  - `./bandit20-do id`
  - <img width="600" height="76" alt="image" src="https://github.com/user-attachments/assets/acb6b21d-08e2-49d4-9e93-add63d040e79" />
  - The `id` command shows that while the real user remains bandit19, the effective user is bandit20, allowing access to restricted files.
  - When run a setuid binary, any command it executes runs with the effective user ID (euid) of the file owner.
- Explored directories:
  - `./bandit20-do ls`  
  - `./bandit20-do ls /etc/bandit_pass`.
  - <img width="700" height="213" alt="image" src="https://github.com/user-attachments/assets/9b7d0d0a-c556-4073-8280-b7706edd6c06" />
- Retrieved the password:
  - `./bandit20-do cat /etc/bandit_pass/bandit20` 

### What I Learned
- Setuid binaries allow temporary privilege escalation based on file ownership.  
- Commands passed as arguments can be executed with higher privileges.  

### Security Insight
- Misconfigured setuid binaries can lead to privilege escalation.  
- Allowing arbitrary command execution through setuid programs is a major security risk.  
