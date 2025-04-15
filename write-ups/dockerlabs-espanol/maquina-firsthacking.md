---
description: 'Dificultad: Muy fácil'
---

# Máquina FIRSTHACKING

Fecha: 19 de Marzo de 2025

Objetivo: 172.17.0.2

***

## Fase de reconocimiento

Comenzamos haciendo un ping a la máquina para ver si nos contesta y está encendida.

```
ping 172.17.0.2
```

Ok, la máquina está encendida, podemos comenzar.

Primero haremos un nmap para ver que protocolos están ejecutándose en la máquina objetivo.

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Captura comando nmap</p></figcaption></figure>

`sC` = Equivalente a --script=default esto lanza algunos scripts simples de reconocimiento

`sV` = Este argumento instruye a Nmap para intentar identificar la versión de los servicios que se detectan. Esto puede ser útil para determinar si un servicio en particular tiene vulnerabilidades conocidas.

Podemos ver que el puerto 21 correspondiente al servicio del FTP, está ejecutando la versión de _vsftdp_ 2.3.4. Podríamos intentar conectarnos por FTP a ese servicio para ver que nos retorna.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Captura comando FTP - conexión rechazada</p></figcaption></figure>

Al intentar conectarme con el usuario root, poniendo una contraseña _random_, la conexión es rechazada. Lo que me hace pensar si existirá algún tipo de vulnerabilidad para el servicio FTP en la versión "_vsftpd_ 2.3.4", vamos a buscar en Google.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Búsqueda en Google de la versión de SFTPD</p></figcaption></figure>

Podemos ver que existe algún tipo de vulnerabilidad relacionada con ese servicio ftp, y posiblemente se trate de un _"backdoor command execution"_ , vamos a seguir investigando.

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Captura pantalla web de rapid7</p></figcaption></figure>

Podemos ver en la captura de pantalla que esta vulnerabilidad puede explotarse mediante un exploit en Metasploit, además de mas detalles acerca de cuando se descubrió la vulnerabilidad y de cuando fue parcheado.

Entonces ahora nos iremos a Metasploit y usaremos el exploit para intentar obtener acceso al FTP.

```
msfconsole
```

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida del arranque de Metasploit</p></figcaption></figure>

Si es tu primera vez en _msfconsole_ y tienes que instalarla de cero, te invito a que revises esta [guía](https://ciberseguridad.alberlome.com/herramientas/ataques-de-diccionario/metasploit) para que veas como realizar la instalación correctamente.

Una vez que tenemos cargado el nmap en la base de datos de _Metasploit_, procedemos a configurar el exploit para poder realizar el ataque.

Usaremos el comando searchsploit:

```
searchsploit vsftpd 2.3.4
```

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida del comando searchsploit</p></figcaption></figure>

Lo descargamos con el siguiente comando:

```
searchsploit -m unix/remote/49757.py
```

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption><p>Descarga del exploit </p></figcaption></figure>

Ahora vamos a ejecutar el exploit. Nos salimos de Metasploit. Y ejecutamos el exploit.

```
python3 49757.py 172.17.0.2
```

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>Salida del comando</p></figcaption></figure>

Para entender mejor, como hemos obtenido una _Shell_ en la máquina remota siendo root, podemos analizar el exploit que es lo que hace, abriendo su código con nano, _Vim_, o tu editor preferido.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption><p>Código fuente del exploit que acabamos de utilizar</p></figcaption></figure>

Simplemente podemos ver que está escrito en Python, (por como se define la función "_handler_").

Comenzamos importando una serie de librerías para poder utilizar _Telnet_, _argparse_, y _signal_.

Comenzamos definiendo una función llamada _Handler_, que tiene como parámetros "_signal\_received_" y "_frame_". Dentro de esta función vemos que imprime por pantalla la palabra _Exiting_ y realiza el comando _exit_(0) que entiendo que se utiliza para cerrar la sesión.

Primero que nada el exploit, ejecuta la función _signal_, a la que le pasa los argumentos de SIGINT, y handler, crea una variable parser con la clase _argparse_ y su función _ArgumentParser_().

Luego utiliza _parser_ para añadir los argumentos a la acción, como host y help, y establece _type_ como _str_.

declara _args_, hosts, el puerto FTP (si tuviéramos que modificar el puerto, se cambiaria aquí)

el usuario, que podemos ver que es una :) y el _pass_, que es _PASS pass_.&#x20;

Luego ejecuta el comando TELNET, con la misma información y el puerto 21 escrito en la variable del FTP, hace un _encoder_ en _ASCII_, y ejecuta el comando TELNET para realizar una llamada a la acción.



