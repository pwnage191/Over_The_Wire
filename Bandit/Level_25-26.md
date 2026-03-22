### Level Info
- **Level:** Bandit Level 25 - Level 26.
- **Category:** Restricted Shell / Pager Escape / Vim Exploitation.

### Goal
Logging in to bandit26 from bandit25 should be fairly easy. The shell for user bandit26 is not /bin/bash, but something else.
Find out what it is, how it works, and how to break out of it.

### Walkthrough
- Log in to bandit25 using the password.
- Identify the shell used by bandit26: `cat /etc/passwd | grep bandit26`
 
- Found that the shell is: `/usr/bin/showtext`
- Understood:
	  - `/usr/bin/showtext` is not a normal shell.
	  - It only displays a file and exits.
	  - It does not allow command execution.
- In the home directory, found: `bandit26.sshkey`
- Localhost login may not work, so save the key in your local machine.
- Use the SSH key to log in: `ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220`
- The session exits immediately because `showtext` runs instead of a shell.
- Minimize the terminal window size so that the content cannot fit in one screen.
- This forces the program to use a pager and shows: `--More--`
- The pager waits for user input to scroll or move to the next line.
- This allows interaction using keys like `space`, `enter`, `q`, and `v`.
- Press `v` to open the content in vim.
- Inside vim:` :set shell=/bin/bash`
- <img width="700" height="280" alt="image" src="https://github.com/user-attachments/assets/1857fecc-b661-4dc6-a66b-308cc30bee9d" />
- Then press Enter, and type `:shell`
- <img width="700" height="279" alt="image" src="https://github.com/user-attachments/assets/4578badf-8573-45fc-a0fe-618a4dfada9b" />
- This spawns a shell as bandit26.
- Read the password: `cat /etc/bandit_pass/bandit26`
- <img width="700" height="262" alt="image" src="https://github.com/user-attachments/assets/278dc283-c681-4fcd-ad69-a1cb2b70d4df" />
- `:set shell=/bin/bash` sets the shell that vim will use, and `:shell` spawns an interactive bash shell using that setting, allowing
   command execution.

### What I Learned
- Some systems restrict users by replacing the shell with a custom program.  
- Pager behavior is triggered when output exceeds screen size.  
- Pagers wait for user input to scroll through content.  
- Vim can be used to spawn a shell and bypass restrictions.  

### Security Insight
- Replacing a shell with a restricted program is not secure if underlying tools allow escape.  
- Interactive programs like pagers and editors can introduce unintended escape paths.  
