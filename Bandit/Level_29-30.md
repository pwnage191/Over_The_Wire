### Level Info
- **Level:** Bandit Level 29 - Level 30.
- **Category:** Git / Branch Enumeration 

### Goal
There is a git repository at `ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo` via port 2220. The password for user
bandit29-git is the same as bandit29. Clone the repository from your local machine and find the password for the next level.

### Walkthrough
- Create a working directory in local machine: `mkdir bandit29`
- Navigate into the directory: `cd bandit29`
- Clone the repository:
  `git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo`
- Enter password for `bandit29-git` (same as bandit29).
- Navigate into the repository: `cd repo`
- List files:  `ls`
- Found: `README.md`
- Read the file: `cat README.md`
- <img width="600" height="358" alt="image" src="https://github.com/user-attachments/assets/85fec841-6ebe-49af-ac95-34ea30cc054a" />
- Observed:
	  - Message indicates that the password is not in production.
	  - This suggests the password is not in the current (master) branch.
- Check available branches:  `git branch -a`
- Found branches:
- <img width="600" height="272" alt="image" src="https://github.com/user-attachments/assets/caa1a107-9395-4774-bfce-ddaaa3565e04" />
- Switched to `dev` branch because the clue "not in production" directly points to a development environment.
- <img width="600" height="494" alt="image" src="https://github.com/user-attachments/assets/9836200a-2212-4b3b-94a3-eee44c8a661c" />
- Read the file: `cat README.md`

### What I Learned
- Git repositories can contain multiple branches with different versions of files.  
- Sensitive data may exist in non-production branches like dev or test.  
- Clues in files can indicate where to search for hidden data.  
- Branch enumeration is an important technique in repository analysis.  

### Security Insight
- Storing sensitive data in development branches is insecure.  
- All branches in a repository must be secured, not just the main branch.  
