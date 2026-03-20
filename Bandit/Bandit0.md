### Level Info
- **Level:** Bandit 0
- **Category:** Linux / File Read / etc.

### Goal
The goal of this level is for you to log into the game using SSH.

### Walkthrough
- Basic syntax:
	- ssh username@ip_address
	- ssh username@host -p port
- Given credentials:- Username: bandit0, password: bandit0
- `ssh bandit0@bandit.labs.overthewire.org -p 2220`
- Establish a secure connection, enumerate the files (ls)
- It displayed `readme`, read the file ( cat readme )
- Read file contents to obtain the password for the next level

### What I Learned
- SSH (Secure Shell) is used to securely connect to remote systems
- Basic file enumeration using `ls`
- Reading file contents using `cat`

### Security Insight
Using encrypted protocols like SSH helps protect credentials from interception, but storing sensitive data in readable files 
can still expose it to unauthorized users
