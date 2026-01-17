#### Challenge:
- Start here:
- Username: natas11
- Password: ( Password obtained from previous level ) 
- URL: http://natas11.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - The page showed "Cookies are protected with XOR encryption" and view page code link.
  - I clicked view page code link, In the PHP source code, I noticed a cookie named data was used to store user preferences.
  - From the code, I understood that this cookie is user‑controlled and its contents are trusted by the server.
  - I also noticed that the value of showpassword inside this cookie directly controls an authorization decision 
    (whether the next level password is shown or not).
  - The cookie was created using this logic:
        - The data array was converted to JSON.
        - The JSON string was XOR‑encrypted using a secret key.
        - The XORed output was Base64‑encoded and stored as a cookie.
  - The default data stored in the cookie was {"showpassword":"no","bgcolor":"#ffffff"}.
  - I observed that if showpassword is set to "yes", the server prints the next level password.
  - The encryption function used XOR, which is reversible,
          plaintext ^ key = ciphertext
          ciphertext ^ plaintext = key
  - I copied the data cookie from the browser and Base64‑decoded it to obtain the raw XORed bytes. ( %3D refers to = )
  - I used cyber chef ( From base64, To hex ( delimiter = none )) => It gives cipher text in hex format.
  - I knew the default plaintext JSON {"showpassword":"no","bgcolor":"#ffffff"}, convert it to the hex format by using cyber chef ( To Hex ).
  - I XORed the ciphertext with the plaintext to recover the key. ( In cyber chef: From hex, XOR (I/P:CP, key:PT))
  - From Hex is used before XOR because XOR works on real bytes, and hex is just text that needs to be converted into bytes first.
      CipherText: 1e6624070a33270e1637200017207555472a384d49663508062b3b0017666d4d462231090322314d18
      PlainText:  7b2273686f7770617373776f7264223a226e6f222c226267636f6c6f72223a2223666666666666227d
  - The recovered key was a short repeating string: eDWo.
  - Because the server uses the same key repeatedly ($key[$i % strlen($key)]), I could now encrypt my own data.
  - I created a new plaintext JSON with {"showpassword":"yes","bgcolor":"#ffffff"}.
  - Using the recovered key, I XOR‑encrypted this new plaintext and then Base64‑encoded the result.
  - In cyber chef, JSON: {"showpassword":"yes","bgcolor":"#ffffff"}
        PlainText: 7b2273686f7770617373776f7264223a22796573222c226267636f6c6f72223a2223666666666666227d0d0a
        Key: eDWo (UTF-8)
        Sequence: ( I\P: PT, From hex, XOR, To Base64 )
  - I Base64‑encoded the result and replaced the data cookie with my forged value.
  - After refreshing the page, the condition showpassword == "yes" became true.
  - The website revealed the password for natas12.

#### Learning Outcomes:
  - Learned how client-side cookies can be modified by users.
  - Understood that XOR encryption is reversible and not secure for protecting sensitive data.
  - Understood how authorization logic can depend on insecure client-side data.

#### Real-World Mapping:
  - Web applications often store user roles or flags in cookies.
  - If cookies are only encrypted and not signed, attackers can forge them.

#### Bug Class:
Broken Authentication / Insecure Cryptographic Design
The application trusts encrypted client-side data for access control, allowing attackers to modify and re-encrypt cookies.

#### Conclusion:
  - This challenge showed that encryption alone is not security.
  - Using XOR without integrity checks makes data fully attacker-controlled.
  - Trusting client-side cookies for authorization leads to logic bypasses.
  - Proper server-side validation and cryptographic signing are required.
  - Never trust client-side data, even if it is encrypted.

