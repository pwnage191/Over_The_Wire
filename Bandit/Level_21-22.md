### Level Info
- **Level:** Bandit Level 21 - Level 22.
- **Category:** Cron Jobs / Scheduled Tasks.

### Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

### Walkthrough
- Log in to bandit21 using the password.  
- Navigate to cron directory:
  - `cd /etc/cron.d/`.  
- List files:
  - `ls`.  
- Output:
  ```
  behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup  otw-tmp-dir
  clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job sysstat
  ```  
- Inspect the relevant cron job:
  - `cat cronjob_bandit22`.  
- Output:
  ```
  @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
  * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
  ```  
- Understood scheduling:
  - `@reboot` runs once when the system starts.  
  - `* * * * *` runs every minute.  
  - Cron format has 5 fields:
    - minute, hour, day of month, month, day of week.  
  - Each `*` means “every”, so this runs every minute.  
- Identified the script being executed:
  - `/usr/bin/cronjob_bandit22.sh`.
- Checked the script:
  - `cat /usr/bin/cronjob_bandit22.sh`.  
- Output:
  ```
  #!/bin/bash
  chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
  cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
  ```  

- Observed that:
  - The script copies the password of bandit22 to a file in `/tmp`.  
  - File permissions are set to `644`, making it readable.  
- Retrieved the password:
  - `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`.  

### What I Learned
- Cron jobs run automatically based on defined schedules.  
- Misconfigured scripts can expose sensitive data in accessible locations like `/tmp`.  

### Security Insight
- Storing sensitive data in world-readable temporary files is insecure.  
- Cron jobs must handle permissions carefully to avoid information leakage.  
- Temporary directories should not be used for storing credentials without proper protection.  
