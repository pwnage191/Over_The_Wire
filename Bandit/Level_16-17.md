### Level Info
- **Level:** Bandit Level 16 - Level 17.
- **Category:** Networking / Port Scanning / SSL-TLS.

### Goal
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the
range 31000 to 32000.

### Walkthrough
- Logged into bandit16 using the obtained password.  
- Scanned the port range to identify active services:
	- `nmap -sV localhost -p 31000-32000`. 
- Observed multiple open ports and checked which ones supported SSL/TLS.
- <img width="689" height="215" alt="image" src="https://github.com/user-attachments/assets/5e268359-3234-4a33-880d-4516a28d47c5" />
- Connected to the SSL/TLS-enabled port:
	- `ncat --ssl localhost 31790`.  
- Entered the current level password.  
- Most ports echoed the input, but one port returned an RSA private key.  
- Copied the private key from the terminal output.  
- Initially tried to use the key inside the Bandit machine, but SSH connection was blocked from localhost.  
- Switched to my local machine:
  - Created a file:
    - `nano bandit17_key`.  
  - Pasted the copied RSA private key.  
  - Set correct permissions:
    - `chmod 600 bandit17_key`.  
- Used the key to connect to the next level:
  - `ssh -i bandit17_key bandit17@bandit.labs.overthewire.org -p 2220`.  

### What I Learned
- Port scanning helps identify active services within a range instead of guessing manually.
- SSL/TLS services require specific tools like `ncat --ssl` or `openssl`, unlike normal TCP connections.
- Not all open ports are useful; some act as decoys and simply echo input.
- Private keys must have strict permissions (`chmod 600`) to be accepted by SSH.

### Security Insight
- Open ports can expose services that may leak sensitive data.  
- Misconfigured services can reveal private keys or credentials.  
