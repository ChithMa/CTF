# MADNESS
## Basic Info
- Platform: Try Hack Me
- Difficulty: Easy
- Date solved: 01-04-2026

## Enumeration
- Nmap scan: nmap -sV <IP>
- Open ports: 22, 80
- Services found: ssh, http

![Nmap](Screenshots/madness-nmap.png)

With port 80 open, web enumeration was the next logical step.

## Web Enumeration

While reviewing the website’s source code, an image file named "thm.jpg" was discovered.

![sourcecode](Screenshots/madness-sourcecode.png)

The image file was downloaded using:
curl -o <file name> "<URL>"

![getjpg](Screenshots/madness-jpg.png)

## File Analysis – Header Verification

To confirm the file type, the following command was used:
"xxd thm.jpg"

![xxd](Screenshots/madness-xxd.png)

### Observation:

The hexadecimal header began with:
"89 50 4E 47"
This signature corresponds to a PNG file, not a JPG. A valid JPG file should begin with:
"FF D8 FF"
This indicated that the file extension had been intentionally altered.

## Modifying the File Header


To correct the file header, the tool hexedit was used:
"hexedit <filename>"

![hexedit](Screenshots/HEXEDIT-madness.png)

After modifying the header, the image was opened using:
"eog thm.jpg"

![image](Screenshots/madness-photo.png)

The image revealed part of a hidden URL:
"th1s 1s h1dd3n"

## Discovering the Hidden Page

Navigating to:
http://<IP>/th1s_1s_h1dd3n/
led to a page requesting a secret code.
Upon inspecting the page source, a hint was found indicating that the secret code was between 1 and 100.

## Brute Forcing the Secret Code

A simple Python script was written to brute-force the code.
 
![python-code](Screenshots/madness-code.png)

After execution, the script revealed:
73

Accessing:
http://<IP>/th1s_1s_h1dd3n/?secret=73

granted access to a new page containing a strange string, suspected to be a password.

![access- to the website](Screenshots/got-access.png)


## Extracting Hidden Data with Steghide

The image was further analyzed using steganography techniques:
"steghide extract -sf thm.jpg"
After entering the suspected password, a file named: "hidden.txt" was extracted.

![steghide output txt file](Screenshots/steghide-madness-thm.png)

The file contained an encrypted string.

## Decoding the Username

The encrypted string was decoded using ROT13, revealing the username:
"joker"

![rot13 decript](Screenshots/Madness-cybercheff-rot13.png) 

## Obtaining SSH Credentials

Another image from the TryHackMe site was downloaded and analyzed with:
"steghide extract -sf <filename>"
By pressing Enter when prompted for a password, a text file containing the SSH password was extracted.
Using the discovered credentials:
ssh joker@<IP>

![ssh-password](Screenshots/madness-password-ssh.png) 
![ssh access](Screenshots/madness-sshaccess.png)

The machine was successfully accessed via SSH.

## User Flag

Within the user’s home directory, a file named "user.txt" was located, containing the user flag.

## Privilege Escalation

To identify potential privilege escalation vectors, SUID binaries were enumerated:
"find / -type f -perm -4000 2>/dev/null"

This revealed a binary:
"screen-4.5.0"

![find exploit](Screenshots/madness-exploit.png)

## Exploiting Screen 4.5.0

Using searchsploit, a known exploit for screen version 4.5.0 was identified.

![searchsploit](Screenshots/madness-searchsploit.png)

The exploit code was copied to the target machine, saved as a .sh file, and executed.

![sh code](Screenshots/madness-sh-code.png)

then execute it and run the exploit and instantly got the root access.

![get root access](Screenshots/madness-rootaccess.png)

Verification with: "id"
confirmed: "uid=0(root)"

## Root Flag
Finally, navigating to the root directory revealed the final flag.

![root flag](Screenshots/madness-root-flag.png)


