---
title:  "Instalar/desinstalar Aplicaciones"
date:   2022-04-25 - 2023-04-05
categories: [Comandos]
tags: [Desinstalar,Instalar,Linux,Deb]
---

Comandos para desinstalar .deb en linux. 

|**- Encontrar ruta completa del package.**

```bash
$ dpkg -l | grep -i my-package
```
**- Desinstalar usando apt.** 

```bash
$ sudo apt remove my-app
```
**-Opciones adicionales.**

```bash
sudo apt-get remove packagename

dpkg --remove packagename
```

Comandos para instalar .bin en linux.

**-Comando para instalación y ejecución**

```bash
sudo chmod a+x name_of_file.bin

./name_of_file.bin
```

*(1,1)*
