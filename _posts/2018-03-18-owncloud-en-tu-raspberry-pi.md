---
id: 61
title: Owncloud en tu Raspberry Pi
date: 2018-03-18T12:52:44+00:00
author: Oscar
layout: post
guid: http://144.217.6.251/?p=61
permalink: /index.php/2018/03/18/owncloud-en-tu-raspberry-pi/
categories:
  - Tutoriales
---
<div>
</div>

<div>
  Los siguientes pasos son el registro de mi instalación de ownCloud en mi Raspberry Pi3, espero sirvan como guía a quien se interese en realizar este proyecto:
</div>

<div>
</div>

  * Instalar Owncloud en la RPI3.
  * Agregar disco externo a la RPI3.
  * Configuraciones de webserver.
  * Configuración de Servicio de DNS dinámico.
  * Instalar cliente en local.

<div>
</div>

#### <span style="text-decoration: underline;"> Instalar Owncloud en la RPI3:</span>

<div>
</div>

<div>
  Primero actualizamos la RPI3:
</div>

<div>
  <pre class="lang:default decode:true">sudo apt-get update</pre>
</div>

<div>
  Descargamos los paquetes necesarios:
</div>

<div>
  <pre class="lang:default decode:true">sudo apt-get install apache2 php5 php5-json php-xml-parser php5-gd php5-sqlite curl libcurl3 libcurl3-dev php5-curl php5-common
</pre>
</div>

