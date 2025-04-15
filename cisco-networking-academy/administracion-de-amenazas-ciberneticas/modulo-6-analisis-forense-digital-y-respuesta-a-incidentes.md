# Módulo 6: Análisis Forense Digital y Respuesta a Incidentes

## 6.1 Manejo de evidencia y atribución del ataque

## 6.1.1 Informática Forense Digital

Ahora que se han investigado e identificado las alertas válidas, ¿Qué se debe hacer con las pruebas? Inevitablemente, el analista especializado en ciberseguridad descubrirá evidencia de actividades delictivas. Con el fin de proteger la organización y para evitar la ciberdelincuencia, es necesario identificar los actores de amenaza, informar a las autoridades competentes y brindar pruebas para respaldar la acusación. Los analistas de ciberseguridad de categoría 1 suelen ser los primeros en descubrir delitos. Deben saber cómo manejar la evidencia correctamente y atribuírsela a los actores de amenaza.

La informática forense digital consiste en la recuperación e investigación de la información que se encuentra en dispositivos digitales en relación con actividades delictivas. Los indicadores de compromiso son la evidencia de que se ha producido un incidente de ciberseguridad. Esta información puede consistir en datos en dispositivos de almacenamiento, en la memoria volátil de la computadora, o los rastros de ciberdelincuencia que se conservan en los datos de la red, como pcaps y registros. Es esencial que se conserven todos los indicadores de compromiso para futuros análisis y atribución de ataques.

En términos generales, la ciberdelincuencia se puede caracterizar como proveniente del interior o el exterior de la organización. Las investigaciones privadas se realizan a individuos dentro de la organización. Estos individuos podrían simplemente comportarse de maneras que violan los acuerdos de usuario o manifestar otra conducta no delictiva. Cuando los individuos son sospechosos de participar en actividades delictivas que involucran el robo o la destrucción de propiedad intelectual, una organización puede optar por involucrar a las autoridades encargadas del orden público, en cuyo caso la investigación se vuelve pública. Los usuarios internos también pueden usar la red de la organización para llevar a cabo otras actividades delictivas que no están relacionadas con la misión de la organización, pero sí violan diversas leyes. En este caso, los funcionarios públicos llevarán a cabo la investigación.

Cuando un atacante externo ataca una red y roba o altera datos, es necesario recopilar evidencia para documentar el alcance del ataque. Diversos organismos reguladores especifican una serie de acciones que una organización debe adoptar cuando se ponen en riesgo distintos tipos de datos. Los resultados de la investigación forense pueden ayudar a identificar las medidas que deben tomarse.

Por ejemplo, las regulaciones de US HIPAA estipulan que, si ocurre una violación de datos que involucra información de pacientes, se debe notificar a las personas afectadas. Si la violación involucra a más de 500 personas en un estado o jurisdicción, se debe notificar también a los medios de comunicación. La investigación de informática forense digital debe utilizarse para determinar qué personas fueron afectadas y certificar la cantidad de individuos involucrados a fin de que pueda efectuarse la notificación correspondiente de acuerdo con las reglas de la HIPAA.

Es posible que la propia organización sea objeto de una investigación. Los analistas de ciberseguridad pueden encontrarse en contacto directo con evidencia forense digital que detalle la conducta de los miembros de la organización. Los analistas deben conocer los requisitos relativos a la preservación y el manejo de dicha evidencia. Si no lo hacen correctamente, esto podría ocasionar sanciones penales para la organización y hasta para el analista de ciberseguridad si se establece que hubo intención de destruir pruebas.

## 6.1.2 El Proceso Forense Digital

Es importante que una organización desarrolle procesos y procedimientos bien documentados para el análisis forense digital. El cumplimiento reglamentario puede exigir esta documentación y las autoridades pueden inspeccionarla en caso de una investigación pública.

La publicación especial 800-86 de NIST _Guía para la Integración de Técnicas Forenses en Respuesta a Incidentes_ es un recurso valioso para las organizaciones que requieren orientación en el desarrollo de planes forenses digitales. Por ejemplo, recomienda que la informática forense se realice mediante el proceso de cuatro fases.

A continuación se describen las cuatro fases básicas del proceso forense de pruebas digitales.

#### **El Proceso Forense de Evidencia Digital**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Paso 1. Recolección\
Esta es la identificación de posibles fuentes de datos forenses y la obtención, el manejo y el almacenamiento de esos datos. Esta etapa es fundamental porque se debe tener especial cuidado para no dañar, perder u omitir datos importantes.

