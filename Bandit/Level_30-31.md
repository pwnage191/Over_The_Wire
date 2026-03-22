### Level Info
- **Level:** Bandit Level 30 - Level 31.
- **Category:** Git / Tags / References.

### Goal
There is a git repository at `ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo` via port 2220. The password for 
user bandit30-git is the same as bandit30. Clone the repository from your local machine and find the password for the next level.

### Walkthrough
- Created a working directory: `mkdir bandit30`
- Navigated into it: `cd bandit30`
- Cloned the repository:
  `git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo`
- Entered password for `bandit30-git`.
- Navigated into repo: `cd repo`
- Checked files:`ls` 
- Read the file: `cat README.md`
- Observed: File contains no useful information.
- Checked commit history: `git log`
- Observed: Only one commit present & no previous versions to analyze.
- Checked branches:  `git branch -a`
- Observed: No additional useful branches.
- Since the repository had only one commit, no useful branches, and no data in files, I inferred that the password might be stored
  in another Git reference like a tag, and verified it using `git tag`.
- Found:`secret`
- Viewed tag: `git show secret`
- This reveals the password for the next level.

### What I Learned
- A tag is a fixed reference pointing to a specific commit.  
• A commit is a Git object that stores a snapshot of files along with metadata such as message, author, and date.  
• A lightweight tag directly points to a commit and does not store any additional metadata.  
• An annotated tag points to a commit and also stores extra metadata like tagger name, date, and a message as a separate object.  
• In this level, a lightweight tag is used, which points to a commit containing the password in its message.

### Security Insight
- Sensitive data can be stored in Git references like tags.  
- Even if files and branches are clean, metadata can expose secrets.  

