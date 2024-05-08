---
title:  "Overthewire Wargames <Bandit>"
date:   2024-02-01
categories: [Bandit]
tags: [Bandit1, SSH, Wargames]
---
`SSH =` protocolo y programa que lo implementa cuya función principal es el acceso remoto a un servidor por medio de un canal seguro.  

``` bash
#Validar si servidor esta activo
$ ping bandit.labs.overthewire.org

#conexión por ssh usuario bandit0 puerto específico. 
$ ssh bandit0@bandit.labs.overthewire.org -p 2220 
$ sshpass -p "PASSWORD" ssh bandit0@bandit.labs.overthewire.org -p 2220

#Solución primer nivel
$ ls
$ cat readme
NHSXQwcBdpmTEzi3bvBHMM9H6
```

``` bash
#Sol 2 lv
$ cat /home/bandit/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
$ cat ./- 
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
$ cat $(pwd)/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
``` 

``` bash
#Sol 3 Lv
$ cat "spaces in this file"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
$ cat ./spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
$ cat /home/bandit2/spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
$ cat s*
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
$ cat /home/bandit2/* 
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
``` 

``` bash
#Sol 3-4 
$ ls
$ cd inhere/
$ ll
$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
$ cat /home/bandit3/inhere/.hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
$ cat /home/bandit3/inhere/.*
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
``` 

``` bash
#Sol 4-5
# human Redeable
$ find . -type f | grep "\-file" | xargs file
./-file01: data
./-file02: data
./-file08: data
./-file06: data
./-file00: data
./-file04: data
./-file05: data
./-file07: ASCII text
./-file03: data
./-file09: data
$ cat /home/bandit4/inhere/-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
``` 

``` bash
#Sol 5-6
# encontrar archivo, no ejecutable de 1033 bytes ||| man find tamanio archivo 
$ find . -type f ! -executable -size 1033c | xargs file
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
$ find . -type f ! -executable -size 1033c | xargs file | xargs
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
``` 

``` bash
#Sol 6-7
#the password for the next level is stored somewhere on the server and has all of the following properties:
    #owned by user bandit7
    #owned by group bandit6
    #33 bytes in size
$ sshpass -p "P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU" ssh bandit6@bandit.labs.overthewire.org -p 2220

$ find . -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
./var/lib/dpkg/info/bandit7.password
$ find . -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null | xargs cat
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
``` 

``` bash
# Sol 7-8
# The password for the next level is stored in the file data.txt next to the word millionth
$ sshpass -p "z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S" ssh bandit7@bandit.labs.overthewire.org -p 2220

$ cat data.txt | grep "millionth"
millionth   TESKZC0XvTetK0S9xNwm25STk5iWrBvP
$ cat data.txt | grep "millionth" | awk 'NF{print $NF}' # Imprimir el argumento final. 
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
$ cat data.txt | grep "millionth"  | awk '{print $2}' # Imprimir segundo argumento. 
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
``` 

``` bash
# Sol 8-9
# The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
$ sshpass -p "TESKZC0XvTetK0S9xNwm25STk5iWrBvP" ssh bandit8@bandit.labs.overthewire.org -p 2220
#sort para ordenar de manera alfabetica el contenido del archivo y uniq -u para identificar la línea que se repite una sola vez. 
$ sort data.txt | uniq -u 
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
``` 

``` bash
# sol 9-10  
# The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
$ sshpass -p "EN632PlfYiZbn3PhVK3XOGSlNInNE00t" ssh bandit9@bandit.labs.overthewire.org -p 2220
# strings permite ver los caracteres legibles para humanos dentro de cualquier archivo. Se complementa con grep para identificar la flag. 
$ strings data.txt | grep "="
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
>8=6
# Tail es para listar los últimos elementos, comando contrario sería Head. 
$ strings data.txt | grep "=====" | tail -n1 | awk 'NF{print $NF}' 
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
``` 

``` bash
# sol 10-11
#  The password for the next level is stored in the file data.txt, which contains base64 encoded data
$ sshpass -p "G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s" ssh bandit10@bandit.labs.overthewire.org -p 2220
# base64 no es un algoritmo de cifrado, se decodifica fácilmente, debido a esto no debe ultizarse como un métodod de cifrado seguro.
$ cat data.txt
$ base64 -d data.txt
6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
``` 