Paso 2. Examen\
Esto implica evaluar y extraer información relevante de los datos recopilados. Esto puede implicar la descompresión o el descifrado de los datos. Es posible que sea necesario eliminar información irrelevante para la investigación. La identificación de evidencia real en grandes recopilaciones de datos puede ser un proceso muy difícil y lento.

Paso 3. Análisis\
Esto implica sacar conclusiones de los datos Se deben documentar las características salientes; por ejemplo: personas, lugares, horas y eventos, entre otras. Este paso puede implicar también la correlación de datos de múltiples fuentes.

Paso 4. Informes\
Esto implica preparar y presentar la información que resulte del análisis. La elaboración de informes debe ser imparcial y se deben ofrecer explicaciones alternativas si corresponde. Deben incluirse las limitaciones del análisis y los problemas que se enfrentaron. También deben hacerse sugerencias para profundizar la investigación y tomar medidas adicionales.

6.1.3 Verifique su Comprensión - Identifique los Pasos en el Proceso de Análisis Forense Digital

6.1.4 Tipos de EvidenciaEn los procedimientos legales y en términos generales, la evidencia se clasifica como directa o indirecta. La evidencia directa es aquella consta de la evidencia que indudablemente poseía el acusado o de afirmaciones de un testigo presencial que vio directamente el comportamiento delictivo.

Adicionalmente, la evidencia se clasifica del siguiente modo:

Mejor evidencia\
Esto es evidencia de que está en su estado original. Esta evidencia podrían ser los dispositivos de almacenamiento utilizados por un acusado o archivos que se pueda probar que no fueron alterados.

Evidencia corroborativa\
Esta es evidencia que respalda una afirmación que se desarrolla a partir de la mejor evidencia.

Evidencia indirecta\
Esta es una evidencia que, en combinación con otros hechos, establece una hipótesis. También se conoce como evidencia circunstancial. Por ejemplo, la existencia de pruebas que demuestren que un individuo ya cometió delitos similares puede respaldar la afirmación de que la persona cometió el delito del que se la acusa.



## 6.1.6 Orden de Recolección de Evidencia

IETF RFC 3227 proporciona pautas para la recolección de evidencia digital. Describe un orden para la recolección de evidencia digital según la volatilidad de los datos. Los datos almacenados en la memoria RAM son los más volátiles y se perderán cuando se apague el dispositivo. Además, podría suceder que los datos importantes en la memoria volátil se sobrescriban mediante procesos rutinarios de la máquina. Por lo tanto, la recolección de evidencia digital debe comenzar con las pruebas más volátiles hasta llegar a las menos volátiles, como se muestra en la figura.

#### Prioridad de Recolección de Evidencia

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Un ejemplo de recolección de evidencia desde la más volátil a la menos volátil es el siguiente:

* Registros de memoria, memoria caché
* Tabla de routing, caché de ARP, tabla de procesos, estadísticas del núcleo, memoria RAM
* Sistemas de archivos temporales
* Medios no volátiles, fijos y extraíbles
* Registros remotos y datos de monitoreo
* Topologías e interconexiones físicas
* Medios de archivado, cinta u otros tipos de copias de respaldo

Deben registrarse detalles de los sistemas desde los que se recopiló la evidencia, lo que incluye quién tiene acceso a los sistemas y en qué nivel de permisos. Estos detalles deben incluir configuraciones de hardware y software para los sistemas desde los que se obtuvieron los datos.

## 6.1.7 Cadena de Custodia

Aunque es posible que la evidencia se haya recopilado de fuentes que respaldan la atribución del delito a un individuo acusado, puede cuestionarse la veracidad de las pruebas aduciendo que podrían haberse alterado o fabricado después de la recopilación. Para contrarrestar este argumento, debe definirse y respetarse una rigurosa cadena de custodia.

La cadena de custodia implica la recolección, el manejo y el almacenamiento seguro de la evidencia. Deben mantenerse registros detallados de lo siguiente:

* ¿Quién descubrió y recopiló la evidencia?
* Todos los detalles sobre el manejo de la evidencia, incluidos momentos, lugares y personal involucrado.
* ¿Quién era el responsable principal de la evidencia, cuándo se le asignó la responsabilidad y cuándo cambió la custodia?
* Quién tiene acceso físico a la evidencia mientras está almacenada. El acceso debe limitarse solamente al personal esencial.

