### Level Info
- **Level:** Bandit Level 20 - Level 21.
- **Category:** Networking / Setuid / Client-Server Interaction.

### Goal
Use the setuid binary `suconnect` to connect to a local port and retrieve the password for the next level by providing the current
level password.

### Walkthrough
- Log in as bandit20.
- <img width="600" height="110" alt="image" src="https://github.com/user-attachments/assets/67827a50-bc7e-4d28-8cc3-3163c6740b06" />
- Observed the setuid binary:
  - `./suconnect`.  
- Managed two sessions:
	  - Opened another SSH session
	  - Started a listener on a chosen port: `nc -lvp 4444` in one session.
- In the second session, executed:
  - `./suconnect 4444`.
  - <img width="770" height="165" alt="image" src="https://github.com/user-attachments/assets/59481539-1961-4338-bac8-5c1162a697b4" />
  - <img width="670" height="85" alt="image" src="https://github.com/user-attachments/assets/abc0dec7-a29f-487d-bbe2-644a11470750" />
- Understood the flow:
	  - `suconnect` connects to `localhost:4444`.  
	  - It waits for input from the listener.  
- Entered the current level password in the listener.  
- The setuid binary:
  - Reads the password.  
  - Compares it with the correct password.  
  - If correct, returns the next level password.
  - <img width="1174" height="192" alt="image" src="https://github.com/user-attachments/assets/35f6b505-7993-4ccf-b6f0-82ab977a852c" />
  - <img width="804" height="157" alt="image" src="https://github.com/user-attachments/assets/12309649-2219-430e-be32-6969fa281089" />

### What I Learned
- In this level, `nc` acts as the server while `suconnect` acts as the client.  
- This client-server role reversal is important to understand for network interactions.  
- Managing multiple sessions is a practical requirement when dealing with interactive network programs.  

### Security Insight
- Exposing authentication mechanisms over local services can be risky if not properly controlled.  
- Improper validation logic in privileged programs can lead to credential leakage.  
