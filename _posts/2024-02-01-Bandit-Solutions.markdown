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

```bash
# solution 16-17 
# The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

sshpass -p "JQttfApK4SeyHwDlI9SXGR50qclOAil1" ssh bandit16@bandit.labs.overthewire.org -p 2220

export TERM=xterm


```
