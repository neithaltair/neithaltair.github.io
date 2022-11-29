---
title:  "Comandos Escaneo Red"
date:   2022-11-29
categories: [Scan]
tags: [Linux,Network,Nmap]
---

Escaneo Red con `NMAP`. 

Scan network with `NMAP`
``` bash
nmap -sP -p <ip> #ping scan

nmap -PN -sV --top-ports 50 --open <ip> #search smb vuln

nmap -PN --script smb-vuln* -p139,445 <ip> #classic scan

nmap -PN -sC -sV -p- -oA <output> <ip> #Full scan, demorado, -oA es opcional

nmap -sU -sC -sV -oA <output> <ip> #udpScan

nmap -sV -PN --script vulners <ip> #scan search vulnerabilities
```


*(1,1)*