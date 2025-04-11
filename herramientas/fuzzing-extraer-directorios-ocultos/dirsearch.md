# DirSearch

**Dirsearch** es una herramienta de **fuerza bruta** utilizada para **descubrir directorios y archivos ocultos** en un servidor web. Al igual que otras herramientas como DirBuster o DirB, Dirsearch se usa comúnmente en pruebas de penetración y auditorías de seguridad para encontrar recursos no documentados que podrían estar expuestos a **riesgos de seguridad**. La herramienta es especialmente útil para **identificar rutas de acceso** no visibles en aplicaciones web, lo que puede ayudar a encontrar directorios sensibles o archivos que no deberían ser accesibles desde la web.

#### **¿Cómo funciona Dirsearch?**

El funcionamiento de **Dirsearch** es sencillo y se basa en la técnica de **fuerza bruta**, similar a otras herramientas de exploración de directorios. A continuación te explico paso a paso cómo funciona Dirsearch:

1. **Selección del Objetivo**:
   *   El primer paso es proporcionar a Dirsearch la URL del servidor web o la aplicación que quieres escanear. Por ejemplo:

       ```bash
       http://example.com
       ```
2. **Selección de un Diccionario de Palabras**:
   * Dirsearch utiliza un diccionario de palabras para realizar el escaneo. El diccionario contiene nombres comunes de directorios y archivos, como `admin`, `login`, `config`, `backup`, entre otros.
   * Puedes utilizar un diccionario **predefinido** o crear el tuyo propio para adaptarlo a tus necesidades específicas. Los diccionarios predefinidos generalmente incluyen cientos o miles de rutas posibles.
3. **Envío de Solicitudes HTTP**:
   *   Dirsearch comienza a generar solicitudes **HTTP** a la URL objetivo combinando las entradas del diccionario con la URL proporcionada. Por ejemplo, si la entrada del diccionario es `admin`, Dirsearch intentará acceder a:

       ```bash
       http://example.com/admin
       ```
   * Dirsearch continuará probando todas las posibles combinaciones de rutas en el diccionario, enviando solicitudes al servidor y esperando las respuestas.
4. **Análisis de las Respuestas HTTP**:
   * Dirsearch analiza las respuestas que recibe del servidor para determinar si el directorio o archivo existe. Las respuestas más comunes son:
     * **200 OK**: El directorio o archivo existe.
     * **301/302 (Redirección)**: Puede indicar que el directorio o archivo existe, pero se redirige a otro recurso.
     * **403 Forbidden**: El directorio o archivo existe, pero el acceso está restringido.
     * **404 Not Found**: El directorio o archivo no existe.
5. **Filtrado y Presentación de Resultados**:
   * Dirsearch muestra los resultados en la consola, indicando las rutas de los directorios o archivos que ha encontrado y los códigos de respuesta HTTP correspondientes.
   * También puede almacenar los resultados en un archivo para su análisis posterior, lo cual es útil para auditorías más grandes o para mantener un registro de las rutas descubiertas.

#### **Características Clave de Dirsearch**:

* **Diccionarios Personalizables**: Dirsearch viene con varios diccionarios predefinidos, pero también permite usar diccionarios personalizados. Puedes usar tus propias listas de rutas específicas si tienes alguna idea de lo que estás buscando.
* **Velocidad de Escaneo**: Dirsearch permite ajustar la velocidad del escaneo utilizando el parámetro `-t`, que indica el número de **hilos concurrentes** (conexiones paralelas). Esto puede hacer que el escaneo sea más rápido o más lento según el entorno.
* **Filtrado de Respuestas**: Puedes configurar Dirsearch para que solo muestre ciertos códigos de respuesta HTTP (por ejemplo, solo mostrar respuestas `200 OK`), lo que facilita la visualización de los resultados más relevantes.
* **Soporte para HTTPS**: Dirsearch es completamente compatible con servidores que usan **HTTPS**, lo que lo hace adecuado para aplicaciones web modernas que implementan seguridad en la capa de transporte.
* **Opciones de Configuración Avanzadas**: Dirsearch ofrece varias opciones de configuración para adaptar el escaneo a las necesidades específicas de los usuarios, como control de tiempo de espera, configuraciones para proxy, entre otras.

