---
description: >-
  Documentación de los write-ups de máquinas con Dockerfiles, detallando la
  resolución paso a paso, análisis de vulnerabilidades y aprendizajes en
  ciberseguridad
---

# 🐳 DockerLabs (Español)

[DockerLabs](https://dockerlabs.es/) es una plataforma que ofrece entornos de práctica y aprendizaje sobre Docker, permitiendo a los usuarios experimentar con contenedores, desplegar aplicaciones y mejorar sus habilidades en administración de sistemas y ciberseguridad.

Su creador y principal contribuidor [_El Pingüino de Mario_](https://www.youtube.com/@ElPinguinoDeMario), es un creador de contenido especializado en Linux y ciberseguridad, que desarrolla máquinas y desafíos para la comunidad, facilitando el aprendizaje en entornos prácticos y realistas.

También existen otras personas que contribuyen a la resolución de las máquinas y a la publicación de los _**write-up**_ que nos permite consultar si en algún momento tenemos alguna duda.

## Cómo descargar e instalar la máquina de prueba

Nos dirigimos a la web de DockerLabs del Pingüino de Mario, y nos descargamos la primera máquina modo "Muy Fácil" que nos encontramos.

<figure><img src="../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

Una vez que estamos en la consola de Kali Linux, nos creamos abrimos un Terminal, nos copiamos la máquina que nos hemos descargado recientemente (llamada "injection") y la pegamos en nuestra carpeta de trabajo.

Abrimos la ruta de la carpeta, descomprimimos el fichero ZIP y tenemos dos ficheros.

<div align="left" data-full-width="false"><figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Extracción del fichero zip</p></figcaption></figure></div>

Ahora modificaremos los permisos de la máquina para que disponga de permisos de ejecución y la ejecutaremos en nuestra Terminal.

<div align="left"><figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Ejecución de la máquina en nuestro Docker local</p></figcaption></figure></div>

Una vez ejecutada, como no tenemos Docker lo primero que hace es instalarlo.

Una vez instalado Docker en esta máquina virtual, termina por decirnos la dirección IP de la máquina que acabamos de desplegar y su dirección IP, para acceder a ella.

<div align="left"><figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Despliegue de la máquina en nuestra terminal</p></figcaption></figure></div>

Una vez que ya hemos terminado y nos ha lanzado la dirección IP de la máquina que acabamos de desplegar, procedemos a comenzar con nuestra operativa.