## 6.1.8 Integridad y Preservación de los Datos

Al recopilar datos, es importante que se conserven en su estado original. La marca de hora de los archivos debe conservarse. Por esto, debe copiarse la evidencia original y los análisis deben realizarse solamente en las copias del original. Esto permite evitar la pérdida o modificación accidental de las pruebas. Dado que las marcas de hora pueden formar parte de la evidencia, se debe evitar abrir archivos desde el medio original.

Deberá registrarse el proceso utilizado para crear copias de la evidencia que se utiliza en la investigación. Siempre que sea posible, las copias deben ser copias directas de nivel de bit de los volúmenes de almacenamiento originales. Debería ser posible comparar la imagen del disco archivado y la imagen del disco investigada para identificar si se ha manipulado el contenido del disco investigado. Por esta razón, es importante archivar y proteger el disco original para mantenerlo en su condición original, sin alteraciones.

La memoria volátil podría contener evidencia forense, por lo que deben utilizarse herramientas especiales para preservar dicha evidencia antes de que el dispositivo se apague y las pruebas se pierdan. Los usuarios no deben desconectar, desenchufar ni apagar máquinas infectadas, a menos que el personal de seguridad lo indique explícitamente.

El seguimiento de estos procesos garantizará que se conserven todas las pruebas de conducta ilícita y que se puedan identificar indicadores de avenencia.

## 6.1.9 Atribución del Ataque

Después de que se ha evaluado el nivel del ciberataque y se ha recopilado y preservado la evidencia, el equipo de respuesta ante los incidentes puede comenzar a identificar el origen del ataque. Como sabemos, existe una amplia variedad de actores de amenazas, que abarca desde individuos descontentos y hackers, hasta ciberdelincuentes y bandas criminales o incluso naciones. Algunos delincuentes actúan desde el interior de la red, mientras que otros pueden estar del otro lado del mundo. La sofisticación de la ciberdelincuencia también varía. Las naciones pueden emplear a grandes grupos de individuos altamente capacitados para llevar a cabo un ataque y ocultar sus rastros, mientras que otros actores de amenaza pueden elegir presumir abiertamente de sus actividades delictivas.

La atribución de una amenaza hace referencia a la acción de determinar a la persona, organización o nación responsable de una intrusión o ataque exitosos.

La identificación de los actores responsables de una amenaza debe darse por medio de la investigación sistemática y fundamentada de la evidencia. Mientras que puede resultar útil especular también sobre la identidad de los agentes de amenaza identificando posibles motivaciones para un incidente, es importante no dejar que esto desvíe la investigación. Por ejemplo, atribuir un ataque a un competidor comercial puede desviar la investigación de la posibilidad de que una banda criminal o una nación sean los responsables.

En las investigaciones con base en evidencias, el equipo de respuesta ante los incidentes correlaciona las tácticas, las técnicas y los procedimientos (TTP, Tactics, Techniques and Procedures) empleados en el incidente con los de otros ataques conocidos. Los ciberdelincuentes, al igual que muchos otros delincuentes, tienen características específicas que se repiten en la mayoría de sus delitos. Las fuentes de inteligencia de amenazas pueden ayudar a relacionar las TTP identificadas por una investigación con fuentes conocidas de ataques similares. Sin embargo, esto pone de relieve un problema con la atribución de la amenaza. Es muy improbable que la evidencia de ciberdelincuencia sea directa. Identificar similitudes entre las TTP de agentes de amenazas conocidos y desconocidos es evidencia circunstancial.

Algunos aspectos de una amenaza que pueden ayudar a la atribución son la ubicación de los hosts o dominios originarios, las características del código utilizado en malware, las herramientas utilizadas y otras técnicas. A veces, en el ámbito de la seguridad nacional, no es posible atribuir abiertamente las amenazas porque esto dejaría al descubierto métodos y capacidades que necesitan protección.

Para las amenazas internas, la administración de activos desempeña un papel fundamental. Descubrir los dispositivos desde donde se inició un ataque puede llevar directamente al agente de amenaza. Las direcciones IP, las direcciones MAC y los registros de DHCP pueden ayudar a rastrear las direcciones usadas en el ataque hasta llegar a un dispositivo específico. Los registros de AAA son muy útiles en este sentido, ya que detallan quién tuvo acceso a los recursos de red, en qué momento lo hizo y qué recursos eran.



## 6.1.10 El Marco MITRE ATT\&CK