``` bash
#sol 11-12
#The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
$ sshpass -p "6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM" ssh bandit11@bandit.labs.overthewire.org -p 2220
#Forma sencilla de root 13, página web para rotar 13 posiciones el escrito.
#Forma desde bash para rotar
$ abcdefghijklm nopqrstuvwxyz
$ cat data.txt | tr '[A-Za-z]''[N-ZA-Mn-za-m]' | awk '{print $NF}'
$ JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
``` 

``` bash
#sol 12-13
#The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)
$ sshpass -p "JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv" ssh bandit12@bandit.labs.overthewire.org -p 2220
# comandos para creacion de carpetas temporales
$ mkdir /tmp/neithaltair
$ cp data.txt /tmp/neithaltair
# Que es el sistema hexadecimal, sistema de enumeración posicional que tiene como base el 16. 

# sponge sobreescribe el archivo ya creado con la información nueva
$ cat data.txt | xxd -r | sponge data.txt
$ cat data.txt | xxd -r > xxd.txt
# Muestra el archivo en hexadecimal
$ cat /etc/hosts | xxd 

# Muestra el archivo con todos los hexadecimales juntos
$ cat /etc/hosts | xxd -ps

#Compactar en una única línea con xargs
$ cat /etc/hosts | xxd -ps | xargs

#Compactar y quitar los espacios con tr
$ cat /etc/hosts | xxd -ps | xargs | tr -d ' '

# Con -r se hace el proceso inverso de lo que se ha puesto en hexadecimal
$ cat /etc/hosts | xxd -ps | xargs | tr -d ' ' >> etchosts
$ cat etchosts | xxd -ps -r

#Se ejecuta file para tener una idea del archivo
$ file xxd
#Se identifican los magic numbers del archivo (list of signatures) para identificar la extensión del archivo.
$ ghex xxd  
#Se establece la extensión del archivo de acuerdo con los magic numbers
$ mv xxd xxd.gz
#Se descomrpime el archivo
$ 7z x xxd.gz
# el archivo descomprimido es data2.bin
# Se realiza el mismo proceso de identificación del archivo con los magic numbers 42 5A 68, extensión de archivo .bz2
# Se descomprimen los archivos hasta el data9.bin
$ cat data9.bin
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
``` 

``` bash
#Sol 13-14
#The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.
$ sshpass -p "wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw" ssh bandit13@bandit.labs.overthewire.org -p 2220

# La llave privada SSH es un archivo que se utiliza para autenticar la identidad del usuario al conectarse a un servidor remoto.

#se ejecuta el comando pero no permitia la conexión con bandit14, el error era que no se estaba asignando el puerto del ssh, por defecto es 22, pero en este caso tenemos configurado el 2220.
$ ssh -i sshkey.private bandit14@localhost -p 2220
$ cat /etc/bandit_pass/bandit14
``` 

`Netcat: nc`= netcat es una herramienta de red que permite a través de intérprete de comandos y con una sintaxis sencilla abrir puertos TCP/UDP en un host, asociar a una shell a un puerto en concreto y forzar acciones. 

Cheat Sheet Netcat:
https://gist.github.com/cmbaughman/c91f41ba7b2cf71106f1

``` bash
#Sol 14-15
#The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

$ sshpass -p "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq" ssh bandit14@bandit.labs.overthewire.org -p 2220

#Se establece la conexión por netcat al propio servidor por el puerto 30000
$ nc localhost 30000 
$ fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

Correct! 
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

``` 

`Identificar los puertos expuestos en linux = ss -nltp`

``` bash
#Sol 15-16
# The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

#Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…
$ sshpass -p "jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt" ssh bandit15@bandit.labs.overthewire.org -p 2220

export TERM=xterm

$ `Identificar los puertos expuestos en linux = ss -nltp`
$ ss -nltp

# Hacer uso de which para identificar la ruta absoluta de un comando que queremos identificar.
$ which nc
/bin/nc

$ which ncat
/usr/bin/ncat

$ ncat --help
$ ncat --help | grep "ssl"
$ cat --ssl 127.0.0.1 30001

--ssl   Connect or listen with SSL
--ssl-cert  Specify SSL certificate file (PEM) for listening
--ssl-key   Specify SSL private key (PEM) for listening
--ssl-verify    Verify trust and domain name of certificates
--ssl-trustfile PEM file containing trusted SSL certificates
--ssl-ciphers   Cipherlist containing SSL ciphers to use
--ssl-alpn  ALPN protocol list to use.

$ ncat --ssl 127.0.0.1 3001 
$ jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1

``` 

