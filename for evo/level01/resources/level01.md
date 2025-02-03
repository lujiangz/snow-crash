# Level 01

## Solution Steps

1. First, we examined the `/etc/passwd` file:

    ```bash
    level01@SnowCrash:~$ cat /etc/passwd
    ```

2. We found a suspicious line in the output:

    ```text
    flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
    ```

3. In this line, we can see an encrypted password hash: `42hDRfypTqqnw`

4. Passwords in the `/etc/passwd` file are typically encrypted using the DES algorithm.

5. We can crack this hash using a password cracking tool like John the Ripper.

## Tools Used
- cat command
- John the Ripper

## Lessons Learned
- The importance of `/etc/passwd` file in Linux systems
- Storing passwords in `/etc/passwd` file in older systems creates a security vulnerability
- Modern systems store passwords in the `/etc/shadow` file

## Notes
- The hash being encrypted with DES algorithm indicates this is an older system
- For security reasons, storing passwords in `/etc/passwd` file is no longer recommended