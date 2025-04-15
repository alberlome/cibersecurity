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

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

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



<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

2.3.1 Herramientas de Pruebas de Red

Hay muchas herramientas disponibles para probar la seguridad de los sistemas y las redes. Algunas de estas herramientas son de código abierto, mientras que otras son herramientas comerciales que requieren licencias.

Las herramientas de software que pueden utilizarse para realizar pruebas de red incluyen:

* **Nmap/Zenmap -** Se utiliza para detectar computadoras y sus servicios en una red y, por lo tanto, crear un mapa de la red.
* **SuperScan -** Este software de análisis de puertos está diseñado para detectar puertos TCP y UDP abiertos, determinar qué servicios se ejecutan en esos puertos y ejecutar consultas, como búsquedas de whois, ping, traceroute y nombres de host.
* **SIEM (Información de Seguridad y Gestión de Eventos) -** Es una tecnología utilizada en las organizaciones empresariales para proporcionar informes en tiempo real y análisis a largo plazo de eventos de seguridad.
* **GFI LANguard -** Es un escáner de red y de seguridad que detecta vulnerabilidades.
* **Tripwire -** Esta herramienta evalúa y valida las configuraciones de TI en relación con las políticas internas, los estándares de cumplimiento y las mejores prácticas de seguridad.
* **Nessus -** Se trata de un software de análisis de vulnerabilidades, que se centra en el acceso remoto, las configuraciones incorrectas y la denegación de servicio contra la pila de TCP/IP.
* **L0phtCrack -** Es una aplicación de auditoría y recuperación de contraseñas.
* **Metasploit -** Esta herramienta proporciona información sobre vulnerabilidades y ayuda en las pruebas de penetración y el desarrollo de firmas de IDS.

**Nota**: Las herramientas de prueba de red evolucionan a un ritmo rápido. La lista anterior incluye herramientas heredadas y su intención es proporcionar un conocimiento de los diferentes tipos de herramientas disponibles.

2.3.2 Nmap y Zenmap

Nmap es un escáner de bajo nivel de uso general que está disponible para el público. Tiene una variedad de características excelentes que pueden utilizarse para el reconocimiento y el mapeo de redes.

La funcionalidad básica de Nmap permite al usuario realizar varias tareas, de la siguiente manera:

* **Escaneo clásico de puertos TCP y UDP** - busca diferentes servicios en un host.
* **Barrido clásico de puertos TCP y UDP** - busca el mismo servicio en varios hosts.
* **Escaneo y barrido sigiloso de puertos TCP y UDP** - Esto es similar a los análisis y barridos clásicas, pero más difícil de detectar por el host de destino o IPS.
* **Identificación remota del sistema operativo** - Esto también se conoce como identificación del sistema operativo.

Las funciones avanzadas de Nmap incluyen análisis de protocolo, conocido como análisis de puertos de Capa 3. Esta función identifica el soporte de protocolo de Capa 3 en un host. Entre los ejemplos de protocolos que se pueden identificar se incluyen GRE y OSPF.

Si bien Nmap puede utilizarse para pruebas de seguridad, también puede utilizarse con fines maliciosos. Nmap tiene una función adicional que le permite utilizar hosts de señuelo en la misma LAN que el host de destino para enmascarar el origen del análisis.

Nmap no tiene características de capa de aplicación y se ejecuta en UNIX, Linux, Windows y OS X. Hay disponibles versiones de consola y gráficas. El programa Nmap y la GUI de Zenmap se pueden descargar de Internet.

2.3.3 SuperScan

SuperScan es una herramienta de análisis de puertos de Microsoft Windows. Se ejecuta en la mayoría de las versiones de Windows y requiere privilegios de administrador.

SuperScan versión 4 tiene una serie de características útiles:

* Velocidad de escaneo ajustable
* Soporte para rangos de IP ilimitados
* Detección de host mejorada mediante varios métodos de ICMP
* Escaneo de TCP SYN
* Escaneo UDP (dos métodos)
* Generación de informes HTML simple
* Análisis del puerto de origen
* Resolución rápida de nombre de host
* Amplias capacidades de captura de anuncios
* Base de datos integrada masiva con descripción de la lista de puertos
* Aleatorización del orden de escaneo de IP y de puertos
* Una selección de herramientas útiles, como ping, traceroute y whois
* Amplia capacidad de enumeración de hosts de Windows

Las herramientas, como Nmap y SuperScan, pueden proporcionar pruebas de penetración eficaces en una red y determinar las vulnerabilidades de la red, a la vez que ayudan a anticipar posibles mecanismos de ataque. Sin embargo, las pruebas de red no pueden preparar a un administrador de red para cada problema de seguridad.



2.3.4 SIEM

Información de Seguridad y Gestión de Eventos (SIEM) es una tecnología utilizada en las organizaciones empresariales para proporcionar informes en tiempo real y análisis a largo plazo de eventos de seguridad. SIEM evolucionó a partir de dos productos previamente separados: Administración de Información de Seguridad (SIM) y Administración de Eventos de Seguridad (SEM). SIEM puede implementarse como software, integrado con Cisco Identity Services Engine (ISE) o como servicio administrado.

SIEM combina las funciones esenciales de SIM y SEM para brindar:

* **Correlación** - Analiza registros y eventos de diferentes sistemas o aplicaciones, lo que acelera la detección de las amenazas de seguridad y la capacidad de reacción ante ellas.
* **Agregación** - Esta función reduce el volumen de los datos de eventos mediante la consolidación de registros de eventos duplicados.
* **Análisis forense** - La capacidad de buscar registros de eventos de fuentes en toda la organización proporciona información más completa para el análisis forense.
* **Retención** - Los registros permiten ver los datos sobre eventos correlacionados y sgregados mediante monitoreo en tiempo real y resúmenes a largo plazo.

