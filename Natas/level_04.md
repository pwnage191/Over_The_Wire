#### Challenge:
- Start here:
- Username: natas4
- Password: ( Password obtained from previous level ) 
- URL: http://natas4.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - It showed "Access disallowed. You are visiting from "" while authorized users should come only from
    "http://natas5.natas.labs.overthewire.org/" and it contains the "Refresh" button.
  - When I click the refresh button, it showed "Access disallowed. You are visiting from "http://natas4.natas.labs.overthewire.org/" 
    while authorized users should come only from "http://natas5.natas.labs.overthewire.org/".
  - I used google to search, " if a website allow only from the particular url? ".
  - It displayed "Yes, a website can be configured to allow access only from specific URLs, a technique called URL filtering or referral-based 
    access control, often done server-side using .htaccess or application code (like PHP/Node.js) to check the HTTP_REFERER header.
  - I use burp suite, to intercept the natas4 login request and refresh request. 
  - In second request, it contains the referer header, I changed to "http://natas5.natas.labs.overthewire.org/".
  - The website allows the user, in view page source showed the password for the next level.

#### Learning Outcomes:
  - Understood that websites may restrict access based on the HTTP Referer header.
  - Saw that HTTP headers are user-controlled and can be modified in a proxy tool.
  - Observed how weak server-side validation leads to access bypass.

#### Real-World Mapping:
  - Attackers can spoof headers to access protected resources.
  - Referer-based access control is unreliable and should not be used for security.

#### Bug Class:
  - Improper Access Control – relying on client-controlled headers for authorization.
  - Client-Side Security Controls - security check happens in the browser, so attackers can easily change it.
  - Origin Validation Errors - the website trusts where the request came from without properly checking it.

#### Conclusion:
By intercepting the request and changing the Referer header to the expected allowed URL, access to the protected page was granted, 
revealing the next password. This demonstrates how trusting user-controlled headers for authorization leads to 
security bypass in real-world systems.
 
