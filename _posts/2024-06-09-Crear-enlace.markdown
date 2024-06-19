---
title:  "Crear enlace simbólico para Postman"
date:   2024-06-09
categories: [Bash]
tags: [Bash, Scripting, Linux]
---
`Crear enlace`

``` bash
# El comando crea un enlace simbólico para que llamando al ejecutable de postman ubicado en /opt/postman, quede en el directorio de /usr/bin y pueda ejecutarse desde terminal solo colocando postman.
sudo ln -s /opt/Postman/Postman /usr/bin/postman

sudo pip3 install mitmproxy2swagger
sudo apt-get install docker-compose
sudo apt-get install docker.io
sudo apt install golang-go

#Establecer nueva contraseña para el usuario. 
sudo passwd kali
# Agregar el usuario  un grupo específico sin eliminarlo de los otros grupos a los que pertenece. 
sudo usermod -a -G sudo neith

#Instalación y enlace simbólico para jwt_tool
cd /opt
sudo git clone https://github.com/ticarpi/jwt_tool
sudo chmod +x jwt_tool.py
sudo ln -s /opt/jwt_tool/jwt_tool.py /usr/bin/jwt_tool 


#Instalación y enlace para kiterunner
sudo git clone https://github.com/assetnote/kiterunner.git
cd kiterunner
sudo make build
cd dist
sudo ln -s /opt/kiterunner/dist/kr /usr/bin/kr


#Arjun
sudo git clone https://github.com/s0md3v/Arjun.git
or
sudo pip3 install arjun
# In case burp
sudo apt install zaproxy 
``` 

