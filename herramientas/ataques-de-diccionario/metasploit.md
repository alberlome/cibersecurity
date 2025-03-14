# Metasploit

Instalar Metasploit de 0

Para eso vamos a ejecutar METASPLOIT.

En esta máquina es la primera vez que voy a instalar METASPLOIT. Para ello tenemos que revisar el estado de la base de datos postgresql, primeramente, para ello lanzaremos el comando.&#x20;

```
service postgresql status
```

Nos retorna el estado de la BBDD postgresql, en mi caso disabled. Eso quiere decir que vamos a intentar levantarla con un  start o sino tendremos que instalarla.

Vale ya tengo levantada la base de datos postgresql



<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Como encender la base de datos postgresql y revisar su estado</p></figcaption></figure>

Iniciar metasploit lanzando el siguiente comando

```
msfconsole
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Output ejecutar metasploit</p></figcaption></figure>

Con el comando HELP podemos ver un montón de información, con todo lujo de detalles todo bien explicado en inglés.&#x20;

Lo primero de todo como es la primera vez que iniciamos Metasploit, vamos a lanzar el comando de inicialización para que cree las bases de datos, tablas, registros, etc... que necesita para funciona.

```
msfdb init
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Output comando msfdb init</p></figcaption></figure>

Este comando es necesario solo la primera vez que instalamos Metasploit en la máquina.

Ahora, cerramos la máquina con un exit y volvemos a ejecutar el comando para iniciar metasploit.

```
msfconsole
```

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Salida del output de bienvenida de metasploit</p></figcaption></figure>

que debemos hacer en metasploit es crearnos un workspace (un área de trabajo) para comenzar.

```
workspace -a [name]
```

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Output de varios parámetros con el comando workspace</p></figcaption></figure>

Lo primero que hice es un NMAP desde aqui en metasploit.

```
nmap -v -A 172.17.0.2
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Output nmap en Metasploit</p></figcaption></figure>

Donde podemos ver que esta usando el protocolo SSH con la versión OpenSSH 7.7 (protocolo 2.0). Si ahora hacemos una búsqueda en la BBDD de las vulnerabilidades del puerto SSH con el siguiente comando.

```
search ssh_version
```

Podemos ver que existen una serie de auxiliares para la versión 2.0 de SSH.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Output del comando search ssh_version</p></figcaption></figure>

Vuelvo a hacer un nmap, y me lo guardo en un fichero xml para subirlo como base de datos a metasploit.

Primero se ha de crear un fichero xml vacio, con el comando:

```
touch results.xml
```

Y luego ejecutamos el comando nmap con estos parámetros:

```
nmap -p- -O -v -oX results.xml 172.17.0.2
```

Si hacemos un cat del fichero en la consola podemos ver lo que ha generado el comando.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Output cat fichero generado por  la herramienta NMAP</p></figcaption></figure>

Ahora ya podemos volver a nuestra terminal con Metasploit, y ejecutar el comando para importar esa base de datos.

```
db_import results.txt
```

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Output db_import</p></figcaption></figure>

Si ahora ejecuto el comando hosts, podemos ver la información que hemos  traído de nuestra importación xml.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Dentro de metasploit es importante dominar los comandos de&#x20;

rhosts&#x20;

options

services

Y visualizar la ayuda (help) para todo aquello que se tengan dudas
