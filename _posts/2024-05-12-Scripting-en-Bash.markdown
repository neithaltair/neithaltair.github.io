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