Una forma de atribuir un ataque es modelar el comportamiento del actor de amenazas. El marco de Tácticas Adversariales, Técnicas y Conocimiento Común (ATT\&CK) de MITRE permite detectar tácticas, técnicas y procedimientos del atacante como parte de la defensa de amenazas y la atribución de ataques. Esto se hace mapeando los pasos de un ataque a una matriz de tácticas generalizadas y describiendo las técnicas que se utilizan en cada táctica. Las tácticas consisten en los objetivos técnicos que un atacante debe lograr para ejecutar un ataque y las técnicas son los medios por los que se realizan las tácticas. Por último, los procedimientos son las acciones específicas tomadas por los actores de amenazas en las técnicas identificadas. Los procedimientos son el uso documentado de técnicas en el mundo real por parte de los actores de amenazas.

El marco MITRE ATT\&CK es una base de conocimiento global sobre el comportamiento de los actores de amenazas. Se basa en la observación y el análisis de ataques en el mundo real con el propósito de describir el comportamiento del atacante, no el ataque en sí. Está diseñado para permitir el intercambio automatizado de información mediante la definición de estructuras de datos para el intercambio de información entre su comunidad de usuarios y MITRE.

La figura muestra un análisis de una explotación de ransomware de la excelente caja de arena en línea ANY.RUN. Las columnas muestran las tácticas de matriz de ataque empresarial, con las técnicas que utiliza el malware dispuestas debajo de las columnas. Al hacer clic en la técnica, se enumeran los detalles de los procedimientos que utiliza la instancia específica de malware con una definición, explicación y ejemplos de la técnica.

**Nota**: Haga una búsqueda en Internet de MITRE ATT\&CK para obtener más información sobre la herramienta.

#### Matriz MITRE ATT\&CK para una Explotación de Ransomware

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



6.1.11 Video del Laboratorio - Recolección de Información del Sistema Después de un Incidente

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## 6.2 La Cadena de Eliminación Cibernética

6.2.1 Pasos de la Cadena de Eliminación Cibernética

La Cadena de Eliminación Cibernética fue desarrollada por Lockheed Martin para identificar y evitar ciberintrusiones. Hay siete pasos a la Cadena de Eliminación Cibernética. Enfocarse en estos pasos ayuda a los analistas a entender las técnicas, herramientas y procedimientos de los actores de amenaza. Al responder a un incidente de seguridad, el objetivo es detectar y detener el ataque lo antes posible en el transcurso de la cadena de eliminación. Cuanto antes se detenga el ataque, menor será el daño y menor será la información que el atacante obtenga acerca de la red atacada.

En la Cadena de Eliminación Cibernética, se detalla qué debe hacer un atacante para alcanzar su objetivo. Los pasos de la Cadena de Eliminación Cibernética se muestran en la figura.

Si el atacante es detenido en cualquier etapa, se rompe la cadena del ataque. Romper la cadena significa que el defensor frustró con éxito la intrusión del actor de amenaza. Los actores de amenaza tienen éxito solamente si completan el paso 7.

**Nota:** Actor de amenaza es el término utilizado en este curso para referirse al participante que instiga el ataque. Sin embargo, Lockheed Martin utiliza el término “adversario” en su descripción de la Cadena de Eliminación Cibernética. Por lo tanto, los términos adversario y actor de amenaza, se usan como sinónimos en este tema.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

## 6.2.2 Reconocimiento

El Reconocimiento tiene lugar cuando el actor de amenaza realiza una búsqueda, reúne inteligencia y selecciona objetivos. Esto le permite determinar al actor de amenaza si vale la pena realizar el ataque. Cualquier información pública puede ayudar a determinar qué, dónde, y cómo fue el ataque realizado. Hay mucha información disponible para el público, especialmente en el caso de organizaciones importantes; esto incluye artículos de prensa, sitios web, actas de conferencias y dispositivos de red orientados al público. Cada vez hay más información disponible sobre los empleados en las redes sociales.

El actor de amenaza escogerá objetivos descuidados o sin protección porque hay una mayor posibilidad de penetrarlos y atacarlos exitosamente. El actor de amenaza analiza toda la información que obtiene para determinar su importancia y ver si revelan otras vías posibles de ataque.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de reconocimiento.

