# Brooklyn Nine Nine

Objective: Obtain the user and root flags.

![d](Screenshots/BrooklynNineNine0.png)

## Reconnaissance & Enumeration
### Network Scanning

We began by sending an ICMP request to verify the host was up, followed by a service version scan using nmap as shown in Brooklyn Nine Nine9.png:

Bash:
- ping 10.48.130.239
- nmap -sV 10.48.130.239
- 
The scan revealed three open ports:
- Port 21: FTP (vsftpd 3.0.3)
- Port 22: SSH (OpenSSH 7.6p1)
- Port 80: HTTP (Apache httpd 2.4.29)
- 
![d](Screenshots/BrooklynNineNine1.png)
![d](Screenshots/BrooklynNineNine2.png)
![d](Screenshots/BrooklynNineNine3.png)
![d](Screenshots/BrooklynNineNine4.png)
![d](Screenshots/BrooklynNineNine5.png)
![d](Screenshots/BrooklynNineNine6.png)
![d](Screenshots/BrooklynNineNine7.png)
![d](Screenshots/BrooklynNineNine8.png)
![d](Screenshots/BrooklynNineNine9.png)
