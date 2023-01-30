---
title:  "Comandos Linux"
date:   2022-05-17
categories: [Linux]
tags: [Linux,Comandos,Bash]
---

1) Dispositivos conectados en la misma red. 
``` bash
$> arp 
```

2) Obtener información de un usuario en Linux. 
``` bash
$> sudo apt install finger
$> finger <username> 
```

3) Cambiar contraseña de usuarios
``` bash
$> sudo passwd <username>
$> passwd
```

4) Zip - unzip
``` bash
$> zip comprimido test* 
$> unzip comprimido
```

5) Comparar y encontrar diferencia entre dos archivos. 
``` bash
$> cmp test1 test2 
$> diff test1 test2 
```

6) Find
``` bash
$> sudo find / -name "archivo*" 
# Encontrar archivos ocultos
$> sudo find . -type f -name ".*"
# Directorios vacíos
$> find . -type f -empty
# Todos los archivos ejecutables
# -perm = permisos de los archivos
$> find . -perm /a=x
```

7) Ip, grep, awk
``` bash
$> ip a | grep eth0 | grep inet | awk '{print $2}'
10.0.2.15/24
```

8) DNS Server
``` bash
$> resolvectl status
```

9) ping
``` bash
$> ping -c 3 google.com
#Especificar tamaño del paquete
$> ping -c 3 -s 500 google.com
```

10) Puertos abiertos en la maquina netstat
``` bash
$> netstat 
$> ss tulpn
```

11) uname Información del sistema operativo
``` bash
$> uname -a
$> sudo apt install neofetch
$> neofetch
```

12) procesos en la máquina. 
``` bash 
$> ps 
$> htop
#Matar proceso en la maquina
$> kill -9 <processID> #-9 para indicar que se matará el proceso. 
```

13) historial de comandos en la consola
``` bash
$> history
```





*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->