<div>
  Descargar OwnCloud, en su última versión (la versión puede variar de acuerdo a nuevas actualizaciones, verificar en <a href="https://owncloud.org/community/">https://owncloud.org/community/</a>):
</div>

<div>
  <pre class="lang:default decode:true">wget https://download.owncloud.org/community/owncloud-9.1.3.tar.bz2
</pre>
</div>

<div>
  Descomprimir el archivo descargado:
</div>

<div>
  <pre class="lang:default decode:true">tar -xjf owncloud-9.1.3.tar.bz2
</pre>
</div>

<div>
  Copiar la carpeta descomprimida en el directorio:
</div>

<div>
  <pre class="lang:default decode:true">sudo cp -r owncloud /var/www/html
</pre>
</div>

<div>
  Hacer al usuario www-data el dueño de todos los archivos:
</div>

<div>
  <pre class="lang:default decode:true">sudo chown -R www-data:www-data /var/www/html
</pre>
</div>

#### 

#### <span style="text-decoration: underline;">Agregar disco externo a la RPI3:</span>

<div>
  Crear directorio donde montaremos nuestro disco en /media
</div>

<div>
  <pre class="lang:default decode:true">sudo mkdir /media/HD500
</pre>
</div>

<div>
  Como identificar nuestro disco
</div>

<div>
</div>

<div>
  Ejecutar:
</div>

<div>
  <pre class="lang:default decode:true">sudo fdisk -l
</pre>
</div>

<div>
  <pre class="lang:default decode:true">Device      Start       End   Sectors   Size Type
/dev/sda1      40    409639    409600   200M EFI System</pre>
</div>

<div>
  Copiar salida anterior.
</div>

<div>
</div>

<div>
  En este momento conectamos nuestro disco externo y ejecutamos nuevamente:
</div>

<div>
  <pre class="lang:default decode:true">sudo fdisk -l</pre>
</div>

<div>
  Comparamos con la salida anterior, donde se identifica claramente la linea que identifica nuestro disco externo:
</div>

<div>
  <pre class="lang:default decode:true">Device      Start       End   Sectors   Size Type
/dev/sda1      40    409639    409600   200M EFI System
/dev/sda2  411648 976445399 976033752 465.4G Linux filesystem</pre>
</div>

<div>
  Montar disco duro externo de manera permanente:
</div>

<div>
  <pre class="lang:default decode:true">sudo nano /etc/fstab
</pre>
</div>

<div>
  Agregamos linea (respetar espacios):
</div>

<div>
  <pre class="lang:default decode:true">/dev/sda2 /media/HD500 ext4 defaults  0 0</pre>
</div>

<div>
  Donde:
</div>

<div>
</div>

<div>
  /dev/sda2: es la identificación de nuestro disco en el sistema
</div>

<div>
  /media/HD500: es la carpeta que creamos para montar nuestro hd externo
</div>

<div>
  ext4: es el formato del disco
</div>

<div>
  defaults: configs por default
</div>

<div>
</div>

<div>
  Verificamos que la edición de nuestro archivo quedo correcta:
</div>

<div>
  <pre class="lang:default decode:true">less /etc/stab</pre>
</div>

<div>
  Una vez seguros de que estamos OK, damos la orden de montar todos los discos al sistema:
</div>

<div>
  <pre class="lang:default decode:true">sudo mount -a</pre>
</div>

<div>
  Creamos la carpeta para nuestros archivos en ownCloud:
</div>

<div>
  <pre class="lang:default decode:true">sudo mkdir /media/HD500/owncloud
sudo mkdir /media/HD500/owncloud/data</pre>
</div>

<div>
  <h4>
  </h4>
  
  <h4>
    <span style="text-decoration: underline;">Configuraciones de webserver:</span>
  </h4>
</div>

<div>
  Hacemos al usuario www-data el dueño del disco montado:
</div>

<div>
  <pre class="lang:default decode:true">sudo chown -R www-data:www-data /media/HD500</pre>
</div>

<div>
  Cambiamos el tamaño máximo de subida de archivos a 1024 mb:
</div>

<div>
  <pre class="lang:default decode:true">sudo nano /etc/php5/apache2/php.ini</pre>
</div>

<div>
  Reiniciamos el servicio apache:
</div>

<div>
  <pre class="lang:default decode:true">sudo service apache2 restart</pre>
  
  <h4>
  </h4>
  
  <h4>
    <span style="text-decoration: underline;">Configuración de Servicio de DNS dinámico:</span>
  </h4>
</div>

<div>
  Este paso es opcional, pero recomendado, aquí configuraremos un servicio de DNS dinámico para que nuestro servidor de OwnCloud sea accesible desde internet y podamos vey y sincronizar nuestros archivos desde cualquier parte.
</div>

<div>
</div>

<div>
  Se recomienda registrarse en un servicio de DNS dinámico del tipo <a href="https://www.noip.com">No-IP</a>, <a href="https://www.dlinkddns.com">dlinkddns</a>, etc. yo usare el de dlink ya que uno de mis dispositivos de red tiene la opción de conectarse de manera nativa a este servicio y reportar mi ip dinámica constantemente.
</div>

<div>
</div>

<div>
  Agregamos  nuestro nombre de servicio de DNS al archivo hosts de nuestro sistema:
</div>

<div>
  <pre class="lang:default decode:true">vi /etc/hosts</pre>
</div>

<div>
  Agrego las siguientes lineas:
</div>

<div>
  <pre class="lang:default decode:true">#owncloud en local
192.168.1.114 tunombredeusuario.dlinkddns.com</pre>
</div>

<div>
  Esto lo hago para que la primera sincronización se realice en el ambito local de mi red y no vaya a resolver el nombre al dns y no pasen los archivos por fuera (por internet)
</div>

<div>
</div>

<div>
  una vez realizado esto ingresamos a la url:
</div>

<div>
</div>

<div>
  http://tunombredeusuario.dlinkddns.com
</div>

<div>
</div>

<div>
  Donde nos aparece la primera interfaz de owncloud y nos pide crear un user y password de adminisrador:
</div>

<div>
</div>

<div>
  Es altamente recomendable no usar nombres por defecto como &#8220;admin&#8221;, root, administrator, administrador, etc.
</div>

<div>
  esto para evitar posibles ataques de fuerza bruta contra el user
</div>

<div>
</div>

<div>
  Seleccionar en la interfaz la opción de almacenamiento y base de datos y en el textbox que se nos despliega debemos ingresar la ruta que creamos para nuestros archivos en nuestro disco externo:
</div>

<div>
</div>

<div>
   /media/HD500/owncloud/data
</div>

<div>
</div>

<div>
  Luego presionamos instalar.
</div>

<div>
</div>

#### <span style="text-decoration: underline;">Instalar cliente en local:</span>

<div>
  Descargamos el cliente local segun nuestro SO:
</div>

<div>
</div>

<div>
  <a href="https://owncloud.org/download/#owncloud-desktop-client">https://owncloud.org/download/#owncloud-desktop-client</a>
</div>

<div>
</div>

<div>
  Configuramos nuestra URL de OwnCloud:
</div>

<div>
   <img class="alignnone size-medium wp-image-289" src="https://www.oscarhenriquezg.net/images/2018/03/owncloud01-300x192.png" alt="" width="300" height="192" srcset="https://www.oscarhenriquezg.net/images/2018/03/owncloud01-300x192.png 300w, https://www.oscarhenriquezg.net/images/2018/03/owncloud01.png 750w" sizes="(max-width: 300px) 100vw, 300px" />
</div>

<div>
</div>

<div>
  Nuestro user y password:
</div>

<div>
  <img class="alignnone size-medium wp-image-290" src="https://www.oscarhenriquezg.net/images/2018/03/owncloud02-300x162.png" alt="" width="300" height="162" srcset="https://www.oscarhenriquezg.net/images/2018/03/owncloud02-300x162.png 300w, https://www.oscarhenriquezg.net/images/2018/03/owncloud02.png 492w" sizes="(max-width: 300px) 100vw, 300px" />
</div>

<div>
</div>

<div>
  Y terminamos la instalación, ya estamos listos para sincronizar nuestros archivos.
</div>

<div>
</div>

<div>
  Como siempre, cualquier duda o comentario es bienvenido 😊
</div>