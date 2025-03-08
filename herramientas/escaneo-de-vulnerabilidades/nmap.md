---
description: >-
  Nmap es uno de los pilares fundamentales de las pruebas de penetración. Es uno
  de los primeros comandos, si no el primero, que ejecutas antes de considerar
  en qué superficie de ataque enfocarte.
---

# Nmap

En la web de [Agr0HacksStuff ](https://agrohacksstuff.io/posts/my-nmap-cheat-sheet/#typical-usage)detalla muy bien los distintos usos de las distintas opciones de parametrización con nmap.

## Que es NMAP

Es la manera de descubrir qué hace el servidor, cómo escucha, cómo interactúa, etc. Es el equivalente digital de caminar alrededor del perímetro de un edificio con una linterna, iluminando ventanas y puertas, buscando métodos de ingreso.

Y vaya que tiene su buena cantidad de argumentos en la línea de comandos para personalizar tus escaneos.

Estoy escribiendo este documento para tener una forma rápida y sencilla de referirme a los comandos que suelo ejecutar con nmap sin tener que consultar su guía de referencia. Ejecutaré algunos comandos estándar que normalmente uso, seguidos de algunos parámetros en los que debería enfocarme. Sin embargo, para el registro, consideraré el objetivo imaginario 10.20.30.40. También cabe mencionar que el tipo de escaneo predeterminado que nmap realiza con TCP es un escaneo SYN, que se hace porque es el menos "agresivo". Por supuesto, un escaneo SYN solo se realiza si el usuario que lo ejecuta tiene la capacidad de capturar paquetes a un nivel bajo (es decir, el usuario root), de lo contrario, se realizará un escaneo CONNECT más "de capa 7", que es menos preciso ya que asume que el sistema operativo puede establecer una conexión adecuada para determinar un puerto abierto válido, pero me estoy metiendo demasiado en detalles.

En cualquier caso, un escaneo privilegiado predeterminado enviará paquetes SYN y registrará cuáles responden con un SYN/ACK en lugar de un REJ o FIN, y luego continuará a partir de ahí (aunque nmap generalmente te indicará si un puerto fue específicamente rechazado, lo que generalmente significa que hay un servicio escuchando en ese puerto pero está filtrado por un firewall local o alguna otra ACL, por lo que no puedes acceder a él desde tu ubicación actual). Creo que la razón original por la que los escaneos SYN son el predeterminado es que son los más sigilosos en comparación, ya que técnicamente no están estableciendo una conexión, sino simplemente iniciando el _**handshake**_. Pero no se engañen: cualquier IDS que valga la pena detectará un escaneo de nmap desde lejos, incluso un escaneo SYN.

## Usos típicos

### Ippsec Special <a href="#ippsec-special" id="ippsec-special"></a>

```
$ sudo nmap -sC -sV -oN portscan -v 10.20.30.40
```

Lo anterior escaneará el objetivo (solo en TCP) en los "1000 puertos más populares de nmap" por defecto. Intentará comunicarse con cada puerto abierto y obtener la versión del software que está escuchando en él (-sV). Si se conecta con éxito a un puerto y determina el servicio en ejecución, intentará ejecutar scripts predeterminados contra él (-sC), lo que realizará una enumeración básica. Por ejemplo, si se conectara a un servidor web en el puerto :80, ejecutaría cosas simples como GET / HTTP/1.1\r\n y devolvería el título de la página. Luego, registrará toda la salida en un archivo llamado portscan en formato "nmap" (-oN portscan), y finalmente será detallado (-v). Ejecutar esto en modo detallado te informará en el momento en que encuentre un puerto abierto, para que puedas intentar tu propia enumeración en el puerto antes de que nmap termine. Esto es útil si tienes prisa o algo así, supongo. Debo mencionar que _**Ippsec**_ generalmente usa -oA \<nombre del servidor> en lugar de lo anterior, pero generalmente no es necesario en un desafío de [_**HackTheBox**_ ](https://www.hackthebox.com/)o algo por el estilo. Aunque es bastante útil en compromisos en el mundo real, supongo.

Finalmente, quiero enfatizar el concepto de ejecutar nmap como root. El comando sudo es necesario ya que nmap utiliza capacidades de captura de paquetes al realizar escaneos, algo que solo root puede hacer. Claro, el binario de nmap seguirá funcionando, pero sin la capacidad de realizar un escaneo SYN, se realizará un escaneo TCP por defecto, que no realiza captura de paquetes, sino que inicia una conexión TCP a cada puerto e intenta negociar con él a nivel de aplicación. Esta capacidad limita la capacidad de nmap para detectar (como ciertamente he presenciado antes), por lo que los escaneos SYN generalmente se consideran la mejor opción, especialmente según la documentación de nmap

### Escanear todos los puertos

```
$ sudo nmap -p- -oN allports -v 10.20.30.40
```

En este escaneo, normalmente lo ejecuto después del comando especial de Ippsec. Esto verificará todos los puertos TCP abiertos en el rango de 0 a 65535. El -p- es una abreviatura del equivalente -p 0-65535. También cabe mencionar que guardo esto en un archivo llamado "allports".

### Escaneo específico de puertos TCP

```
$ sudo nmap -sU -oN udp-portscan -v 10.20.30.40
```

### Escaneo específico de puertos UDP

```
$ sudo nmap -sU -oN udp-portscan -v 10.20.30.40
```

Ten en cuenta que no estoy ejecutando escaneos de versión ni de scripts predeterminados, aunque podría hacerlo. Esto solo escaneará los primeros 1000 puertos más populares (según nmap). Ten en cuenta que esto tomará mucho tiempo ya que es UDP, y UDP no tiene que responder con una respuesta a una conexión de puerto si no quiere. Por lo tanto, intentará conectarse al puerto, enviar solicitudes de conexión predeterminadas al puerto y esperar una respuesta. Si no obtiene una, se dará por vencido y continuará, así que, como implica el seudónimo, UDP realmente significa _**Unreliable Damn Protocol**_ (Protocolo Maldito No Confiable).

### Escanear todos los puertos UDP

```
$ sudo nmap -sU -p- -oN udp-im-running-out-of-options -v 10.20.30.40
```

Si alguna vez ejecuto esto, es porque estoy completamente sin ideas, ya que esto tarda una eternidad en terminar. Esto escaneará todos los puertos de 0 a 65535 en UDP, utilizando el mismo método de "conectar y esperar" mencionado anteriormente. Esto toma tanto tiempo que generalmente ni siquiera me molesto con esto.

### Bypass de algunos IDS y firewalls

```
$ sudo nmap -Pn --source-port=9090 -f 10.20.30.40
```

YMMV con lo anterior. Esto se conectará desde un puerto de origen específico (para la evasión potencial de firewall), así como fragmentar los paquetes para engañar a IDS también.

### LLAMAR A TODOS LOS TIMBRES

```
$ sudo nmap -p- -T5 --max-retries 0 -v -oA allports --script /usr/share/nmap/scripts/ 10.20.30.40
```

Esto escaneará el objetivo con “agresión extrema”. También establece las retransmisiones sin límite, por lo que seguirá golpeando la puerta hasta que alguien responda, básicamente. Cuando lo hagan, lánzales todo lo que tengas, intentando ejecutar todos los scripts disponibles contra el puerto, sin preocuparte por la discreción. Esto es lo que ejecutas cuando quieres que sepan que estás ahí.



### Descubrimiento de Hosts mediante _"ping-seep"_ en una subred entera

```
$ sudo nmap -sn 10.20.30.0/24
```

Esto realizará un **ICMP ECHO** (además de algunas verificaciones similares adicionales) a todos los hosts en la subred **10.20.30.0/24**. No es raro que los hosts bloqueen ICMP, por lo que este puede no ser el método definitivo para determinar si un host realmente está ahí.

En muchas redes, también es posible bloquear ICMP en un firewall si estás atravesando redes. Así que si tu red es, por ejemplo, **10.10.10.0/24** y estás intentando hacer un **ping-**_**sweep**_ a **20.20.20.0/24**, un firewall puede bloquear ICMP por completo, por lo que no tendrás éxito ahí.

Tendrás mejores resultados si estás realmente dentro de la red que estás intentando escanear. Dicho esto, **nmap** hace un poco más que simplemente ejecutar un **ping** en todos los hosts, por lo que este método es un poco mejor que un **ping** estándar.

{% hint style="info" %}
Nota para cualquiera que esté ejecutando en una máquina virtual, específicamente en VMWare.
{% endhint %}

Si estás ejecutando esto en _**VMWare**_ dentro de una red **NAT**, ejecuta esto para hacer un **"ping-sweep"**:

```
$ sudo nmap -sn --unprivileged 10.20.30.0/24
```

Al realizar un **ping&#x20;**_**sweep**_ en un conjunto muy específico de condiciones, específicamente ejecutando una máquina virtual dentro de _**VMWare**_ con la configuración de red en **NAT** (que es la configuración predeterminada), es posible que obtengas una salida incorrecta en la que todos los hosts de la subred serán considerados activos.

La razón de esto es que, al operar con la bandera **-sn**, **nmap** verificará si un host de destino está activo utilizando los siguientes métodos:

* **nmap** recibe una respuesta **ICMP** a un paquete **ICMP ECHO\_REQUEST**.
* **nmap** recibe una respuesta **ICMP** a un paquete **ICMP TIMESTAMP\_REQUEST**.
* **nmap** recibe una respuesta **TCP SYN/ACK** a un paquete **443/TCP SYN**.
* **nmap** recibe una respuesta **TCP RST** a un paquete **80/TCP ACK**.

Al ejecutar **nmap** desde una máquina virtual en _**VMWare**_ como se indicó anteriormente, la red configurada puede generar una respuesta **TCP RST** a todos los paquetes **80/TCP ACK**, lo que puede engañar a **nmap** haciéndole creer que todos los hosts están activos.

Establecer la bandera **--**_**unprivileged**_ hará que **nmap** se ejecute asumiendo que no eres un usuario privilegiado con la capacidad de capturar tráfico en la red, por lo que se limitará a verificar solo conexiones al puerto **443**.

La mejor solución para esto es ejecutar tu máquina virtual en **modo puente (**_**bridged**_ _**mode**_**)** al realizar este escaneo para obtener resultados más precisos.



### Descubrimientos de Hosts: List Scan

```
$ sudo nmap -sL 10.20.30.0/24
```

Esto no es tan fiable porque no envía ningún paquete a los hosts de destino. Solo realiza búsquedas inversas en el servidor de nombres sobre las direcciones IP. Aun así, sigue siendo bastante encubierto, ya que no estás enviando paquetes a los hosts individuales, solo negociando con un servidor de nombres.

