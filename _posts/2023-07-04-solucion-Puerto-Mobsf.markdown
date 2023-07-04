---
title:  "Solución puerto Mobsf"
date:   2023-07-04
categories: [Tools]
tags: [RedTeam,Mobsf,Settings]
---

Durante el uso de mobsf en el puerto 8000, identifique que a pesar de haber cerrado la terminal, el proceso no se cerró de la manera adecuada y el puerto 8000 seguía ocupado al intentar ejecutar la herramienta. 

De manera que me toco revisar que procesos pudieron quedar pegados al puerto y "matarlos". 


``` bash
#Verificar si hay algún proceso en ejecución que esté utilizando el puerto. 
sudo lsof -i :8000

#Una vez identificados los procesos, con la identificación del PID los cierro. 
kill 446203 
```

Solucionado, el puerto vuelve a estar disponible. 

![image](/genes/memes/estoyAprendiendo.png)

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->