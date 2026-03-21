
### Level Info
- **Level:** Bandit Level 14 - Level 15
- **Category:** Networking / Port Interaction

### Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

### Walkthrough
- Log into bandit14 using the obtained password  
- Connect to the service using:
  - `nc localhost 30000`  
- Wait for the connection (blank line appears)  
- Enter the current level password and press Enter  
- The service validates the input and returns the password for the next level  

- Alternative one-liner:
  - `echo "<current_password>" | nc localhost 30000`  

### What I Learned
- Learned how to interact with services running on a specific TCP port.  
- Understood how to use `nc` (netcat) for client-server communication  

### Security Insight
- Open ports can expose services that accept input and return sensitive data  
- Attackers can interact with such services to extract data using simple tools like `nc`  
