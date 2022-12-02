---
title:  "Solucion Juice Shop"
date:   2022-12-01
categories: [JuiceShop]
tags: [JuiceShop,Documento]
---

**PRUEBA DE INGRESODOCUMENTACI´ON**

**Plataforma Juice Shop**

![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image1.png){width="1.575in"
height="1.8888888888888888in"}

> **Neith Altair Machuca Bernal**
>
> **~~´Indice~~** 1
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image1.png){width="0.4722222222222222in"
> height="0.5666655730533683in"}
>
> **1. Herramientas** **2** 1.1. BurpSuite . . . . . . . . . . . . . . .
> . . . . . . . . . . . . . . . . 2 1.2. ExifTool . . . . . . . . . . .
> . . . . . . . . . . . . . . . . . . . . . 2 21.3. Dirbuster . . . . .
> . . . . . . . . . . . . . . . . . . . . . . . . . .
>
> 1.4. ParrotOS . . . . . . . . . . . . . . . . . . . . . . . . . . . .
> . . . 2
>
> **2. Documentaci´on** **3** 2.1. Nivel 1 . . . . . . . . . . . . . . .
> . . . . . . . . . . . . . . . . . . 3 2.2. Nivel 2 . . . . . . . . . .
> . . . . . . . . . . . . . . . . . . . . . . . 8 2.3. Nivel 3 . . . . .
> . . . . . . . . . . . . . . . . . . . . . . . . . . . . 13

+--------+--------------------+-----+-------------------------+
| **1.** | > **Herramientas** | > 2 | ![](vertopal_b4e60213ff |
|        |                    |     | 364c8292ac9ef499a8fa6d/ |
|        |                    |     | media/image1.png){width |
|        |                    |     | ="0.4722222222222222in" |
|        |                    |     | height=                 |
|        |                    |     | "0.5666655730533683in"} |
+--------+--------------------+-----+-------------------------+

Las herramientas utilizadas para la resoluci´on de la prueba fueron:

> Chrome.
>
> BurpSuite.
>
> Dirbuster.
>
> ExifTool.
>
> Parrot OS.
>
> **1.1.** **BurpSuite**
>
> es una herramienta para realizar auditor´ıas de seguridad a
> aplicaciones Web. Integra diferentes componentes de pentesting y
> funcionalidades para realizar las pruebas y permite combinar pruebas
> tanto autom´aticas como manuales. La herramienta Burp Suite est´a
> desarrollada y mantenida por la empresa PortSwigger.
>
> **1.2.** **ExifTool**
>
> ExifTool es un programa de software gratuito y de c´odigo abierto para
> leer, escribir y manipular im´agenes, audio, video y metadatos.
>
> **1.3.** **Dirbuster**
>
> es una aplicaci´on Java multi hilo dise˜nada para obtener por fuerza
> bruta los nombres de directorios y archivos en servidores Web.
>
> **1.4.** **ParrotOS**
>
> Parrot OS es una distribuci´on GNU/Linux basada en Debian con un
> enfoque en la seguridad inform´atica. Est´a dise˜nado para pruebas de
> penetraci´on, evaluaci´on y an´alisis de vulnerabilidades, an´alisis
> forense de computadoras, navegaci´on web an´onima, y practicar
> criptograf´ı.

