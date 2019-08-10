---
id: 136
title: Less is More
date: 2018-09-02T17:20:47+00:00
author: Oscar
layout: post
guid: http://144.217.6.251/?p=136
permalink: /index.php/2018/09/02/less-is-more/
switch_like_status:
  - "1"
swp_cache_timestamp:
  - "416979"
categories:
  - Linux
  - MiniPost
---
Sí, _**less is more**_, como lo dijo antaño [Ludwig Mies van der Rohe](https://es.wikipedia.org/wiki/Ludwig_Mies_van_der_Rohe) padre de la arquitectura y del diseño minimalista, bueno en este caso y en el contexto de linux diremos que &#8220;**_less_** is more than _**more**_&#8220;.

Así es, este a veces olvidado comando nos entrega más y mejores posibilidades que el tradicional _more_, en los siguientes aspectos:

**Búsquedas**: Nos ayuda con el resaltado del texto a buscar.

**Archivos grandes**: _less_ no necesita leer el archivo completo para abrirlo, esto se nota mucho en archivos grandes, lo que maneja con mas soltura que _more_ o _cat_.

**Navegación**: En algunas versiones de linux el comando more te permite solo avanzar en el archivo desplegado, con more podemos navegar dearriba abajo

Algunos trucos que he usado:

less como tail -f: **less +F /var/log/syslog  
** Busquedas con less: **less +/CRON /var/log/syslog**

Ahora leyendo sobre el tema veo que hay quienes dicen que&#8221;_<a href="http://www.jedsoft.org/most/index.html" target="_blank" rel="noopener">most</a> is better than less_&#8221; :O  
**most** aún no está tan estandarizado, pero se ve interesante. Habría que probarlo.

A ver si te animas a cambiar el viejo more por el less: **echo &#8220;alias more=’less’&#8221;>> .bash_profile**