**Crear un escritorio temporal = mktemp -d**

```bash
# solution 16-17 
# The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

sshpass -p "JQttfApK4SeyHwDlI9SXGR50qclOAil1" ssh bandit16@bandit.labs.overthewire.org -p 2220

export TERM=xterm

# Sumamente importante la doble comilla para imprimir de manera correcta el bucle for
#!/bin/bash
for i in $(seq 1 10); do
    echo "test $i"
done;

#!/bin/bash
for port in $(seq 31000 32000); do
 (echo '' > /dev/tcp/127.0.0.1/$port) 2>/dev/null && echo "[+] $port abierto"
done

#aún no funciona, creo que llevo 3-4 días probando de que funcione el código en máquina virtual, en máquina física, en linux subsystem for linux, en todo!, y al avanzar en el video, veo que hay nmap.... :). 

nmap --open -T5 -v -n -p31000-32000 127.0.0.1
# T5 Escaneo agresivo. 
# -n: Esta opción indica a Nmap que no realice resolución de DNS durante el escaneo. Esto significa que Nmap no intentará resolver las direcciones IP de los hosts encontrados en nombres de dominio. Utilizar esta opción puede hacer que el escaneo sea más rápido y evitar problemas de resolución de nombres de dominio.

ncat --ssl 127.0.0.1 31790

JQttfApK4SeyHwDlI9SXGR50qclOAil1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

# Las claves privadas deben de contar con el privilegio 600
$ chmod 600 id_rsa

#Para localizar la clave id-rsa
$ cd ~/.ssh

#Una vez en el directorio .ssh, puedes listar los archivos utilizando el comando ls:
ls

#Si la clave id_rsa existe, aparecerá en la lista.

$ ssh -i id_rsa bandit17@bandit.labs.overthewire.org -p 2220

#Me logeo en el servidor usando la clave del id_rsa, pero en la ruta: "/etc/bandit_pass/bandit17", es posible ver la clave del nivel. 
VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e

#Se valida la clave -- 200 OK
```

```bash
#There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

#NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

#Hacemos uso del diff para identificar las líneas que cambian entre los dos archivos. 
$ diff passwords.old passwords.new

hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg

$ ssh -p "hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg" ssh bandit18@bandit.labs.overthewire.org -p 2220
```
Ejemplos de uso del comando diff.
https://eltallerdelbit.com/comando-diff-ejemplos/

```bash
#The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
sshpass -p "hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg" ssh bandit18@bandit.labs.overthewire.org -p 2220

#Es posible agregar un comando al final del intento de conexión y que se ejecute antes de que el bashrc cierre la conexión. 
sshpass -p "hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg" ssh bandit18@bandit.labs.overthewire.org -p 2220 bash

#Con eso se abre una bash, es persistente y es posible acceder a los ficheros y directorios. 
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```

```bash
#To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
sshpass -p "awhqfNnAbc1naukrpqDYcF95h7HoMTrC" ssh bandit19@bandit.labs.overthewire.org -p 2220 bash

#SUID es un permiso de archivo especial para archivos ejecutables que permite a otros usuarios ejecutar el archivo con los permisos efectivos del propietario del archivo. SGID, por el contrario, es un permiso de archivo especial que también se aplica a los archivos ejecutables y permite a otros usuarios heredar el GID efectivo del propietario del grupo de archivos.

#SUID significa “establecer ID de usuario” (Set owner User ID) y SGID significa “establecer ID de grupo” (Set Group ID up on execution).

export TERM=xterm
# Para ejecutar el archivo como si fuera bandit20 se hace uso del bash -p
$ ./bandit20-do bash -p

$ whoami
#Otra opción sería el ./bandit20-do sh, pero no funciono, al hacer el whoami seguía apareciendo como bandit19

$ cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```

