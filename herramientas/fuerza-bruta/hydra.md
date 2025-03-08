---
description: >-
  Es una herramienta de fuerza bruta y ataques de diccionario. Su objetivo
  principal es automatizar intentos de inicio de sesión contra servicios y
  protocolos para identificar debilidades.
---

# Hydra

## Propósito principal

Crackeo de contraseñas: Prueba combinaciones de usuarios y contraseñas contra servicios en red (ej.: SSH, FTP, HTTP, RDP) para detectar credenciales comprometidas.

Evaluación de resistencia: Verifica si los sistemas son susceptibles a ataques de autenticación por no aplicar políticas robustas (bloqueo de intentos, complejidad de contraseñas, etc.).

## **Protocolos y servicios compatibles** <a href="#id-2-protocolos-y-servicios-compatibles" id="id-2-protocolos-y-servicios-compatibles"></a>

Hydra soporta **más de 50 protocolos**, incluyendo:

* **Servicios web**: HTTP/HTTPS (formularios de login, APIs, WordPress).
* **Protocolos de red**: SSH, FTP, Telnet, SMB, SMTP, RDP, VNC.
* **Bases de datos**: MySQL, PostgreSQL, Oracle.
* **Otros**: LDAP, SIP, ICQ, incluso servicios personalizados mediante módulos.

## **Casos de uso en auditorías y pentesting** <a href="#id-3-casos-de-uso-en-auditorias-y-pentesting" id="id-3-casos-de-uso-en-auditorias-y-pentesting"></a>

**Pruebas de autenticación web**: Ataques a paneles de administración (ej.: WordPress, Joomla).

**Evaluación de servicios expuestos**: Validar si un servidor FTP o SSH permite credenciales por defecto o fácilmente adivinables.

**Simulación de ataques reales**: Identificar si un sistema bloquea múltiples intentos fallidos (protección contra _**brute-force**_).

```
hydra -l usuario -P diccionario.txt ssh://192.168.1.100
```