+----------+----------------------+-----+------------------------+
| **2.**   | > **Documentaci´on** | > 3 | ![](                   |
|          |                      |     | vertopal_b4e60213ff364 |
|          |                      |     | c8292ac9ef499a8fa6d/me |
|          |                      |     | dia/image1.png){width= |
|          |                      |     | "0.4722222222222222in" |
|          |                      |     | height="               |
|          |                      |     | 0.5666655730533683in"} |
+==========+======================+=====+========================+
| **2.1.** | > **Nivel 1**        |     |                        |
+----------+----------------------+-----+------------------------+

> Una vez se accede a la p´agina, se consulta informaci´on para entender
> el funcionamiento. Como procedimiento inicial, se realiza la
> ejecuci´on de un DirBuster para obtener mediante fuerza bruta nombres
> de directorios y archivos en servidores Web.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image2.png){width="2.7555555555555555in"
> height="2.2041655730533685in"}\
> Imagen 1
>
> Como se evidencia, mediante el uso de esta herramienta se resuelve el
> reto Handling Error. Al evidenciar que el proceso toma mucho tiempo se
> cancela y se procede a revisar el c´odigo HTML de la p´agina, esta
> acci´on suele ser de ayuda y el paso principal en varios CTF.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image3.png){width="2.7555555555555555in"
> height="2.202777777777778in"}\
> Imagen 2
>
> 4
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image1.png){width="0.4722222222222222in"
> height="0.5666655730533683in"}
>
> Se revisan las fuentes de la p´agina y se identiﬁca el archivo
> main-es2018.js, en´el se revisan los path contenidos y se obtiene el
> app-score-board.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image3.png){width="3.15in"
> height="2.5194433508311462in"}\
> Imagen 3
>
> Para la soluci´on de los pr´oximos niveles se realiza la conﬁguraci´on
> del proxy y la herramienta BurpSusite.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image4.png){width="2.3625in"
> height="1.8902766841644794in"}\
> Imagen 4
>
> La soluci´on del nivel Zero Stars, se hace uso de la herramienta
> BurpSuit donde se intercepta el feedback enviado y se reemplaza el
> valor de rating por 0.
>
> En Privacy Policy, solo es necesario realizar el proceso de registro y
> acceder a la pol´ıtica de privacidad de la p´agina. En la ﬂag
> Repetitive Registration se
>
> 5
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image1.png){width="0.4722222222222222in"
> height="0.5666655730533683in"}
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image5.png){width="2.3625in"
> height="1.2930555555555556in"}\
> Imagen 5
>
> identiﬁca como pista el DRY (Dont Repit Yourself), para esta soluci´on
> se realiza el registro de un nuevo usuario y se evidencia error al
> comparar el campo Password con Repeat Password, como se evidencia en
> la captura se puede enviar una contrase˜na diferente en el primer
> campo y no realiza la correcta validaci´on.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image6.png){width="2.3625in"
> height="1.4097222222222223in"}\
> Imagen 6
>
> En Missing code, se revisa la informaci´on de la ﬂag, la cual dirige a
> photo Wall, all´ı se evidencia que una de las im´agenes no carga de
> manera correcta, se revisa c´odigo HTML y se evidencia la incorrecta
> implementaci´on del car´acter HASH en la ruta de la imagen, la
> representaci´on de esta caracter en una URL es /23, por lo que se
> reemplaza por los HASH y se logra ver la imagen del gato.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image7.png){width="1.575in"
> height="1.2944433508311461in"}\
> Imagen 7

  --- -----------------------------------------------------------------------------------------------------------------------------
  6   ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image1.png){width="0.4722222222222222in" height="0.5666655730533683in"}
  --- -----------------------------------------------------------------------------------------------------------------------------

> Para solucionar Conﬁdential Document se usa como orientaci´on el Code
> Snippet de la ﬂag, se accede al directorio /ftp y all´ı se pueden
> observar m´ultiples directorios y archivos, como acquisitions.md el
> cual da soluci´on a la ﬂag.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image8.png){width="2.3625in"
> height="1.8111100174978128in"}\
> Imagen 8
>
> La soluci´on de Bully chatbot, es el reiterado env´ıo de la palabra
> coupon al chat, para acceder a este chat es necesario estar logueado
> en la p´agina.
>
> ![](vertopal_b4e60213ff364c8292ac9ef499a8fa6d/media/image9.png){width="2.3625in"
> height="2.0375in"}\
> Imagen 9
>
> DOM XSS la explotaci´on de la vulnerabilidad XSS se realiza ejecutando
> el comando anexado en la ﬂag en la barra de busqueda, de igual forma
> se ejecuta el mismo comando para la ﬂag Bonus Payload.

+---+----------+--------------------------------------+
| 1 | \<iframe | > src=\"javascript:alert('xss ')\"\> |
+---+----------+--------------------------------------+

*(1,1)*