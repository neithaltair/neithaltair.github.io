---
title:  "Janus Vulnerability Mobile"
date:   2023-05-02
categories: [Pentest]
tags: [Vulnerabilities,Mobile,Android]
---

 `Signer Certificate` Al momento de realizar el análisis estático de una vulnerabilidad móvil se pude evidenciar las firmas con las que cuenta. 

`v1 signature: True
v2 signature: True
v2 signature: False`

De acuerdo a las firmas que contenga puede o no ser vulnerable a Janus: 
* V1 = vulnerablea Janus en todas las versiones de Android. 
* V2 = mitiga vulnerabilidad en Janus desde Android 5.0 a superiores de 8.0. 
* v3 = la firma v3 es un complemento y refuerzo de seguridad para la aplicación, en caso de que se identifiquen nuevas vulnerabilidades que no puedan ser mitigadas solo con la v2. 

![image](/genes/vulnerabilidades/janus/janusFirma.png)

Configuración ideal para aumentar la serguridad del aplicativo es contar con las 3 versiones de las firmas.
 
 `v1 signature: True
v2 signature: True
v2 signature: True`


*(1,1)*