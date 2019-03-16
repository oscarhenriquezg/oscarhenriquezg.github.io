---
id: 52
title: 'Benchmark por defecto: Apache vs Nginx'
date: 2017-07-25T23:33:18+00:00
author: Oscar
layout: post
guid: http://144.217.6.251/?p=52
permalink: /index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/
swp_pinterest_image_url:
  - ""
swp_cache_timestamp:
  - "417236"
categories:
  - Benchmark
---
Este es el primer post de lo que espero sea una serie, donde realizare algunos benchmark a productos o tecnologías &#8220;recién sacadas de la caja&#8221;, la idea es analizarlos en su instalación por defecto, sin ningún tipo de tunning de performance, seguridad, etc.

Una vez dicho lo anterior, la pregunta a resolver el día de hoy es:

> **Con sus configuraciones por defecto, ¿Cuál servidor web tendrá mejor rendimiento Apache o Nginx?**

<img class="wp-image-219 size-thumbnail aligncenter" src="https://www.oscarhenriquezg.net/images/2017/07/apache_vs_nginx-150x150.png" width="150" height="150" /> 

Hoy he querido probar [Apache](http://httpd.apache.org/) y [Nginx](https://nginx.org/en/) en sus instalaciones por defecto en un ambiente Debian Linux. Me ha tocado trabajar con ambos Web Servers y la verdad a ambos los he encontrado bastante sólidos y confiables, pero hoy tenemos una pregunta y vamos a ver cómo responderla 😀

<!--more-->Características del Ambiente de Pruebas:

### **Hardware**

En cuanto a hardware vamos a utilizar VPS del proveedor Digital Ocean, ya que son las que tenía a mano y me permiten tener 2 servidores de exactamente las mismas características para hacer la contienda lo más justa posible.

**Tipo de Servidor:** VPS (Virtual Private Server)  
**Proveedor:** DigitalOcean  
**Memoria:** 512 MB  
**Disco:** 20 GB Solid State  
**Procesador:** Intel(R) Xeon(R) CPU E5-2650L v3 @ 1.80GHz, 1 core.

<span style="text-decoration: underline;">Nombres de servidores:</span>

<p class="p1">
  <strong>Server1:</strong> debian-512mb-ny-01-<strong><em>apache</em></strong><br /> <strong>IP:</strong> 67.205.147.162<br /> <strong>Ubicación:</strong> New York City, site 1, DigitalOcean
</p>

<p class="p1">
  <strong>Server2:</strong> debian-512mb-ny-01-<strong><em>nginx</em></strong><br /> <strong>IP:</strong> 198.211.116.62<br /> <strong>Ubicación:</strong> New York City, site 1, DigitalOcean
</p>

<div id='gallery-1' class='gallery galleryid-52 gallery-columns-1 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/do-droplets/'><img width="300" height="170" src="https://www.oscarhenriquezg.net/images/2017/03/DO-Droplets-300x170.png" class="attachment-medium size-medium" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/DO-Droplets-300x170.png 300w, https://www.oscarhenriquezg.net/images/2017/03/DO-Droplets-768x436.png 768w, https://www.oscarhenriquezg.net/images/2017/03/DO-Droplets-700x398.png 700w, https://www.oscarhenriquezg.net/images/2017/03/DO-Droplets.png 998w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </div></figure>
</div>

#### Sistema Operativo

Como sistema operativo he elegido Debian Linux en su versión 8.7 (Jessie) de 64 bits, que es la última versión estable del sistema operativo a la fecha (19 de marzo de 2017).

<div id='gallery-2' class='gallery galleryid-52 gallery-columns-1 gallery-size-large'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/os-ips-servers/'><img width="720" height="167" src="https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers-1024x238.png" class="attachment-large size-large" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers-1024x238.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers-300x70.png 300w, https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers-768x179.png 768w, https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers-700x163.png 700w, https://www.oscarhenriquezg.net/images/2017/03/OS-IPs-servers.png 1306w" sizes="(max-width: 720px) 100vw, 720px" /></a>
  </div></figure>
</div>

Una vez iniciado el servidor virtual le damos su respectivo apt-get update para que todos sus repositorios estén frescos y con las últimas versiones del software disponible para el sistema.

#### Instalación de Web Servers

Respecto a la instalación de los servidores web lo haremos de la manera más sencilla posible, sin módulos adicionales ni documentación extra ni nada que venga aparte de la instalación por defecto del servidor mismo.

Para Apache usaremos:

`#apt-get install apache2`

Con el comando anterior se nos instala Apache en su versión 2.4.10

Para Nginx usaremos:

`#apt-get install nginx`

Con el comando anterior se nos instala Nginx en su versión 1.6.2

Completadas las instalaciones por defecto iremos a probar que el servicio se esté entregando de manera correcta por el puerto 80 y nos debería mostrar sus respectivos index por defecto como se ve a continuación:

Default Index e IPs de cada server:

<div id='gallery-3' class='gallery galleryid-52 gallery-columns-2 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/default-index-apache/'><img width="300" height="172" src="https://www.oscarhenriquezg.net/images/2017/03/default-index-apache-300x172.png" class="attachment-medium size-medium" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/default-index-apache-300x172.png 300w, https://www.oscarhenriquezg.net/images/2017/03/default-index-apache-768x441.png 768w, https://www.oscarhenriquezg.net/images/2017/03/default-index-apache-1024x588.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/default-index-apache-700x402.png 700w, https://www.oscarhenriquezg.net/images/2017/03/default-index-apache.png 1051w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/default-index-nginx/'><img width="300" height="172" src="https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx-300x172.png" class="attachment-medium size-medium" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx-300x172.png 300w, https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx-768x441.png 768w, https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx-1024x588.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx-700x402.png 700w, https://www.oscarhenriquezg.net/images/2017/03/default-index-nginx.png 1051w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </div></figure>
</div>

Ya que el index por defecto de Apache tenía un mayor tamaño en kilobytes que el de Nginx, decidí crear un nuevo index muy sencillo y creativo 😉 , el que monte como index por defecto en ambos servidores, para que exista igualdad de condiciones (esto para que no se sospeche que esta leve diferencia de tamaño puediera dar una ventaja a ngnix ya que sería más liviana la página a servir):

```html
<html>
<header>
<title>Hola Mundo</title>
</header>
<body><br>Hello world :D<br></body>
</html>
```

<div id='gallery-4' class='gallery galleryid-52 gallery-columns-1 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/index-hellow-world/'><img width="300" height="153" src="https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world-300x153.png" class="attachment-medium size-medium" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world-300x153.png 300w, https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world-768x393.png 768w, https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world-1024x524.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world-700x358.png 700w, https://www.oscarhenriquezg.net/images/2017/03/index-hellow-world.png 1107w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </div></figure>
</div>

Listo, hasta aquí ya tenemos preparado el ambiente para realizar la prueba, pero me falta la herramienta a utilizar para probar el ambiente preparado, cuando ya estaba desenfundando el clásico JMeter, me tropecé con [OctoPerf](https://octoperf.com/) leyendo [uno de mis blogs favoritos](https://www.genbetadev.com/herramientas/12-herramientas-imprescindibles-para-asegurar-la-calidad-del-software-y-sus-alternativas) y me pareció la ocasión perfecta para probarlo.

## Jugando con Octoperf

[OctoPerf](https://octoperf.com/) es un servicio web que nos entrega la posibilidad de usar Jmeter como [SaaS](https://es.wikipedia.org/wiki/Software_como_servicio) (Software as a Service), lo que lleva todas (o al menos la mayoría) de las características de Jmeter a una interfaz web amigable y lo mejor de todo es que te da la posibilidad de obtener una completa reportería de tus proyectos de prueba con posibilidad de descargar reportes en PDF con todos los datos obtenidos de tus proyectos.

Entonces ahora nos ponemos en la labor de armar el set de pruebas, sus características y el tipo de reportería que queremos obtener, la verdad que fue un proceso muy, muy facil y rapido en solo 6 pasos:

  1. Creamos un nuevo proyecto
  2. Seleccionamos &#8220;Website/URL&#8221; para indicar que estresamos una dirección web (también nos permite importar configuraciones de proyectos de Jmeter 😀 )
  3. Definimos la URL a estresar y el método http a usar, en este caso un simple [GET](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).
  4. Acá se nos permite configurar algunos parámetros de nuestro escenario de pruebas, aquí fue donde me llevo una grata sorpresa y quiero hacer un pequeño paréntesis:  
    _El servicio de OctoPerf nos permite seleccionar desde donde le vamos a &#8220;pegar&#8221;a nuestra URL  y como opciones nos da los servicios de Digital Ocean y sus distintos Datacenters, como también los de Amazon y sus respectivos Datacenters. Ya que mis servidores a estresar están en Digital Ocean en uno de sus datacenters de nueva york, selecciono entonces el mismo proveedor y la misma ubicación, de esta forma aseguramos encontrarnos dentro de la misma red y quizás hasta dentro del mismo datacenter, lo que nos ayuda en tener mejores tiempos de respuesta entre servidores._
  5. En el quinto paso definimos el número de VUs (Virtual Users) en mi caso 50 y luego le damos a &#8220;Launch 50VUs&#8221;. En este caso la prueba se realizará durante 10 minutos, ascendiendo desde 1 VU en el minuto cero, llegando a los 50 VUs en el minuto 5 y manteniéndose así hasta los 10 minutos, como se aprecia en la siguiente gráfica.

<div id='gallery-5' class='gallery galleryid-52 gallery-columns-1 gallery-size-large'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/50-vus/'><img width="720" height="221" src="https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332-1024x314.png" class="attachment-large size-large" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332-1024x314.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332-300x92.png 300w, https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332-768x235.png 768w, https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332-700x215.png 700w, https://www.oscarhenriquezg.net/images/2017/03/50-vus-e1501035899332.png 1142w" sizes="(max-width: 720px) 100vw, 720px" /></a>
  </div></figure>
</div>

Ya con ganas de darle &#8220;play&#8221;e iniciar la prueba recuerdo el monitoreo en la capa de SO (Sistema Operativo), al momento de idear esta prueba siempre quise considerar también el consumo de recursos a nivel de SO, algo sencillo, pero que mida online lo básico (CPU, MEM, HD).

#### Preparación de monitoreo en Linux

Aprovechando las infinitas posibilidades que nos entrega la shell en un servidor linux, lo primero que se me ocurre para realizar un monitoreo efectivo y sencillo es generar un script que me tome los parámetros de CPU, memoria y disco y los guarde para su posterior análisis. Para no reinventar la rueda y googleando un poco llego justo a lo que necesito en el siguiente post de systeen.com:

<blockquote class="wp-embedded-content" data-secret="LX7QcuS6Fk">
  <p>
    <a href="http://www.systeen.com/2016/05/07/bash-script-monitor-cpu-memory-disk-usage-linux/">Bash Script to Monitor CPU, Memory and Disk Usage on Linux</a>
  </p>
</blockquote>



Con un par de modificaciones lo adapto a mi necesidad agregando una columna con la hora, minuto y segundos del momento en que se toma la muestra y cambie el tiempo de espera entre toma de muestras a 1 segundo. Quedando así:

<pre class="lang:sh decode:true ">#! /bin/bash
printf "Memory\t\tDisk\t\tCPU\t\tTIME\n"
end=$((SECONDS+3600))
while [ $SECONDS -lt $end ]; do
MEMORY=$(free -m | awk 'NR==2{printf "%.2f%%\t\t", $3*100/$2 }')
DISK=$(df -h | awk '$NF=="/"{printf "%s\t\t", $5}')
CPU=$(top -bn1 | grep load | awk '{printf "%.2f%%\t\t\n", $(NF-2)}')
HH=$(date +"%T")
echo "$MEMORY$DISK$CPU$HH"
sleep 1
done</pre>

Ya con el script de monitoreo listo, lo pruebo y registra justo lo que necesito. Como quiero ver en línea el registro de las muestras y también registrarlo en un archivo CSV para su posterior análisis lo ejecuto con un [tee](http://linux.101hacks.com/unix/tee-command-examples/) y queda andando mas menos así:

<div id='gallery-6' class='gallery galleryid-52 gallery-columns-1 gallery-size-medium'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/shell-monitoreo/'><img width="300" height="202" src="https://www.oscarhenriquezg.net/images/2017/03/shell-monitoreo-300x202.png" class="attachment-medium size-medium" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/shell-monitoreo-300x202.png 300w, https://www.oscarhenriquezg.net/images/2017/03/shell-monitoreo.png 349w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </div></figure>
</div>

### Pruebas en curso

Ya por fin iniciamos las pruebas y vemos cómo se van comportando online los servidores ante la carga (ojo en los títulos de cada ventana, en la primera imagen me quedaron cruzadas las ventanas :-P):

<div id='gallery-7' class='gallery galleryid-52 gallery-columns-1 gallery-size-large'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/running-tests-00/'><img width="720" height="450" src="https://www.oscarhenriquezg.net/images/2017/03/running-tests-00-1024x640.png" class="attachment-large size-large" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/running-tests-00-1024x640.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-00-300x188.png 300w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-00-768x480.png 768w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-00-700x438.png 700w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-00.png 1440w" sizes="(max-width: 720px) 100vw, 720px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/running-tests-01/'><img width="720" height="450" src="https://www.oscarhenriquezg.net/images/2017/03/running-tests-01-1024x640.png" class="attachment-large size-large" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/running-tests-01-1024x640.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-01-300x188.png 300w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-01-768x480.png 768w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-01-700x438.png 700w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-01.png 1440w" sizes="(max-width: 720px) 100vw, 720px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/running-tests-02/'><img width="720" height="450" src="https://www.oscarhenriquezg.net/images/2017/03/running-tests-02-1024x640.png" class="attachment-large size-large" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/running-tests-02-1024x640.png 1024w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-02-300x188.png 300w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-02-768x480.png 768w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-02-700x438.png 700w, https://www.oscarhenriquezg.net/images/2017/03/running-tests-02.png 1440w" sizes="(max-width: 720px) 100vw, 720px" /></a>
  </div></figure>
</div>

### Resultados

OctoPerf nos da un detallado informe de lo obtenido que podemos visualizar online y descargar como PDF también, aquí dejo los resultados, para que revisen todos los detalles:

[OctoPerf-test-nginx  
](https://www.oscarhenriquezg.net/images/2017/03/OctoPerf-test-nginx.pdf) [OctoPerf-test-apache](https://www.oscarhenriquezg.net/images/2017/03/OctoPerf-test-apache.pdf)

La comparación de consumo de recursos de Hardware se las debo, quedó en un excel perdido donde grafique los resultados y eran casi iguales, con un leve menor consumo para el servidor con Nginx.

### Interpretación

**Resumen de Estadísticas y gráfico de Apache:**

<div id='gallery-8' class='gallery galleryid-52 gallery-columns-2 gallery-size-full'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/statistics-summary-apache/'><img width="729" height="576" src="https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-apache.png" class="attachment-full size-full" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-apache.png 729w, https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-apache-300x237.png 300w, https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-apache-700x553.png 700w" sizes="(max-width: 729px) 100vw, 729px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/graphic-summary-apache/'><img width="723" height="533" src="https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-apache.png" class="attachment-full size-full" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-apache.png 723w, https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-apache-300x221.png 300w, https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-apache-700x516.png 700w" sizes="(max-width: 723px) 100vw, 723px" /></a>
  </div></figure>
</div>

Apache responde todas sus solicitudes sin errores en un tiempo promedio de respuesta de 7 milisegundos.

**Resumen de Estadísticas y gráfico de Nginx:**

<div id='gallery-9' class='gallery galleryid-52 gallery-columns-2 gallery-size-full'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/statistics-summary-nginx/'><img width="724" height="539" src="https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-nginx.png" class="attachment-full size-full" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-nginx.png 724w, https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-nginx-300x223.png 300w, https://www.oscarhenriquezg.net/images/2017/03/statistics-summary-nginx-700x521.png 700w" sizes="(max-width: 724px) 100vw, 724px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='http://163.250.212.113/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/graphic-summary-nginx/'><img width="724" height="538" src="https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-nginx.png" class="attachment-full size-full" alt="" srcset="https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-nginx.png 724w, https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-nginx-300x223.png 300w, https://www.oscarhenriquezg.net/images/2017/03/graphic-summary-nginx-700x520.png 700w" sizes="(max-width: 724px) 100vw, 724px" /></a>
  </div></figure>
</div>

Nginx pudo recibir más &#8220;golpes&#8221; y responderlos todos sin errores y en un menor tiempo de respuesta promedio.

### Mi Veredicto

**_Nginx Win!!!_**, no fue un _fatality_ ni un _flawless_ victory, fue una llegada con final fotográfico como dirían en la hípica, pero queda claro que Nginx obtuvo mejores resultados que Apache en cuanto a hits que pudo recibir y en cuanto a tiempo promedio de respuesta.

Se podría decir que las diferencias son mínimas, pero tengamos en consideración que esta prueba ha sido realizada solo con 50 usuarios, en un ambiente de igualdad de condiciones para ambos servidores, estas pequeñas diferencias se acentúan muchísimo en ambientes productivos donde se está respondiendo a miles de peticiones y cada milisegundo vale ORO (_he visto servicios venirse abajo por demorar milisegundos demás en una operación_).

**NOTA**: _Estas pruebas han sido realizadas entre el 18 y 19 de Marzo de 2017, con las últimas versiones del software de los vendors mencionados anteriormente en la  fecha indicada._

Cualquier [comentario](http://vps117915.vps.ovh.ca/index.php/2017/07/25/benchmark-por-defecto-apache-vs-nginx/#respond) o sugerencia para futuras pruebas es bienvenido 😀