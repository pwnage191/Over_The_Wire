### Level Info
- **Level:** Bandit Level 28 - Level 29.
- **Category:** Git / Version History / Information Disclosure.

### Goal
There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via port 2220. The password for user
bandit28-git is the same as bandit28. Clone the repository from your local machine and find the password for the next level.

### Walkthrough
- Create a working directory in local machine: `mkdir bandit28`
- Navigate into the directory: `cd bandit28`
- Clone the repository:
  `git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo`
- Enter password for `bandit28-git` (same as bandit28).
- Navigate into the repository: `cd repo`
- List files: `ls`
- Found: `README.md`
- Read the file: `cat README.md`
- Observed:
  -  Password is hidden or replaced (e.g., `password: xxxxx`).
  -  This indicates the password was present earlier and later removed.
  -  <img width="800" height="334" alt="image" src="https://github.com/user-attachments/assets/a80e80a2-b34a-4c85-86fd-66971d15a3a4" />
- Check commit history:  `git log`
- <img width="800" height="675" alt="image" src="https://github.com/user-attachments/assets/b77e5ee1-ec4a-42e2-b1de-166a3ddf36b0" />
- Observed commits:
	  - `fix info leak`
	  - `add missing data`
	  - `initial commit`
- Understood:
	-  "fix info leak" means sensitive data was removed.
	-  The password likely exists in the previous commit.
- View previous commit:  `git show <commit ID>`
- This reveals the original password before it was removed.

### What I Learned
- Git stores full history of changes, even after data is removed.  
- Commit messages help identify when sensitive data was added or removed.  
- If data is hidden in the current version, previous commits may still contain it.  

### Security Insight
- Removing sensitive data from current files does not remove it from Git history.  
- `git filter-branch` or `git rebase` rewrites the commit history to remove sensitive data completely.
- They modify past commits so the secret is no longer present in any version.