| Tácticas del adversario                                                                                                                                                                                                                                                                                                                                                                                       | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Planear y realizar investigaciones:</p><ul><li>Recolectar correos electrónicos</li><li>Identificar empleados en redes sociales</li><li>Recopilar información de relaciones públicas (comunicados de prensa, premios, asistentes a conferencias, etc.)</li><li>Descubrir servidores orientados a Internet</li><li>Realizar escaneos de la red para identificar direcciones IP y puertos abiertos.</li></ul> | <p>Descubrir la intención del adversario:</p><ul><li>Alertas de registro web y datos de búsqueda histórica</li><li>Análisis del navegador del minado de datos</li><li>Crear guías para detectar comportamientos que indiquen actividad de reconocimiento</li><li>Priorizar la defensa en torno a las tecnologías y las personas a las que apunta la actividad de reconocimiento.</li></ul> |



## 6.2.3 Armamentización

El objetivo de este paso es utilizar la información de reconocimiento para desarrollar un arma contra sistemas o individuos que sean blancos específicos en la organización. Para el desarrollo de esta arma, el diseñador utilizará las vulnerabilidades de los activos que se detectaron y las incorporará en una herramienta que pueda implementarse. Después de que la herramienta se haya utilizado, se espera que el actor de amenaza haya logrado su objetivo de tener acceso al sistema o la red de destino, lo que afecta el estado de un objetivo o de toda la red. El actor de amenaza examinará en más detalle la seguridad de la red y los activos para poner de manifiesto debilidades adicionales, obtener el control de otros activos e implementar ataques adicionales.

No es difícil elegir un arma para el ataque. El actor de amenaza solo necesita ver qué ataques están disponibles para las vulnerabilidades que detectó. Hay muchos ataques prediseñados y ampliamente probados. Uno de los problemas de estos ataques es que, debido a que son tan conocidos, es muy probable que también los conozcan los defensores. A menudo, es más eficaz utilizar un ataque de día cero para evitar los métodos de detección. Un ataque de día cero utiliza un arma desconocida para los defensores y los sistemas de seguridad de la red. El actor de amenaza puede elegir desarrollar su propia arma específicamente diseñada para evitar la detección, con la información que obtuvo sobre la red y los sistemas. Los atacantes han aprendido a crear numerosas variantes de sus ataques para evadir las defensas de la red.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de armamentización.

| Tácticas del adversario                                                                                                                                                                                                                                                                                       | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Preparar y organizar la operación:</p><ul><li>Obtener una herramienta automatizada para entregar la carga útil de malware (arma)</li><li>Seleccionar o crear un documento para presentar a la víctima.</li><li>Seleccionar o crear una puerta trasera y una infraestructura de comando y control</li></ul> | <p>Detectar y recolectar artefactos de armamento:</p><ul><li>Asegurarse de que las reglas y firmas de IDS estén actualizadas.</li><li>Realizar un análisis completo de malware.</li><li>Crear detecciones para el comportamiento de las armas conocidos.</li><li>¿Es el malware antiguo, "listo para usar" o nuevo que podría indicar un ataque personalizado?</li><li>Recopilar archivos y metadatos para análisis futuros.</li><li>Determinar qué artefactos de armamento son comunes a qué campañas.</li></ul> |



## 6.2.4 Entrega

Durante este paso, el arma se transmite al objetivo mediante un vector de entrega. Esto puede ocurrir usando un sitio web, un medio USB extraíble o un archivo adjunto de correo electrónico. Si no se entrega el arma, el ataque no tiene éxito. El actor de amenaza utilizará muchos métodos diferentes para aumentar las posibilidades de entrega de la carga útil, como encriptar las comunicaciones, modificar el código para que parezca legítimo u ocultar el código. Los sensores de seguridad son tan avanzados que pueden detectar el código malicioso, a menos que se altere para evitarlo. El código puede modificarse para parecer inocente y tener la capacidad de realizar las acciones necesarias, aunque podría demorar más tiempo en ejecutarse.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de entrega.

| Tácticas del adversario                                                                                                                                                                                                                                                                   | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Lanzar malware al objetivo:</p><ul><li>Directo contra servidores web</li><li><p>Entrega indirecta a través de:</p><ul><li>Correo electrónico malicioso</li><li>Malware en memoria USB</li><li>Interacciones en las redes sociales</li><li>Sitios web comprometidos</li></ul></li></ul> | <p>Bloquear la entrega de malware:</p><ul><li>Analizar la ruta de infraestructura utilizada para la entrega.</li><li>Comprender los servidores objetivo, las personas y los datos disponibles para atacar.</li><li>Inferir la intención del adversario en función de los objetivos.</li><li>Recopilar registros web y de correo electrónico para la reconstrucción forense.</li></ul> |

