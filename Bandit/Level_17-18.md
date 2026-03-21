### Level Info
- **Level:** Bandit Level 17 - Level 18.
- **Category:** File Comparison.

### Goal
There are 2 files in the home directory: `passwords.old` and `passwords.new`. The password for the next level is in `passwords.new` and
is the only line that has been changed between `passwords.old` and `passwords.new`.

### Walkthrough
- Listed the files : `ls -l`.  
- Compared both files to find the difference:
  - `diff passwords.new passwords.old`.  
- Output:
  ```
  42c42
  < x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
  ---
  > gvE89l3AhAhg3Mi9G2990zGnn42c8v20
  ```  

- `42c42` means line 42 was changed.  
  - `c` stands for change.  
  - Other diff symbols:
    - `a` means add.  
    - `d` means delete.  

- The line starting with `<` belongs to `passwords.new`.  
- The line starting with `>` belongs to `passwords.old`.  
- The changed line in `passwords.new` is the required password.  

### What I Learned
- Comparing files line by line helps quickly identify changes instead of manually checking large files.  
- `diff` clearly marks differences using symbols (`<` for new file, `>` for old file, `c/a/d` for change types).  

### Security Insight
- Keeping old credential files like `passwords.old` is risky because it exposes previous passwords.  
- Once credentials are rotated, old versions should be deleted instead of stored alongside new ones.  
- Leaving such files accessible can lead to unintended information disclosure.  
