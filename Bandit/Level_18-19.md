### Level Info
- **Level:** Bandit Level 18 - Level 19.
- **Category:** SSH / Shell Behavior / Misconfiguration.

### Goal
The password for the next level is stored in a file `readme` in the home directory. However, `.bashrc` has been modified to log you 
out immediately when you log in via SSH.

### Walkthrough
- Tried to log in normally using SSH, but the session closed immediately.  
- Identified that `.bashrc` is executed on login and contains a command that forces logout.  
- Understood that:
  - `.bashrc` runs during interactive shell sessions.  
  - The shell acts as an interface between the user and the kernel.  
  - Normally, when a command like `ls` is entered, the shell creates a process and sends it to the kernel for execution.  
- Instead of using an interactive shell, used a non-interactive SSH command to bypass `.bashrc`.  

- Executed:
  - `sshpass -p <password> ssh bandit18@bandit.labs.overthewire.org -p 2220 ls`  
  - This logs in and directly runs `ls` without opening an interactive shell.  
  - This bypasses the `.bashrc` logout.  
  - Observed the `readme` file in the directory.  

- Retrieved the password:
  - `sshpass -p <password> ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`  
  - This directly executes `cat readme` on the remote system.  
  - The password for the next level is displayed.  

### What I Learned
- Interactive shells execute startup files like `.bashrc`, which can affect login behavior.  
- Non-interactive SSH commands can bypass such configurations.  
- SSH can execute commands using a non-interactive shell, which skips startup files like `.bashrc` 
- Misconfigured shell initialization files can restrict or break normal access.  

### Security Insight
- Misconfigured `.bashrc` files can disrupt user access or be abused for denial of service.  
- Restricting interactive shells alone is not sufficient, as non-interactive execution may still be possible.  
 
