### Level Info
- **Level:** Bandit Level 32 - Level 33  
- **Category:** Shell (Restricted Shell Bypass)

### Goal
Escape the restricted shell and retrieve the password for the next level.

### Walkthrough
- Login to the level using `ssh bandit32@bandit.labs.overthewire.org -p 2220`
- Observe that the shell only accepts uppercase commands and blocks normal inputs like `whoami`
- Commands like `echo $0` fail because input is converted to uppercase before execution
- Run `$0`, which expands before uppercase conversion and executes the current shell
- This spawns a new shell instance without restrictions
- Retrieve the password using `cat /etc/bandit_pass/bandit33`
- <img width="673" height="374" alt="image" src="https://github.com/user-attachments/assets/965fdead-7d1e-495c-99c4-71033f9d565f" />
- $SHELL shows the restricted login shell, while $0 shows the actual running shell, which can be used to escape restrictions.
- <img width="658" height="139" alt="image" src="https://github.com/user-attachments/assets/73c1c6e5-c289-4fe7-8231-811098d9f574" />

### What I Learned
- Restricted shells can modify input before execution, such as converting to uppercase
- `$0` is a shell variable that contains the path of the current shell (e.g. `/bin/sh`)
- Running `$0` starts a new instance of the shell
- Variable expansion can occur before input filtering, enabling bypass

### Security Insight
- Input filtering alone is not secure if evaluation happens before enforcement
- Any shell variable resolving to a valid command can bypass restrictions if expansion occurs before filtering
