---
title:  "Frida-Server SSL Pinning"
date:   2024-06-19
categories: [SSL Pinning]
tags: [SSL Pinning, Server, Pentesting]
---
`Descargar e instalar frida server en dipositivo rooteado`. 

1. Dispositivo rooteado. 
2. Activar depuración USB en el celular (Modo desarrollador). 
3. Identificar arquitectura del dispositivo para tener el server de frida en el dispositivo.

``` bash
> adb shell getprp ro.product.cpu.abi
```

4. Tener instalado Magisk (Solo si la aplicación no permite la ejecución en dispositivos root). 

``` bash
> adb push frida-server-16.3.3-android-arm64 /data/local/tmp
#Ejecutar frida server en el dispositivo en la ruta /data/local/tmp
> ./frida-server-16.3.3-android-arm64 &
```

5. Configurar la máquina en puente, para poder interceptar con burp. 

`En el PC`.

1. Instalar frida-tools. 

2. Instalar objection.

``` bash
> gitclone https://www.github.com/objection.
> pip3 install objection
> pip3 install -r requirements.txt
> python3 setup.py
> sudo pip3 install --upgrade objection

sudo docker run --net host -it withsecurelabs/drozer console connect --server localhost
``` 