SIEM brinda detalles sobre el origen de actividad sospechosa, incluyendo:

* Información del usuario (nombre, estado de autenticación, ubicación, grupo de autorización, estado de cuarentena)
* Información del dispositivo (fabricante, modelo, versión del sistema operativo, dirección MAC, método de conexión a la red y ubicación)
* Información de postura (cumplimiento del dispositivo con la política de seguridad corporativa, versión de antivirus, parches del SO, cumplimiento de la política de administración de dispositivos móviles)

Con esta información, los ingenieros de seguridad de la red pueden evaluar rápidamente y con precisión la importancia de cualquier evento de seguridad y de responder las preguntas criticas:

* ¿Quién está asociado con este evento?
* ¿Es un usuario importante con acceso a la propiedad intelectual o a la información confidencial?
* ¿El usuario está autorizado para acceder a ese recurso?
* ¿El usuario tiene acceso a otros recursos delicados?
* ¿Qué clase de dispositivo se está utilizando?
* ¿Este evento representa un posible problema de cumplimiento?



2.4.1 Pruebas de Penetración

Las pruebas de penetración son una forma de probar las áreas de debilidad en los sistemas mediante el uso de diversas técnicas maliciosas. Una prueba de penetración simula los métodos que un atacante usaría para obtener acceso no autorizado a una red y comprometer los sistemas, y permite que una organización comprenda cuán bien toleraría un ataque real.

Es importante tener en cuenta que las pruebas de penetración no son lo mismo que las pruebas de vulnerabilidad, que sólo _identifican_ problemas potenciales. Las pruebas de penetración implican piratear un sitio web, una red o un servidor con el permiso de una organización para intentar obtener acceso a los recursos mediante diversos métodos que utilizarían los piratas informáticos reales.

Uno de los motivos principales por los que una organización utiliza las pruebas de penetración es para buscar y corregir las vulnerabilidades antes de que lo hagan los ciberdelincuentes. La prueba de penetración también se conoce como hackeo ético.

**Seleccione la imagen para los diferentes niveles de prueba de penetración.**



2.4.2 Fases de Penetración

Hay cuatro fases que conforman una prueba de penetración.

**Seleccione los encabezados para obtener más información.**

Fase 1: Planificación

Establece las reglas de participación para realizar la prueba.



Fase 2: Detección

Realiza un reconocimiento del objetivo para obtener información. Esto puede incluir:

* Las técnicas pasivas, que no requieren una participación activa en el sistema de destino y se denominan huellas, por ejemplo, pueden consultar el sitio web de la organización u otras fuentes públicas para obtener información.
* Reconocimiento activo, como escaneo de puertos, que requiere una participación activa con el objetivo.



Fase 3: Ataque

En esta fase, se busca obtener acceso o penetrar el sistema mediante la información recopilada en la fase anterior. El probador intenta obtener privilegios mayores y quizás profundizar en la red a través del movimiento lateral. Para moverse lateralmente por la red, el probador debe pivotar a través de varios sistemas. El probador puede intentar instalar herramientas adicionales o plantar una puerta trasera; este proceso se conoce como persistencia. Luego, el probador limpiará el sistema y eliminará cualquier señal que haya quedado.



Fase 4: Elaboración de reportes

En esta fase, el probador entrega a la organización documentación detallada que incluye las vulnerabilidades identificadas, las medidas tomadas y los resultados.





2.4.3 Tipos de Ejercicios

Algunas organizaciones crean equipos que compiten para realizar ejercicios de penetración que son más extensos que una prueba de penetración.

Por ejemplo, en tal situación, puede haber tres o cuatro equipos:

* El equipo rojo es el adversario, intenta atacar el sistema pasando desapercibido.
* Los miembros del equipo azul son los defensores e intentan frustrar los esfuerzos del equipo rojo.
* El equipo blanco es un equipo neutral que definir los objetivos y las reglas y supervisa el ejercicio. Los miembros del equipo blanco son menos técnicos, pero poseen conocimientos sobre gestión y cumplimiento. El equipo blanco es el árbitro de este ejercicio.
* A veces, también hay un equipo morado, donde los miembros del equipo rojo y azul trabajan juntos para identificar vulnerabilidades y explorar formas de mejorar los controles.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

2.4.4 Avatar

Sin embargo, otras organizaciones pueden realizar un programa de recompensa por errores. Este es un esfuerzo formal para identificar cualquier error que pueda generar una vulnerabilidad. Los programas de recompensa por errores generalmente están abiertos al público e incluyen aplicaciones/resultados entregados en línea y, posiblemente, una recompensa monetaria.



2.4.5 Analizador de Paquetes

Los analizadores de paquetes, o analizadores de protocolos de paquetes, interceptan y registran el tráfico de red. Realizan las siguientes funciones — ya sea con fines legítimos, como la resolución de problemas o con fines ilegítimos, como comprometer los datos:

* Análisis de problemas de red.
* Detección de intentos de intrusión en la red.
* Aislamiento del sistema explotado.
* Registro del tráfico.
* Detección de usos indebidos de la red.

\
2.4.6 Resultado del Analizador de Protocolos

El análisis de paquetes es como espiar a alguien.

Sucede cuando alguien está examinando todo el tráfico de red a medida que pasa a través de su NIC, independientemente de si el tráfico está dirigido a ellos o no. Los delincuentes logran realizar análisis de paquetes de la red utilizando software, hardware o una combinación de ambos.

La imagen muestra cómo el análisis de paquetes puede ver todo el tráfico de la red o apuntar a un protocolo, servicio o incluso una cadena de caracteres específicos, como un nombre de usuario o una contraseña. Algunos analizadores de paquetes de la red observan todo el tráfico y modifican todo el tráfico o parte de este.





