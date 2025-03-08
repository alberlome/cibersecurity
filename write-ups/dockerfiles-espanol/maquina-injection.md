---
description: 'Dificultad: Muy fácil'
---

# Máquina INJECTION

Fecha: 07 de Marzo de 2025

Objetivo: 172.17.0.2

***





## **Fase de Reconocimiento**

En esta fase lo mas importante es obtener la mayor enumeración de información disponible acerca de nuestro objetivo.&#x20;

Ahora nos abrimos una terminal y lanzamos un comando contra la máquina para comprobar si nos responde.

```bash
ping 172.17.0.2
```

Podemos ver que nos está retornando paquetes ICMP, así que está encendida.

<div align="left"><figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Ping a la máquina víctima</p></figcaption></figure></div>

Ahora lanzaremos un comando nmap para comenzar con la enumeración de servicios, y puertos que tiene disponibles esta maquina.

<pre class="language-bash"><code class="lang-bash"><strong>nmap -sV 172.17.0.2
</strong></code></pre>

<div align="left"><figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Nmap averiguando que servicios están disponibles</p></figcaption></figure></div>

## Fase de Explotación

Hemos encontrado los siguientes puertos:&#x20;

* 22/tcp open ssh OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)&#x20;
* 80/tcp open http Apache httpd 2.4.52 ((Ubuntu))

Disponemos de una conexión por SSH y un Apache, que estará sirviendo una web. Vamos a probar a entrar en esa web desde un navegador, poniendo en la URL del navegador esa dirección IP.

<div align="left"><figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Web de login realizada en PHP</p></figcaption></figure></div>

Al entrar podemos ver un login y password. Vamos a revisar su código fuente para ver si encontramos algún indicio mas.

Vamos a probar con las típicas contraseñas... de _admin_, _administrator_... y parece que tampoco pasamos de la autenticación.

Hemos intentado conectarnos por SSH y tampoco hemos conseguido entrar, dado que nos pide una contraseña con el usuario Kali.

Ok, podemos probar con la herramienta **DirBuster**, pero no logro hacerla funcionar.

### SQL Injection

Parece que me estoy desviando del camino. Puede que si realizo una _**SQL Injection,**_ vamos a probar con la inyección SQL clásica para intentar entrar por este método introduciendo _"**admin' or 1=1-- -**"_ para que siempre sea verdadero, y cualquier cosa en la _**password**_.

<div align="left"><figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>Probando la inyección SQL</p></figcaption></figure></div>

Y _vuala_, acabamos de acceder al sistema. Vemos como la web nos entrega un mensaje de bienvenida para el usuario Dylan. Y nos revela la contraseña del mismo.

## Fase de Post-Explotación

Podría ser que esa contraseña sirva para entrar por la consola SSH, y así poder hacer una escalada de privilegios y ya entrar hasta en la cocina...

```bash
ssh dylan@172.17.0.2
```

Ponemos la contraseña que hemos encontrado y...

<div align="left"><figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure></div>

Buscamos los ficheros con permisos de usuario root

```
find / -perm -4000 -user root 2>/dev/null
```

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Acabamos de obtener acceso a la máquina.

```
sudo env /bin/sh
```

<div align="left"><figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

Fin de la auditoría.

```bash
                             | |
  _____      ___ __   ___  __| |
 / _ \ \ /\ / / '_ \ / _ \/ _` |
| (_) \ V  V /| | | |  __/ (_| |
 \___/ \_/\_/ |_| |_|\___|\__,_|
```
