# Módulo 2: Pruebas de Seguridad de la Red



2.1.1 Escaner de vulnerabilidades

Un escáner de vulnerabilidades evalúa las computadoras, los sistemas informáticos, las redes o las aplicaciones en busca de debilidades. Los escáneres de vulnerabilidades ayudan a automatizar la auditoría de seguridad escaneando la red en busca de riesgos de seguridad y produciendo una lista prioritaria para abordar las debilidades.

* Uso de contraseñas predeterminadas o contraseñas comunes.
* Parches faltantes.
* Puertos abiertos.
* Errores en la configuración del software y los sistemas operativos.
* Direcciones IP activas, incluyendo dispositivos inesperados conectados

El escáner de vulnerabilidades es clave para identificar vulnerabilidades, configuraciones incorrectas y la falta de controles de seguridad para las organizaciones con redes que incluyen segmentos, routers, firewalls, servidores y otros dispositivos.

Los escáneres de vulnerabilidades más utilizados en el mercado incluyen Nessus, Retina, Core Impact y GFI LanGuard.

Sus funciones incluyen:

* Realizar auditorías de cumplimiento
* Proporcionar parches y actualizaciones
* Identificar configuraciones incorrectas
* Compatibilidad con dispositivos móviles e inalámbricos
* Rastrear malware
* Identificar los datos sensibles



2.1.2 Tipos de Escaneos

Categorías de escaneo

* **Los escáneres de red** analizan los hosts en busca de puertos abiertos, enumeran información sobre usuarios y grupos y buscan vulnerabilidades conocidas en la red.
* **Los escáneres de aplicaciones** acceden al código fuente de la aplicación para probar una aplicación desde el interior (no ejecutan la aplicación).
* **Los escáneres de aplicaciones web** identifican vulnerabilidades en las aplicaciones web.

Escaneos Intrusivos

Los escaneos intrusivos intentan aprovechar vulnerabilidades e incluso pueden inutilizar el objetivo, mientras que un análisis no intrusivo intentará no causar daño al objetivo.

En un escaneos con credenciales, los nombres de usuario y las contraseñas proporcionan acceso autorizado a un sistema, lo que permite que el escáner recopile más información. Los escaneos sin credenciales son menos invasivos y ofrecen un punto de vista externo.

Sin embargo, todos los tipos de escáner pueden identificar erróneamente una vulnerabilidad donde no existe ninguna. Esto se conoce como falso positivo, mientras que no identificar una vulnerabilidad existente es un falso negativo. Los escaneos con credenciales arrojan menos falsos positivos y menos falsos negativos.

Debe revisar todos los registros y las configuraciones para solucionar las vulnerabilidades que requieren atención.

2.1.3 - Utilidades de Diagnóstico de la Línea de Comandos

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

2.1.4 Automatización de la Seguridad

SIEM

Los sistemas de Información de Seguridad y Gestión de Eventos (SIEM) utilizan recopiladores de registros para agregar datos de registros de fuentes como dispositivos de seguridad, dispositivos de red, servidores y aplicaciones. Los registros pueden generar muchos eventos en un día, por lo que los sistemas SIEM ayudan a reducir el volumen de eventos mediante la combinación de eventos similares para reducir la carga de datos del evento. SIEM identifica las desviaciones de la norma y luego toma las medidas correspondientes.

Los objetivos de un sistema SIEM para el monitoreo de la seguridad son:

* Identificar amenazas internas y externas
* Supervisor la actividad y el uso de recursos
* Realizar informes de cumplimiento para las auditorías
* Soportar respuesta a incidentes

Cuando el sistema SIEM detecta un problema potencial, puede registrar información adicional, generar una alerta e instruir a otros controles de seguridad para detener el progreso de una actividad. Los sistemas avanzados de SIEM incluyen análisis de comportamiento de usuarios y entidades que buscan patrones que dependen del sentimiento humano para reconocer una amenaza antes de que se convierta en una amenaza.

La cantidad de datos registrados de sistemas críticos es una consideración importante al implementar un sistema SIEM, ya que usted debe revisar los informes generados. Los sistemas SIEM son costosos de adquirir y mantener, y solo son rentables si la organización genera millones de eventos en un día.

\
SOAR

Las herramientas de Orquestación de Automatización y Respuesta (SOAR) permiten que una organización recopile datos sobre amenazas de seguridad de diversas fuentes y responda a eventos de bajo nivel sin intervención humana. SOAR tiene tres funcionalidades importantes:

* Administración de amenazas y vulnerabilidad
* Respuesta ante incidentes de seguridad
* Automatización de las operaciones de seguridad

Una organización puede integrar SOAR en su solución SIEM.



<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

