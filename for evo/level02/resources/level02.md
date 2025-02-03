# Level02

## Starting Point
When we log into the Level02 account, we encounter a file named `level02.pcap`.

## Solution Steps

1. First, let's copy the PCAP file to our local machine:
```bash
scp -P 4242 level02@localhost:/home/user/level02/level02.pcap .
```

2. Open the file with Wireshark and apply the TCP filter.

3. When examining the packets, we see a login attempt containing some control characters:

Important Hex Characters:
- `0x0d`: Carriage Return (CR)
- `0x7f`: Delete character

4. When analyzing the traffic in Wireshark, we can see keyboard inputs and deletion operations. We can obtain the actual password by considering the Delete (0x7f) characters.

5. We can proceed to the next level using the password we obtained.

## Key Points
- PCAP files capture network traffic
- TCP filtering in Wireshark is important
- Understanding control characters is necessary