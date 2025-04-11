# GoBuster

**GoBuster** es una herramienta de **fuerza bruta** diseñada para realizar **descubrimiento de directorios y archivos ocultos** en servidores web, similar a otras herramientas como DirBuster o Dirsearch. Es particularmente popular en pruebas de penetración y auditorías de seguridad debido a su **rendimiento** y su capacidad de **trabajar rápidamente** en la identificación de rutas y recursos no documentados en aplicaciones web.

#### **¿Cómo funciona GoBuster?**

GoBuster opera mediante la técnica de **fuerza bruta**, donde prueba una serie de **palabras** o **combinaciones de rutas** contra un servidor web para identificar directorios, archivos o subdominios ocultos. Esta técnica le permite descubrir contenido que no es accesible directamente desde la interfaz pública del sitio web.

A continuación, se explica el proceso detallado de cómo funciona GoBuster:

#### **1. Selección del Objetivo**:

El primer paso es proporcionar la URL del servidor web o la aplicación que quieres escanear. Por ejemplo, si deseas escanear `http://example.com`, ese será el objetivo para el escaneo.

#### **2. Selección de un Diccionario de Palabras**:

GoBuster usa un **diccionario de palabras** (un archivo de texto que contiene una lista de posibles directorios o archivos) para realizar las búsquedas. Estos diccionarios pueden contener nombres comunes de directorios como `admin`, `login`, `uploads`, entre otros.

Puedes usar diccionarios predefinidos que la comunidad ha creado, o puedes crear uno personalizado con nombres de archivos y directorios que desees investigar.

#### **3. Realización de Solicitudes HTTP**:

GoBuster utiliza las entradas del diccionario para construir **solicitudes HTTP**. A medida que procesa cada palabra del diccionario, prueba a acceder a rutas en el servidor web de la siguiente manera:

* Si el diccionario contiene `admin`, GoBuster intentará acceder a `http://example.com/admin`.

GoBuster construye la URL y envía una solicitud HTTP al servidor, observando la respuesta para determinar si el directorio o archivo existe.

#### **4. Análisis de las Respuestas HTTP**:

Cuando GoBuster recibe una respuesta del servidor, la analiza para obtener información sobre la existencia del directorio o archivo. Las respuestas clave incluyen:

* **200 OK**: El directorio o archivo existe.
* **301/302 (Redirección)**: Puede haber una redirección a otro recurso o directorio.
* **403 Forbidden**: El acceso está prohibido, pero el recurso existe.
* **404 Not Found**: El recurso no existe en el servidor.

Con base en las respuestas del servidor, GoBuster presenta los resultados, destacando las rutas que han sido exitosas (con códigos de estado HTTP como 200 o 301).

#### **5. Presentación de Resultados**:

GoBuster mostrará los resultados directamente en la consola, indicando las rutas descubiertas y los códigos de estado HTTP correspondientes. Los resultados pueden ser almacenados en un archivo para análisis posterior, lo que es útil cuando se realizan auditorías más grandes o cuando se quiere mantener un registro de las rutas descubiertas.

#### **Características Clave de GoBuster**:

1. **Alto Rendimiento**:
   * GoBuster es conocido por su **velocidad** debido a que está escrito en **Go** (el lenguaje de programación Go). Esto le permite realizar escaneos mucho más rápidos en comparación con otras herramientas similares que están escritas en lenguajes más lentos.
2. **Soporte para Directorios y Subdominios**:
   * GoBuster no solo se puede usar para escanear **directorios** y **archivos**, sino que también tiene un modo especial para descubrir **subdominios** a través de su funcionalidad de **DNS brute forcing**. Esto lo hace útil tanto para explorar la estructura de una aplicación web como para buscar subdominios ocultos.
3. **Diccionarios Personalizables**:
   * Puedes usar diccionarios predefinidos o crear los tuyos propios. Los diccionarios pueden ser de **grande o pequeña escala**, dependiendo de lo que necesites probar.