#### **Comando Básico para Ejecutar Dirsearch**:

El comando básico para ejecutar Dirsearch es el siguiente:

```bash
python3 dirsearch.py -u http://example.com
```

Esto iniciará el escaneo sobre la URL proporcionada, utilizando un diccionario por defecto.

**Ejemplo con un Diccionario Personalizado:**

```bash
python3 dirsearch.py -u http://example.com -w /ruta/a/mi/diccionario.txt
```

En este caso, se usa un diccionario personalizado para probar las rutas.

**Ejemplo con Mayor Velocidad (usando múltiples hilos):**

```bash
python3 dirsearch.py -u http://example.com -t 50
```

Este comando usará 50 hilos concurrentes para realizar el escaneo más rápidamente.

#### **Herramientas y Opciones Avanzadas**:

*   **`-e`**: Esta opción permite especificar las extensiones de archivo que Dirsearch debe probar. Por ejemplo, si solo te interesa encontrar archivos `.php` o `.html`, puedes usar:

    ```bash
    python3 dirsearch.py -u http://example.com -e php,html
    ```
*   **`-x`**: Permite excluir ciertos códigos de estado HTTP de los resultados. Si solo te interesan los resultados con **código 200 (OK)**, puedes usar:

    ```bash
    python3 dirsearch.py -u http://example.com -x 404,403
    ```
*   **`-o`**: Esta opción permite guardar los resultados en un archivo de texto para su análisis posterior:

    ```bash
    python3 dirsearch.py -u http://example.com -o resultado.txt
    ```

#### **Casos de Uso Comunes**:

1. **Pruebas de Penetración**: Dirsearch se utiliza con frecuencia en pruebas de penetración para descubrir recursos ocultos en un servidor web, como paneles de administración, archivos de configuración, directorios de respaldo, etc. Estos recursos pueden ser sensibles y representar un riesgo de seguridad si no están debidamente protegidos.
2. **Auditoría de Seguridad**: Los administradores de sistemas y profesionales de seguridad utilizan Dirsearch para auditar sus propios servidores en busca de **directorios o archivos expuestos** accidentalmente.
3. **Exploración de APIs**: Dirsearch también puede usarse para descubrir puntos de acceso ocultos en **APIs web** o **endpoints** no documentados.

#### **Precauciones y Consideraciones**:

* **Uso Ético**: Dirsearch debe utilizarse **solo en entornos donde tengas permiso explícito** para realizar escaneos. El uso sin autorización de esta herramienta para escanear servidores ajenos puede ser ilegal y está penado por la ley.
* **Impacto en el Rendimiento**: Los escaneos de directorios pueden generar una carga significativa en el servidor, especialmente si se usan muchos hilos o un diccionario grande. Siempre es recomendable realizar estos escaneos de manera responsable para evitar afectar el rendimiento del servidor.
* **Evitar la Detección**: El uso de Dirsearch en entornos de producción puede ser detectado por sistemas de protección, como firewalls o sistemas de detección de intrusos (IDS). Asegúrate de realizar las pruebas de manera controlada y preferentemente en entornos de prueba.

#### **Conclusión**:

**Dirsearch** es una herramienta poderosa y flexible para descubrir directorios y archivos ocultos en servidores web. Su enfoque de fuerza bruta, junto con la personalización de diccionarios y la capacidad de ajustar la velocidad del escaneo, la convierte en una excelente opción para pruebas de penetración y auditorías de seguridad. Sin embargo, siempre debe usarse con responsabilidad y con permisos adecuados para evitar problemas legales o técnicos.