## 6.2.5 Explotación

Una vez aplicada el arma, el actor de la amenaza la utiliza para quebrar la vulnerabilidad y obtener el control del objetivo. Los objetivos de ataque más comunes son las aplicaciones, las vulnerabilidades de sistemas operativos y los usuarios. El atacante debe utilizar un ataque que tenga el efecto deseado. Esto es muy importante porque, si se ejecuta el ataque incorrecto, está claro que no funcionará, pero los efectos secundarios imprevistos, como una denegación de servicio o reinicios reiterados del sistema, causarán una atención indebida que podría informar fácilmente a los analistas de ciberseguridad sobre el ataque y las intenciones del actor de la amenaza.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de aprovechamiento.

| Tácticas del adversario                                                                                                                                                                                                                                                                                                                                                                                    | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Explotar una vulnerabilidad para obtener acceso:</p><ul><li>Usar vulnerabilidades de software, de hardware o humanas</li><li>Adquirir o desarrollar el ataque</li><li>Utilizar un ataque desencadenado por el adversario para las vulnerabilidades del servidor</li><li>Usar un ataque activado por la víctima, como abrir un archivo adjunto de correo electrónico o un enlace web malicioso</li></ul> | <p>Entrene a los empleados, asegure el código y endurezca los dispositivos:</p><ul><li>Capacitar a los empleados de concientización sobre la seguridad y hacer pruebas periódicas de correo electrónico</li><li>Capacitar a desarrolladores web para asegurar el código</li><li>Escaneo regular de vulnerabilidades y pruebas de penetración</li><li>Medidas de endurecimiento de puntos finales</li><li>Auditoría de puntos finales para determinar de forma forense el origen del ataque</li></ul> |



## 6.2.6 Instalación

En este paso, el actor de amenaza establece una puerta trasera al sistema para poder seguir teniendo acceso al objetivo. Para preservar esta puerta trasera, es importante que el acceso remoto no alerte a los analistas de ciberseguridad ni a los usuarios. Para ser eficaz, el método de acceso debe sobrevivir a los análisis antimalware y al reinicio de la computadora. Este acceso persistente también puede permitir las comunicaciones automatizadas, que resultan especialmente eficaces cuando se necesitan varios canales de comunicación al comandar una _botnet_.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de instalación.

| Tácticas del adversario                                                                                                                                                                                                                                                                                                                                             | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Instalar una puerta trasera persistente:</p><ul><li>Instalar <em>webshell</em> en el servidor web para un acceso persistente.</li><li>Crear un punto de persistencia agregando servicios, clave de ejecución automática, etc.</li><li>Algunos adversarios modifican la marca de tiempo del malware para que aparezca como parte del sistema operativo.</li></ul> | <p>Detectar, registrar y analizar la actividad de instalación:</p><ul><li>HIPS para alertar sobre rutas de instalación comunes.</li><li>Determinar si el malware requiere privilegios elevados o privilegios de usuario</li><li>Auditoría de puntos finales para descubrir creaciones de archivos anormales.</li><li>Determinar si el malware es una amenaza conocida o una nueva variante.</li></ul> |

## 6.2.7 Comando y Control

En este paso, el objetivo es establecer el comando y control (CnC o C2) con el sistema objetivo. Los hosts atacados suelen enviar información fuera de la red a un controlador en Internet. Esto ocurre porque la mayoría del malware requiere la interacción manual para exfiltrar datos de la red. El actor de amenaza utiliza los canales de CnC para emitir comandos al software que instala en el objetivo. El analista de ciberseguridad debe ser capaz de detectar comunicaciones de CnC para descubrir el host atacado. Esto puede hacerse con tráfico no autorizado de Internet Relay Chat (IRC) o tráfico excesivo hacia los dominios sospechosos.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de comando y control.

Se ve mejor en modo horizontal.

| Tácticas del adversario                                                                                                                                                                                                                                                                                                                     | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Abrir un canal para la manipulación de los objetivos:</p><ul><li>Abrir un canal de comunicación bidireccional a la infraestructura CNC</li><li>Los canales CNC más comunes son a través de protocolos web, DNS y de correo electrónico</li><li>La infraestructura CnC puede ser propiedad del adversario o de otra red víctima</li></ul> | <p>Última oportunidad para bloquear la operación:</p><ul><li>Investigar posibles nuevas infraestructuras CnC</li><li>Descubrir la infraestructura CnC a través del análisis de malware</li><li>Aísle el tráfico DNS a los servidores DNS sospechosos, especialmente DNS dinámico</li><li>Evite el impacto bloqueando o deshabilitando el canal CnC</li><li>Consolidar el número de puntos de presencia de Internet</li><li>Personalizar las reglas de bloqueo de los protocolos CnC en los servidores proxy web</li></ul> |

