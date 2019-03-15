---
id: 191
title: Fuerza bruta con Hydra y diccionario
date: 2017-07-28T16:25:39+00:00
author: Oscar
layout: post
guid: http://vps117915.vps.ovh.ca/?p=191
permalink: /index.php/2017/07/28/fuerza-bruta-con-hydra-y-diccionario/
swp_pinterest_image_url:
  - ""
swp_cache_timestamp:
  - "417259"
categories:
  - Seguridad
  - Software
---
Hace tiempo me vi en el caso de querer ingresar a un router que habían configurado hace mucho tiempo y no recordaban sus credenciales, pero si recordaban que era algo fácil como una serie de números o letras, algo así me dieron como pista :-/

Probe con los datos por defecto admin/<blank> y nada, 1234, qwerty, etc. y nada, pense en resetear de fabrica, pero no podia afectar a los usuarios de la red en ese momento y como ya sabía que la password era débil, entonces no me quedaba más que ponerme bruto 😀

  1. Me baje un diccionario básico, el más básico que encontré fue este [500-worst-passwords.txt](https://wiki.skullsecurity.org/images/c/ca/500-worst-passwords.txt)  con solo 4KB, me pareció que era muy pequeño, pero el nombre me gusto, así que no dude en probarlo.
  2. Desenfunde la vieja confiable: [THC HYDRA](http://sectools.org/tool/hydra/)

<img class="wp-image-193 aligncenter" src="https://www.oscarhenriquezg.net/images/2017/07/hydra_vieja_confiable-300x225.png" alt="" width="216" height="162" srcset="https://www.oscarhenriquezg.net/images/2017/07/hydra_vieja_confiable-300x225.png 300w, https://www.oscarhenriquezg.net/images/2017/07/hydra_vieja_confiable.png 308w" sizes="(max-width: 216px) 100vw, 216px" /> 

<!--more-->

Como ya hace tiempo no ocupaba esta herramienta me puse a leer el manual y a probar lo que necesitaba, el router entregaba una ventana de autenticación básica vía http del siguiente tipo:

<img class="aligncenter wp-image-202 " src="https://www.oscarhenriquezg.net/images/2017/07/http-basic-1024x434.png" alt="" width="523" height="222" srcset="https://www.oscarhenriquezg.net/images/2017/07/http-basic-1024x434.png 1024w, https://www.oscarhenriquezg.net/images/2017/07/http-basic-300x127.png 300w, https://www.oscarhenriquezg.net/images/2017/07/http-basic-768x326.png 768w, https://www.oscarhenriquezg.net/images/2017/07/http-basic-700x297.png 700w, https://www.oscarhenriquezg.net/images/2017/07/http-basic.png 1354w" sizes="(max-width: 523px) 100vw, 523px" /> 

Hydra es muy versátil en cuanto al tipo de autenticaciones que soporta, según nos indica su documentación:

> _Suported services: adam6500 asterisk cisco cisco-enable cvs ftp ftps http\[s]-{head|get|post} http[s]-{get|post}-form http-proxy http-proxy-urlenum icq imap[s] irc ldap2[s] ldap3[-{cram|digest}md5\]\[s\] mssql mysql nntp oracle-listener oracle-sid pcanywhere pcnfs pop3[s] rdp redis rexec rlogin rpcap rsh rtsp s7-300 sip smb smtp[s] smtp-enum snmp socks5 teamspeak telnet[s] vmauthd vnc xmpp_

En mi caso ya conocía el nombre de usuario &#8220;admin&#8221; ya tenía la mitad del trabajo hecho, sabía que la password era una combinación sencilla y sabía que la autenticación era básica vía http, entonces fui armando el comando a ejecutar:

**-l**: Indico el login (_admin_ en mi caso)  
**-P**: Indico la ruta del archivo de passwords a utilizar (el diccionario _500-worst-passwords.txt_ en mi caso)  
**-e**: Realiza algunos chequeos adicionales **_n_**= prueba null como password **_s_**= prueba el login como password.  
**-f**: Termina la ejecución una vez encuentra la password.  
**-V**: Verbose, muestra los intentos de passwords que va probando por pantalla.

Quedando el comando así:

<pre class="theme:terminal lang:default decode:true">hydra -l admin -P /Users/miuser/Desktop/500-worst-passwords.txt -e ns -f -V 192.168.1.1 http-get</pre>

Probé sin mucha fé y a los segundos ya tenía la clave en mis manos: _**abc123**_, jajaja como no haberlo pensado antes.

Un buen sitio donde encontrar muchos diccionarios de todo tipo es este: <https://github.com/danielmiessler/SecLists/tree/master/Passwords> créditos para el usuario _danielmiessler_ de github que se dio el trabjo de recolectar estos archivos.