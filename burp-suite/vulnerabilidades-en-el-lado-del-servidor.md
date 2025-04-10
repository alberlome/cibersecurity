---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Vulnerabilidades en el lado del servidor

## ¿Qué es un _**"path traversal"**_?

_**"Path traversal"**_ también se conoce como directorio transversal. Estas vulnerabilidades permiten a un atacante leer archivos arbitrarios en el servidor que ejecuta una aplicación. Esto puede incluir:

* Código y datos de la aplicación.&#x20;
* Credenciales para sistemas back-end.&#x20;
* Archivos sensibles del sistema operativo.

En algunos casos, un atacante podría escribir en archivos arbitrarios del servidor, lo que le permitiría modificar los datos o el comportamiento de la aplicación y, en última instancia, hacerse con el control total del servidor.

## Lectura de archivos arbitrarios mediante path traversal

Imagine una aplicación de compras que muestra imágenes de artículos en venta. Esto podría cargar una imagen usando el siguiente HTML:

```
<img src="/loadImage?filename=218.png">
```

La URL **`loadImage`** toma un parámetro de _**nombre de archivo**_ y devuelve el contenido del archivo especificado. Los archivos de imagen se almacenan en el disco en la ubicación **`/var/www/images/`**. Para devolver una imagen, la aplicación añade el nombre del archivo solicitado a este directorio base y utiliza una API del sistema de archivos para leer el contenido del archivo. En otras palabras, la aplicación lee desde la siguiente ruta de archivo:

```
/var/www/images/218.png
```

Esta aplicación no implementa defensas contra ataques path traversal. Como resultado, un atacante puede solicitar la siguiente URL para recuperar el archivo _**/etc/passwd**_ del sistema de archivos del servidor:

```
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```

This causes the application to read from the following file path:

```
/var/www/images/../../../etc/passwd
```

La secuencia _**../**_ es válida dentro de una ruta de archivo, y significa subir un nivel en la estructura de directorios. Las tres secuencias consecutivas _**../**_ suben desde _**/var/www/images/**_ hasta la raíz del sistema de ficheros, por lo que el fichero que se lee es:

```
/etc/passwd
```

En los sistemas operativos basados en Unix, se trata de un archivo estándar que contiene detalles de los usuarios registrados en el servidor, pero un atacante podría recuperar otros archivos arbitrarios utilizando la misma técnica.

En Windows, tanto _**../**_ como _**..\\**_ son secuencias válidas para atravesar directorios. El siguiente es un ejemplo de un ataque equivalente contra un servidor basado en Windows:

```
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```

## Laboratorio: Recorrido de rutas de archivos, caso simple

Este laboratorio contiene una vulnerabilidad de path traversal en la visualización de imágenes de productos.

Para resolver el problema, recupere el contenido del archivo _**/etc/passwd**_.

## **Solución del laboratorio**

Me he ido a la web, he abierto en una nueva pista una de las imágenes, he pegado en la barra de direcciones siendo reemplazado el parámetro que llevaba a la imagen por esto ../../../etc/passwd"

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption><p>La respuesta del servidor al realizar la petición</p></figcaption></figure>

La respuesta del servidor me retorna _**"root"**_

../../../etc/passwd

Tambien he probado instalando BURP SUITE Community Edition. Y siguiendo los pasos de este [video](https://www.youtube.com/watch?v=XhieEh9BlGc) he podido conseguir el mismo resultado pero en la herramienta Burp suite.

Primero poner a escuchar a Burp Suite el navegador mediante un proxy.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Salida por pantalla de la petición a la web</p></figcaption></figure>

Seleccionar la opción de "REPEATER" para poder enviar cabeceras.

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Enviar al "Repetidor"</p></figcaption></figure>

Una vez que estamos en repeater, volveremos a enviar una petición.

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Vemos como nos reporta código ofuscado la imágen</p></figcaption></figure>

Ahora vamos a probar a poner la ../../../etc/passwd y ver si el servidor es susceptible a esta forma de intrusión. Para ello&#x20;

Primero modificamos el parámetro de file=55.png, quitamos la imagen y ponemos nuestra cadena de texto con el directorio passwd.

Luego una vez modificado pulsamos en el botón "Send", y finalmente verificamos que tenemos passwd de root.

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>













