---
description: 'Dificultad: Muy fácil'
---

# Máquina INJECTION

Esta máquina la podemos encontrar en la web de [**DockerLabs**](https://dockerlabs.es/), perteneciente a ["El Pingüino de Mario"](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg), que está categorizada como "muy fácil" y que he decido comenzar por ella.

Como una de las cosas mas importantes dentro de una auditoría informática ya sea de ciberseguridad o no, es la enumeración de lo que vayamos descubriendo, se hace indispensable disponer de una enumeración adecuada a los hechos que se van produciendo.



**Paso Cero**

Activada la VPN a Suiza, con una máquina virtual Kali Linux, nos vamos a la web de DockerLabs del Pingüino de Mario, y nos descargamos la primera máquina modo "Muy Fácil" que nos encontramos.

Una vez que estamos en la consola de Kali Linux, nos creamos abrimos un Terminal, nos copiamos la máquina que nos hemos descargado recientemente (llamada "injection") y la pegamos en nuestra carpeta de trabajo.

Abrimos la ruta de la carpeta, descomprimimos el fichero ZIP y tenemos dos ficheros.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Extracción del fichero zip</p></figcaption></figure>

Ahora modificaremos los permisos de la máquina para que disponga de permisos de ejecución y la ejecutaremos en nuestra Terminal.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Ejecución de la máquina en nuestro Docker local</p></figcaption></figure>

Una vez ejecutada, como no tenemos Docker lo primero que hace es instalarlo.

Una vez instalado Docker en esta máquina virtual, termina por decirnos la dirección IP de la máquina que acabamos de desplegar y su dirección IP, para acceder a ella.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Despliegue de la máquina en nuestra terminal</p></figcaption></figure>

Ok, nos abrimos una terminal y lanzamos un comando contra la máquina para comprobar si nos responde.

```bash
ping 172.17.0.2
```

Podemos ver que nos está retornando paquetes ICMP, así que está encendida.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Ahora lanzaremos un comando nmap para comenzar con la enumeración de servicios, y puertos que tiene disponibles esta maquina.

```bash
nmap -sV 172.17.0.2
```

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Hemos encontrado los siguientes puertos:&#x20;

* 22/tcp open ssh OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)&#x20;
* 80/tcp open http Apache httpd 2.4.52 ((Ubuntu))

Disponemos de una conexión por SSH y un Apache, que estará sirviendo una web. Vamos a probar a entrar en esa web desde un navegador, poniendo en la URL del navegador esa dirección IP.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Web de login realizada en PHP</p></figcaption></figure>

Al entrar podemos ver un login y password. Vamos a revisar su código fuente para ver si encontramos algún indicio mas.

Vamos a probar con las típicas contraseñas... de _admin_, _administrator_... y parece que tampoco pasamos de la autenticación.

Hemos intentado conectarnos por SSH y tampoco hemos conseguido entrar, dado que nos pide una contraseña con el usuario Kali.

Ok, podemos probar con la herramienta **DirBuster**, pero no logro hacerla funcionar.



