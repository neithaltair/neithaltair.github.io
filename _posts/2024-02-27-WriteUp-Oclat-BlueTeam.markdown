---
title:  "Solución Máquina Oclat Blue Team"
date:   2024-03-03
categories: [CTF]
tags: [Oclat,Remediación,BlueTeam]
---
Se procede a realizar la solución de la máquina OCLAT, nivel fácil. 
`OCLAT`.

Mitigación de la vulnerabilidad. 

``` bash
# Opción 1
$ netdiscover
# Opción 2 Netdiscovet con un rango de ip
$ netdiscover -r 192.168.1.0/24
# Opción 3 NMAP
$ sudo nmap -sS 192.168.1.0/24
``` 

![image](/genes/oclat/netdiscover.png)

Identificamos la máquina vulnerable y nos enfocamos en ella, escaneo agresivo con nmap, se puede agresivo al estar en la red local, no tenemos un SOC que vaya a mandarnos a los de seguridad. 

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->