```bash
#There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

sshpass -p "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" ssh bandit20@bandit.labs.overthewire.org -p 2220

export TERM=xterm

# Crear comunicación a traves de netcat, para abrir un puerto a la escucha. 

#Se abren dos ventanas de terminal cada una conectada al nivel bandit20

#Ventana 1
# netcat -n =  Indica que se debe desactivar la resolución de DNS para evitar la resolución inversa de direcciones IP / es para no obtener el dominio de la ip.
# l = listen = Indica que netcat debe estar en modo de escucha, es decir, esperará una conexión entrante en lugar de intentar establecer una conexión saliente.
# v = verbose =  Habilita el modo "verbose" (detallado), lo que significa que netcat imprimirá información detallada sobre las conexiones.
# p = puerto= Especifica el puerto en el que netcat debe escuchar conexiones entrantes. En este caso, está configurado para escuchar en el puerto 4646
$ nc -nlvp 4646
$ VxCazJaVykI6W36BkBU0mJTCM8rR95XT

#Ventana 2
$ ./suconnect 4646
```
[image](/genes/bandit/bandit20.png)


```bash
#A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed. 
sshpass -p "NvEJF7oVjkddltPSrdKEFOllh9V1IBcq" ssh bandit21@bandit.labs.overthewire.org -p 2220

#Cron es un administrador de tareas de Linux que permite ejecutar comandos en un momento determinado, por ejemplo, cada minuto, día, semana o mes. Si queremos trabajar con cron, podemos hacerlo a través del comando crontab.

#El formato de configuración de cron es el siguiente: Minuto Hora Dia-del-Mes Mes Dia-de-la-Semana Comando-a-Ejecutar

#El intervalo de tiempo se especifica mediante 5 campos que representan, de izquierda a derecha:

#Minutos: de 0 a 59.
#Horas: de 0 a 23.
#Día del mes: de 1 a 31.
#Mes: de 1 a 12.
#Día de la semana: de 1 a 6 lunes a sábado (1=lunes, 2=martes, etc.) y 0 o 7 el domingo.
#Si quisiéramos especificar todos los valores posibles de un parámetro (minutos, horas, etc.) podemos hacer uso del asterisco (*). Esto implica que si en lugar de un número utilizamos un asterisco, el comando indicado se ejecutará cada minuto, hora, día de mes, mes o día de la semana, como en el siguiente ejemplo:

#* * * * * /home/user/script.sh

export TERM=xterm

$ cd /etc/cron.d/
$ ls -la
# Leer el contenido del archivo cronjob_bandit22
$ cat cronjob_bandit22

@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

#Leer el contenido del script que se ejecuta
$ cat /usr/bin/cronjob_bandit22.sh &> /dev/null

#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

# Acceder al directorio y al archivo que se identifica en el script para identificar la contraseña
$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```

```bash
sshpass -p "WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff" ssh bandit22@bandit.labs.overthewire.org -p 2220

#A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

#NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

$ cd /etc/cron.d/
$ cat cronjob_bandit23.sh

@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null

$ cat /usr/bin/cronjob_bandit23.sh

#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

$ echo I am user bandit 23 | md5sum | awk '{print $1}'

8ca319486bfbbc3663ea0fbe81326349

$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349

QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
```

```bash
sshpass -p "QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G" ssh bandit23@bandit.labs.overthewire.org -p 2220

#A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

#NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

#NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

export TERM=xterm

/var/spool/bandit24/foo
# Si se va a copiar un archivo dentro de la ruta seleccionada es necesario especificar que otros usuarios o grupos o TODOS pueden ejecutar el archivo
 
 # Creamos un directorio temporal
 $ mktemp -d
 /tmp/tmp.Hna6s3eBMy
#Vamos a crear una variable que apunte directamente al directorio temporal.
# Se almacena en la variable dir_name, el nombre del directorio creado. 
 $ dir_name=$(mktemp -d)
 /tmp/tmp.asd4j3j

 $ echo $dir_name
 /tmp/tmp.asd4j3j
#Se crea un script dentro de la ruta.  
 $ cd $dir_name
 /tmp/tmp.asd4j3j $

#Se le asignan los permisos de ejecución para otros, para todos al script
$ chmod +x script.sh
# Tamb se le dan permisos a otros usuarios sobre el directorio para que sea posible el escribir la contraseña dentro del directorio
$ chmod o+wx $dir_name

# Como todo se ejecuta bajo los permisos del usuario de bandit24, se realiza la lectura de la contraseña en la ruta de bandit_pass y se almacenará en la ruta del directorio temporal. Se le dan permiso de lectura a otros sobre el archivo para asegurar de que sea posible ver el contenido. 
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.OMPTnwSjfW/bandit24.log
chmod o+r /tmp/tmp.OMPTnwSjfW/bandit24.log

$ cp script.sh carga.sh
$ cp carga.sh /var/spool/bandit24/foo
# se ejecuta el watch -n 1 para ver el estado del directorio segundo a segundo.
/tmp/tmp.OMPTnwSjfW/$ watch -n 1 ls -l

VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar

```