4. **Control de Velocidad**:
   * GoBuster permite configurar el número de **hilos concurrentes** (conexiones paralelas) para el escaneo, lo que te permite ajustar el rendimiento y evitar sobrecargar el servidor objetivo.
5. **Filtrado de Resultados**:
   * GoBuster permite filtrar los resultados por el **código de estado HTTP** (por ejemplo, mostrar solo los resultados con código `200 OK`), lo que hace más fácil encontrar los directorios o archivos que realmente existen en el servidor.

#### **Comando Básico para Ejecutar GoBuster**:

Un comando básico para ejecutar GoBuster y buscar directorios es el siguiente:

```bash
gobuster dir -u http://example.com -w /ruta/al/diccionario.txt
```

* `dir`: Indica que GoBuster realizará un escaneo de directorios.
* `-u http://example.com`: Define la URL del objetivo.
* `-w /ruta/al/diccionario.txt`: Define el diccionario de palabras a utilizar para la búsqueda.

**Ejemplo con un Diccionario Personalizado:**

Si quieres usar un diccionario personalizado, el comando sería:

```bash
gobuster dir -u http://example.com -w /path/to/your/wordlist.txt
```

**Ejemplo con Subdominios:**

Si quieres buscar subdominios en lugar de directorios, puedes usar el siguiente comando:

```bash
gobuster dns -d example.com -w /ruta/al/diccionario.txt
```

* `dns`: Esto le indica a GoBuster que realice una búsqueda de subdominios.
* `-d example.com`: El dominio de nivel superior (TLD) para buscar subdominios.
* `-w /ruta/al/diccionario.txt`: El diccionario de palabras para probar subdominios.

**Ejemplo con Varias Opciones:**

Puedes también ajustar otros parámetros como el número de hilos concurrentes:

```bash
gobuster dir -u http://example.com -w /ruta/al/diccionario.txt -t 50
```

* `-t 50`: Utiliza 50 hilos concurrentes, lo que acelera el escaneo.

#### **Casos de Uso Comunes de GoBuster**:

1. **Pruebas de Penetración**:
   * GoBuster es una herramienta muy útil en las pruebas de penetración para descubrir directorios y archivos sensibles que podrían estar expuestos accidentalmente o no documentados en un servidor web.
2. **Auditoría de Seguridad**:
   * Los administradores de sistemas y auditores de seguridad utilizan GoBuster para identificar posibles **vulnerabilidades** al descubrir rutas y recursos que no deberían ser accesibles.
3. **Exploración de Aplicaciones Web y APIs**:
   * Es útil para encontrar directorios ocultos o recursos no documentados en aplicaciones web y **APIs**, que podrían estar mal configurados o expuestos a **riesgos de seguridad**.
4. **Investigación de Subdominios**:
   * GoBuster es excelente para buscar **subdominios ocultos** de un dominio objetivo, lo que puede revelar recursos adicionales en un servidor o infraestructura que no son fácilmente visibles.

#### **Precauciones y Consideraciones**:

* **Uso Ético**: GoBuster debe ser utilizado **solo en entornos con permiso explícito** para realizar escaneos. El uso de esta herramienta sin autorización puede ser ilegal y violar las políticas de privacidad y seguridad.
* **Impacto en el Rendimiento**: GoBuster puede generar una carga significativa en el servidor debido a que realiza múltiples solicitudes simultáneas. Debes usarlo con responsabilidad para evitar afectar el rendimiento del servidor o generar bloqueos.
* **Detección**: Si realizas un escaneo de manera masiva, puede ser detectado por **sistemas de protección**, como firewalls o sistemas de detección de intrusos. Asegúrate de usar la herramienta con precaución y dentro de los límites legales.

#### **Conclusión**:

**GoBuster** es una herramienta rápida y eficiente para **descubrir directorios, archivos y subdominios ocultos** en servidores web. Su diseño basado en **Go** le permite realizar escaneos rápidos y es especialmente útil para **pruebas de penetración** y auditorías de seguridad. Al igual que otras herramientas de fuerza bruta, GoBuster debe usarse con ética y en entornos controlados, siempre con el debido permiso para evitar problemas legales y técnicos.
