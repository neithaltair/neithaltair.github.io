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

`1. trap ctrl_c INT` = establece una acción específica que se ejecutará cuando se reciba la señal de interrupción (SINGINT), que normalmente se genera cuando el usuario presiona CTRL+C en la terminal. 

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

`2. Utilidad = js-beautify`

```bash
$ curl -s -X GET https://htbmachines.github.io/bundle.js > bundle.js
# sponge se utiliza para "absorber" la salida estándar y luego escribirla en un archivo una vez que la entrada estándar ha terminado de leerse. Esto puede ser especialmente útil cuando se necesita modificar un archivo y luego guardar los cambios en el mismo archivo
$ cat bundle.js | js_beautify | sponge bundle.js
# El comando de arriba no me funcionó
$ js_beautify bundle.js | sponge bundle.js
# Se hace uso del parámetro -i para que no tenga en cuenta el capitalCase a la hora de buscar la palabra. 
$ cat bundle.js | grep -i "tenta"
```

`3. Creación de parámetros para el Script`

While getopts

`Getopts`: es una utilidad de bash para analizar opciones y argumentos pasados al script. 

```bash
#Indicadores
#Se pueden declarar variables con declare y con let. Se hace uso del parametro -i para indicar que será un valor integer. 
declare -i parameter_counter=0

#"m:h = especifíca las opciones que el script aceptará. en este caso las opciones son -m y -h. La m tiene dos puntos depués (un solo punto indica un argumento opcional, dos puntos indican uno obligatorio)."
while getopts "m:h" arg in; do
    case $arg in
        m) let parameter_counter+=1;;
        h) helpPanel;;
    esac
done

```

#Pendiente repasar a detalle la implementación del $OPTARG. entender mejor la parte de arg in. 