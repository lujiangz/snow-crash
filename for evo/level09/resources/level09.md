# Level 09

## Initial State
When we log in as Level09 user, we see two files:
- level09 (executable file)
- token (file containing encrypted text)

## Exploration

First, let's examine the files:

```bash
level09@SnowCrash:~$ cat token 
f4kmm6p|=�p�n��DB�Du{��

level09@SnowCrash:~$ ./level09 
You need to provied only one arg.

level09@SnowCrash:~$ ./level09 token 
tpmhr

level09@SnowCrash:~$ ./level09 "1111"
1234
```

## Analysis
Upon examining the program, we understand that it encrypts characters by adding their index values. For example:
- Character at index 0 + 0
- Character at index 1 + 1
- Character at index 2 + 2
and so on.

## Solution

We write a Python script to decrypt this:

```python
import sys

hash = sys.argv[1]
decrypted_hash = ""
for i in range(0,len(hash)):
    decrypted_hash = decrypted_hash + chr(ord(hash[i]) - i)
print(decrypted_hash)
```

### Testing
```bash
$ python /tmp/decrypt.py "1234"
1111
```

### Getting the Flag
We pass the contents of the token file to our script:
```bash
$ python /tmp/decrypt.py `cat token`
```

This command will give us the flag.