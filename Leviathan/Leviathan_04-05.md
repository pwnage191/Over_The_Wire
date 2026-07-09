### Level
- Leviathan 04 -> Leviathan 05
- Category: Binary Data Decoding

### Leviathan 4
- I started by exploring the file system and found the `.trash` directory.
- Inside the directory, I found a binary file (`bin`) with the SetUID permission.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/e9eb27ac-dad7-42c2-810c-6055b4dc9b20" />
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/67b2d8c1-aa9e-43f0-a035-72520f5da283" />
- I ran the binary, and it displayed a sequence of binary digits (`0`s and `1`s).
- I used `ltrace` to determine where the program was reading the data from.
- The program read the data from `/etc/leviathan_pass/leviathan5`.
- I wrote a small Python script to convert the binary data into a string.
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/bea44c6e-59d4-46ca-8997-de46335969cc" />
- <img width="800" alt="image" src="https://github.com/user-attachments/assets/a7bfb274-3219-43f0-92aa-c0ccb7511800" />
- The decoded string revealed the password for the next level.

### Learning Drops
- `ltrace` can be used to identify which library functions are called by a binary program and to determine which files the program accesses
  (for example, through functions like `fopen()`).
- `fopen()` is a C library function used to open a file. Internally, it calls the `open()` system call to access the file.
