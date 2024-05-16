---
title:  "Scripting en BASH"
date:   2024-05-13
categories: [Bash]
tags: [Bash, Scripting, Linux]
---
`Scripting en Bash`

* Creación de una menú con GETOPTS que permita alternar entre una serie de funciones existentes.
* Creación de funciones.
* Uso y empleo de condiciones en BASH.
* Control de flujo de programa frente a CTRL+C

`trap ctrl_c INT` = establece una acción específica que se ejecutará cuando se reciba la señal de interrupción (SINGINT), que normalmente se genera cuando el usuario presiona CTRL+C en la terminal. 

Estructura de comando trap
``` bash
trap accion señal
trap ctrl_c INT
``` 

`¿Por qué la señal es INT?`
La señal INT en el comando, es el nombre de la señal de interrupción en el sistema UNIX/LINUX. 

La señal INT (INTERRUPT) es generada cuando el usuario presiona ctrl+c en la terminal. Concida para solicitar la terminación de un programa o para abortar una operación en curso de manera controlada. 


`CURL`
``` bash
# Curl es la herramienta.
# -X GET: especifica el método HTTP a utilizar en la solicitud. En este caso 'GET' indica que se quiere realizar una solicitud GET.
$ curl -X GET https://htbmachines.github.io
$ curl -X GET https://htbmachines.github.io/bundle.js
``` 

`Utilidad = js-beautify`

```bash
$ curl -s -X GET https://htbmachines.github.io/bundle.js > bundle.js
# sponge se utiliza para "absorber" la salida estándar y luego escribirla en un archivo una vez que la entrada estándar ha terminado de leerse. Esto puede ser especialmente útil cuando se necesita modificar un archivo y luego guardar los cambios en el mismo archivo
$ cat bundle.js | js_beautify | sponge bundle.js
# El comando de arriba no me funcionó
$ js_beutify bundle.js | sponge bundle.js

```