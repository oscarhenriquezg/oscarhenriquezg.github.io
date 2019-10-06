---
id: 136
title: Less is More
date: 2018-09-02T17:20:47+00:00
author: Oscar
layout: post

switch_like_status:
  - "1"
swp_cache_timestamp:
  - "416979"
categories:
  - Linux
  - MiniPost
---
Sí, less is more, como lo dijo antaño [Ludwig Mies van der Rohe](https://es.wikipedia.org/wiki/Ludwig_Mies_van_der_Rohe)   padre de la arquitectura y del diseño minimalista, bueno en este caso y en el contexto de linux diremos que “less is more than more“.
Así es, este a veces olvidado comando nos entrega más y mejores posibilidades que el tradicional more, en los siguientes aspectos:   

{% if post.excerpt != post.content %}
    <a href="{{ site.baseurl }}{{ post.url }}">Read more</a>
{% endif %}   


**Búsquedas**: Nos ayuda con el resaltado del texto a buscar.

**Archivos grandes**: less no necesita leer el archivo completo para abrirlo, esto se nota mucho en archivos grandes, lo que maneja con mas soltura que more o cat.

**Navegación**: En algunas versiones de linux el comando more te permite solo avanzar en el archivo desplegado, con less podemos navegar de arriba a abajo

Algunos trucos:
less como tail -f: 
```sh
less +F /var/log/syslog
```
Busquedas con less:
```sh
less +/CRON /var/log/syslog**
```
Ahora leyendo sobre el tema veo que hay quienes dicen que "most is better than less" :O
[most](http://www.jedsoft.org/most/index.html) aún no está tan estandarizado, pero se ve interesante. Habría que probarlo.

A ver si te animas a cambiar el viejo more por el less: 
```sh
cd
echo “alias more=’less’” >> .bash_profile
```
