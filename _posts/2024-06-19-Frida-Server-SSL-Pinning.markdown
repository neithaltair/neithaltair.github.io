---
title:  "Frida-Server SSL Pinning/Drozer"
date:   2024-06-19
categories: [SSL Pinning, Drozer]
tags: [SSL Pinning, Server, Pentesting]
---
`Descargar e instalar frida server en dipositivo rooteado`. 

1. Dispositivo rooteado. 
2. Activar depuración USB en el celular (Modo desarrollador). 
3. Identificar arquitectura del dispositivo para tener el server de frida en el dispositivo.

``` bash
> adb shell getprp ro.product.cpu.abi
```

4. Tener instalado Magisk (Solo si la aplicación no permite la ejecución en dispositivos root, para agregar la aplicacion objetivo en la lista de denegación). 

``` bash
> adb push frida-server-16.3.3-android-arm64 /data/local/tmp
#Ejecutar frida server en el dispositivo en la ruta /data/local/tmp
> ./frida-server-16.3.3-android-arm64 &
```

5. Configurar la máquina en puente, para poder interceptar con burp. 

`En el PC`.

1. Instalar frida-tools. 

2. Instalar objection.

``` bash
> gitclone https://www.github.com/objection.
> pip3 install objection
> pip3 install -r requirements.txt
> python3 setup.py
> sudo pip3 install --upgrade objection
```

`Ejecutar comando de frida para listar aplicaciones`

``` bash
frida-ps -U -a

objection -g com.aplicacion.nombre explore

> android sslpinning disable
```


``` bash
> sudo nano drozer.sh
adb forward tcp:31415 tcp:31415
sudo docker run --net host -it withsecurelabs/drozer console connect --server localhost
#Se crea el enlace simbólico para que solo sea ejecutar nombre de la herramienta. 
sudo ln -S /home/kali/Documents/drozer/drozer.sh /usr/data/bin/drozer
``` 

`Instalación apk vulnerable`
```bash
$ adb install sieve.apk
Performing Streamed Install
adb: failed to install sieve.apk: Failure [INSTALL_FAILED_DEPRECATED_SDK_VERSION: App package must target at least SDK version 23, but found 17]

#Solución error
1. Descomprimir apk para modificar el apktool.yml y cambiar el valor del target SDK version.

sdkInfo:
  minSdkVersion: 18
  targetSdkVersion: 24

2. Empaquetar, firmar de nuevo el archivo y volver a instalar.

3. Funciona, sale un error de compatibilidad, pero funciona, 
```

`DROZER`

Package: Find the name of the package filtering by part of the name. 
```bash
#Encontrar el package filtrando por el nombre. 
dz> run app.package.list -f vulnerable

Attempting to run shell module
com.app.damnvulnerablebank (DamnVulnerableBank)

# Información básica del package. 
dz> run app.package.info -a com.app.damnvulnerablebank

Attempting to run shell module
Package: com.app.damnvulnerablebank
  Application Label: DamnVulnerableBank
  Process Name: com.app.damnvulnerablebank
  Version: 1.0
  Data Directory: /data/user/0/com.app.damnvulnerablebank
  APK Path: /data/app/~~0njZ5wMIcY8pNtm9UfJCSA==/com.app.damnvulnerablebank-hJKz3GQoPmNBR64j0Y7gCg==/base.apk
  UID: 10260
  GID: [3003]
  Shared Libraries: [/system/framework/android.test.base.jar]
  Shared User ID: null
  Uses Permissions:
  - android.permission.INTERNET
  - android.permission.USE_BIOMETRIC
  - android.permission.USE_FINGERPRINT
  - android.permission.POST_NOTIFICATIONS
  Defines Permissions:
  - None


#Leer manifest
dz> run app.package.manifest com.app.damnvulnerablebank

Attempting to run shell module
<manifest versionCode="1"
          versionName="1.0"
          compileSdkVersion="29"
          compileSdkVersionCodename="10"
          package="com.app.damnvulnerablebank"
          platformBuildVersionCode="29"
          platformBuildVersionName="10">
  <uses-sdk minSdkVersion="21"
            targetSdkVersion="29">
  </uses-sdk>


#Superficie de ataque
dz> run app.package.attacksurface com.app.damnvulnerablebank

Attempting to run shell module
Attack Surface:
  6 activities exported
  0 broadcast receivers exported
  0 content providers exported
  0 services exported


#Activities
# listar actividades exportadas
run app.activity.info -a com.app.damnvulnerablebank

Attempting to run shell module
Package: com.app.damnvulnerablebank
  com.app.damnvulnerablebank.CurrencyRates
    Permission: null
  com.app.damnvulnerablebank.SendMoney
    Permission: null
  com.app.damnvulnerablebank.ViewBalance
    Permission: null
  com.app.damnvulnerablebank.SplashScreen
    Permission: null
  androidx.biometric.DeviceCredentialHandlerActivity
    Permission: null
  com.google.firebase.auth.internal.FederatedSignInActivity
    Permission: com.google.firebase.auth.api.gms.permission.LAUNCH_FEDERATED_SIGN_IN
```

El valor 'android:exported' de un componente de actividad exportado está configurado en 'true' en el archivo AndroidManifest.xml.

```xml
<activity android:exported="true" android:name="com.app.damnvulnerablebank.SendMoney">
<activity android:exported="true" android:name="com.app.damnvulnerablebank.ViewBalance"/>
<activity android:exported="true" android:name="androidx.biometric.DeviceCredentialHandlerActivity" android:theme="@style/DeviceCredentialHandlerTheme"/>

#Configuración de <activity> de manera correcta.
<activity android:name="com.app.damnvulnerablebank.ResetPassword"/>
<activity android:name="com.app.damnvulnerablebank.ViewBeneficiary"/>
```

```bash
#Start Activity
dz> run app.activity.start --component com.app.damnvulnerablebank com.app.damnvulnerablebank.CurrencyRates
dz> run app.activity.start --component com.app.damnvulnerablebank com.app.damnvulnerablebank.SendMoney
dz> run app.activity.start --component com.app.damnvulnerablebank com.app.damnvulnerablebank.ViewBalance
dz> run app.activity.start --component com.app.damnvulnerablebank com.app.damnvulnerablebank.SplashScreen


#Start activity with adb
adb shell am start -n com.app.damnvulnerablebank/com.app.damnvulnerablebank.SendMoney

#Content provider / Services
#list service
dz> run app.service.info -a com.app.damnvulnerablebank


```





