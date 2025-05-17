# ¿Cómo proteger tu coche frente al robo a través del puerto OBD2?

En los últimos años, los robos de vehículos a través del puerto OBD2 se han disparado. Este conector, diseñado originalmente para facilitar el diagnóstico de averías, se ha convertido en una de las principales vías de acceso para los ladrones más sofisticados. ¿La buena noticia? Existen varias estrategias para protegerte. Aquí te cuento una evolución lógica que han seguido muchas personas hasta dar con una solución inteligente y discreta. Pero primero que nada, mucha gente se preguntará que es un puerto OBD2?

### **Como lo hacen para robarte el coche**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FGB6BsEvNkH6qj3tNZygi%2Fuploads%2FB6pgNqKEEsqH2Vl383kQ%2FStolen-fiesta.mp4?alt=media&token=f8a81a57-dd34-42c9-849b-9421a6bd100e" %}

### **Introducción al puerto ODB2**

El sistema OBD2 (On-Board Diagnostics II) es una pieza clave en el mantenimiento y diagnóstico de vehículos modernos. No solo permite a los técnicos identificar fallos en los sistemas electrónicos, sino que también es una herramienta indispensable para los propietarios que desean conocer el estado de su coche. Gracias a su conectividad estandarizada y la facilidad de acceso, el puerto OBD2 se ha convertido en el lenguaje universal entre los vehículos y las herramientas de diagnóstico.

El OBD2 ha transformado la forma en que se monitorean los coches, facilitando la identificación de problemas que van desde pequeños errores en los sensores hasta problemas más graves en el motor o el sistema de transmisión. Al permitir que las computadoras a bordo generen códigos de error (DTCs), este sistema ha hecho posible que tanto los talleres como los usuarios realicen diagnósticos precisos y rápidos.

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption><p>Estructura interna de un puerto ODB2</p></figcaption></figure>

### **¿Qué es el OBD2 y para qué sirve el conector?**

El conector OBD2 es el punto de entrada principal para realizar diagnósticos en los vehículos. Ubicado generalmente debajo del tablero, el conector OBD2 cuenta con 16 pines que sirven para diferentes funciones de comunicación entre el vehículo y la herramienta de escaneo. Este conector puede ser utilizado tanto por herramientas de diagnóstico cableadas como inalámbricas, dependiendo del tipo de tecnología que utilice el dispositivo. En lo personal, he utilizado tanto versiones con cables como aquellas que funcionan a través de Bluetooth o Wi-Fi, y las segundas realmente agilizan el proceso, sobre todo en situaciones donde no puedes estar físicamente en el coche.

El OBD2 no solo proporciona acceso a los códigos de error del vehículo, sino que también permite la lectura de datos en tiempo real, tales como la velocidad del motor, el consumo de combustible y la eficiencia de los sistemas de emisiones. Esta versatilidad es lo que ha hecho que el OBD2 sea un estándar en la industria automotriz.

### **Tipos de conectores OBD2: A y B**

Existen dos tipos principales de conectores OBD2: Tipo A y Tipo B. El conector tipo A es común en vehículos ligeros y funciona con una salida de 12V, mientras que el tipo B se utiliza principalmente en vehículos pesados y trabaja con 24V. Ambos tienen la misma estructura de 16 pines, pero su capacidad de transmisión de datos varía.

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

### **Explicación detallada del Pinout OBD2**

Cada pin en el conector OBD2 tiene una función específica. Aquí está la descripción de los pines más relevantes:

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption><p>Pinout ODB2 conector</p></figcaption></figure>

* **Pin 4 y 5**: Son los pines de conexión a tierra, tanto para el chasis como para la señal.
* **Pin 16**: Proporciona la energía de la batería al dispositivo de diagnóstico.
* **Pin 6 y 14**: Son los pines para la comunicación de la red CAN (Controller Area Network), utilizados para la mayoría de los vehículos modernos.
* **Pin 7 y 15**: Estos pines están reservados para la comunicación mediante los protocolos ISO 9141-2 e ISO 14230-4 (KWP2000).

Cada fabricante puede tener configuraciones personalizadas para ciertos pines, lo que significa que algunos vehículos podrían tener funciones adicionales a través de otros pines.&#x20;

### **Protocolos de comunicación más usados en el OBD2**

Los vehículos utilizan diferentes protocolos para la comunicación a través del conector OBD2. Algunos de los más comunes incluyen:

* **ISO 15765-4 (CAN Bus)**: Protocolo más reciente y el más utilizado en vehículos a partir de 2008.
* **ISO 9141-2**: Utilizado principalmente en vehículos europeos y asiáticos.
* **SAE J1850**: Empleado en vehículos estadounidenses, especialmente por General Motors y Ford.

