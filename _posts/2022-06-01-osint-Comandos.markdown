---
title:  "Comandos Osint"
date:   2022-06-01
categories: [Linux]
tags: [Linux,Comandos,Bash,Osint]
---

Comandos Osint `Osint`. 

``` bash
#!/bin/bash
#Author: NeithAltair
 
 #Tomar IP del dominio
 ping=$(ping -c 1 $1 | grep "PING" | cut -d " " -f3 | tr -d "()")
 
 #TheHarvester - domain, verify hostname, googledorks, dns brute force, shodan for discoverHosts
 theHarvester -d $1 -v -g -s -c -b google -f h_Goog-$1
 theHarvester -d $1 -v -g -s -c -b bing -f h_Bing-$1
 theHarvester -d $1 -v -g -s -c -b linkedin -f h_Link-$1
 theHarvester -d $1 -v -g -s -c -b twitter -f h_Twit-$1
 theHarvester -d $1 -v -g -s -c -b googleplus -f h_Googplus-$1
 theHarvester -d $1 -v -g -s -c -b google-profiles -f h_GoogProf-$1
 
 #dmitry - Subdominios, whois, netcraft.com, possible email addresses, port scan
 dmitry $1 -o dmitry-$1
 dmitry $1 -n -s -e -w -i 
 sublist3r -d $1 > sublist3r-$1.txt
 knockpy $1 > knockpy-$1.txt
 
 #nmap
 nmap -sV -Pn --open --script vulners $ping > nmap-$1
 
 rm -r *.xml

```


``` bash

dmitry: option requires an argument -- 'o'
Usage: dmitry [-winsepfb] [-t 0-9] [-o %host.txt] host
  -o     Save output to %host.txt or to file specified by -o file
  -i     Perform a whois lookup on the IP address of a host
  -w     Perform a whois lookup on the domain name of a host
  -n     Retrieve Netcraft.com information on a host
  -s     Perform a search for possible subdomains
  -e     Perform a search for possible email addresses
  -p     Perform a TCP port scan on a host
* -f     Perform a TCP port scan on a host showing output reporting filtered ports
* -b     Read in the banner received from the scanned port
* -t 0-9 Set the TTL in seconds when scanning a TCP port ( Default 2 )

```

*(1,1)*