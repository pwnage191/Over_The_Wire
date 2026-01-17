#### Challenge:
- Start here:
- Username: natas7
- Password: ( Password obtained from previous level ) 
- URL:      http://natas7.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - That website showed two links, Home and About.
  - When I clicked, I noticed the URL parameter value changed.
  - I opened the view page source and found the hint.
  - The hint was "<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->".
  - In the Url, I entered the path into the page parameter.
  - The webpage revealed the password for the next level.

#### Learning outcomes:
  - Observe URL parameters for clues or vulnerabilities.
  - Server files may be exposed through path traversal.
  - Page content can be controlled through URL manipulation.

#### Real-world mapping:
  - Attackers modify URL parameters to access unauthorized files.
  - Developers sometimes rely on weak filtering on file paths.
  - Configuration passwords stored in system directories can leak.

#### Bug class:
  - Path Traversal – attacker accesses files outside intended directory.
  - Information Disclosure – sensitive file contents revealed.

#### Conclusion:
User-controlled file paths are risky. If the server fails to validate requested paths, attackers can read protected system files 
and expose credentials. Always sanitize input and implement proper access controls.


