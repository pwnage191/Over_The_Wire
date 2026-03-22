### Level Info
- **Level:** Bandit Level 31 - Level 32  
- **Category:** Git (Push / .gitignore)

### Goal
Push a file named `key.txt` with the required content to the remote repo.

### Walkthrough
- Clone the repo using `git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo`
- Go into the repo using `cd repo`
- Read instructions using `cat README.md`
- Create the file using `echo "May I come in?" > key.txt`
- Try adding it, but it is ignored using `git add key.txt`
- Check ignore rules using `cat .gitignore`
- <img width="700" height="112" alt="image" src="https://github.com/user-attachments/assets/f4088af0-a918-4cf9-8df0-310ed2587b92" />
- Force add the file using `git add -f key.txt`
- Set Git identity using `git config user.name "bandit31"` and `git config user.email "bandit31@overthewire.org"`
- Commit the file using `git commit -m "add key.txt"`
- Push changes using `git push origin master`
- Server verifies and returns the password
- <img width="700" height="299" alt="image" src="https://github.com/user-attachments/assets/bac1a878-a662-4e93-895c-0db9c1074342" />

### What I Learned
- .gitignore rules can block files based on patterns like *.txt
- The `-f` option forces Git to add files ignored by .gitignore
- Git requires username and email because each commit stores author identity as metadata
- Git can be used to push data to a remote repo, not just read from it

### Security Insight
- A file is not tracked when Git ignores it and does not include it in commits.
- Ignored files can still be force-added using `-f`, so restrictions can be bypassed
