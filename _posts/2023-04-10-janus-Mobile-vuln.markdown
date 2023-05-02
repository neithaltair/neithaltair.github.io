---
title:  "Janus Vulnerability Mobile"
date:   2023-04-13
categories: [Pentest]
tags: [Vulnerabilities,Web,Pentesting]
---

Que configuraciones permiten el autocompletado de contraseñas, cuales no. 

Una reciente configuración es: `<input type="password" autocomplete="current-password" />"`

Esta configuración permite que el navegador que tenga la contraseña del usuario la introduzca. `(Riesgo de seguridad)`

![image](/genes/vulnerabilidades/autocomplete/autocomplete.png)

Configuración ideal para recomendar contraseñas seguras al usuario `autocomplete="new-password"`, no es funcional utilizar esta configuración si se utiliza un autocompletado de contraseña. 

Una configuración correcta para deshabilitar el autocompletado desde el lado del desarrollador es: 

``` html
<input type="password" autocomplete="off" />

```

`Es posible que el navegador de la opción de guardar la contraseña, pero es importante que el desarrollo de la página sobre todo para páginas de banca no den la opción de guardar o autocompletar las contraseñas del usuario.`


*(1,1)*