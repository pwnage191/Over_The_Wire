#### Challenge:
- Start here:
- Username: natas13
- Password: ( Password obtained from previous level ) 
- URL: http://natas13.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - The page showed a file upload form with the message: "Choose a JPEG to upload (max 1KB)".
  - I noticed a view sourcecode link and clicked it.
  - In the PHP source code, I observed the file upload logic.
  - Generates a random filename, takes the extension from the user controlled filename field, validate the header of the file &
    Does not validate the actual file content.
  - I created a PHP payload file:
            <?php
            echo file_get_contents('/etc/natas_webpass/natas14');
            ?>
  - I saved it as yes.php on my laptop.
  - I opened the hex editor, for adding the header of jpg.
  - This added some non-printable (garbage) bytes before the php code.
  - PHP still executed the file correctly because the PHP interpreter starts parsing only from the `<?php` tag and ignores any data before it.
  - Open browser dev tools (Inspect -> Elements), Change: filename=random.php and upload the file.
  - The server generated a random file name, gave me a clickable link to the uploaded file.
  - I clicked the uploaded file URL. Because the file extension was .php, the server executed the php code.
  - It revealed the next level password.

#### File Upload Bypass Logic:
  - I uploaded the file with the .jpg extension, but the actual file type and content were php.
  - I modified the magic header of the file to bypass the security check.
  - PHP reads the code only from the <?php tag, and any data before it is treated as garbage.
  - I changed the hidden field from filename=random.jpg to filename=random.php, which sent the file to the PHP interpreter and
    caused it to execute.

#### Learning Outcomes:
  - Learned that PHP interprets code only from the <?php tag, ignoring preceding binary data.
  - Identified the risk of trusting partial server-side validation (header-only checks).

#### Real‑World Mapping:
  - Systems that validate only file extension or magic bytes, not full file content.
  - Upload directories configured as executable, allowing scripts to run.
  - Leads to Remote Code Execution (RCE), data theft, or full server takeover.

#### Bug Class:
Insecure File Upload
Failure to properly validate uploaded files allows attackers to execute arbitrary code on the server.

#### Conclusion:
This challenge demonstrates how relying only on file headers for validation is insufficient.
Proper file handling must include strict content validation and storing uploads outside the web root.
