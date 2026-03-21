### Level Info
- **Level:** Bandit Level 15 - Level 16
- **Category:** Networking / SSL-TLS

### Goal
Submit the current level password to localhost:30001 using **SSL/TLS encryption** to retrieve the next level’s password.

### Walkthrough
- Log into bandit15 using the obtained password  
- Connect to the secure service using:
  - `openssl s_client -connect localhost:30001` 
  - After the TLS connection is established, messages like `read R BLOCK` may appear,  this is normal and does not indicate a problem.
    The connection is waiting for input, so enter the password and press Enter.
- A TLS connection is established  
- Enter the current level password and press Enter  
- The server verifies the input and returns the next level password  
- Alternative method:
  - `ncat --ssl localhost 30001`  

### What I Learned
- Learned how to interact with services over SSL/TLS encryption  
- Learned the difference between plain TCP (`nc`) and encrypted communication (SSL/TLS)  
	- **nc** :  basic tool for TCP/UDP communication with no encryption (plain text)  
	- **ncat** :  enhanced version of nc with additional features and optional SSL/TLS support  
	- **openssl s_client** : tool specifically used to establish and test secure SSL/TLS encrypted connections  

### Security Insight
- Services using SSL/TLS protect data from being intercepted in plain text  
- Encryption ensures confidentiality during data transmission  
