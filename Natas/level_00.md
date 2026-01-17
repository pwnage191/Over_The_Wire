#### Challenge
- Start here:
- Username: natas0
- Password: natas0
- URL: http://natas0.natas.labs.overthewire.org

#### My path: 
  - I opened the website in browser.
  - The visible UI doesn't show any password, so i visited the page source.
  - It shows "You can find the password for the next level on this page."
  - When I inspected the page, one of the comments held the password for natas1.

#### Learning outcomes:
  - Never trust UI alone → inspect source
  - Developers leak secrets accidentally
  - Sensitive data must be hidden server-side

#### Real world mapping:
  - This simulates information disclosure vulnerability
  - Similar to exposed credentials or internal comments in bug bounty
  - Bug class: Improper Information Disclosure 

