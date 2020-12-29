
---
id: 1000
title: Trucazos SSH
date: 2020-02-22T10:15:38+00:00
author: Oscar
layout: post
categories:
  - Software
---

Trucazos SSH

Dejo acá registro de estos trucazos SSH que nos pueden salvar la vida:

```
ssh-copy-id root@server.com:
```


Copio mi llave publica al .ssh/authorized_keys del server.com y así no me pide más pass para entrar.

```
ssh -t root@server.com comandoaejecutar
```


Corro un comando remoto en el server, sin meterme al server, también puedo mandar procesos al backgroud con &

```
ssh -D 8080 root@server.com
```


Creo un proxy socks en el server ssh y me permite navegar configurándolo en mi navegador.

```
ssh -X root@server.com
```


Corro una app con GUI en el servidor y se me muestra en mi máquina. Lo pruebo con xclock o firefox o cualquier otra app con GUI.

Túnel SSH
Escenario:

Necesito llegar al server2, pero no tengo tráfico directo, entonces utilizo el server1 como puente para llegar al server2.

```
ssh -L 2020:server2:22 root@server1
```


Desde mi pc me conecto al server1, abro el puerto 2020 y lo apunto al puerto 22 de server2.

Luego desde mi pc me conecto al puerto 2020 de server1 y me entrega una pasarela directa al servicio SSH que se está entregando en el server2.

De esta manera sin llegar de forma directa al server2 puedo consumir sus servicios desde mi pc.

http://163.250.212.40/wp/wp-content/uploads/2020/02/img_5e4eab3355a51.png

 

Túnel reverso SSH
Escenario:

El user (negro) necesita llegar al server2, pero no puede ya que el server2 esta tras un firewall.

```
ssh -R 2020:server2:22 user@server1
```


El usuario habilitador (rojo) expone el puerto 22 del server2 en el puerto 2020 del server1 ya que el user (negro) no llega directamente al puerto 22 del server2 porque hay un firewall que se lo impide.

http://163.250.212.40/wp/wp-content/uploads/2020/02/Diagrama2-1-1024x