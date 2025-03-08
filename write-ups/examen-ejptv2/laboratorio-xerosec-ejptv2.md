---
description: 'Dificultad: Difícil'
---

# Laboratorio Xerosec eJPTv2

Fecha: 06 de Marzo de 2025

Esta máquina la podemos encontrar en el canal de youtube de [xerosec ](https://www.youtube.com/watch?v=v20IsEd5nUU)donde nos presenta el Write-up de un **laboratorio** creado por el como entrenamiento para el examen de certificación del eJPTv2.

En el examen lo que determina si has superado la prueba o no, es el cuestionario de tipo test. Preguntas sobre la maquina, sobre el entorno del examen, etc. El examen no es un CTF, la metodología es ligeramente diferente, hay algunas máquinas donde no hay que escalar privilegios o máquinas en las que no te van a hacer preguntas y son "rabbit holes".

Conforme vayas resolviendo preguntas, podrás ver que te ayudan a resolver o afianzar las anteriores.

Letter engagement eJPTv2, es una carta que reúne las condiciones de la auditoria. En el examen usamos una máquina externa a la que nos vamos a conectar de forma remota, que tiene un número de herramientas que puede ser que no sean las que tu tienes en tu máquina.

Esa máquina no tiene conexión a internet, por lo tanto no puedes descargar mas herramientas.

Dispondremos un esquema de la configuración de red que disponemos en la carta de las condiciones. No tiene porque reflejar la configuración real del examen. Cuando comprometemos esta máquina se va a poner a prueba nuestra capacidad de hacer PIVOTING en una máquina.

Te especifica que todas las redes son /24 de Clase C.

Objetivos del examen es resolver las preguntas de tipo test y que están divididas en diferentes categorías.

Herramientas recomendadas que vamos a disponer durante el examen:

* Nmap
* Dirbuster
* Nikto
* WPScan
* CrackMapExec
* The Metasploit Framework
* Searchsploit
* Hydra

Enfocar esta simulación como si fuera una Auditoría de Caja Negra.

## Laboratorio uno - Primera máquina

Vamos a enumerar toda la red, todas las máquinas y optimizar esa enumeración de la mejor forma posible. No se tocan todas las técnicas del examen en este laboratorio, y poder determinar a la hora de poner mas énfasis a la hora de mejorar sus conocimientos.

Tomar notas, tomar capturas de pantalla (flameshot) es la mejor para hacer screenshots. (Notion + Flameshot combinación ganadora)

Draw.io, hacer el esquema de red --> app.diagrams.net

<figure><img src="../../.gitbook/assets/Esquema de la red.png" alt=""><figcaption><p>Esquema dibujado en Obsidian</p></figcaption></figure>

Vamos a descubrir cual es mi máquina atacante que me han dado para hacer el examen.

```
~ ip a
```

<figure><img src="../../.gitbook/assets/listar ip maquina.png" alt=""><figcaption><p>Retorno de consola del comando ejecutado ip a</p></figcaption></figure>

Donde podemos ver que la IP de nuestra MAQUINA KALI ATACANTE es 10.0.2.100

## Fase Recolección

Comenzar con la fase de enumeración de host discovery y port scanning.

Primero que nada nos crearemos una carpeta de trabajo, para almacenar las evidencias que vayamos encontrando.

Lo primero que tenemos que hacer es enumerar a que maquinas tenemos alcance desde esta máquina. Para ello ejecutaremos el comando NMAP con el que podemos hacer un barrido de red con ping usando el parámetro que se llama (-sn barrido c).

```
nmap -sn 10.0.2.0/24 
```

Esto hará que nmap inunde la red, enviando paquetes ICMP a todas las maquinas del segmento de red, y así podremos ver si tenemos conectividad con ellas. Lo que nos retorna esta salida por pantalla:

<figure><img src="../../.gitbook/assets/Pasted image 20250305163157.png" alt=""><figcaption><p>Comando nmap salida por pantalla</p></figcaption></figure>

10.0.2.1 sería la puerta de enlace que nos haría "Virtualbox", y luego el resto de máquinas que menos la nuestra.

Ahora ya tenemos una ligera idea de la distribución de la red, podemos crear nuestro esquema en draw.

Una vez que ya tenemos las máquinas descubiertas vamos a tirar de unas flags para acelerar un poco el escaneo por parte de nmap, la clásica min-rate de 5000, el -p- para recorrer todos el rango de los puertos, --open para que solo se nos guarde en ese reporte solo la información de los puertos abiertos, y sobre todas las ip's que se detallan a continuación y que el formato de salida con el parámetro -o de output -oN en un archivo con formato NMAP en un fichero llamado tcp\_scan.txt. Si tuviermos que escanear los puertos UDP, tendría que escanear estos.

```bash
sudo nmap -sS --min-rate 5000 -p- --open 10.0.2.43, 45, 46, 53, 55 -oN tcp_scan.txt
```

Si pulsamos la tecla INTRO, podemos ver el tiempo que le queda para terminar, y el porcentaje escaneado.

Esto va a darnos un fichero con todos los servicios y puertos a los que podemos acceder.

El parametro -pn evita el envio del paquete ICMP, y hace que ralentice el escaneo por parte de NMAP y genera ruido en la red.

<figure><img src="../../.gitbook/assets/Pasted image 20250305165013.png" alt=""><figcaption><p>Salida por pantalla del comando nmap</p></figcaption></figure>

Este es el barrido del escaneado de NMAP.

Cuidado con las máquinas de bulto que no todas son las máquinas son objetivo del ataque.

Que nos interersa ahora, nos interesa enumerar la versión de los servicios/softwares que están corriendo estas máquinas. Necesitamos optimizar esto, para hacerlo, usaremos una expresión regular muy sencilla.

Si no fijamos, empiezan siempre por un número 123/tcp, y así usar GREP para extraer la información relevante de la captura de NMAP.

Que extraiga todas las líneas que empiecen del 0 al 9.

```bash
grep '[0-9]$' tcp_scan.txt
```

Nos arroja un resultado tal que así.

<figure><img src="../../.gitbook/assets/Pasted image 20250305165350.png" alt=""><figcaption><p>Extraer la información mas importante de nmap</p></figcaption></figure>

Si le metemos el acento circuncejo al principio de la expresión regular, nos retornara aquellas líneas que comienzan por un número del 0 al 9 en su primer carácter

```bash
grep '^[0-9]$' tcp_scan.txt
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305165601.png" alt=""><figcaption><p>Haciendo greo del escaneo de nmap</p></figcaption></figure>

Ahora solo queremos los números y queremos quitar los números y organizarlo en dos columnas.

Para ello usaremos un cut de la información, que a partir del campo field solo queremos el -f1.

```bash
grep '^[0-9]$' tcp_scan.txt | cut -d '/' -f1
```

Y solo extraer aquello que necesitemos.

<figure><img src="../../.gitbook/assets/Pasted image 20250305165703.png" alt=""><figcaption><p>Listado de puertos a partir del output de nmap</p></figcaption></figure>

Ahora nos fijamos que estamos viendo que hay puertos que nos sobran porque están repetidos. Entonces ahora haremos un sort -u, para ello. Por lo tanto el comando se quedaría tal que así:

```bash
grep '^[0-9]$' tcp_scan.txt | cut -d '/' -f1 | sort -u
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305165903.png" alt=""><figcaption><p>Listado de puertos a partir del output de nmap</p></figcaption></figure>

Ahora queremos redirigir esto a xargs, en este contexto XARGS, va a redirigir el output a todo en una línea.

<figure><img src="../../.gitbook/assets/Pasted image 20250305170128.png" alt=""><figcaption></figcaption></figure>

en caso de NMAP necesitamos un formato de lista, con un separador de , (comas) en cada uno de ellos. Ahora vamos a sustituir con TR (translate) esos espacios en blanco a , (comas).

```bash
grep '^[0-9]$' tcp_scan.txt | cut -d '/' -f1 | sort -u | xargs | tr ' ' ','
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305170249 (1).png" alt=""><figcaption><p>Listado de puertos preparado para usar en comandos</p></figcaption></figure>

Con esto podríamos hacer un ALIAS para tenerlo disponible siempre.

Ahora vamos a proporcionarle a NMAP la lista de puertos que hemos recopilado. Para ello utilizaremos el siguiente comando:

Parámetros: -sC sirve para lanzar los scripts básicos de reconocimiento -sV sirve para que se enumere la versión de los servicios que están corriendo por los puertos abiertos y el nombre del software. -Pn me quita el host discovery -oN fichero output de salida para NMAP --open esto evita que en el archivo generado de nmap no se vean informacion de puertos cerrados en otras maquinas.

Lo mas recomendable es utilizar de nuevo --open en este segundo escaneo para tener un output de nmap lo mas limpio posible.

```bash
nmap -p135,139,22,25,445,49670,80 -sC -sV 10.0.2.43, 45, 46, 53, 55 -Pn -oN Full_scan.txt --open
```

Abrir el fichero en modo background con el ampersand & Mousepad nos abre en un editor de textos visual (similar al notepad) el fichero

```bash
mousepad Full_scan.txt&
```

Para que no se cierre el mousepad si se cierra accidentalmente la ventana

```bash
disown 
```

Podemos ver el fichero separado por IP's

Podemos ver el HOSTNAME de la MAQUINA 43. Pues me iré al DRAW.IO, y seguiré máquina por máquina rellenando la información relevante que vaya encontrando.

Vamos a comenzar por la MAQUINA 43.

<figure><img src="../../.gitbook/assets/Pasted image 20250305210006.png" alt=""><figcaption></figcaption></figure>

Tenemos un servicio SSH en el protocolo 22, version OPENSSH 7.4p1 Debian

* 80 http Apache
* 445 Samba

Primero crear una carpeta con el numero de la IP o del host

```bash
mkdir 10.0.2.43
```

Tenemos un servicio web en el puerto 80. Control + U para ver el código fuente. Mirar si existe un robots.txt

Podemos utilizar **dirbuster** para hacer una búsqueda de directorios: **OWASP DirBuster**

**DirBuster** tiene una interfaz visual, y es algo mas intuitiva que las herramientas command-line .

Filtros pre-configurados en **dirBuster**

<figure><img src="../../.gitbook/assets/Pasted image 20250305210424.png" alt=""><figcaption></figcaption></figure>

La URL objetivo, puerto 80, especificado previamente por el protocolo.

Se nos ofrece la opción de buscar el dicccionario de forma manual.

El que vamos a utilizar se encuentra en la ruta: **usr/share/worklists/dirbuster/directory-list-lowercase-2-3-medium.txt**

y debajo tenemos una serie de opciones, si dejamos esto marcado se va a hacer fuerza bruta, y va a ser recursivo, si es recursivo va a ser muy lento. En este caso no nos va a hacer falta y se desactivan los **brute force files.** Pulsamos START Podemos cambiar los hilos de ejecución a 200, para que vaya mas rápido.

No parece que nos estén enviando nada relevante. Entonces vamos a atacar los puertos SMB.

Parametro -L de List Parametro -N intentar entrar sin contraseñas validas

```bash
smbclient -L 10.0.2.43 -N
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305211408.png" alt=""><figcaption><p>Output comando smbCliente -L</p></figcaption></figure>

Una de las desventajas de SMB Clients es que a pesar de listar los recursos compartidos, no te lista los permisos que tienes sobre esos recursos compartidos.

**smbmap** para listar los permisos que tenemos sobre esos recursos.

```bash
smbmap -H 10.0.2.43
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305211547.png" alt=""><figcaption><p>Salida del comando SMBMap</p></figcaption></figure>

Y además de listar los recursos compartidos, nos lista los permisos que tenemos. En este caso parece ser por los visto que tenemos acceso anónimo.

Tambien podríamos haber usado **CrackMapExec** o **NetExec**, aunque en el contexto del examen no vamos a econtrar aun NetExec. Vamos a pasarle los siguiente parámetros.

Parámetros -u para proporcionar un usuario. Como no tenemos usuario, vamos a poner -u ' ' -p para la contraseña. Igual cadena vacía porque no la sabemos. --shares para listar los recursos compartidos de la máquina mediante SMB sin proporcionar credenciales.

```bash
crackmapexec smb 10.0.2.43 -u ' ' -p ' ' --shares
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305212016.png" alt=""><figcaption><p>Output comando crackmapexec</p></figcaption></figure>

Podemos ver que hemos obtenido información un poco mas detallada que con SMB Client. Si nos fijamos nos indica que tenemos permisos de lectura con una **null-session**. Esto lo podemos enumerar de una forma mas exhaustiva con **enum4linux**, se nos va a listar mas todavía.

Abusamos del protocolo SMB para obtener mas información.

```bash
enum4linux  10.0.2.43 
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305212632.png" alt=""><figcaption><p>Output comando enum4linux</p></figcaption></figure>

Le pasamos la ip, se nos esta enumerando información adicional, con mucha información incluso podemos ver usuarios, información que ya habíamos sacado antes. Esta herramienta nos permite enumerar el directorio linux en SMB

**smbclient** te permite un acceso mediante una consola interactiva a un recurso remoto que se encuentre en un servicio SMB. Por ejemplo:

```
smbclient //10.0.2.43/anonymous
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305212951.png" alt=""><figcaption><p>Output smbclient</p></figcaption></figure>

Ponemos contraseña la que sea, y nos deja entrar. Ahora vamos a meterle el parámetro -N para poder entrar con una null-session.

```
smbclient //10.0.2.43/anonymous -N
```

Así a través del prompt no nos pedirán ninguna contraseña para el usuario.

<figure><img src="../../.gitbook/assets/Pasted image 20250305213131.png" alt=""><figcaption></figcaption></figure>

dir o ls para listar los recursos compartidos

Vamos a traernos un fichero que se llama "attention.txt" si hubiera mas ficheros podríamos traernos mas información.

Con el comando de SMB, get podemos descargarnos el fichero encontrado.

```smb
smb: \> get attention.txt 
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305213342.png" alt=""><figcaption></figcaption></figure>

Ya se nos ha descargado el fichero y ahora vamos a ver su contenido con un cat.

```bash
cat attention.txt
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305213441.png" alt=""><figcaption></figcaption></figure>

Podemos ver que el fichero incluye posibles, enumeraciones de contraseñas.

Vamos a coger esas contraseñas y vamos a guardárnoslas en un fichero que se llame passwords. Para ello nos creamos un fichero.

```bash
nano passwords.txt 
```

Pero lo vamos a guardar en el formato típico de un diccionario de contraseñas que es una contraseña por línea.

<figure><img src="../../.gitbook/assets/Pasted image 20250305213717.png" alt=""><figcaption></figcaption></figure>

Control + O - guardar y salir de nano

Vimos que había un usuario que se llamaba NOBody y otro usuario que se llamaba Helios.

Con el parámetro --users en crackmapexec podemos encontrar los usuarios.

```bash
crackmapexec smb 10.0.2.43 -u '' -p '' --users
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305214016.png" alt=""><figcaption></figcaption></figure>

Tenemos un usuario llamado HELIOS y 3 contraseñas. Ahora vamos a intentar VALIDAR esas contraseñas. Para ello vamos a usar crackmapexec para ello.

Vamos a utilizar el siguiente usuario HELIOS con el fichero passwords.txt que nos habíamos generado.

```bash
crackmapexec smb 10.0.2.43 -u helios -p passwords.txt 
```

Esto va a probar esas 3 contraseñas intentando iniciar sesión con el usuario Helios.

<figure><img src="../../.gitbook/assets/Pasted image 20250305214239.png" alt=""><figcaption></figcaption></figure>

En este caso parece que todos los resultados son negativos, me está diciendo que esas 3 contraseñas no son validas. Pero si utilizamos sbnmap con el parámetro -H con la misma numeración.

```bash
smbmap -H 10.0.2.43 -u helios -p qwerty
```

Si probamos con el password hallado "\[\[qwerty]]" podemos ver el siguiente resultado, y vislumbrar que efectivamente se establece una sesión por SMB y vemos permisos para otros recursos que antes no podíamos ver.

<figure><img src="../../.gitbook/assets/Pasted image 20250305221657.png" alt=""><figcaption></figcaption></figure>

Entonces podemos deducir que en este caso, con "Crackmapexec" sigue fallandonos si intentamos entrar con las mismas credenciales y con smnmap nos está funcionando.

<figure><img src="../../.gitbook/assets/Pasted image 20250305221847.png" alt=""><figcaption></figcaption></figure>

Para tener en cuenta siempre hay que enumerar con distintas herramientas porque unas pueden fallar y otras no.

Vamos a coger smbclient para intentar iniciar sesión en el recurso que se nos esta enumerando y vamos a pasarle -U mayúscula para darle el usuario, y pasarla por el prompt (porque -p suele fallar)

```bash
smbclient //10.0.2.43/helios -U helios
```

Metemos la contraseña que encontramos: qwerty

<figure><img src="../../.gitbook/assets/Pasted image 20250305224021.png" alt=""><figcaption></figcaption></figure>

y BOOM, tenemos acceso dentro del usuario al SMB y si hacemos un listar directorios (comando dir) podemos ver que existen dos ficheros dentro de esa carpeta.

<figure><img src="../../.gitbook/assets/Pasted image 20250305224125.png" alt=""><figcaption></figcaption></figure>

Ahora estos archivos podríamos llevárnoslos todos a la carpeta de trabajo con dos comandos para hacerlo mas cómodo.

Usando mget \* nos va a preguntar, quieres llevarte a tu máquina research.txt? despues te preguntaria por el siguiente archivo y así constantemente. Para evitar esto y ser mas eficiente podemos hacer lo siguiente.

prompt , este comando nos evita confirmación de cada uno de los archivos compartidos por SMB.

Primero escribiremos el comando

```bash
prompt
mget *
```

Aquí tendríamos los dos ficheros en local.

<figure><img src="../../.gitbook/assets/Pasted image 20250305224649.png" alt=""><figcaption><p>Fichero research.txt</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250305224751.png" alt=""><figcaption><p>Fichero todo.txt</p></figcaption></figure>

Esa raíz un poco rara, puede ser una ruta oculta que no esta contemplada en el diccionario de dirBuster. Vamos a comprobar si esa ruta existe a nivel de sistemas, para ello nos vamos al navegador y pegaremos esa cadena en la url.

![](<../../.gitbook/assets/Pasted image 20250305224928.png>)

Y bingo, nos encontramos con un sitio Wordpress.

<figure><img src="../../.gitbook/assets/Pasted image 20250305224948.png" alt=""><figcaption><p>Wordpress encontrado en puerto 80</p></figcaption></figure>

Pero parece que no se está generando correctamente, que no se encuentran los ficheros del navegador en las URLS correctas.

Si miramos el código fuente podemos ver que hay un montón de recursos que están intentando realizar peticiones al dominio symfonos.local para poder generarse correctamente.

¿Qué tenemos que hacer ahora?

Está aplicando Virtual Hosting y lo que tenemos que hacer es modificar nuestro fichero etc/hosts para que sirva de una "especie" de servidor DNS local y así asociar la IP de la máquina víctima al dominio symfonos.local.

Esto es un clásico. Listamos el fichero con el siguiente comando

sudo nano de los /etc/hosts

<figure><img src="../../.gitbook/assets/Pasted image 20250305225352.png" alt=""><figcaption></figcaption></figure>

Nos aparecerá este fichero vacío. Y vamos a asignar a la máquina víctima el nombre del dominio symfonos.local, así cuando se haga referencia al dominio se hará referencia a la IP y cuando se haga referencia a la IP se hará referencia al dominio, de forma que cuando insertemos el dominio en la URL se llamará a los recursos llamando a su vez a la IP. Se va a resolver a la IP.

<figure><img src="../../.gitbook/assets/Pasted image 20250305225459.png" alt=""><figcaption></figcaption></figure>

Si por ejemplo hacemos un comando:

```bash
ping -c1 symfonos.local
```

Podemos ver que está resolviendo la IP de la máquina víctima, de la misma forma va a funcionar. Si cambiamos el nombre en la URL y en vez de escribir la URL, escribimos el nombre que hemos puesto accederemos también a la web.

<figure><img src="../../.gitbook/assets/Pasted image 20250305225748.png" alt=""><figcaption></figcaption></figure>

Y eso nos permitirá ver el wordpress en su totalidad como fue concebido originalmente con todos sus recursos.

<figure><img src="../../.gitbook/assets/Pasted image 20250305225820.png" alt=""><figcaption></figcaption></figure>

Vemos que hay un usuario a nivel de sistema wp admin.

Otro clásico en Wordpress ir al wp-admin para validar, probar con ese usuario, probar con otros usuarios, probar fuerza bruta, y probar con **wpScan**.

<figure><img src="../../.gitbook/assets/Pasted image 20250305225935.png" alt=""><figcaption><p>wp-admin panel wordpress</p></figcaption></figure>

Si nos fijamos, solo nos indica que la contraseña para el usuario "admin" no existe por lo tanto podemos deducir que el usuario "admin" existe a nivel de wordpress, y solo nos faltaría averiguar su contraseña.

Todo esto lo podemos automatizar con WpScan, podriamos utilizar o generar algún diccionario que ya exista.

En este escenario tenemos un wordpress expuesto. Tened en cuenta que para otros existen otros CMS bastante comunes que pueden aparecerte en el examen que puede ser Joomla o Drupal. Para estos otros CMS existen herramientas especificas como **JoomSCAN** y **DrupSCAN** para Drupal.

Ya que sabemos que existe "admin" podemos hacer un ataque de fuerza bruta contra ese usuario.

```bash
wpscan -U admin -P /usr/share/wordlists/rockyou.txt -url http://symfonos.local/h3l105
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305230500.png" alt=""><figcaption><p>Output WPScan</p></figcaption></figure>

Vamos a ejecutarlo, no es necesario actualizar la base de datos. Y ahora esta realizando un ataque de login, inicio de sesión y se están ejecutando fuerza bruta. Aquí podemos ver como se están probando todas las contraseñas posibles del diccionario rockyou contra el usuario admin.

<figure><img src="../../.gitbook/assets/Pasted image 20250305230614.png" alt=""><figcaption></figcaption></figure>

Es bastante común que los problemas se resuelvan mediante técnicas de fuerza bruta.

Vamos a realizar un simple escaneo de la URL con el siguiente comando:

```bash
wpscan --url http://symfonos.local/h3l105
```

Este comando entre otras cosas, enumera versiones, y tambien enumera plugins instalados dentro del wordpress, como mail-masta o site-editor, con el numero de version.

En la carta de compromiso, tambien se nos recomendaba searchesploit, el famoso sitio web ExloitDB para enumerar vulnerabilidades sobre estos plugins, dado que sería otro vector de ataque.

```bash
searchesploit wordpress mail masta
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305231122.png" alt=""><figcaption></figcaption></figure>

Y vemos que se nos esta ofreciendo 3 potenciales exploit para ese plugin.

Uno con una SQL Injection, otro que usa un esploit de pythin y otro que usa el 40290, que es un exploit informativo.

También podríamos enumerar el site editor lanzando el siguiente comando:

_Importante no utilizar el - (guión) para buscar los plugins con la herramienta **searchsploit**_

```bash
searchesploit wordpress site editor
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305231303.png" alt=""><figcaption></figcaption></figure>

Y efectivamente hay un CSRF, que esto no aplica en este escenario y un Local File Intrusion, así que tenemos dos plugins vulnerables a un local File Intrusion.

Vamos a usar el primero de mail masta.

Para echarle un vistazo a este exploit, simplemente usamos el siguiente comando, podríamos hacer uso de la propia enumeración de exploitDB que en este caso sería la que hemos averiguado anteriormente.

<figure><img src="../../.gitbook/assets/Pasted image 20250305231705.png" alt=""><figcaption></figcaption></figure>

```
searchsploit -x 40290
```

Y esto nos da la posibilidad de echar un vistazo en formato paginado al código del exploit. Para hacerlo mas cómodo puedes traértelo a tu propia maquina con el siguiente comando.

```
searchsploit -m 40290
```

-m es de "move" y sirve para mover el fichero a nuestra máquina.

<figure><img src="../../.gitbook/assets/Pasted image 20250305232005.png" alt=""><figcaption></figcaption></figure>

```
cat 40290.txt
```

o

```
mousepad 40290.txt
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305232055.png" alt=""><figcaption></figcaption></figure>

Se nos presenta un fichero donde se ve lo que hace el exploit para conseguir lo que buscamos. Vemos cosas interesantes para hacer un resumen, que vemos diferentes archivos potencialmente vulnerables, y enumeraría el htcpasswd haciendo uso de este endpoint, de este count otset contemplado dentro de este script de php usando ese parámetro dentro del php.

Por lo tanto nos vamos a la raíz de este WordPress

<figure><img src="../../.gitbook/assets/Pasted image 20250305232302.png" alt=""><figcaption></figcaption></figure>

Ejecutamos y efectivamente nos retorna el passwd de la máquina victima.

<figure><img src="../../.gitbook/assets/Pasted image 20250305232338.png" alt=""><figcaption><p>Output directo de la llamada</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250305232430.png" alt=""><figcaption><p>Output formateada por el código fuente del navegador</p></figcaption></figure>

Aquí podríamos enumerar algún usuario, como por ejemplo el usuario "nobody" que no es muy interesante, pero nos damos cuenta de que el usuario HELIOS si que dispone de una shell asociada.

<figure><img src="../../.gitbook/assets/Pasted image 20250305232637.png" alt=""><figcaption><p>Usuario que nos interesa</p></figcaption></figure>

Ante que podríamos tirar para convertir un LFI. Para convertir un LFI en un RCE, vamos a tener en cuenta que las máquinas de la eJTPv2, por lo general son máquinas fáciles, y la resolución es mas sencilla. Por lo tanto una de las técnicas para conseguir una ejecución remota de comandos, sería atentar ante una ID\_RDSA de algún usuario valido del sistema.

Si el usuario apache www-data tiene acceso al sistema, con la ID-RSA de Helios podríamos ganar privilegios en el sistema sin proporcionar contraseña.

Sabiendo que el directorio del usuario Helios, el directorio Home, podemos escribir el directorio **/home/.ssh/id\_rsda** que es la carpeta conocida para los usuarios.

#### Y.... premio.

<figure><img src="../../.gitbook/assets/Pasted image 20250305233141.png" alt=""><figcaption><p>ID_RSA del Usuario Helios</p></figcaption></figure>

Con esta IDRSA podríamos ganar acceso al sistema directamente sin tener que escribir ninguna contraseña. Estamos viendo que esta id\_rdsa esta encriptada. Pero vamos a intentar descifrarla.

Como el usuario Helios existe en la máquina victima yo podría intentar acceder mediante SSH con el usuario helios para intentar entrar en el sistema con el usuario victima.

```bash
ssh helios@10.0.2.43
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305233438.png" alt=""><figcaption></figcaption></figure>

Y vemos que es curioso porque este no es el mensaje típico, me esta diciendo que no tengo permisos y que se necesita los requisitos para iniciar sesión en la maquina victima. Y aquí se está teniendo en cuenta la clave pública. En el contexto de clave publica, y clave privada en SSH, se utiliza la clave privada que hace las veces una especie de llave, que abre la clave pública que se encuentra alojada en el sistema víctima en este caso, y lo que hace con esa llave es abrir la clave pública que en este contexto, en esta analogía haría las veces de cerrojo.

Entonces normalmente este mensaje de error tiene una entrada adicional, password, public key. Pero no se puede iniciar sesión con contraseña, porque a pesar de tener este usuario, no podríamos hacer un ataque con Hidra ni ninguna herramienta conocida contra el protocolo SSH porque el acceso mediante contraseña esta inhabilitado. Por eso necesitamos forzosamente una ID\_RSA para iniciar sesión en el sistema.

copiar la clave del navegador y pegar en un fichero de nombre id\_rsa con el comando nano.

nano id\_rsa



<figure><img src="../../.gitbook/assets/Pasted image 20250305234158.png" alt=""><figcaption><p>Fichero nano con la id_rsa del usuario Helios</p></figcaption></figure>

Ahora nos copiamos todo el contenido de la id\_rsa y como nombre le ponemos id\_rsa. Y ahora si intentamos iniciar sesión en la máquina víctima, para empezar vamos a ver un error diferente.

```c
ssh -i id_rdsa helios@10.0.2.43
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305234054.png" alt=""><figcaption></figcaption></figure>

Este error hace alusión a los permisos asignados a esa RSA, una RSA para que funcione correctamente debe de tener un permiso asignado 600, en notación octal. Para cambiar esos permisos podemos hacerlo con _**chmod**_ y modificar esos permisos para darle los permisos necesarios para poder usar esa clave sesión, usando el siguiente comando.

```bash
chmod 600 id_rsa
```

Volvemos a intentar entrar en SSH.

```bash
ssh -i id_rsa helios@10.0.2.43
```

<figure><img src="../../.gitbook/assets/Pasted image 20250305234502.png" alt=""><figcaption></figcaption></figure>

Y nos está pidiendo una contraseña. Ya hemos previsto que la id\_rsa estaba efectivamente encriptada y la contraseña no la sabemos. Para hallar esa contraseña puedes crackear la contraseña de asociada a esa ID\_RSA extrayendo los hashes de la propia ID\_RSA.

Para ella se utiliza

```c
ssh2john id_rsa
```

Como primer argumento de la id\_rsa vamos a generar esos hashes, algo que viéndolo a simple vista para nosotros es algo indescifrable.

<figure><img src="../../.gitbook/assets/Pasted image 20250305235102.png" alt=""><figcaption></figcaption></figure>

Pero si esto nos lo llevamos a un archivo de salida con el siguiente parámetro:

```bash
ssh2john id_rsa > hashes.txt
```

Y estos hashes intentamos crackearlos con herramientas como JohnTheRipper, o HashCat, vamos a poder obtener la contraseña en texto claro para esa RSA. Para ello usaremos el parámetro --wordlist y vamos a usasr el clásico diccionario rocky.txt con el siguiente parametro:

.\* Recordar que es muy importante que tiene que haber un igual porque sino no funciona y estaría intentando crackear el propio diccionario por el orden de los parámetros.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Esto lo que va a hacer es intentar crackear junto con el diccionario, para sacar la contraseña. Esta herramienta suele ser muy efectivo.

<figure><img src="../../.gitbook/assets/Pasted image 20250305235733.png" alt=""><figcaption></figcaption></figure>

Ok, ahora si vamos a intentar acceder a la máquina victima e intentar iniciar sesión con el usuario Helios.

Volvemos a ejecutar el comando ssh.

ssh -i id\_rsa helios@10.0.2.43

<figure><img src="../../.gitbook/assets/Pasted image 20250305235848.png" alt=""><figcaption></figcaption></figure>

Nos pide la contraseña, escribimos la palabra hallada: xerox

Y por fin disponemos de acceso a la máquina mediante SSH al usuario Helios.

<figure><img src="../../.gitbook/assets/Pasted image 20250305235943.png" alt=""><figcaption><p>Hemos entrado como Helios</p></figcaption></figure>

Y ya estamos dentro. Que nos toca ahora, en un escenario de un CTF normal nos tocaría escalar privilegios, pero en la certificación de la eJTPv2 puede diferir el objetivo, alomejor tienes que leer algún archivo en esa máquina u otra cosa.

Enumeración clásica, vamos a lanzar un comando

```
sudo -l 
```

Vamos a lanzar un comando para ver tareas que se estén ejecutando en un crontab en estos momentos.

```
car /etc/crontab
```

<figure><img src="../../.gitbook/assets/Pasted image 20250306000156.png" alt=""><figcaption></figcaption></figure>

Y parece que tampoco hay nada ejecutándose en estos momentos.

Enumerar archivos o herramientas que contengan permisos SUID

```
find / -perm -4000 -ls 2>/dev/null
```

Donde -perm -4000 (que sería permisos SUID en notación octal) y lo redirigimos al /dev/null para que no nos enseñe los errores, y también podríamos añadir la flag -ls para que nos liste información adicional acerca de los permisos sobre los archivos.

<figure><img src="../../.gitbook/assets/Pasted image 20250306000615.png" alt=""><figcaption><p>Salida de ficheros con permisos SUID 4000</p></figcaption></figure>

Interesante y que difiere de lo común vemos diferentes ficheros ejecutables, y uno que destaca que se llama /opt/statuscheck. Vamos a ver que hace este ejecutable. Importante tener en cuenta que siempre que lo hagamos bajo este conexto lo vamos a ejecutar como usuario root.

```
 /opt/statuscheck
```

<figure><img src="../../.gitbook/assets/Pasted image 20250306000738.png" alt=""><figcaption></figcaption></figure>

Esto es lo relevante en este contexto que se hace bajo **root**, y parece que lo que esto está haciendo es obtener las cabeceras de respuesta ante una petición. Si queremos ver que hace esto haciendo un cat, pero vamos a ver que tipo de fichero es haciendo un file.

```bash
file  /opt/statuscheck
```

<figure><img src="../../.gitbook/assets/Pasted image 20250306000924.png" alt=""><figcaption></figcaption></figure>

Si esto hacemos un CAT nos va a mandar un output de locura. Que podemos hacer entonces para poder saber que esta haciendo esa herramienta por detrás. Utilizando Strings, podemos intentar visualizar las cadenas de caracteres legibles por parte de un humano en un archivo.

```
strings /opt/statuscheck
```

<figure><img src="../../.gitbook/assets/Pasted image 20250306001111.png" alt=""><figcaption></figcaption></figure>

Esto es lo que podemos ver, tremendo output enorme, y lo que aquí podemos destacar es la via intencionada, se hace un curl -i a localhost. Donde esta aqui el fallo, se esta llamando de forma relativa a ese ejecutable CURL no se esta llamando de forma absoluta, en el momento que tu ejecutes esa herramienta, va a buscarlo en el path en el que se este ejecutando esa herramienta.

Si yo lanzo el parámetro "curl" sin mas, lo está buscando en el path del sistema. Si hacemos un echo $PATH, vemos lo que tenemos aquí.

<figure><img src="../../.gitbook/assets/Pasted image 20250306001334.png" alt=""><figcaption></figcaption></figure>

Cuando se ejecuta ese opt/statuscheck lo que esta haciendo por detras es buscar ese binario, en esa ruta, que ocure si yo modifico lo que vale el PATH, para hacer un PATH HIJACKING.

Podemos hacer un export de la variable PATH para igualarla a lo siguiente.

```java
export PATH=/tmp:$PATH
```

Esto lo que va a hacer es añadir el valor TMP: aquí al principio y lo siguiente va a ser la variable PATH que vale en ese otro momento.

<figure><img src="../../.gitbook/assets/Pasted image 20250306001558.png" alt=""><figcaption></figcaption></figure>

Si nos fijamos al lanzar el comando hemos modificado el valor de la ruta del PATH. Ahora tenemos /tmp y no /usr, como primera ruta donde donde se va a buscar ese binario curl cuando se ejecute ese opt/statuscheck.

Entonces, ahora vamos a movernos a esa carpeta de /tmp. (Hemos elegido TMP porque en esa carpeta normalmente todos los usuarios potencialmente tienen permisos de escritura.)

```bash
cd /tmp
```

Y nos creamos un archivo curl que va a contener el tipo de shell que quiero obtener cuando se ejecute este PATH HIJACKING.

```bash
nano curl
```

Este fichero va a contener el tipo de shell /bin/bash -p.

<figure><img src="../../.gitbook/assets/Pasted image 20250306002904.png" alt=""><figcaption></figcaption></figure>

Y a este archivo que solo tiene permisos de lectura

<figure><img src="../../.gitbook/assets/Pasted image 20250306002022.png" alt=""><figcaption></figcaption></figure>

Le asigno permisos de ejecución.

```bash
chmod 777 curl 
file curl
```

<figure><img src="../../.gitbook/assets/Pasted image 20250306002122.png" alt=""><figcaption></figcaption></figure>

Esto sigue siendo un ASCII TEXT, pero si el archivo lo ejecuto,

```bash
./curl
```

estoy abriendo una sesión aunque, parezca que no. SI haces un

```bash
exit
```

me está saliendo de la sesión actual.

<figure><img src="../../.gitbook/assets/Pasted image 20250306002307.png" alt=""><figcaption></figcaption></figure>

Al ejecutar ese curl, lo que hemos hecho es iniciar una sesión dentro de esta sesión. Está anidada, cuando hago exit salgo a la principal.

Que va a ocurrir ahora cuando ejecutemos ese opt/statuscheck, que en el momento que se vaya a llamar al binario de curl, va a hacer el siguiente recorrido.

Se va a encontrar un archivo de curl en tmp y se va a ejecutar ese archivo de curl.

<figure><img src="../../.gitbook/assets/Pasted image 20250306002602.png" alt=""><figcaption></figcaption></figure>

Y quienes somos si ejecutamos un **whoami**, pues somos Helios. Porque aquí tenemos que acompañar esa bin/bash con el parámetro -p.

Cuando ejecutamos un bash con permisos necesitamos que ese bash se ejecute con permisos privilegiados para que conserve los permisos del usuario efectivo al ejecutar ese bash.

<figure><img src="../../.gitbook/assets/Pasted image 20250306002759.png" alt=""><figcaption></figcaption></figure>

Bien, ya somos root. Ahora vamos a probar que sucedería si modificamos el fichero curl y ponemos lo siguiente para intentar iniciar sesión en la ejecución de esa herramienta para ejecutar una bin/bash

Ahora hemos acabado con la primera máquina de simulación de máquinas de este laboratorio de simulación de la eJPTv2.

**Minuto del video 1:32:53 para siguiente laboratorio.**
