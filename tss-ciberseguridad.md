# 🛡️ TSS Ciberseguridad

Practica

Crear una red en la que esté el Windows 7, XP, 2008 y 2003

Hallar dos vulnerabilidades por objetivo.

Lo primero que todo lo suyo sería encender todas las máquinas al mismo tiempo para simular una red en la que existieran todos esos HOST levantados al mismo tiempo. Pero como mi máquina no tiene los recursos necesarios para levantar 5 maquinas virtuales con solvencia, y realizar el escaneo de NMAP contra la red poniendo el /24, voy a resolver la práctica máquina a máquina.

```
db_nmap 192.168.44.0/24 -sP -v
```

Windows 7

Nos vamos directamente a Metasploit en nuestra máquina Kali Linux, nos generamos un nuevo _workspace_ para esta práctica, y lanzamos _db\_nmap_ desde _Metasploit_.

```
db_nmap -p- 192.168.44.134 -sS -v -O
```

<figure><img src=".gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

He usado el nmap con el comando "_db\__" para que los resultados obtenidos nos los guarde directamente en la base de datos del _workspace_ que estamos utilizando, para posteriormente atacarlos.

Podemos ver que se están usando 3 servicios en los siguientes puertos.

<figure><img src=".gitbook/assets/image (30).png" alt=""><figcaption><p>Salida por pantalla de los servicios detectados</p></figcaption></figure>

Ahora para averiguar todo lo relacionado acerca de los servicios que tiene disponibles la máquina voy a ejecutar el siguiente comando de nmap.

```
db_nmap -sV --version-intensity 5 192.168.44.134
```

<figure><img src=".gitbook/assets/image (31).png" alt=""><figcaption><p>Captura de pantalla de la ejecución de dicho comando</p></figcaption></figure>

Una vez incluidos en los registros de la base de datos de nuestro workspace, continuamos y vamos a intentar de hallar las vulnerabilidades de algunos de estos servicios que puedan ser explotados.

Podemos ver que para MSRPC, existe un exploit

<figure><img src=".gitbook/assets/image (32).png" alt=""><figcaption><p>Salida por pantalla de la búsqueda</p></figcaption></figure>

Si escribimos info 0, podemos ver que el exploit trata de realizar un "buffer overflow" (sobrecarga del buffer) sobre el interfaz RPC de Microsoft.

Por netbios ssn, me aparecen estos

<figure><img src=".gitbook/assets/image (33).png" alt=""><figcaption><p>Salida del comando search netbios</p></figcaption></figure>

Vamos a ir a por la vulnerabilidad del RPC de Windows.

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

Me he percatado de que necesito el nombre del _HostName_ víctima. Para poder averiguarlo voy a buscar una vulnerabilidad contra _NetBIOS_.

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption><p>Salida del comando Netbios</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (37).png" alt=""><figcaption><p>Salida por pantalla del Scanner Netbios para averiguar el nombre</p></figcaption></figure>

Nombre Netbios: WIN-AS7K2BT0SNN

Ahora si que podemos volver a nuestro vulnerabilidad anterior (MSRPC), y completar el campo que nos faltaba para poder explotarla.

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

Bien una vez completada la información procederemos a realizar el ataque.

ENcontre en search algo que me ofrecia mas información acerca del host mediante un escaner de RDP. Ahora en services tengo la siguiente información.

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>



