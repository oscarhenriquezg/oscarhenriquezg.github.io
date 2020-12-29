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
  
  
Los siguientes pasos son el registro de mi instalación de ownCloud en mi Raspberry Pi3, espero sirvan como guía a quien se interese en realizar este proyecto:

  * Instalar Owncloud en la RPI3.
  * Agregar disco externo a la RPI3.
  * Configuraciones de webserver.
  * Configuración de Servicio de DNS dinámico.
  * Instalar cliente en local.

#### Instalar Owncloud en la RPI3:


Primero actualizamos nuestro raspbian en la RPI3:


    sudo apt-get update -y

Luego instalamos los paquetes necesarios

    sudo apt-get install apache2 php5 php5-json php-xml-parser php5-gd php5-sqlite curl libcurl3 libcurl3-dev php5-curl php5-common


  Descargamo OwnCloud, en su última versión (la versión puede variar de acuerdo a nuevas actualizaciones, verificar en [https://owncloud.org/community/](https://owncloud.org/community) y descomprimimos el archivo descargado:


    wget https://download.owncloud.org/community/owncloud-9.1.3.tar.bz2
    tar -xjf owncloud-9.1.3.tar.bz2


  Copiamos la carpeta descomprimida en el directorio web y Hacemos al usuario www-data el dueño de todos los archivos::

    sudo cp -r owncloud /var/www/html
    sudo chown -R www-data:www-data /var/www/html



#### Agregar disco externo a la RPI3:


Ahora debemos crear directorio donde montaremos nuestro disco en /media

    sudo mkdir /media/HD500

Como identificar nuestro disco

 Ejecutar:
 
    sudo fdisk -l
Obtenemos una salida similar a esta:

    Device      Start       End   Sectors   Size Type
    /dev/sda1      40    409639    409600   200M EFI System


  Copiar salida anterior.

  En este momento conectamos nuestro disco externo y ejecutamos nuevamente:


    sudo fdisk -l</pre>


  Comparamos con la salida anterior, donde se identifica claramente la linea que identifica nuestro disco externo (/dev/sda2):

    Device      Start       End   Sectors   Size Type
    /dev/sda1      40    409639    409600   200M EFI System
    /dev/sda2  411648 976445399 976033752 465.4G Linux filesystem



  Montar disco duro externo de manera permanente editando el archivo fstab:

    sudo vi /etc/fstab


  Agregamos linea (respetar espacios):

    /dev/sda2 /media/HD500 ext4 defaults  0 0

  Donde:

  **/dev/sda2**: es la identificación de nuestro disco en el sistema


  **/media/HD500**: es la carpeta que creamos para montar nuestro hd externo

  **ext4: es el formato del disco

 ** defaults**: configs por default


  Verificamos que la edición de nuestro archivo quedo correcta:


    less /etc/fstab

Una vez seguros de que estamos OK, damos la orden de montar todos los discos al sistema:

    sudo mount -a


  Creamos la carpeta para nuestros archivos en ownCloud:


    sudo mkdir /media/HD500/owncloud
    sudo mkdir /media/HD500/owncloud/data</pre>


#### Configuraciones de webserver:</span>

  Hacemos al usuario www-data el dueño del disco montado:

    sudo chown -R www-data:www-data /media/HD500</pre>


  Cambiamos el tamaño máximo de subida de archivos a 1024 mb:
  
    sudo nano /etc/php5/apache2/php.ini


  Reiniciamos el servicio apache:

    sudo service apache2 restart</pre>
  
#### Configuración de Servicio de DNS dinámico:

  Este paso es opcional, pero recomendado, aquí configuraremos un servicio de DNS dinámico para que nuestro servidor de OwnCloud sea accesible desde internet y podamos ver y sincronizar nuestros archivos desde cualquier parte.


  Se recomienda registrarse en un servicio de DNS dinámico del tipo <a href="https://www.noip.com">No-IP</a>, <a href="https://www.dlinkddns.com">dlinkddns</a>, etc. yo usare el de dlink ya que uno de mis dispositivos de red tiene la opción de conectarse de manera nativa a este servicio y reportar mi ip dinámica constantemente.


  Agregamos  nuestro nombre de servicio de DNS al archivo hosts de nuestro sistema:

    vi /etc/hosts


  Agrego las siguientes lineas:
  
    #owncloud en local
    192.168.1.114 tunombredeusuario.dlinkddns.com</pre>
 
 
  Esto lo hago para que la primera sincronización se realice en el ambito local de mi red y no vaya a resolver el nombre al dns y no pasen los archivos por fuera (por internet)


  una vez realizado esto ingresamos a la url:


  http://tunombredeusuario.dlinkddns.com




  Donde nos aparece la primera interfaz de owncloud y nos pide crear un user y password de adminisrador:


  Es altamente recomendable no usar nombres por defecto como &#8220;admin&#8221;, root, administrator, administrador, etc. esto para evitar posibles ataques de fuerza bruta contra el user


  Seleccionar en la interfaz la opción de almacenamiento y base de datos y en el textbox que se nos despliega debemos ingresar la ruta que creamos para nuestros archivos en nuestro disco externo:
 
      /media/HD500/owncloud/data

  Luego presionamos instalar.



#### Instalar cliente en local:

  Descargamos el cliente local segun nuestro SO:

[https://owncloud.org/download/#owncloud-desktop-client](https://owncloud.org/download/#owncloud-desktop-client)

Configuramos nuestra URL de OwnCloud:

![](https://www.oscarhenriquezg.net/images/2018/03/owncloud01-300x192.png)

  Nuestro user y password:

![](https://www.oscarhenriquezg.net/images/2018/03/owncloud02-300x162.png)


  Y terminamos la instalación, ya estamos listos para sincronizar nuestros archivos.

Como siempre, cualquier duda o comentario es bienvenido 😊
