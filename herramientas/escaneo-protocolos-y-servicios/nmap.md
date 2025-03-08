# Nmap

## Parámetros mas usados en NMAP

A continuación, se describen los parámetros más comunes de NMAP y su utilidad en las auditorías de seguridad:

***

### **1. `-sn` – Escaneo de Hosts Activos (Ping Scan)**

**Uso:** Este parámetro se utiliza para descubrir qué hosts están activos en la red sin hacer un escaneo completo de puertos.\
**Ejemplo:**

```bash
nmap -sn 192.168.1.0/24
```

**Propósito:** Permite identificar rápidamente los dispositivos en una red.

***

### **2. `-iL [archivo]` – Escaneo de una lista de IPs**

**Uso:** Permite escanear una lista de direcciones IP contenida en un archivo de texto.\
**Ejemplo:**

```bash
nmap -iL ips.txt
```

**Propósito:** Es útil cuando se tiene un archivo con múltiples direcciones IP que se quieren escanear todas juntas.

***

### **3. `-p [puertos]` – Escaneo de Puertos Específicos**

**Uso:** Escanea puertos específicos o un rango de puertos.\
**Ejemplo:**

```bash
nmap -p 22,80,443 192.168.1.1
```

**Propósito:** Permite realizar un escaneo enfocado solo en puertos que se consideren relevantes para la auditoría.

***

### **4. `-sV` – Detección de Versiones de Servicios**

**Uso:** Detecta la versión de los servicios que están corriendo en los puertos abiertos.\
**Ejemplo:**

```bash
nmap -sV 192.168.1.1
```

**Propósito:** Este parámetro es fundamental para identificar vulnerabilidades específicas de versiones de software y servicios.

***

### **5. `-O` – Detección de Sistema Operativo**

**Uso:** Detecta el sistema operativo del host objetivo.\
**Ejemplo:**

```bash
nmap -O 192.168.1.1
```

**Propósito:** Ayuda a identificar el sistema operativo de la máquina de destino, lo cual es útil para explotar vulnerabilidades específicas de ese sistema.

***

### **6. `-sS` – Escaneo SYN (Half-Open Scan)**

**Uso:** Realiza un escaneo de puertos utilizando el método SYN, que es sigiloso y no establece una conexión completa.\
**Ejemplo:**

```bash
nmap -sS 192.168.1.1
```

**Propósito:** Es uno de los métodos más utilizados para realizar escaneos sigilosos, ya que no completa el proceso de enlace de 3 vías de la conexión TCP.

***

### **7. `-T[0-5]` – Control de la Velocidad del Escaneo**

**Uso:** Ajusta la velocidad del escaneo, donde `-T0` es muy lento y `-T5` es muy rápido.\
**Ejemplo:**

```bash
nmap -T4 192.168.1.1
```

**Propósito:** Controla el nivel de agresividad del escaneo, balanceando la velocidad con la posibilidad de detección.

***

### **8. `-n` – Deshabilitar Resolución DNS**

**Uso:** Desactiva la resolución de nombres DNS, lo que hace que el escaneo sea más rápido.\
**Ejemplo:**

```bash
nmap -n 192.168.1.1
```

**Propósito:** Usado cuando se desea evitar la resolución DNS y agilizar el escaneo.

***

### **9. `-oA [archivo_base]` – Guardar Resultados en Diferentes Formatos**

**Uso:** Guarda los resultados del escaneo en tres formatos diferentes: XML, NMAP y GNMAP.\
**Ejemplo:**

```bash
nmap -oA resultado 192.168.1.1
```

**Propósito:** Permite guardar los resultados de manera estructurada para su posterior análisis o para integrarlos con otras herramientas como Metasploit.

***

### **10. `-sU` – Escaneo de Puertos UDP**

**Uso:** Realiza un escaneo de puertos UDP.\
**Ejemplo:**

```bash
nmap -sU 192.168.1.1
```

**Propósito:** Se utiliza para escanear puertos UDP, que no siempre son tan evidentes como los puertos TCP. Los puertos UDP suelen ser más lentos de escanear.

***

### **11. `-v` – Modo Verboso**

**Uso:** Aumenta el nivel de detalle de la salida del escaneo.\
**Ejemplo:**

```bash
nmap -v 192.168.1.1
```

**Propósito:** Permite obtener más detalles durante el escaneo, lo que puede ser útil para el diagnóstico de la red o el análisis de los resultados.

***

### **12. `--min-rate [n]` – Control de la Velocidad Mínima de Envío de Paquetes**

**Uso:** Establece la cantidad mínima de paquetes por segundo que se enviarán durante el escaneo.\
**Ejemplo:**

```bash
nmap --min-rate 6000 192.168.1.1
```

**Propósito:** Utilizado para controlar la velocidad del escaneo y evitar la sobrecarga en la red o en los dispositivos objetivos.
