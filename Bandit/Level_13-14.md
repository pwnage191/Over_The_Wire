### Level Info
- **Level:** Bandit Level 13 - Level 14.
- **Category:** SSH Key Authentication.

### Goal
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, 
instead of a password, a private SSH key is provided to log into the next level.

### Walkthrough
- Log into bandit13 using the obtained password.  
- Enumerate the files using `ls -la`, which shows `sshkey.private` and `HINT`.  
- The private key is used to remotely connect to bandit14.  
- The `HINT` file indicates that connecting from bandit13 to bandit14 via `localhost` is blocked (internal SSH is restricted).  
- Attempting `ssh -i sshkey.private bandit14@localhost -p 2220` fails (internal connection blocked).  

- Copy the private key to the local machine:
  - `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`
  - `scp` securely copies files from a remote server to your local machine.  
  - `-P 2220` specifies the port.  
  - `.` means current directory.  

- Set correct permissions:
  - `chmod 600 sshkey.private`
  - This ensures only the owner can read/write the key.  
  - SSH requires this to prevent others from accessing the private key.  
  - A private key must be accessible only to its owner (no read/write for others), otherwise SSH treats it as compromised and
    refuses to use it.

- Connect externally using the private key:
  - `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`

- Read the password:
  - `cat /etc/bandit_pass/bandit14`

### What I Learned
- SSH uses asymmetric cryptography for authentication and secure key exchange.  
- After the key exchange, a symmetric session key is used for fast encrypted communication.  
- Learned how to use a private key to authenticate without a password.  
- Understood the importance of proper key permissions for secure authentication.  

### Security Insight
- Exposure of a private key can lead to unauthorized access (account compromise).  
- Only the corresponding public key should be stored on the server for authentication.  
