---
title:  "Solución Máquina Oclat Blue Team"
date:   2024-03-03
categories: [CTF]
tags: [Oclat,Remediación,BlueTeam]
---
Se procede a realizar la solución de la máquina OCLAT, nivel fácil. 
`OCLAT`.

Mitigación de la vulnerabilidad. 

Primero intento lograr conectarme en la máquina a través de ssh, pero no funcionan los datos encontrados en el ftp. 

Procedo a enumerar los servicios con las versiones, posteriormente con `searchsploit` identifíco posibles exploits. 

``` bash
# 
$ sudo apt install exploitdb

$ searchsploit vsftpd 3.0.3
$ searchsploit openssh 7.2p2
 linux/remote/40136.py
# No recordaba cual era la ruta donde esta el script.
# buscamos el archivo, ingresamos el posible path y 2>/dev/null para que no muestre los errores.  
$ find / -name "40136.py" -path "*/linux/remote/*" 2>/dev/null
# la ruta.
/usr/share/exploitdb/exploits/linux/remote/40136.py
``` 

![image](/genes/oclat/netdiscover.png)

Identificamos la máquina vulnerable y nos enfocamos en ella, escaneo agresivo con nmap, se puede agresivo al estar en la red local, no tenemos un SOC que vaya a mandarnos a los de seguridad. 

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->