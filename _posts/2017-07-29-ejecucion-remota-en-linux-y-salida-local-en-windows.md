---
id: 58
title: Ejecución remota en Linux y salida local en Windows
date: 2017-07-29T19:25:45+00:00
author: Oscar
layout: post
swp_pinterest_image_url:
  - ""
swp_cache_timestamp:
  - "417328"
categories:
  - Informática
  - Linux
  - Software
---
¿Cómo ejecutar un comando remoto en un servidor linux y obtener su salida en una archivo local en windows?

Ojo que no solamente vamos a "ver" la salida en un emulador de terminal, como Putty u otro, en local, sino que buscaremos que la salida sea escrita en un archivo local.


![alt text](https://www.oscarhenriquezg.net/images/2017/07/lin-to-win-commands.png "diagrama simple")


En una ocasión me vi enfrentado a la siguiente problemática, debía realizar el análisis en tiempo real de un log de una aplicación que estaba escribiendo constantemente (500kb x minuto aprox.) Todo bien hasta aquí, el problema es lo siguiente:


* Solo tengo acceso remoto a ese log a través de ssh y haciendo *sudo* a otro usuario para poder leerlo.
* No tengo permiso de instalación sobre el servidor remoto que guarda el log.
* Accedo al log desde windows a través de putty.


Mi idea era traer el log a un archivo local en mi entorno en Windows y ahí analizarlo con [Kibana](https://unpocodejava.wordpress.com/2013/07/30/que-es-kibana/), una herramienta de análisis de logs en tiempo real (a mi gusto mejor que [Splunk](https://www.splunk.com/es_es)), para identificar patrones, graficar estadísticas, etc.

Para traerme el log necesitaria alguna shell o aplicación que haga algo así como:

```sh
tail -f /serverremoto/archivoremoto.log >> /windowslocal/archivolocal.log
```

Después de probar algunos comandos y googlear sobre el tema encontré lo que necesitaba:



He usado la herramienta [PuTTYLink](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) (plink.exe) del conjunto de herramientas de PuTTY.

Esta herramienta te permite ejecutar comandos en un servidor remoto y direccionar la salida de modo local. Básicamente el comando sería algo así:

```sh
plink.exe root@miserver -pw S3cr3tp4ss "tail -f ArchivoRemoto.log" >> Archivolocal.log
```


De este modo escribo la salida del tail -f del *ArchivoRemoto.log* al *Archivolocal.log* en mi sistema de archivos local, luego este archivo local lo puedo tratar con herramientas de análisis de logs como Kibana.


Hubiera sido muy distinto si fuera entre sistemas linux o si pudiera instalar herramientas en el servidor remoto o mejor aún contar con un servidor de syslog desde donde _stremearme_ el archivo para consumirlo, pero tenía las limitaciones que comentaba al principio del post y bueno hay que saber jugar en cualquier cancha como dicen por ahí.

De todas maneras si alguien conoce otra forma de resolverlo o alguna herramienta que lo permita, por favor comenten para ver si se puede mejorar esta solución básica que he encontrado.

Espero esto le sea de ayuda a alguien más.


**NOTA:** *Este post lo escribí basándome en un post que realicé hace un tiempo en el foro de elhacker.net: [Traeme log remoto a archivo local para análisis en tiempo real](https://foro.elhacker.net/gnulinux/traeme_log_remoto_a_archivo_local_para_analisis_en_tiempo_real-t453449.0.html;msg2073648#msg2073648)*