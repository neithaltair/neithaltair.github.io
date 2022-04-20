---
title:  "Taller Metasploit"
date:   2022-04-18
categories: [Laboratorio]
tags: [Linux, Bash, Metasploit, Metasploitable2]
---
##Laboratorio Metasploit.##

`Objetivo`: realizar la explotación de la vulnerabilidad CVE-2011-0762 en el servicio VSFTPD V2.3.4 para conseguir una shell e interactuar con el servidor vulnerado, haciendo uso de las herramientas Metaesploitable2 y el SO Kali Linux. 

**1.** Configuración de las maquinas virtuales, se establece la configuración de **Network Adapter** en **NAT**.

<!-- IMAGEN -->
![image](/genes/meta/1.png)

**2.** Desde la maquina Kali se realiza un escaneo de la red para identificar la IP de la maquina víctima (se hace uso de un script personal desarrollado en Bash). 

<!-- IMAGEN -->
![image](/genes/meta/reconocimientoRed.png)

**3.** Una vez identificada la maquina victima con la **Ip 192.168.36.135**, se realiza la ejecución del comando `sudo nmap -sV --script vulners 192.168.36.135` para identificar los servicios del equipo y posibles vulnerabilidades. 

Se logra identificar el servicio VSFTPD 2.3.4  en el puerto 21. 

![image](/genes/meta/3.png)

**4.** Desde Metasploitable se realiza la busqueda del servicio, logrando identificar el exploit `exploit/unix/ftp/vsftpd_234_backdoor`, se ejecuta el comando `show options` para ver las opciones de configuración. 

![image](/genes/meta/4.png)

**5.** Se pueden ver las opciones `RHOST = para indicar IP o hostname del servidor` y `RPORT que por defecto marcara el puerto 21`.

   **5.1** Se ejecuta el comando `show payloads`. 
   **5.2** Se indica el payload a usar: `use payload payload/cmd/unix/interact`
   **5.3** Se ejecuta el ataque. 

![image](/genes/meta/5.png)

**6.** Una vez comprometido el sistema, se realiza ejecución de comandos para comprobar el acceso al sistema. `Se evidencia la IP con el comando ip a`. 

![image](/genes/meta/6.png)

**7.** Con el comando `uname -a` se obtiene la información concreta del SO. 
    **7.1** Con el comando `useradd -o --uid 0 neith` se realiza la creación de un nuevo usuario en el sistema. 
    **7.2** Al usuario neith se le asigna la contraseña altair con el comando `echo neith:altair | chpasswd`

![image](/genes/meta/7.png)

**8.** A través de la herramienta telnet se establece conexión con la maquina victima y se realiza login con el usuario creado. 

![image](/genes/meta/8.png)

**9.** Con el comando `cat /etc/passwd` se validan los usuario del sistema. 

![image](/genes/meta/9.png)

<!-- BLOQUE DE CODIGO
``` bash
``` -->
*(1,1)*
