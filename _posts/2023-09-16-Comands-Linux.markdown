---
title:  "Ejecución - instalación en carpeta /opt"
date:   2023-09-16
categories: [Tools]
tags: [Linux,Instalacion,opt]
---

``` bash
/opt/volatility$ mkdir volatility
/opt/Downloads$ mv volatility.zip /opt/volatility 
/opt/volatility$ cd volatility
/opt/volatility$ unzip volatility.zip
#Pasar todo el contenido de volatility a la carpeta actual
/opt/volatility$ mv volatility/* .

#Ejecución de Mobsf desde Docker
#Realizando una comparativa entre mobsf de manera local y el mobsf desplegado desde docker se evidencia que al ser desplegado desde docker se reportan una mayor cantidad de posibles vulnerabilidades asociadas a la apk analizada. 
docker pull opensecurity/mobile-security-framework-mobsf:latest
#Correr mobsf
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest



```