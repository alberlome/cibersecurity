# Vulnerabilidades de autenticación

Conceptualmente, las vulnerabilidades de autenticación son fáciles de entender. Sin embargo, suelen ser críticas debido a la clara relación entre la autenticación y la seguridad.

Las vulnerabilidades de autenticación pueden permitir a los atacantes obtener acceso a datos sensibles y funcionalidades. También exponen una superficie de ataque adicional para más explotaciones. Por esta razón, es importante aprender a identificar y explotar las vulnerabilidades de autenticación, así como a evadir las medidas de protección comunes.

En esta sección, explicamos:

* Los mecanismos de autenticación más comunes utilizados por los sitios web.
* Las posibles vulnerabilidades en estos mecanismos.
* Las vulnerabilidades inherentes en los diferentes mecanismos de autenticación.
* Las vulnerabilidades típicas que se introducen por una implementación incorrecta.
* Cómo puedes hacer que tus propios mecanismos de autenticación sean lo más robustos posible.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## ¿Cuál es la diferencia entre autenticación y autorización?

La autenticación es el proceso de verificar que un usuario es quien dice ser. La autorización implica verificar si un usuario tiene permiso para realizar una acción.

Por ejemplo, la autenticación determina si una persona que intenta acceder a un sitio web con el nombre de usuario Carlos123 realmente es la misma persona que creó la cuenta.

Una vez que Carlos123 ha sido autenticado, sus permisos determinan lo que está autorizado a hacer.

Por ejemplo, puede estar autorizado a acceder a información personal de otros usuarios o realizar acciones como eliminar la cuenta de otro usuario.

## Ataques de fuerza bruta

Un ataque de fuerza bruta es cuando un atacante utiliza un sistema de prueba y error para adivinar las credenciales válidas de un usuario. Estos ataques suelen ser automatizados utilizando listas de palabras con nombres de usuario y contraseñas. La automatización de este proceso, especialmente mediante herramientas dedicadas, permite a un atacante realizar una gran cantidad de intentos de inicio de sesión a alta velocidad.

El ataque de fuerza bruta no siempre consiste solo en hacer conjeturas completamente aleatorias sobre nombres de usuario y contraseñas. Al utilizar también lógica básica o conocimientos públicos, los atacantes pueden afinar los ataques de fuerza bruta para hacer conjeturas mucho más fundamentadas. Esto aumenta considerablemente la eficiencia de tales ataques. Los sitios web que dependen del inicio de sesión basado en contraseñas como su único método de autenticación de usuarios pueden ser muy vulnerables si no implementan una protección adecuada contra los ataques de fuerza bruta.

## Fuerza bruta en nombres de usuario

Los nombres de usuario son especialmente fáciles de adivinar si siguen un patrón reconocible, como una dirección de correo electrónico. Por ejemplo, es muy común ver inicios de sesión de empresas en el formato **nombre.apellido@algunaempresa.com**. Sin embargo, incluso si no hay un patrón obvio, a veces las cuentas de alto privilegio se crean utilizando nombres de usuario predecibles, como admin o administrador.

Durante una auditoría, verifica si el sitio web divulga potenciales nombres de usuario públicamente. Por ejemplo, ¿puedes acceder a los perfiles de usuario sin iniciar sesión? Aunque el contenido real de los perfiles esté oculto, el nombre utilizado en el perfil a veces es el mismo que el nombre de usuario de inicio de sesión. También debes revisar las respuestas HTTP para ver si se divulgan direcciones de correo electrónico. En ocasiones, las respuestas contienen direcciones de correo electrónico de usuarios con altos privilegios, como administradores o soporte de TI.

## Fuerza bruta en contraseñas

Las contraseñas también pueden ser objeto de ataques de fuerza bruta, con la dificultad variando según la fortaleza de la contraseña. Muchos sitios web adoptan algún tipo de política de contraseñas, que obliga a los usuarios a crear contraseñas de alta entropía que, al menos teóricamente, son más difíciles de descifrar utilizando solo fuerza bruta. Esto generalmente implica la imposición de contraseñas con:

* Un número mínimo de caracteres
* Una mezcla de letras minúsculas y mayúsculas
* Al menos un carácter especial

Sin embargo, aunque las contraseñas de alta entropía son difíciles de descifrar solo con computadoras, podemos usar un conocimiento básico del comportamiento humano para explotar las vulnerabilidades que los usuarios introducen sin saberlo en este sistema. En lugar de crear una contraseña fuerte con una combinación aleatoria de caracteres, los usuarios suelen elegir una contraseña que puedan recordar y tratan de ajustarla para que cumpla con la política de contraseñas. Por ejemplo, si "_mypassword_" no es permitido, los usuarios podrían intentar algo como "Mypassword1!" o "Myp4\$$w0rd".

En los casos donde la política exige que los usuarios cambien sus contraseñas de manera regular, también es común que los usuarios solo hagan pequeños cambios predecibles en su contraseña preferida. Por ejemplo, "Mypassword1!" se convierte en "Mypassword1?" o "Mypassword2!".

Este conocimiento sobre las credenciales probables y los patrones predecibles significa que los ataques de fuerza bruta pueden ser mucho más sofisticados y, por lo tanto, efectivos, que simplemente iterar a través de todas las posibles combinaciones de caracteres.

## Enumeración de nombres de usuario

La enumeración de nombres de usuario ocurre cuando un atacante es capaz de observar cambios en el comportamiento de un sitio web para identificar si un nombre de usuario dado es válido.

La enumeración de nombres de usuario suele ocurrir en la página de inicio de sesión, por ejemplo, cuando se ingresa un nombre de usuario válido pero una contraseña incorrecta, o en los formularios de registro cuando se ingresa un nombre de usuario que ya está registrado. Esto reduce significativamente el tiempo y el esfuerzo necesarios para realizar un ataque de fuerza bruta en un inicio de sesión, ya que el atacante puede generar rápidamente una lista corta de nombres de usuario válidos.