## 6.2.8 Acciones sobre Objetivos

El paso final de la Cadena de Eliminación Cibernética es cuando el actor de amenaza logra su objetivo original. Este puede ser el robo de datos, la ejecución de un ataque de DDoS, o el uso de la red atacada para crear y enviar correo electrónico no deseado o mina de Bitcoin. Llegado este momento, el actor de amenaza está profundamente arraigado en los sistemas de la organización, ocultando sus movimientos y cubriendo sus rastros. Es extremadamente difícil eliminar el actor de amenaza de la red.

La tabla resume algunas de las tácticas y defensas que se utilizan durante el paso de acciones en objetivos.

Se ve mejor en modo horizontal.

| Tácticas del adversario                                                                                                                                                                                                                                                                                                             | Defensa del SOC                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Coseche las recompensas de un ataque exitoso:</p><ul><li>Collect user credentials</li><li>Escalada de privilegios</li><li>Reconocimiento interno</li><li>Movimiento lateral a través del medio ambiente.</li><li>Recopilar y filtrar datos</li><li>Destruir sistemas</li><li>Sobrescribir, modificar o corromper datos</li></ul> | <p>Detectar mediante el uso de pruebas forenses:</p><ul><li>Establecer manual de respuesta a incidentes</li><li>Detectar la filtración de datos, el movimiento lateral y el uso no autorizado de credenciales</li><li>Respuesta inmediata del analista para todas las alertas</li><li>Análisis forense de puntos finales para una clasificación rápida</li><li>Network packet captures to recreate activity</li><li>Realizar evaluación de daños</li></ul> |

\
6.3 El Modelo de Diamante del Análisis de Intrusiones
-----------------------------------------------------

## 6.3.1 Descripción General del Modelo de Diamante

El Modelo de Diamante del Análisis de Intrusión está compuesto de cuatro partes, como se muestra en la figura. El modelo representa un incidente o evento de seguridad. En el Modelo de Diamante, un evento es una actividad de tiempo limitado que está restringido a un paso específico donde el adversario utiliza la capacidad sobre la infraestructura para atacar una víctima para lograr un resultado específico.

Las cuatro características principales de un evento de intrusión son el adversario, la capacidad, la infraestructura y la víctima:

Adversario\
Estas son las partes responsables de la intrusión.

\
Capacidad\
Esta es una herramienta o técnica que utiliza el adversario para atacar a la víctima

\
Infraestructura\
Esta es la ruta o rutas de red que los adversarios utilizan para establecer y mantener el comando y control de sus capacidades.

\
Víctima\
Este es el objetivo del ataque. Sin embargo, la víctima podría ser el objetivo inicial y, luego, el atacante puede utilizarla como parte de la infraestructura para iniciar otros ataques.

El adversario usa capacidades sobre la infraestructura para atacar a la víctima. El modelo puede interpretarse como diciendo: «El adversario usa la infraestructura para conectarse con la víctima. El adversario desarrolla la capacidad de explotar a la víctima». Por ejemplo, un adversario podría usar una funcionalidad como el malware sobre la infraestructura de correo electrónico para aprovecharse de la víctima.

Las metacaracterísticas amplían un poco el modelo para incluir los siguientes elementos importantes:

Marca de hora\
Esto indica la hora de inicio y fin de un evento y es una parte integral de la agrupación de actividad maliciosa.

Fase\
Este concepto es análogo al de los pasos en la Cadena de Eliminación Cibernética; la actividad maliciosa incluye dos o más pasos ejecutados seguidamente para lograr el resultado deseado.

Resultado\
Esto definir lo que el adversario obtuvo en el evento. Los resultados pueden documentarse como uno o más de los siguientes: confidencialidad afectada, integridad afectada y disponibilidad afectada.

Dirección\
Esto indica la dirección del evento en el Modelo de Diamante. Algunas direcciones son adversario a infraestructura, infraestructura a víctima, víctima a infraestructura e infraestructura a adversario.

Metodología\
Esto se utiliza para clasificar el tipo general del evento, como exploración de puertos, suplantación de identidad, ataque de entrega de contenido, saturación SYN, etc.

