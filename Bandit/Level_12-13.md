### Level Info
- **Level:** Bandit Level 12 - Level 13.
- **Category:** Decompression.

### Goal
The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed.

### Walkthrough
- Log into bandit12 using the obtained password.  
- Enumerate the files using `ls -l`, which shows `data.txt`.  
- Check the file type → ASCII text.  
- View the first few lines using `head -2 data.txt ` -> confirms hexadecimal format.  

- Create a working directory:
  - `cd /tmp`.
  - `mkdir challenger`.
  - `cd challenger`.
  - `/tmp` is used because the home directory is shared/read-only in OverTheWire, so a temporary workspace is required.  

- Copy the file:
  - `cp ~/data.txt .`.

- Reverse the hexdump to binary:
  - `xxd -r data.txt > hexdump.bin`.
  - `file hexdump.bin` -> identifies compression type.  

- Decompress step by step (repeat as needed):
  - Gzip:
    - `mv hexdump.bin file.gz`.
    - `gunzip file.gz`.
    - `file file`.
  - Bzip2:
    - `mv file file.bz2`.
    - `bunzip2 file.bz2`.
    - `file file`.
  - Tar:
    - `file file` -> POSIX tar archive.  
    - `tar -xf file`.  

- Continue the cycle:
  - Identify -> Rename -> Decompress -> Repeat.  
  - Multiple layers of gzip, bzip2, and tar are nested.  

- Final step:
  - `file data`  -> ASCII text.  
  - `cat data` -> reveals the password.  

### What I Learned
- Hexadecimal is a human-readable representation of data, not the actual file content.  
- Binary contains real bytes, including magic numbers (file signatures).  
- File types are identified using binary signatures, not hex text.  
- Hex must be converted back to binary (`xxd -r`) before analysis.  
- Learned to handle multi-layer compression using a systematic approach.  

### Security Insight
- Storing sensitive data in multiple compressed layers does not provide real security.  
- Attackers can systematically extract each layer using standard tools.  
- Proper encryption (not compression) is required to protect sensitive data.  
