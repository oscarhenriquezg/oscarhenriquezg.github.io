---
id: 58
title: Ejecución remota en Linux y salida local en Windows
date: 2017-07-29T19:25:45+00:00
author: Oscar
layout: post
guid: http://144.217.6.251/?p=58
permalink: /index.php/2017/07/29/ejecucion-remota-en-linux-y-salida-local-en-windows/
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

Ojo que no solamente vamos a &#8220;ver&#8221; la salida en un emulador de terminal, como Putty u otro, en local, sino que buscaremos que la salida sea escrita en un archivo local.

<img class="size-medium wp-image-211 aligncenter" src="http://vps117915.vps.ovh.ca/wp-content/uploads/2017/07/lin-to-win-commands-300x151.png" alt="" width="300" height="151" srcset="http://163.250.212.113/wp-content/uploads/2017/07/lin-to-win-commands-300x151.png 300w, http://163.250.212.113/wp-content/uploads/2017/07/lin-to-win-commands.png 592w" sizes="(max-width: 300px) 100vw, 300px" /> En una ocasión me vi enfrentado a la siguiente problemática, debía realizar el análisis en tiempo real de un log de una aplicación que estaba escribiendo constantemente (500kb x minuto aprox.) Todo bien hasta aquí, el problema es lo siguiente:

<ul style="list-style-type: square;">
  <li>
    Solo tengo acceso remoto a ese log a través de ssh y haciendo <i>sudo</i> a otro usuario para poder leerlo.
  </li>
  <li>
    No tengo permiso de instalación sobre el servidor remoto que guarda el log.
  </li>
  <li>
    Accedo al log desde windows a través de putty.
  </li>
</ul>

<!--more-->

Mi idea era traer el log a un archivo local en mi entorno en Windows y ahí analizarlo con [Kibana](https://unpocodejava.wordpress.com/2013/07/30/que-es-kibana/), una herramienta de análisis de logs en tiempo real (a mi gusto mejor que [Splunk](https://www.splunk.com/es_es)), para identificar patrones, graficar estadísticas, etc.

Para traerme el log necesitaria alguna shell o aplicación que haga algo así como:

<div class="code">
  <pre class="lang:default decode:true">tail -f /serverremoto/archivoremoto.log &gt;&gt; /windowslocal/archivolocal.log</pre>
</div>

<p class="p1">
  <b></b><span class="s1">Después de probar algunos comandos y googlear sobre el tema encontré lo que necesitaba:</span>
</p>

<p class="p2">
  He usado la herramienta <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">PuTTYLink</a> (plink.exe) del conjunto de herramientas de PuTTY.
</p>

<p class="p2">
  Esta herramienta te permite ejecutar comandos en un servidor remoto y direccionar la salida de modo local. Básicamente el comando sería algo así:
</p>

<pre class="lang:default decode:true">plink.exe root@miserver -pw S3cr3tp4ss "tail -f ArchivoRemoto.log" &gt;&gt; Archivolocal.log</pre>

<p class="p2">
  De este modo escribo la salida del tail -f del <i>ArchivoRemoto.log </i>al <i>Archivolocal.log</i> en mi sistema de archivos local, luego este archivo local lo puedo tratar con herramientas de análisis de logs como Kibana.
</p>

<p class="p2">
  Hubiera sido muy distinto si fuera entre sistemas linux o si pudiera instalar herramientas en el servidor remoto o mejor aún contar con un servidor de syslog desde donde <em>stremearme</em> el archivo para consumirlo, pero tenía las limitaciones que comentaba al principio del post y bueno hay que saber jugar en cualquier cancha como dicen por ahí.
</p>

<p class="p2">
  De todas maneras si alguien conoce otra forma de resolverlo o alguna herramienta que lo permita, por favor comenten para ver si se puede mejorar esta solución básica que he encontrado.
</p>

<p class="p2">
  Espero esto le sea de ayuda a alguien más.
</p>

<p class="p1">
  <em><strong>NOTA:</strong> Este post lo escribí basándome en un post que realicé hace un tiempo en el foro de elhacker.net: <a href="https://foro.elhacker.net/gnulinux/traeme_log_remoto_a_archivo_local_para_analisis_en_tiempo_real-t453449.0.html;msg2073648#msg2073648"><b>Traeme log remoto a archivo local para análisis en tiempo real</b></a></em>
</p>