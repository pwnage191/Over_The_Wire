#### Challenge:
- Start here:
- Username: natas12
- Password: ( Password obtained from previous level ) 
- URL: http://natas12.natas.labs.overthewire.org 

#### My path: 
  - I opened the website.
  - The page showed a file upload form with the message: "Choose a JPEG to upload (max 1KB)".
  - I noticed a view sourcecode link and clicked it.
  - In the PHP source code, I observed the file upload logic.
  - Generates a random filename, takes the extension from the user controlled filename field, Does not validate the actual file content.
  - To confirm this behavior, I created a test file containing:
        <?php echo "Hello I am here"; ?>
  - I saved the file with a .jpg extension on my laptop.
  - While uploading, I modified the hidden filename field in browser developer tools to random.php.
  - After uploading, the application returned a clickable link.
  - When I clicked the link, the message “Hello I am here” was displayed.
  - This confirmed that the server decides how to handle the file based only on the extension, which is client-controlled.
  - I created a PHP payload file:
            <?php
            echo file_get_contents('/etc/natas_webpass/natas13');
            ?>
  - I saved it as shell.php on my laptop.
  - Open browser dev tools (Inspect -> Elements), Change: filename=random.php and upload the file.
  - The server generated a random file name, gave me a clickable link to the uploaded file.
  - I clicked the uploaded file URL. Because the file extension was .php, the server executed the php code.
  - It revealed the next level password.

#### Learning Outcomes:
  - Learned how file upload vulnerabilities occur due to missing validation.
  - Learned that user-controlled filename fields are dangerous.

#### Real World Mapping:
If file type validation is weak, this often leads to remote code execution (RCE).

#### Bug Class:
Unrestricted File Upload
The application allows attackers to upload and execute arbitrary files because it does not properly validate file type or content.

#### Conclusion:
This challenge shows how trusting user-controlled file uploads can lead directly to remote code execution.
