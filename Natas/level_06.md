#### Challenge:
- Start here:
- Username: natas6
- Password: ( Password obtained from previous level ) 
- URL:      http://natas6.natas.labs.overthewire.org 

My path:
  - I opened the website with credentials.
  - It showed an input box and a view page source link.
  - When I clicked view page source, it displayed the source code & contained the php code.
  - I saw "include includes/secret.inc", I went to the file path.
  - It contained the secret key the page is expecting in the form input.
  - When i entered that key in the input field, it revealed the next level password.

#### Learning outcomes:
  - Follow linked files to find sensitive information
  - Hardcoded secrets are insecure
  - Never trust page source or file paths to hide data

#### Real-world mapping:
  - Developers sometimes store API keys/passwords in included files
  - Misconfigured file permissions expose sensitive files
  - Attackers crawl directories/files during recon to find secrets

#### Bug class:
  - Information Disclosure – sensitive data exposed publicly
  - Hardcoded Credentials – passwords stored directly in code/files
  - Insecure File Inclusion – referenced files can be accessed directly

#### Conclusion:
Secrets hidden in source files are not secure, any referenced file can be accessed and read by attackers. 
Proper authentication and secure storage must be implemented.
