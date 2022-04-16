---
title:  "Nmap Personal"
date:   2022-04-16
categories: [Tip]
tags: [Linux,Bash]
---

![image](/genes/nmap/bash.jpeg)

Generación de código personal en Bash, permite realizar el escaneo de una red, identificando sistema operativo y puertos abiertos. (Tener en cuenta segmento de red a escanear). 

``` bash
#!/bin/bash
for range in $(seq 1 1 255)
 do
  ip=192.168.36.$range
  equipos=$(ping -b -c 1 $ip | grep "64 bytes" | cut -d " " -f 6 | tr -d "ttl=")
  if [ "$equipos" = "" ]
  then
    continue
  elif [ $equipos -le 64 ]
  then
          echo "Linux $ip"
  elif [ $equipos -ge 65 ]
  then 
        echo "Windows $ip"
  fi
  for port in $(seq 1 1000); do
  timeout 1 bash -c "echo > /dev/tcp/$ip/$port" 2>/dev/null && echo "-----Port $port -OPEN"
  done; wait
done
```
<!-- IMAGEN -->
*(1,1)*

<!-- Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help]. -->