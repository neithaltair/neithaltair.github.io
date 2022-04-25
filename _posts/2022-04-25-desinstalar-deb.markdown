---
title:  "Desinstalar .deb Linux"
date:   2022-04-25
categories: [Tip]
tags: [Desinstalar,Linux,Deb]
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

*(1,1)*
