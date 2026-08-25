# Hack The Box - Reactor

## Overview
**Machine:** Reactor  
**Platform:** Hack The Box  
**OS:** Linux  
**Difficulty:** Easy/Medium
---

![nmap](Screenshots/Reactor-0.png)

## 1. Enumeration
Start with an Nmap scan:

```bash
nmap -sV 10.129.245.214
```

![nmap](Screenshots/Reactor-1.png)
The scan reveals two interesting ports:
```bash
22/tcp    open    ssh
3000/tcp  open    unknown
```

Port 22 is running:
```bash
OpenSSH 9.6p1 Ubuntu
```
Port 3000 identifies itself as a Next.js application:
```bash
X-Powered-By: Next.js
```
The Nmap response also reveals that the application is returning normal HTTP responses.
So the initial attack surface is:
```bash
22   → SSH
3000 → Next.js web application
```

## 2. Investigating the Web Application

![nmap](Screenshots/Reactor-2.png)

Opening the application on port 3000 shows that it is a Next.js application.
The JavaScript source also contains:

```bash
rendererPackageName: 'react-dom'
version: '19.0.0-rc-66855b96-20241106'
```

This identifies the React/React-DOM version used by the application.

The important lesson here is that seeing react-dom in JavaScript doesn't automatically mean that React itself is the vulnerability. It is simply one of the libraries used by the Next.js application.

## 3. Finding the SQLite Database

![nmap](Screenshots/Reactor-3.png)

![nmap](Screenshots/Reactor-4.png)
![nmap](Screenshots/Reactor-5.png)
![nmap](Screenshots/Reactor-6.png)
![nmap](Screenshots/Reactor-7.png)
![nmap](Screenshots/Rwactor-8.png)