Recursos\
Existen uno o más recursos externos utilizados por el adversario para el evento de intrusión, como software, conocimiento del adversario, información (por ejemplo, nombre de usuario/contraseñas) y activos para llevar a cabo el ataque (hardware, fondos, instalaciones, acceso a la red).

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

6.3.2 Cómo Desplazarse por el Modelo de Diamante

Como analistas especializados en ciberseguridad, es posible que se les pida que utilicen el Modelo de Diamante del Análisis de Intrusiónes para diagramar una serie de eventos de intrusión. El Modelo de Diamante es ideal para ilustrar de qué manera el atacante pasa de un evento al siguiente.

Por ejemplo, en la figura, un empleado informa que su computadora se comporta de manera extraña. El técnico de seguridad realiza un análisis del host que indica que la computadora está infectada con malware. Un análisis del malware revela que el malware contiene una lista de nombres de dominio de CnC. Estos nombres de dominio se resuelven en una lista de direcciones IP. Luego, estas direcciones IP se utilizan para identificar al adversario, así como para investigar los registros a fin de determinar si otras víctimas de la organización utilizan el canal de CnC.

#### Caracterización de un ataque del Modelo de Diamante

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

6.3.3 El Modelo de Diamante y la Cadena de Eliminación Cibernética

Los adversarios no ejecutan un solo evento. En cambio, los eventos se entretejen en una cadena en la que cada evento debe completarse con éxito antes del siguiente. Esta serie de eventos puede asignarse a la Cadena de Eliminación Cibernética analizada previamente en el capítulo.

En el siguiente ejemplo (que se muestra en la figura), se ejemplifica el proceso integral de un adversario a medida que atraviesa verticalmente la Cadena de Eliminación Cibernética, utiliza un host afectado para desplazarse horizontalmente hacia otra víctima, y empieza otro subproceso de la actividad:

1. El adversario realiza una búsqueda web sobre la empresa víctima Gadgets, Inc. y recibe, como parte de los resultados, el nombre de dominio gadgets.com.
2. El adversario utiliza gadgets.com, el dominio que acaba de detectar, para realizar una nueva búsqueda de “administrador de red gadgets.com”. Así, descubre publicaciones de usuarios en los foros alegando que son administradores de red de gadgets.com. Los perfiles de usuario revelan sus direcciones de correo electrónico.
3. El adversario envía correos electrónicos de suplantación de identidad con un troyano adjunto a los administradores de red de gadgets.com.
4. Un administrador de red (NA1) de gadgets.com abre el archivo adjunto malicioso. Esto ejecuta el ataque incluido y permite seguir con la ejecución de código.
5. El host atacado de NA1 envía un mensaje HTTP Post a una dirección IP para registrarla con un controlador de CnC. El host atacado de NA1 recibe una respuesta HTTP.
6. Mediante ingeniería inversa, se revela que el malware tiene direcciones IP adicionales configuradas que actúan como una copia de respaldo si el primer controlador no responde.
7. Mediante un mensaje de respuesta HTTP de CnC enviado al host de NA1, el malware comienza a actuar como un web proxy para nuevas conexiones de TCP.
8. Mediante la información del proxy ejecutado en el host de NA1, el adversario realiza una búsqueda web con las palabras “la investigación más importante de todos los tiempos” y encuentra a la víctima 2, Interesting Research Inc.
9. El adversario consulta la lista de contactos de correo electrónico de NA1 para buscar contactos de Interesting Research, Inc. y descubre el contacto del Director principal de investigaciones de Interesting Research, Inc.
10. El Director principal de investigaciones de Interesting Research, Inc. recibe un correo electrónico de phishing dirigido desde la dirección de correo electrónico de NA1 de Gadget, Inc. enviado desde el host de NA1 con la misma carga útil del evento 3.

El adversario tiene ahora dos víctimas afectadas desde las que puede iniciar ataques adicionales. Por ejemplo, el adversario podría analizar la lista de contactos del Director Principal de Investigaciones en busca de posibles víctimas adicionales. El adversario también podría configurar otro proxy para exfiltrar todos los archivos del Director Principal de Investigaciones.

**Nota:** Este ejemplo es una adaptación del ejemplo del Departamento de Defensa de los Estados Unidos de la publicación “El Análisis de Intrusiones del Modelo de Diamante”.

#### Ejemplos de Hilo de Actividad

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>





