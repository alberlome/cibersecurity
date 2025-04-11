---
description: Nmap es
---

# Fuzzing: Extraer directorios ocultos

```
Herramientas en Kali Linux
- Dirb
- Dirsearch
- GoBuster
- BurpSuite
```

En el mundo de la **seguridad informática**, dos de las técnicas más poderosas para descubrir vulnerabilidades son **Fuzzing** y la **extracción de directorios ocultos**. Ambas se utilizan para encontrar debilidades en aplicaciones web y sistemas, y aunque se emplean de manera diferente, juntas forman parte de las mejores prácticas para **fortalecer la seguridad** de una infraestructura digital. Aquí te explicamos qué son y cómo se relacionan con la **recolección de información** y la **identificación de fallos de seguridad**.

#### **Fuzzing: La Búsqueda Automática de Errores**

**Fuzzing** es una técnica automatizada de prueba de seguridad utilizada para encontrar vulnerabilidades en aplicaciones, sistemas o redes. Consiste en enviar **entradas aleatorias o malformadas** a un programa para observar cómo responde. El objetivo principal del fuzzing es identificar errores de **validación de entradas**, **desbordamientos de buffer** o cualquier tipo de comportamiento inesperado que pueda comprometer la seguridad.

**¿Cómo funciona el Fuzzing?**

1. **Generación de Entradas**: Un "fuzzer" (la herramienta que realiza el fuzzing) genera entradas aleatorias o específicas que no están previstas por el sistema. Estas entradas pueden ser números, cadenas de texto, caracteres especiales o datos malformados.
2. **Envió de las Entradas**: Estas entradas se envían a la aplicación o sistema objetivo, como una API, servidor web o software.
3. **Monitoreo de Comportamientos**: El sistema se monitorea en busca de **fallos o comportamientos inesperados**. Si el sistema cae, se produce un error crítico o se descubre una vulnerabilidad, se registra la información para su análisis.

**¿Por qué es importante el Fuzzing?**

El fuzzing es fundamental para **encontrar fallos de seguridad** que no son evidentes mediante pruebas tradicionales, como la validación de formularios o la seguridad de las entradas del usuario. Puede descubrir vulnerabilidades como **inyección de código**, **desbordamientos de buffer** o **fallos de validación**, que podrían ser explotadas por atacantes. Es una técnica que se utiliza principalmente para **probar aplicaciones web, APIs y software** de manera automatizada.

**Herramientas de Fuzzing:**

* **AFL (American Fuzzy Lop)**: Una de las herramientas más populares y potentes para realizar fuzzing, especialmente para aplicaciones C/C++.
* **Burp Suite**: Ofrece capacidades de fuzzing para probar aplicaciones web y buscar vulnerabilidades.
* **Peach Fuzzer**: Una herramienta flexible de fuzzing que se puede aplicar a una variedad de protocolos y sistemas.
* **ZZUF**: Una herramienta para fuzzing de aplicaciones que permite enviar entradas aleatorias a diferentes tipos de aplicaciones.

***

#### **Extracción de Directorios Ocultos: Descubriendo Recursos No Documentados**

La **extracción de directorios ocultos** es una técnica utilizada para identificar rutas o archivos que no están visibles para el usuario común, pero que pueden ser accesibles si se conoce su ubicación exacta. Estos directorios o archivos pueden contener **información sensible**, configuraciones críticas o incluso puntos de entrada que los atacantes pueden explotar para acceder a un sistema.

**¿Cómo se realiza la extracción de directorios ocultos?**

1. **Escaneo de Directorios**: Herramientas especializadas buscan directorios o archivos ocultos dentro de una aplicación web o servidor. Estas herramientas intentan acceder a rutas que **no son fácilmente accesibles** a través de la navegación normal, pero que pueden existir en el sistema.
2. **Diccionarios de Directorios**: Usualmente se emplean diccionarios con nombres comunes de directorios y archivos, como `/admin/`, `/backup/`, `/config/`, `/secret/`, etc. También se pueden usar combinaciones personalizadas para **agotar** las posibles rutas ocultas.
3. **Acceso a Archivos y Configuraciones Sensibles**: Si un directorio oculto contiene archivos de configuración, contraseñas, datos de usuario o información crítica, **la extracción de estos directorios** puede dar acceso a recursos no autorizados.

**Herramientas para Extracción de Directorios Ocultos:**

* **DirBuster**: Herramienta que utiliza diccionarios de palabras comunes para buscar directorios y archivos ocultos en servidores web.
* **Dirsearch**: Una herramienta rápida y eficiente para buscar directorios y archivos ocultos, que soporta listas de palabras personalizadas.
* **Gobuster**: Herramienta en Go para realizar búsquedas de directorios y archivos, ideal para pruebas de penetración.
* **Burp Suite**: Con su funcionalidad de **Intruder**, se pueden hacer ataques de fuerza bruta para encontrar directorios ocultos y recursos no documentados.

**¿Por qué es importante esta técnica?**

La **extracción de directorios ocultos** puede revelar información crítica que no está destinada a ser visible para los usuarios. A menudo, los atacantes exploran estos directorios en busca de **puntos de entrada vulnerables**, como paneles de administración, scripts de configuración o archivos con credenciales, que podrían ser utilizados para **comprometer un servidor o sistema**. Los administradores de sistemas también utilizan esta técnica como parte de su **auditoría de seguridad** para asegurarse de que no haya recursos no protegidos o accesibles accidentalmente.

***

#### **Relación entre Fuzzing y Extracción de Directorios Ocultos**

Ambas técnicas tienen un enfoque común en la **detección de vulnerabilidades**, pero se aplican de manera diferente:

* **Fuzzing** se centra en probar entradas **malformadas** o **inesperadas** en un sistema para encontrar vulnerabilidades.
* **La extracción de directorios ocultos**, por otro lado, se enfoca en descubrir **recursos no documentados** en un sistema, los cuales pueden estar expuestos a riesgos si no están adecuadamente protegidos.

Sin embargo, ambas son esenciales en la **recolección de información** durante un **análisis de seguridad**, y pueden ser complementarias en una auditoría o en un proceso de pruebas de penetración.

#### Conclusión

Tanto el **fuzzing** como la **extracción de directorios ocultos** son técnicas fundamentales para identificar vulnerabilidades y puntos débiles en sistemas y aplicaciones. El fuzzing permite descubrir errores de validación o fallos en el manejo de entradas, mientras que la extracción de directorios ocultos ayuda a encontrar recursos sensibles que pueden ser utilizados para acceder a un sistema de manera no autorizada. Juntas, estas técnicas forman parte de un enfoque integral para **fortalecer la seguridad** y proteger los sistemas de posibles **ataques**.

