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
``` 
