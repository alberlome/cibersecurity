# Máquina JaulaCon2025

Nombre: JaulaCon 2025\
Objetivo: 172.19.142.216

***

Fase de Recopilación

Comenzamos realizando un ping a la máquina objetivo.

ping 172.19.142.216

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Seguimos con un nmap para ver que nos detecta en la máquina objetivo, y lo almacenamos en un fichero como primera prueba.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>Output comando nmap</p></figcaption></figure>

Tenemos un puerto 80, y un puerto 22 ssh. Vamos a visitarlos.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption><p>Web puerto 80</p></figcaption></figure>

Vale en el puerto, 80, tenemos una página web con los estilos rotos parece, vamos a revisar el código fuente de la web.

Vamos a hacer un poquito de fuzzing.

Visitamos la URL robots.txt

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Vamos a usar la herramienta GoBuster, para buscar si tiene directorios ocultos.

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Output comando GoBuster</p></figcaption></figure>

He buscado tanto en directorios como en ficheros y me ha encontrado solo los siguientes directorios. /0 y /admin, este último me redirige a un sitio web llamado jaulacon2025.thl

He revisado con Wappalyzer lo que está corriendo en la máquina objetivo.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Output Wappalyzer</p></figcaption></figure>

Podemos ver que está usando un CMS poco común llamado "Bludit", vamos a buscar si existe alguna vulnerabilidad para ese CMS.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Output exploitDB</p></figcaption></figure>

Vale podemos ver que existen múltiples exploits para este CMS, ahora nos queda averiguar la versión del CMS.

Buscando la versión en el view-source del código fuente de la página web.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Source-code página web</p></figcaption></figure>

Buscando por el nombre de versión, he visto ese fichero de bootstrap y otro de JQuery, que estaban siendo importados desde un directorio "bl-kernel", que le llama Bludit Core, así que vamos a visitar esa carpeta.

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Output directorio bl-kernel</p></figcaption></figure>

Eso significa que la opción _followSymLinks_ en el servidor Apache, está configurada por defecto y podemos visitar los directorios y ficheros de ese directorio en el servidor.

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
