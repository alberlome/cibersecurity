# DirB

**DirB** (o **DirBuster**) es una herramienta utilizada en pruebas de penetración y auditorías de seguridad para **realizar descubrimientos de directorios y archivos ocultos** en servidores web. La herramienta funciona mediante el uso de un enfoque de **fuerza bruta** para buscar directorios y archivos no documentados, a menudo conocidos como **directorios ocultos**, que pueden estar presentes en un servidor pero no ser fácilmente accesibles desde la interfaz pública del sitio web.

#### **¿Cómo funciona DirB?**

El funcionamiento de DirB se basa en realizar **peticiones HTTP** a un servidor web con diferentes combinaciones de rutas y nombres de directorios/archivos. A continuación, DirB evalúa las respuestas del servidor para determinar si un directorio o archivo existe, basándose en códigos de respuesta HTTP como:

* **200 OK**: Significa que el directorio o archivo existe y es accesible.
* **403 Forbidden**: El directorio o archivo existe, pero el acceso está restringido.
* **404 Not Found**: El directorio o archivo no existe en el servidor.
* **301 Moved Permanently** o **302 Found**: Puede indicar que un directorio o archivo ha sido redirigido a otro recurso, lo que también es información útil.

#### **Pasos en el proceso de escaneo de DirB**:

1. **Selección del Objetivo**:
   * El usuario proporciona la URL del servidor o aplicación web que se quiere analizar, por ejemplo: `http://example.com`.
2. **Selección de Diccionario de Palabras**:
   * DirB utiliza diccionarios de palabras para realizar el escaneo. Estos diccionarios contienen una lista de nombres comunes de directorios y archivos, como `admin`, `login`, `config`, `uploads`, etc. Los diccionarios pueden ser **estándar**, **personalizados**, o incluso **descargados** de repositorios públicos.
3. **Realización de Solicitudes HTTP**:
   * DirB genera **solicitudes HTTP** para cada entrada del diccionario, construyendo la URL en función de la lista de directorios/archivos a probar.
   * Por ejemplo, si el diccionario contiene `admin`, DirB probará `http://example.com/admin` y observará la respuesta del servidor.
4. **Análisis de Respuestas**:
   * En función de los códigos de estado HTTP obtenidos, DirB clasifica las respuestas:
     * **200 (OK)**: El directorio o archivo existe.
     * **403 (Forbidden)**: El directorio o archivo existe, pero el acceso está restringido.
     * **404 (Not Found)**: El directorio o archivo no existe.
     * Otros códigos, como 301 o 302, pueden indicar redirecciones, lo que podría revelar la presencia de directorios ocultos.
5. **Resultados**:
   * DirB muestra los resultados de las pruebas de forma interactiva o guarda la salida en un archivo para su posterior análisis. Los **directorios encontrados** se presentan con su **código de estado HTTP** y la **ruta completa** que permite acceder a ellos.

#### **Características Principales de DirB**:

* **Diccionarios Personalizables**: Puedes usar diccionarios estándar o personalizar los tuyos propios. DirB tiene un diccionario por defecto, pero puedes añadir otros específicos a tus necesidades.
* **Velocidad de Escaneo**: DirB puede configurarse para ser más rápido (aumentando el número de hilos o conexiones concurrentes) o más lento (para evitar sobrecargar el servidor o hacer que el ataque sea más silencioso).
* **Soporte de HTTP/HTTPS**: DirB es compatible con servidores que usan tanto **HTTP** como **HTTPS**. Esto es útil ya que muchas aplicaciones web modernas operan sobre HTTPS.
* **Filtrado de Resultados**: DirB permite filtrar los resultados según el código de respuesta HTTP o el tamaño del archivo/del directorio, lo que facilita la identificación de directorios relevantes.

#### **Comando Básico para Ejecutar DirB**:

```bash
dirb http://example.com /path/to/wordlist.txt
```

Este comando realizará un escaneo sobre el sitio web `http://example.com` utilizando el diccionario de palabras especificado en `/path/to/wordlist.txt`.

Si deseas realizar un escaneo más rápido, puedes aumentar el número de **hilos** (conexiones concurrentes) que utiliza DirB:

```bash
dirb http://example.com /path/to/wordlist.txt -t 50
```

Aquí, `-t 50` indica que se usarán 50 hilos para las solicitudes concurrentes.

#### **Usos Comunes de DirB**:

1. **Pruebas de Penetración**:
   * DirB es muy popular entre los **profesionales de seguridad** y **penetration testers** para **identificar directorios ocultos** o vulnerabilidades en servidores web.
2. **Descubrimiento de Archivos y Directorios No Documentados**:
   * Es útil para encontrar archivos que **no deberían estar accesibles** o que **no están bien protegidos**, como `backup`, `config`, `logs`, entre otros.
3. **Auditoría de Seguridad**:
   * Los administradores de sistemas y auditores de seguridad también utilizan DirB para **revisar sus propios servidores** y asegurarse de que no haya directorios o archivos expuestos sin protección adecuada.
4. **Exploración de Webs y APIs**:
   * DirB también se usa para explorar rutas de **APIs web** que pueden tener recursos no documentados o endpoints expuestos.

#### **Precauciones y Consideraciones**:

* **Uso Ético**: DirB debe utilizarse solo en entornos donde tengas **permiso explícito** para realizar escaneos. El uso no autorizado de DirB para realizar pruebas de penetración sin consentimiento es ilegal y puede tener consecuencias graves.
* **Impacto en el Rendimiento**: El fuzzing de directorios puede generar una carga significativa en el servidor, por lo que debe hacerse con **precaución** para no sobrecargar el sistema ni interrumpir el servicio.
* **Evitar la Detección**: Si se realiza un escaneo masivo, es posible que sea detectado por sistemas de seguridad como **firewalls** o **sistemas de detección de intrusos** (IDS). Para evitar esto, se pueden ajustar las configuraciones de DirB para que la actividad sea menos ruidosa.

#### **Conclusión**:

DirB es una herramienta muy útil y poderosa para la **recolección de información** durante una auditoría de seguridad, especialmente cuando se busca **descubrir directorios ocultos** y archivos sensibles en aplicaciones web. Al realizar escaneos de fuerza bruta en servidores, puede ayudarte a identificar posibles **vulnerabilidades o puntos de entrada no autorizados**, que podrían ser utilizados para explotar el sistema. Sin embargo, su uso debe ser siempre **ético** y **autorizado**, y debe tenerse en cuenta su impacto en el servidor objetivo.
