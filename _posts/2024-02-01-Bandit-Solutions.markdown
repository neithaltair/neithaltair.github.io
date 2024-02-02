---
title:  "Overthewire Wargames <Bandit>"
date:   2024-02-01
categories: [Bandit]
tags: [Bandit1, SSH, Wargames]
---
Insertar Video
[Crear carpeta compartida VirtualBox](https://youtu.be/ZQZFmZz-v7s)

#Resaltar
Escaneo Red con `NMAP`. 

#Insertar imagenes
![image](/genes/malware/additions.png)


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

#Sol 2 lv
$ cat /home/bandit/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
$ cat ./- 
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
$ cat $(pwd)/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

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

#Sol 5-6
# encontrar archivo, no ejecutable de 1033 bytes ||| man find tamanio archivo 
$ find . -type f ! -executable -size 1033c | xargs file
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
$ find . -type f ! -executable -size 1033c | xargs file | xargs
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

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

# Sol 7-8
# The password for the next level is stored in the file data.txt next to the word millionth
$ sshpass -p "z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S" ssh bandit7@bandit.labs.overthewire.org -p 2220

$ cat data.txt | grep "millionth"
millionth   TESKZC0XvTetK0S9xNwm25STk5iWrBvP
$ cat data.txt | grep "millionth" | awk 'NF{print $NF}' # Imprimir el argumento final. 
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
$ cat data.txt | grep "millionth"  | awk '{print $2}' # Imprimir segundo argumento. 
TESKZC0XvTetK0S9xNwm25STk5iWrBvP


# Sol 8-9
# The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
$ sshpass -p "TESKZC0XvTetK0S9xNwm25STk5iWrBvP" ssh bandit8@bandit.labs.overthewire.org -p 2220



```

bandit0 = NHSXQwcBdpmTEzi3bvBHMM9H66vVXjL
