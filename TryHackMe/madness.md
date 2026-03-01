# MADNESS
## Basic Info
- Platform: Try Hack Me
- Difficulty: Easy
- Date solved: 01-03-2026

## Enumeration
- Nmap scan: nmap -sV <IP>
- Open ports: 22, 80
- Services found: ssh, http
![Nmap](Screenshots/madness-nmap.png)

by going in to the sourcecode of the website I sow a image call thm.jpg
![sourcecode](Screenshots/madness-sourcecode.png)

got that image using the following command
curl -o <file name> "<URL>"
![getjpg](Screenshots/madness-jpg.png)
