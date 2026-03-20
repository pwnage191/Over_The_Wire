### Level Info
- **Level:** Bandit Level 11 - Level 12
- **Category:** Encoding

### Goal
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have 
been rotated by 13 positions.

### Walkthrough
- Log into bandit11 using the obtained password  
- Enumerate the files using `ls -l`, which shows `data.txt`  
- View the file using `cat data.txt` (ROT13 is mentioned in the challenge)  
- ROT13 shifts each letter by 13 positions, and since the alphabet has 26 letters, applying it twice returns the original text  
- Use the command: `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`  
  - `tr` replaces characters from one set with corresponding characters in another  
  - `'A-Za-z'` to `'N-ZA-Mn-za-m'` shifts each letter by 13 positions with wrap-around  
  - ROT13 is self-inverse, so applying it twice returns the original text  

### Alternate Method
- Use CyberChef and apply the `ROT13` recipe to decode the content  
- The decoded output reveals the password  

### What I Learned
- Learned how ROT13 encoding works and how to decode it using `tr`  
- Understood that simple substitution ciphers provide no real security  

### Origin
- ROT13 was commonly used in early internet communities like Usenet (1980s–90s)  
- It was used to hide spoilers, jokes, or puzzle answers  
- The idea was simple: if you don’t want to see the content, don’t decode it  

### Security Insight
- ROT13 is a weak substitution cipher and offers no real security  
- Encoded data can be easily reversed by unauthorized users  
