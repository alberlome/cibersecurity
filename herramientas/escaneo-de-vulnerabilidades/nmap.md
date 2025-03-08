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



## **Banderas mas usadas**

### Detectar Sistema Operativo

```
$ sudo nmap -O 10.20.30.40
```

Esto realiza una inspección a nivel bastante bajo para determinar el sistema operativo del objetivo. Es un poco más detallado que las diferencias estándar de TTL entre Linux y Windows (el TTL de los paquetes en Linux comienza en 64, mientras que en Windows comienza en 128). También intenta realizar alguna negociación con el objetivo para determinar la previsibilidad de la secuencia TCP, lo que puede usarse para identificar ciertas versiones de un sistema operativo. Evidentemente, también es posible estimar el tiempo de actividad del objetivo observando la opción de marca de tiempo TCP, pero esto solo es visible al agregar la bandera -v de modo detallado.

### Escaneo rápido

```
$ sudo nmap --min-rate 10000 10.20.30.40
```

Usa esto con moderación. Si quieres enviar paquetes al objetivo lo más rápido posible, ajusta el valor de --min-rate a algo alto, como 10,000. Esto enviará al menos 10,000 paquetes al objetivo por segundo (posiblemente más rápido), por lo que hacerlo tan alto aumentará los falsos positivos (o falsos negativos). Úsalo solo si sabes que la red no está tan congestionada o tiene una cantidad razonable de ancho de banda. Esto no es necesario a menos que tengas prisa o algo similar. Igualmente, puedes especificar --max-rate 1 para enviar un paquete por segundo, o 0.1 para enviar un paquete cada 10 segundos, etc., para ser lento y pausado.

### Mejor forma de aumentar/disminuir la velocidad

```
$ sudo nmap -T 0 10.20.30.40
```

Puedes usar la bandera -T y elegir un número del 0 al 5 para establecer una plantilla de tiempo. Esto es equivalente a configurar unas 10 banderas diferentes para especificar tiempos de ida y vuelta, paralelismo, retrasos de escaneo y reintentos (entre otras cosas). Una plantilla de tiempo de 0 será "paranoica", lo que será extremadamente lenta, operando bajo el radar tanto como sea posible a costa de tiempo, y una plantilla de 5 será extremadamente rápida y agresiva, lo que podría causar problemas en el host objetivo. Se debe tener precaución de no usar una plantilla de tiempo de 5 a menos que estés dispuesto a aceptar que el resultado final sea una denegación total de servicio, pero entre tú, yo y el farol, si tu host se cae después de un escaneo rápido con nmap, mi opinión experta es que no tiene ningún derecho a estar disponible en ninguna red desde el principio. Como referencia, una plantilla de tiempo de 3 es la plantilla de escaneo por defecto.

### Acortar el Ippsec Special <a href="#shorten-the-ippsec-special" id="shorten-the-ippsec-special"></a>

```
$ sudo nmap -A 10.20.30.40
```

Esto realizará una verificación de versión, escaneo de scripts por defecto, detección de sistema operativo y realizará un traceroute mientras lo hace. Claro, puedes usar esto en lugar de cualquiera de las otras cosas que mencioné antes.

### Logging

```
$ sudo nmap -oA portscan 10.20.30.40
```

Hay varios formatos a los que puedes exportar. -oA exporta a los tres principales, que son salida normal (-oN), en formato que se puede buscar con grep (-oG) y XML (-oX). Proporciónale un nombre de archivo y creará 3 archivos con diferentes extensiones. Por supuesto, un agradecimiento a -oS filename, que exporta en formato script.

### Resolución de DNS

```
$ sudo nmap -Pn 10.20.30.40
```

Si sabes con certeza que el host está en línea pero no responde a los pings, usa la bandera -Pn para omitir el descubrimiento estándar del host e intentar escanear de la manera tradicional. Esto saltará el primer paso de determinar si el host está realmente activo. Si no incluyes esto, lo primero que hará nmap será sus comprobaciones estándar de "¿estás vivo?" para determinar si el host está activo. Si falla esas comprobaciones, asumirá que el host está caído y no continuará con el escaneo. Sin embargo, algunos hosts bloquearán directamente los paquetes ICMP y solo abrirán los puertos que necesitan. En ese caso, agregarías esta bandera para deshabilitar las comprobaciones y asumir que el host está activo de todos modos. Luego intentará conectarse a los puertos a los que normalmente se conecta y determinar qué está escuchando.

