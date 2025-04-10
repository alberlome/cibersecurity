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

# Vulnerabilidades del lado del servidor

## **Laboratorio: Funcionalidad de administración desprotegida con URL impredecible**

Pasos para Resolver el Laboratorio. Descubra la ubicación del panel de administración:

&#x20;\- Busca en varias páginas de la aplicación para encontrar pistas sobre la ubicación del panel de administración.

&#x20;\- Busque comentarios en el código fuente HTML, parámetros de URL u otras partes de la aplicación que puedan revelar su ubicación.

Accede al panel de administración:\
Una vez que tengas la ubicación, navega al panel de administración dentro de la aplicación.&#x20;Elimine el usuario 'carlos'\


<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Se encuentra evidencia dentro de un fichero html, que contiene un script donde indica la url de /admin-lcogod, donde hay dos usuarios Carlos y  Viener y eliminamos Carlos, para completar el laboratorio.
