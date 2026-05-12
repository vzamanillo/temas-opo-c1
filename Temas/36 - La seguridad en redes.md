# SEGURIDAD EN REDES Y PUESTOS DE USUARIO

## 1. SEGURIDAD PERIMETRAL Y CONTROL DE ACCESOS

La seguridad perimetral protege la red interna (LAN) de las amenazas externas (Internet).

* DMZ (Zona Desmilitarizada): Segmento de red aislado donde se ubican los servidores que deben ser accesibles desde fuera (ej. servidor web) para evitar que, si son atacados, el intruso acceda a la red interna.
* Control de Accesos: Proceso de verificar la identidad (Autenticación) y los permisos (Autorización) de un usuario. Se basa en tres factores: algo que sabes (clave), algo que tienes (token) y algo que eres (biometría).

## 2. CORTAFUEGOS (FIREWALLS)

Sistema que filtra el tráfico de red entrante y saliente basado en reglas de seguridad.

* De filtrado de paquetes: Inspecciona cabeceras (IP origen/destino, puertos).
* De inspección de estado (Stateful): Vigila el estado de las conexiones activas.
* Next-Generation Firewall (NGFW): Incluye funciones avanzadas como antivirus de red e inspección profunda de aplicaciones. [9, 10, 11, 12, 13]

## 3. TÉCNICAS CRIPTOGRÁFICAS Y PROTOCOLOS SEGUROS

La criptografía garantiza la confidencialidad e integridad de la información.

* Simétrica: Una sola clave para cifrar y descifrar (rápida, ej. AES).
* Asimétrica (Clave Pública): Una clave pública para cifrar y una privada para descifrar (ej. RSA). Es la base de la Firma Electrónica.
* Protocolos Seguros:
  * HTTPS (TLS): Cifra la navegación web.
  * SSH: Acceso remoto seguro (sustituye a Telnet).
  * SFTP: Transferencia segura de archivos.

## 4. REDES PRIVADAS VIRTUALES (VPN)

Crean un "túnel" cifrado sobre una red pública (Internet) para conectar de forma segura a usuarios remotos o sedes con la red central. [22]

* Protocolos comunes: IPsec, OpenVPN y L2TP.
* Ventaja: Permite que un trabajador acceda a recursos internos como si estuviera físicamente en la oficina.

## 5. SEGURIDAD EN EL PUESTO DEL USUARIO (ENDPOINT)

El eslabón más débil suele ser el terminal del usuario final. Medidas clave:

* Antimalware / EDR: Protección activa contra virus, ransomware y amenazas avanzadas.
* Hardening (Bastionado): Configuración segura del sistema operativo (desactivar servicios innecesarios, cerrar puertos).
* Actualizaciones: Instalación crítica de parches de seguridad.
* Cifrado de disco: (Ej. BitLocker) Protege los datos en caso de robo físico del equipo.
* Concienciación: Formar al usuario en la detección de Phishing e ingeniería social.

Aquí tienes la comparativa entre IDS e IPS, un detalle técnico muy común en los exámenes y documentos de seguridad de red:

## IDS vs. IPS: Vigilancia frente a Acción

Ambos sistemas analizan el tráfico de red en busca de patrones sospechosos o ataques conocidos (firmas), pero su forma de actuar es distinta:

| Característica | IDS (Intrusion Detection System) | IPS (Intrusion Prevention System) |
| --- | --- | --- |
| Función | Detecta y alerta. Es un sistema pasivo. | Previene y detiene. Es un sistema activo. |
| Acción | Envía una notificación al administrador cuando ve algo raro. | Corta la conexión o bloquea el tráfico malicioso al instante. |
| Ubicación | Se coloca "a un lado" del tráfico (copia de los datos). | Se coloca "en línea" (el tráfico pasa a través de él). |
| Analogía | Es una cámara de seguridad que te avisa si alguien entra. | Es un vigilante en la puerta que impide el paso al intruso. |

* Punto clave: El mayor riesgo de un IPS es un "falso positivo" (confundir tráfico legítimo con un ataque), ya que podría bloquear un servicio crítico de la empresa por error. Por eso, muchos administradores configuran el sistema primero como IDS y, cuando están seguros de las reglas, lo activan como IPS.
