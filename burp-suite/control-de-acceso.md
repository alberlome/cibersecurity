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

# Control de acceso

## ¿Qué es el control de accesos?

El control de acceso es la aplicación de restricciones sobre quién o qué está autorizado a realizar acciones o acceder a recursos. En el contexto de las aplicaciones web, el control de acceso depende de la autenticación y la gestión de sesiones:

La autenticación confirma que el usuario es quien dice ser.&#x20;

La gestión de la sesión identifica qué peticiones HTTP posteriores están siendo realizadas por ese mismo usuario.&#x20;

El control de acceso determina si el usuario está autorizado a llevar a cabo la acción que está intentando realizar.&#x20;

Los controles de acceso rotos son comunes y a menudo presentan una vulnerabilidad de seguridad crítica. El diseño y la gestión de los controles de acceso es un problema complejo y dinámico que aplica restricciones empresariales, organizativas y legales a una implementación técnica. Las decisiones de diseño de los controles de acceso tienen que ser tomadas por humanos, por lo que el potencial de errores es alto.

<figure><img src="../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption><p>Imagen de BurpSuite - WebSecurity - </p></figcaption></figure>



## Escalar privilegios verticalmente

Si un usuario puede acceder a una funcionalidad a la que no tiene permiso de acceso, entonces se trata de una escalada vertical de privilegios. Por ejemplo, si un usuario que no es administrador puede acceder a una página de administrador en la que puede eliminar cuentas de usuario, se trata de una escalada vertical de privilegios.



## Funcionalidad desprotegida&#x20;

En su forma más básica, la escalada vertical de privilegios surge cuando una aplicación no impone ninguna protección para la funcionalidad sensible. Por ejemplo, las funciones administrativas pueden estar enlazadas desde la página de bienvenida de un administrador, pero no desde la página de bienvenida de un usuario. Sin embargo, un usuario podría acceder a las funciones administrativas navegando a la URL de administración correspondiente.

Por ejemplo, un sitio web puede alojar funciones sensibles en la siguiente URL:

```
https://insecure-website.com/admin
```

Cualquier usuario puede acceder a ella, no sólo los usuarios administrativos que tienen un enlace a la funcionalidad en su interfaz de usuario. En algunos casos, la URL administrativa podría revelarse en otras ubicaciones, como el archivo _**robots.txt**_:

```
https://insecure-website.com/robots.txt
```

Incluso si la URL no se revela en ninguna parte, un atacante puede ser capaz de utilizar una lista de palabras para forzar la ubicación de la funcionalidad sensible.

## Laboratorio: Funcionalidad de administración desprotegida

Este laboratorio tiene un panel de administración desprotegido.

Resuelve el laboratorio borrando el usuario _**carlos**_.

Tenemos este sitio web

<figure><img src="../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

Vamos a hacer una pequeña investigación y visitaremos el fichero _**robots.txt**_ para ver si nos aporta algo mas de información.

En el fichero robots.txt hallamos la siguiente ruta:

<figure><img src="../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

Copiamos la ruta y la pegamos en el navegador.

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

Y podemos ver que tenemos acceso a las funciones de borrado de usuarios. Procedemos a eliminar al usuario Carlos.

## Funcionalidad no protegida - Continuación

En algunos casos, la funcionalidad sensible se oculta dándole una URL menos predecible. Este es un ejemplo de la llamada "seguridad por oscuridad". Sin embargo, ocultar la funcionalidad sensible no proporciona un control de acceso eficaz porque los usuarios podrían descubrir la URL ofuscada de varias maneras.

Imagina una aplicación que aloja funciones administrativas en la siguiente URL:

```
https://insecure-website.com/administrator-panel-yb556
```

Esto podría no ser directamente adivinable por un atacante. Sin embargo, la aplicación podría filtrar la URL a los usuarios. La URL podría revelarse en JavaScript que construye la interfaz de usuario basándose en el rol del usuario:

```
<script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script>
```

Este script añade un enlace a la interfaz de usuario del usuario administrador. Sin embargo, el script que contiene la URL es visible para todos los usuarios independientemente de su rol.

## Laboratorio: Funcionalidad de administración desprotegida con URL impredecible

Este laboratorio tiene un panel de administración desprotegido. Se encuentra en una ubicación impredecible, pero la ubicación se revela en algún lugar de la aplicación.

Resuelve el laboratorio accediendo al panel de administración, y usándolo para eliminar al usuario _**carlos**_.

Esta es la web objetivo

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

Esta es la web objetivo







