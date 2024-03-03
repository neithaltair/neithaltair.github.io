---
title:  "Solución Máquina Oclat"
date:   2024-02-22
categories: [CTF]
tags: [Oclat,CTF,RedTeam]
---
Se procede a realizar la solución de la máquina OCLAT, nivel fácil. 
`OCLAT`.

Empezamos tranqui, enumeración de los hosts en la red: 

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

![image](/genes/oclat/ftpNmap.png)

Identificamos que el servicio FTP en el puerto 21 es vulnerable a login anonymous.
``` bash
# Opción adicional script para identificar el ftp anonymous
$ nmap -Pn -n -p21 -sV --script ftp-anon {IP}
``` 
![image](/genes/oclat/ftpLogin.png)

Nos logeamos, revisamos que archivos hay en la ruta, los descargamos y los leemos ;) 

![image](/genes/oclat/userRoot.png)

Identificámos el usuario root y el usuario USER, los cargamos y solucionado. 

![image](/genes/oclat/cargado.png)

`Conclusiones:`
**1**: Según la situación podemos o no podemos hacer ruido al realizar los escaneos, lo ideal es tratar de siempre hacer la menor cantidad de ruido posible. 
**2**: El servicio ftp se puede encontrar en impresoras un vector de ataque interesante sería la carga de archivos maliciosos.
**3**: La flag estaba bien, me tomo como 6 intentos darme cuenta de que el error era un 0 en lugar de una O. 

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->