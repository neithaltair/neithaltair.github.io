---
title:  Backup Apk Mobile with adb"
date:   2023-05-05
categories: [Pentest]
tags: [Vulnerabilities,Mobile,Android,Backup]
---

 `Warning` Application data can be backed up [android:allowBackup=true]

```bash
#conectar el dispositivo
adb devices
adb connect [IP]

#Backup de todo el movil
adb backup -all
adb backup -apk nombre_paquete_aplicacion

#listar los paquetes del dispositivo. 
adb shell pm list packages

#Listar todas los paquetes basados en un usuario
adb shell pm list packages -3

#Para restablecer el bakcup
adb restore [nombre_del_paquete]

#Crear el backup y guardarlo
adb -apk [nombre_del_paquete] /home/user/{ruta}/backup.ab
```

**Para ver la información del backup generado**

```bash
#instalar sqlite3
sudo install sqlite3

#Comando para crear copia del archivo de backup en formato tar.
adb pull /ruta/al/archivo/backup.ab backup.tar

#descomprimir el archivo con el siguiente comando. 
tar -xvf backup.tar

#creara una carpeta llamada apps. Dentro de la carpeta estara el archivo databases con bases utilizadas.
sqlite nombre_base_de_datos.db

#Una vez abierta la consola sqlite, ejecutar comandos sql, para ver la informacion almacenada.
.tables
```




*(1,1)*