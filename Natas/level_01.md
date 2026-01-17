#### Challenge:
- Start here:
- Username: natas1
- Password: ( Password obtained from previous level ) 
- URL:   http://natas1.natas.labs.overthewire.org 

#### My Path:
Method 1:
  - I opened the website.
  - It shows "You can find the password for the next level on this page, but rightclicking has been blocked!"
  - I tried to right-click, but a popup displayed "right clicking has been blocked!".
  - I searched for a shortcut for right‑click on Google, and it showed Shift + F10.
  - It didn’t work.
  - Next, I used the shortcut for view page source (Ctrl + U).
  - It worked. One of the comments held the password for the next level.

Method 2:
  - I used the key "F12" to open the dev tools.
  - Go to the elements tab, see the code, One of the comments held the password for the next level.

Method 3:
  - I use Google to know how to unblock the right-click.
  - Open DevTools (F12 or Ctrl+Shift+I).
  - Open DevTools settings (gear icon or F1).
  - Disable JavaScript in the settings panel.
  - Reload the page to bypass the right-click block.
  - Now, it allows you to right-click.

#### Learning outcomes:
  - Use browser shortcuts (Ctrl+U, F12)
  - Bypass simple client-side restrictions
  - Understand that right-click blocking is not real security
  - Disable JavaScript to remove page restrictions

#### Real-world mapping
  - Client-side protection is weak
  - Security through obscurity fails: Developers hiding passwords in page source = insecure practice.
  - JavaScript-dependent security is breakable: If security depends only on JS, users can disable it.
  - Finding sensitive data exposure: Similar mistakes happen in real web apps (API keys, credentials leaked).

#### Conclusion: 
  This challenge demonstrates that client-side restrictions can be easily bypassed using developer tools. Never rely on 
JavaScript or UI blocks for real security.