Recurso para las tareas cron:

https://www.site24x7.com/es/tools/crontab/cron-generator.html

```bash
#A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
#You do not need to create new connections each time.

sshpass -p "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar" ssh bandit24@bandit.labs.overthewire.org -p 2220

export TERM=xterm

#1. La forma inicial puede ser el ejecutar un comando de bash para que se genere un listado de las combinaciones a utilizar. 

$ tempor=${mktemp -d}
$ cat $tempor
$ cd $tempor

$ for pin in {0000..9999}; do echo VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i; done > bf.txt

# Grep -v = excluir el match
# Grep -vE = excluir más de un match: grep -vE "first|second"
$ cat bf.txt | nc localhost 30002 | grep -vE "Wrong*|Please enter"

p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d
```

```bash
#Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

sshpass -p "p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d" ssh bandit25@bandit.labs.overthewire.org -p 2220

export TERM=xterm

#El truco de este nivel parte en que la implementación del more imprime todo el contenido del archivo al tener pocos caracteres, de manera que es necesario reducir el tamaño de la ventana del terminal para poder insertar nuevos valores y comandos. 

#Se realiza la búsqueda sobre el archivo de passwd para identificar que shell esta utilizando el usuario. 
$ cat /etc/passwd | grep "bandit26"
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

# Accedemos al archivo para validar su contenido. 
$ cat /usr/bin/showtext

#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0

#El more permite insertar comandos si no se ejecuta en su totalidad, cuando hay pocas líneas se puede reducir el tamaño de la terminal para que quede como en "ejecución".

#una vez se ejecuta y se despliega el banner de bandit26 se le da V para entrar al modo visual, se le da shift esc : , para poder ejecutar comandos.

# De manera que se procede a establecer el shell.
$ set shell=/bin/bash

# De nuevo se ejecuta el "ESC + shift + :" y se ejecuta un shell, como ya se estableció que la shell será una bin bash, se abrirá la terminal. 

$ whoami
bandit26

$ cat /etc/bandit_pass/bandit26
c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1
```

```bash
#Good job getting a shell! Now hurry and grab the password for bandit27!

bandit26@bandit:$ ls

text.txt
bandit27-do

bandit26@bandit:$ ./bandit27-do whoami
bandit27

bandit26@bandit:$ ./bandit27-do cat /etc/bandit_pass/bandit27

YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS

```

```bash
sshpass -p "YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS" ssh bandit27@bandit.labs.overthewire.org -p 2220

#There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.

#Clone the repository and find the password for the next level.

# Se supone que se debe clonar el repositorio para poder encontrar la contraseña del siguiente nivel, pero es necesario utilizar el puerto 2220, y por defecto esta en el 22. 

$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo 

#Así funciona en el video, pero no en la práctica, de manera que vamos a probar con ssh://usuario@dominio.com:puerto/repositorio

$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
# Efectivamente era la solución.
$ cd repo
$ ls
$ cat README
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR

```

```bash
sshpass -p "AVanL161y9rsbcJIsFHuw35rjaOM19nR" ssh bandit28@bandit.labs.overthewire.org -p 2220

$ temp=$(mktemp -d)
$ cd $temp
$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
$ cd repo/

$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.
## credentials
- username: bandit29
- password: xxxxxxxxxx

$ git log
commit 14f754b3ba6531a2b89df6ccae6446e8969a41f3 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Oct 5 06:19:41 2023 +0000

    fix info leak

$ git show 14f754b3ba6531a2b89df6ccae6446e8969a41f3
 - username: bandit29
-- password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
+- password: xxxxxxxxxx

tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
```