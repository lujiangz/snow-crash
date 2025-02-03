# Level 00

## Research process

1. We used the `find` command to locate files belonging to flag00 user in the system:
```bash
find / -user flag00 2>/dev/null
```

Command explanation:
- `/`: Search from root directory
- `-user flag00`: Search for files belonging to flag00 user
- `2>/dev/null`: Suppress error messages

2. Two files were found as a result:
```bash
/usr/sbin/john
/rofs/usr/sbin/john
```

3. We examined the contents of the files using `cat` command:
```bash
level00@SnowCrash:~$ cat /usr/sbin/john
cdiiddwpgswtgt

level00@SnowCrash:~$ cat /rofs/usr/sbin/john
cdiiddwpgswtgt
```

## Decryption

1. Encrypted text: `cdiiddwpgswtgt`
2. We tried various encryption methods using [dcode.fr](https://www.dcode.fr) website
3. We detected that ROT (Caesar) encryption method was used
4. When decrypted: `nottoohardhere`

## Flag
Flag for Level 00: `nottoohardhere`

## Learned Lessons
- File search techniques in Unix systems
- ROT/Caesar encryption method
- Linux file permissions and user privileges
- Error redirection (`2>/dev/null`)