### Escaneo de Nmap a través de un proxy

```
$ sudo nmap -sT --proxy socks4://40.40.50.50:5789 10.20.30.40
```

Suponiendo que tienes un proxy socks4 escuchando en 40.40.50.50:5789, esto intentará canalizar toda la comunicación a través del proxy para llegar al lado remoto. Ten en cuenta que solo puedes usar escaneos TCP a través de aquí debido a la naturaleza del tráfico a través de proxy. Otra opción es usar _**proxychains**_

## Nmap Scripts <a href="#nmap-scripts" id="nmap-scripts"></a>

Personalmente, no encuentro que los scripts de nmap sean tan útiles, aunque ocasionalmente tienden a sorprenderme. Siento que hay herramientas mejores y más flexibles para lograr lo que nmap puede hacer con scripts, pero si tienes la capacidad, ¿por qué no aprender?

### Ejecutar Scripts Seguros y Revisar Servicios Vulnerables

```
$ sudo nmap -p 22,80,443 --script "vuln and safe" 10.20.30.40
```

Ten en cuenta que estoy especificando puertos. Puedes ejecutar todos los scripts que están categorizados como "Seguros" (que generalmente no generan muchas alertas), así como revisar servicios vulnerables (que generalmente generan alertas). Por ejemplo, esto no solo intentará realizar una comprobación de versión en el servidor web, sino también intentar ver si es vulnerable a algo como el ataque [_Slowloris_](https://en.wikipedia.org/wiki/Slowloris_\(cyber_attack\)).

### Http-enum

```
$ sudo nmap -p 80 --script http-enum 10.20.30.40
```

Este script funciona de manera similar a [Nikto](https://hackertarget.com/nikto-website-scanner/). Busca varios archivos interesantes que pueden estar en el servidor. Existen herramientas mejores que este script.

### Smb-enum-users

```
$ sudo nmap -p 139,445 --script smb-enum-users --script-args 'smbusername="admin",smbpassword="password"' 10.20.30.40
```

Lo anterior es bastante interesante, hay que admitirlo. Puedes intentar iniciar sesión en un servicio SMB y volcar los usuarios. Puede que haya mejores herramientas, pero es una buena opción tenerla. Si omites los argumentos del script, intentará iniciar sesión como un usuario invitado sin contraseña.

## LDAP <a href="#ldap" id="ldap"></a>

Nmap definitivamente tiene algunos scripts de enumeración LDAP bastante decentes que he utilizado en más de una ocasión.

### **ldap-rootdse**

```
$ sudo nmap -p 389 --script ldap-rootdse 10.20.30.40
```

Lo anterior intentará negociar con el servidor LDAP y obtener el DSE, que es la Entrada Específica del DSA (donde DSA significa Agente del Sistema de Directorio). Esto es útil para encontrar el contexto de nombres por defecto, el nombre del equipo y varias otras cosas interesantes sobre un servidor LDAP (como un servidor AD).

### **ldap-search**

```
$ sudo nmap -p 389 --script ldap-search --script-args 'ldap.username="<ldap bind string>",ldap.password="<ldap password>", etc' 10.20.30.40
```

Esto realizará una búsqueda LDAP contra el objetivo. Esto es interesante, pero sinceramente es mejor usar _**ldapsearch**_ para esto. De todos modos, puedes leer sobre cómo usarlo aquí si tienes curiosidad.

Sin embargo, más allá de lo anterior, no hay mucho motivo para usar el último. Existe un script ldap-brute que, como lo adivinaste, realiza un ataque de fuerza bruta sobre la autenticación LDAP bind. Pero hay scripts mejores y más flexibles para hacer exactamente eso. _**CrackMapExec**_ es el primero que me viene a la mente. Lo hace bien, lo hace rápido y lo hace más fácil que el script de nmap.

\
Conclusión
----------

Lo mejor que puedo mencionar aquí es que nmap es una herramienta súper útil. Tiene un motor de scripting que, en mi opinión, es en su mayoría innecesario. Es útil al principio, pero siempre hay herramientas mejores para lograr lo que necesitas. Desde el inicio hasta el control total, nmap suele ser uno de los primeros pasos que tomarías, pero en la mayoría de los casos sirve para determinar dónde enfocarse a continuación. Es muy útil al inicio de un ataque, también útil después de intentar moverse lateralmente dentro de una red. Pero los scripts son simplemente indiferentes.
