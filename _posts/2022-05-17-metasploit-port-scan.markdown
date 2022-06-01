---
title:  "Escaneo de IP y puertos con Metasploit"
date:   2022-05-17
categories: [Linux]
tags: [Linux,Comandos,Bash]
---

Implementación de search `udp_sweep`. 

``` bash

$ sudo msfdb init && msfconsole

msf6 > search udp_sweet

msf6 > use auxiliary/scanner/discovery/udp_sweep

```

![image](/genes/laboratorio/1.png)

Para el escaneo de puertos `portscan`

``` bash

msf6 > search portscan

msf6 > use auxiliary/scanner/portscan/syn

```

*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->