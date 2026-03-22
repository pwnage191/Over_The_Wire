### Level Info
- **Level:** Bandit Level 22 - Level 23.
- **Category:** Cron Jobs / Hashing / File Access.

### Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/` for the 
configuration and see what command is being executed.

### Walkthrough
- Log into bandit22 using the password.  
- Navigate to cron directory:
  - `cd /etc/cron.d/`.  
- List files: `ls`.  
- Output:
  ```
  behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup  otw-tmp-dir
  clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job sysstat
  ```  
- Inspect the relevant cron job:
	- `cat cronjob_bandit23`.  
	-  Output:
  ```
  @reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
  * * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
  ```  

- Understood the cron entry:
  - `@reboot` runs once when the system starts.  
  - `* * * * *` runs every minute.  
  - Cron format fields: minute, hour, day of month, month, day of week.  
  - `bandit23` is the user executing the script.  
  - `/usr/bin/cronjob_bandit23.sh` is the script being executed.  
  - `&> /dev/null` redirects both stdout and stderr to `/dev/null`.  

- In simple:
  - Run `/usr/bin/cronjob_bandit23.sh` as user bandit23 every minute and at system startup, without showing any output.  

- Checked the script:
  - `cat /usr/bin/cronjob_bandit23.sh`.  

- Output:
  ```
  #!/bin/bash
  myname=$(whoami)
  mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
  echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
  cat /etc/bandit_pass/$myname > /tmp/$mytarget
  ```  

- Understood the logic:
  - Gets the username using `whoami`.  
  - Creates a hash from the string `I am user <username>`.  
  - Uses the hash as a filename in `/tmp`.  
  - Copies the password into that file.  

- Reproduced the hash manually:
  - `echo I am user bandit23 | md5sum | cut -d ' ' -f 1`.  

- Output:
  ```
  8ca319486bfbbc3663ea0fbe81326349
  ```  

- Retrieved the password:
  - `cat /tmp/8ca319486bfbbc3663ea0fbe81326349`.  

### What I Learned
- Cron jobs can automate scripts that expose sensitive data if not handled securely.  
- Hashing is sensitive to even small changes like newline characters.  
- Reproducing script logic exactly is important to get correct results.  

### Security Insight
- Writing sensitive data to predictable locations like `/tmp` is insecure.  
- Using weak or predictable hashing logic can expose sensitive file paths. 

### Rule of Thumb
- Always mimic exactly what the script does.  
- If the script uses `echo`, hashing includes a newline.  
- If the script uses `echo -n`, hashing excludes the newline.  
