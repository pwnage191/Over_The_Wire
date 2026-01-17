#### Challenge:
- Start here:
- Username: natas8
- Password: ( Password obtained from previous level ) 
- URL:      http://natas8.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - That website showed an input box and view page source link.
  - When I clicked view page source, it displayed the source code & contained the php code.
  - I found the hint that was "$encodedSecret = "3d3d516343746d4d6d6c315669563362".
  - The PHP code also had "return bin2hex(strrev(base64_encode($secret)));".
  - I used cyberchef to reverse the encoding, first convert into hex, reverse and base64. I found the secret.
  - I entered the secret into the input box and clicked submit, it revealed the next level password.

#### Learning Outcomes:
  - Reverse encoding steps (hex → reverse → base64).
  - Use tools (CyberChef) to transform encoded values.

#### Real-world mapping:
  - Developers accidentally expose logic that reveals secrets.
  - Attackers can reverse encoding to extract sensitive data.

#### Bug class:
  - Improper information disclosure.
  - Client-side reversible encoding.
