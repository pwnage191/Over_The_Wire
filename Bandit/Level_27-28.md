### Level Info
- **Level:** Bandit Level 27 - Level 28.
- **Category:** Git / Remote Repository / Information Disclosure.

### Goal
There is a git repository at `ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo` via port 2220. The password for 
user bandit27-git is the same as bandit27. Clone the repository from your local machine and find the password for the next level.

### Walkthrough
- Create a working directory in local machine: `mkdir Github`
- Navigate into the directory: `cd Github`
- Clone the repository:
  `git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo`
- Enter password for `bandit27-git` (same as bandit27).
- After cloning, a folder is created: `repo`
- Navigate into the repository: `cd repo`
- List files: `ls`
- Found: `README`
- Read the file:`cat README` 
- Password was revealed.
- <img width="800" height="443" alt="image" src="https://github.com/user-attachments/assets/ef272e87-8d8c-49e4-8487-68bf4ff708fc" />
- <img width="800" height="509" alt="image" src="https://github.com/user-attachments/assets/44ed5cea-6103-4062-aeb5-2664b309f7d9" />

### What I Learned
- Git repositories can be cloned from remote servers using SSH.  
- `git clone` creates a local copy of the repository including its contents.  

### Security Insight
- Storing sensitive data like passwords in repositories is insecure.  
- Even simple files like README can expose credentials if not handled properly.  