La elección del protocolo depende del fabricante y del modelo del vehículo. En mi experiencia, la mayoría de las herramientas de escaneo modernas pueden manejar múltiples protocolos, lo que facilita la lectura de datos sin importar el tipo de coche.

Bien ahora que ya tenemos algo mas de conocimiento de que es el puerto ODB2, tipos de conectores hay A o B; para que se emplean cada uno de sus pines y que protocolos de comunicación son los mas usados, vamos a pasar a comentar como podemos protegernos de un ataque a este puerto en nuestro coche, con 3 posibles soluciones:

### Primera solución: cortar el puerto original y crear un adaptador personalizado

En un primer intento por evitar el acceso directo, algunos entusiastas de la automoción decidieron cortar el conector OBD2 original del coche, modificar la disposición de los pines y crear un adaptador personalizado.

Así, cualquier intento de conexión con un escáner OBD estándar fallaría… **a menos que se tuviera el adaptador intermedio** con la nueva configuración de pines.

El inconveniente: **cortar el conector original es una medida muy agresiva**, irreversible para muchos, y con posibles implicaciones en la garantía del vehículo o en revisiones técnicas como la ITV.

Existen muchos conectores a la venta para realizar esta operación en las mas distinguidas plataformas de comercio online.

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption><p>Conectores a la venta para esto</p></figcaption></figure>

### Segunda solución: bloquear físicamente el puerto con un candado o chapa antirrobo

Como **alternativa menos invasiva**, surgió la idea de **bloquear el puerto OBD2 físicamente**. Esto se puede hacer instalando una chapa metálica con tornillería antirrobo o incluso una especie de candado especial que **impide acceder al conector**.

Aunque esta solución es más sencilla de implementar y reversible, no deja de ser visible. **Y como ya sabemos, si algo se ve, se puede forzar**. Si un ladrón tiene tiempo o las herramientas adecuadas, podría acabar accediendo igualmente.

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption><p>Candado para el puerto ODB</p></figcaption></figure>

### Última solución: el _Dummy_ OBD

Y ahora viene lo más interesante. Una idea cada vez más extendida y **mucho más eficaz a nivel de disuasión y seguridad, que me gusta mucho**: el _**Dummy**_**&#x20;OBD**.

Este sistema nos permite:

* **Reubicar el puerto OBD2 original** del coche a otro lugar más discreto y difícil de encontrar.
* Instalar en el hueco original un **puerto falso (**_**dummy**_**)** que no está conectado a la centralita.
* Y opcionalmente, **conectarlo a una sirena o sistema de alarma** que se active en cuanto alguien intente conectar algo en ese puerto trampa.

Este método **engaña a los ladrones**, que creen estar accediendo al puerto real, cuando en realidad están **activando una alerta o perdiendo el tiempo** con un conector inútil. No es la técnica mas infalible del mundo, porque se podrían poner a buscar el conector original desmontando paneles, pero en primera instancia ya el tener que perder el tiempo en tener que averiguar que está pasando, puede hacer que muchos ladrones dejen el robo.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Conector con sirena</p></figcaption></figure>

### ¿Dónde conseguir estos dispositivos?

Buscando cómo fabricar mis propios cables personalizados y adaptadores, me encontré con una web que ya tiene todo esto desarrollado y probado:

👉 [**https://www.dummyobd.com/**](https://www.dummyobd.com/)

Aquí puedes encontrar los siguientes productos:

* **Reubicación de ODB**: Que sirve para reposicionar en otro lugar el puerto ODB2 original.
* **Puerto ficticio**: Poner un señuelo en el lugar del original, pero que confunda al intruso dándole señales que no le van a conducir a nada, haciéndole perder tiempo y desesperarse.
* **Puerto ficticio con sirena**: Este sería lo mismo que el puerto ficticio, pero además podemos conectarlo a una sirena independiente del coche o sistema de seguridad.

**También he visto que en Aliexpress, Amazon, y otras plataformas** existen todos los productos que he ido comentando en este artículo.

### Conclusión

Proteger el puerto OBD2 ya no es una opción, es una necesidad si quieres dormir tranquilo. Tanto si eres un manitas del bricolaje automovilístico como si prefieres soluciones ya preparadas, **existen opciones para todos los gustos y niveles de intervención**.

Y tú, ¿Cuál vas a instalar?



Ficheros incluidos:

{% file src="../.gitbook/assets/Stolen-fiesta.mp4" %}
