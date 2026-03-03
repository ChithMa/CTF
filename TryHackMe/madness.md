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

use xxd tool to check the file is a jpg file or not and found that the file is actually a png file by looking at the hexadecimal header. this shows the header as 8950 4e47 but this header is refer to png files jpg should have the header of 
FF D8 FF

![xxd](Screenshots/madness-xxd.png)

now we want to change the header to open the file to a jpg or JFIF to do further investigation.

we can u the following command to get the editable file.
- hexedit <filename>

![hexedit](Screenshots/HEXEDIT-madness.png)
![image](Screenshots/madness-photo.png)
 then after run "eog" command to opent the image. in the image i got a part of a url that is "th1s 1s h1dd3n". then i types that part in the URL and got a new web page that asking for a secret code. and checked the source code and found a hint saying the secreat code is between 1 and 100. then i type the following code.
 

![python-code](Screenshots/madness-code.png)
