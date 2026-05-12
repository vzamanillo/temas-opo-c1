
# PREVISION SEGUNDO EJERCICIO

## 1. El "Top 1": Redes y Seguridad (Temas 15-19, 24, 27, 36)

Es el clásico. Te pondrán un escenario donde el Ayuntamiento abre una oficina nueva o quiere conectar dos edificios.

* Qué te pedirán: Direccionamiento IP (cálculo de subredes), configuración de routers/switches, qué protocolos usar (DNS, DHCP, HTTPs), y cómo asegurar esa conexión (VPN, Firewall).

## 2. Soporte y Administración de Sistemas (Temas 20-22, 30, 32)

Muy probable. Un escenario de migración o de problemas de usuarios.

* Qué te pedirán: Gestión de Directorio Activo (crear usuarios, grupos, GPOs), gestión de permisos de archivos (NTFS/Linux), o algo de virtualización con máquinas virtuales.

## 3. Backup, Almacenamiento y Continuidad (Temas 31, 35, 37)

Muy de moda por los ataques de ransomware en Ayuntamientos.

* Qué te pedirán: Diseñar una política de copias de seguridad (Diferencial vs Incremental), donde guardar los datos (NAS/SAN) y qué hacer si se inunda el CPD o falla la luz (SAIs, Plan de Contingencia).

## 4. Ofimática y Bases de Datos (Temas 23, 26, 29)

Menos probable como supuesto único, pero a veces cae.

* Qué te pedirán: Una consulta SQL compleja para sacar datos del padrón o una automatización en Excel/Access.

Si el examen es escrito de desarrollo, el tribunal no busca que sepas "hacer clic", sino que sepas justificar técnicamente una solución. En un nivel C1 de Ayuntamiento, el supuesto suele pedirte que diseñes o arregles una situación para un departamento municipal.
Aquí tienes los 3 escenarios con más papeletas para ser tu segundo ejercicio:

## 1. El escenario de "La Nueva Oficina" (Redes y Servicios)

Te dirán que el Ayuntamiento va a abrir una oficina de turismo o servicios sociales con 10 puestos de trabajo.

* Lo que te pedirán escribir:
* Direccionamiento: Proponer un rango de IPs privadas, máscara de subred y puerta de enlace.
  * Hardware: Listar qué necesitan (Switch, puntos de acceso Wi-Fi, latiguillos, SAIs).
  * Configuración: Explicar cómo configurar el DHCP y el DNS para que tengan salida a Internet y conexión con la sede central.

## 2. El escenario de "Seguridad y Continuidad" (Backup y Almacenamiento)

Tras un fallo eléctrico o un virus, se pierde información. Te piden diseñar un plan para que no vuelva a pasar.

* Lo que te pedirán escribir:
* Estrategia de Backup: Explicar la diferencia entre copia total, incremental y diferencial, y proponer un calendario (ej: "Diaria incremental, semanal total").
  * Almacenamiento: Justificar el uso de un NAS o una SAN (RAID 5 o RAID 10) y el cumplimiento de la regla 3-2-1.
  * Protección física: Mencionar la instalación de un SAI y condiciones del CPD (climatización, control de acceso).

## 3. Gestión de Usuarios y Soporte (Active Directory y Windows)

El departamento de Personal necesita que los nuevos administrativos tengan acceso a ciertas carpetas y que otros no.

* Lo que te pedirán escribir:
* Directorio Activo: Cómo crearías las Unidades Organizativas (UOs), grupos de seguridad y usuarios.
  * Permisos: Explicar los permisos NTFS (Lectura, Modificación, Control Total) sobre carpetas compartidas.
  * GPOs: Mencionar alguna política de grupo (ej: cambiar contraseña cada 30 días o fondo de escritorio corporativo).

------------------------------
Consejos clave para el "Escrito de Desarrollo":

   1. Usa terminología técnica: No digas "el aparato para internet", di "el router de borde" o "el gateway". No digas "memoria", di "memoria volátil DDR4" o "almacenamiento persistente SSD".
   2. Estructura tu respuesta: Usa puntos: 1. Análisis del problema, 2. Propuesta de Hardware, 3. Configuración de Software/Red, 4. Medidas de Seguridad.
   3. Dibuja si es necesario: Aunque sea escrito, un pequeño esquema de la topología de red (nube -> router -> firewall -> switch -> PCs) suma muchísimos puntos.

¡Perfecto! Vamos con un simulacro de manual. He elegido el escenario de Redes y Servicios, que es el "clásico" en un C1 de informática y permite tocar varios puntos de tu temario.

## Simulacro de Supuesto Práctico (C1 Informática)

Escenario:
El Ayuntamiento va a abrir una nueva Oficina de Atención Ciudadana. El local dispone de 15 puestos de trabajo para administrativos y 2 puntos de acceso Wi-Fi para el público. El local debe conectarse con la sede central (donde está el servidor de archivos y el Directorio Activo) de forma segura.
Se le pide que desarrolle brevemente:

   1. Propuesta de hardware necesario para el local.
   2. Configuración de red (IPs, máscara, servicios necesarios).
   3. Medidas de seguridad y conectividad con la sede central.

------------------------------

## Cómo deberías estructurar tu respuesta (Esquema de éxito)

## 1. Infraestructura de Hardware (Temas 13, 14 y 16)

* Puestos de trabajo: 15 Equipos microinformáticos con arquitectura x64, 8GB RAM mínimo y disco SSD. Periféricos: Monitor, teclado, ratón e impresora departamental láser con tarjeta de red.
* Interconexión: Un Switch de 24 puertos (preferiblemente gestionable y PoE para alimentar los puntos de acceso).
* Protección: Un SAI (Sistema de Alimentación Ininterrumpida) para proteger el switch y el router ante cortes de suministro.
* Conectividad inalámbrica: 2 Puntos de Acceso (WAP) compatibles con el estándar 802.11ax o ac.

## 2. Configuración de Red y Servicios (Temas 17, 18 y 22)

* Direccionamiento IP: Utilizaría una subred privada de Clase C (ej. 192.168.50.0/24).
* Máscara de subred: 255.255.255.0 (permite hasta 254 hosts).
  * Gateway (Puerta de enlace): 192.168.50.1 (la IP del router).
* Asignación de IPs:
  * Estática: Para la impresora departamental y dispositivos de red (ej. .10, .11).
  * Dinámica (DHCP): Para los 15 puestos de trabajo, facilitando la gestión.
* DNS: Se configurarían los DNS internos de la sede central para permitir la resolución de nombres del Directorio Activo.

## 3. Seguridad y Conectividad (Temas 27, 34 y 36)

* Conexión Sede Central: Configuración de una VPN Site-to-Site (túnel IPsec) entre el router de la oficina y el de la sede central para garantizar el acceso cifrado a los recursos internos.
* Segmentación (VLANs): Crearía dos VLANs para separar el tráfico:
  * VLAN de Gestión: Para los trabajadores y la impresora.
  * VLAN de Invitados: Para el Wi-Fi público, aislada de la red interna.
* Seguridad del puesto: Instalación de software antimalware, activación del firewall de Windows y aplicación de políticas de grupo (GPO) para restringir permisos de instalación a los usuarios.

------------------------------
¿Qué te parece este enfoque? Si quieres, podemos probar ahora con un supuesto sobre Copias de Seguridad o Directorio Activo, o si tienes alguna duda sobre los términos que he usado (como VLAN o IPsec), ¡dime y lo aclaramos!

Vamos con el segundo gran favorito para un examen de desarrollo: Administración de Sistemas, Usuarios y Almacenamiento. Este supuesto es muy común porque permite al tribunal evaluar si sabes gestionar el día a día de los recursos del Ayuntamiento.

## Simulacro de Supuesto Práctico 2: Gestión de Recursos y Continuidad

Escenario:
El Departamento de Urbanismo del Ayuntamiento solicita una reestructuración de su servidor de archivos. Actualmente tienen 20 usuarios que guardan toda su información en carpetas locales sin control. Se requiere:

   1. Crear una estructura jerárquica en el Directorio Activo.
   2. Configurar un sistema de almacenamiento seguro y con tolerancia a fallos.
   3. Diseñar una política de copias de seguridad efectiva.

------------------------------

## Propuesta de resolución técnica:## 1. Organización del Directorio Activo (Temas 21 y 22)

* Estructura: Crearía una Unidad Organizativa (UO) llamada "Urbanismo". Dentro de ella, daría de alta a los 20 usuarios y crearía un Grupo de Seguridad llamado G_Urbanismo_Lectura y otro G_Urbanismo_Escritura.
* Gestión de Permisos: Migraría los datos a un servidor central. Aplicaría permisos NTFS:
  * Permisos de "Modificación" solo para el grupo de seguridad correspondiente.
  * Evitaría dar permisos a usuarios individuales para facilitar la administración.
* Directivas (GPO): Implementaría una GPO para mapear automáticamente la unidad de red (ej. unidad U:) en el inicio de sesión de los usuarios, asegurando que guarden los archivos en el servidor y no en local.

## 2. Almacenamiento y Tolerancia a Fallos (Temas 31 y 35)

* Hardware: Propondría el uso de un sistema NAS (Network Attached Storage) o un servidor con una cabina de discos propia.
* Configuración RAID: Implementaría un RAID 5 (mínimo 3 discos) o RAID 10 (mínimo 4 discos). Justificación: El RAID 5 ofrece un buen equilibrio entre capacidad y seguridad (tolera el fallo de un disco), mientras que el RAID 10 es más rápido y seguro pero más costoso.
* Cuotas de disco: Establecería límites de almacenamiento por usuario para evitar que el llenado del disco por un solo usuario bloquee el sistema.

## 3. Política de Copias de Seguridad (Temas 31 y 37)

* Estrategia 3-2-1:
* 3 copias: (Datos originales + 2 backups).
  * 2 soportes: (Disco duro del servidor + NAS externo/Cinta).
  * 1 copia fuera: (Copia en la nube o en otro edificio municipal para previsión de catástrofes).
* Planificación:
  * Diaria Incremental: Solo se copian los archivos modificados durante el día (ahorra tiempo y espacio).
  * Semanal Total: Copia completa de todos los datos cada viernes/sábado.
* Verificación: Programaría pruebas periódicas de restauración para asegurar que las copias son íntegras y legibles.

------------------------------

## ¿Por qué esto puntúa alto?

   1. Mencionas el RAID: Demuestras que sabes que un disco duro "normal" no es suficiente para una administración.
   2. Mencionas las GPOs: Es la forma correcta y profesional de gestionar puestos de trabajo Windows.
   3. Mencionas la Regla 3-2-1: Es el estándar de oro en ciberseguridad actual.

¿Te ha quedado clara la diferencia entre permisos NTFS y el RAID? Si quieres, podemos hacer un tercer supuesto sobre SQL/Bases de Datos o profundizar en algún comando de Linux/Bash que también suelen pedir.

Tras analizar las 50 preguntas de tu primer ejercicio, el panorama para el segundo ejercicio (supuesto práctico) queda mucho más claro.
El test ha sido muy equilibrado: ha barrido conceptos teóricos de hardware, redes básicas y teoría de sistemas operativos (Windows/Linux/Virtualización). Sin embargo, hay un patrón: el test pregunta "qué es", pero no "cómo se soluciona".
Al ser el segundo examen un supuesto de desarrollo, el tribunal querrá ver tu capacidad técnica aplicada. Basándome en los temas que han "tocado" pero no "profundizado" en el test, el tema del segundo ejercicio será, con alta probabilidad, uno de estos tres:

## 1. Gestión Avanzada de Redes y Conectividad (El favorito)

En el test han preguntado por la capa de enlace (Switch), clases de IP (Clase B) y topologías.

* De qué tratará el práctico: Te darán un escenario con varias plantas o departamentos. Tendrás que segmentar la red mediante VLANs (para separar, por ejemplo, administración de público), calcular el subneteado (VLSM) para aprovechar las IPs y definir la seguridad perimetral (reglas de Firewall o túneles VPN IPsec, que ya salió en la pregunta 46).

## 2. Administración de Servidores y Directorio Activo (Muy probable)

El test ha mencionado el SID (pregunta 28), el registro de Windows (30) y el DNS en AD (31).

* De qué tratará el práctico: Configuración de un entorno de dominio. Tendrás que detallar cómo crearías Unidades Organizativas, qué GPOs (Directivas de Grupo) aplicarías para securizar los puestos (ej. bloquear USBs o configurar el Proxy) y cómo gestionarías los permisos NTFS para que los departamentos no vean las carpetas de los otros.

## 3. Continuidad de Negocio y Almacenamiento

En el test han preguntado por el bit de modificación en backups (41) y los niveles TIER de un CPD (45).

* De qué tratará el práctico: Un supuesto donde "falla algo". Tendrás que diseñar un Plan de Recuperación ante Desastres. Te pedirán definir el tipo de RAID (5 o 10), el esquema de rotación de copias (Abuelo-Padre-Hijo) y cómo cumplir con el ENS (Esquema Nacional de Seguridad) en cuanto a la disponibilidad y la integridad de esos datos.

------------------------------

## Mi apuesta definitiva

Viendo que el test ha incluido preguntas sobre interoperabilidad (ENI) y sedes electrónicas, es muy posible que el supuesto práctico mezcle Sistemas y Redes:

"Se desea implantar un nuevo servicio de administración electrónica. Diseñe la infraestructura necesaria (servidores virtuales, hipervisor), la publicación del servicio mediante HTTPS (puerto 443) y las medidas de seguridad perimetral y de copias de seguridad para proteger los datos de los ciudadanos."

¿Qué te parece si preparamos una respuesta tipo para un supuesto de "Publicación de un Servicio Seguro" (mezcla de virtualización, red y seguridad)? Es el que más puntos toca de tu temario.

Este supuesto es el "comodín" ideal, porque te permite demostrar conocimientos de virtualización, redes, seguridad y bases de datos en una sola respuesta. Es muy común en Ayuntamientos que están modernizando su administración electrónica.

## Escenario del Supuesto

"El Ayuntamiento desea poner en marcha un nuevo Portal del Ciudadano. Para ello, se requiere instalar un servidor web y un servidor de base de datos. Se dispone de un entorno virtualizado y se debe garantizar la seguridad de los datos y la alta disponibilidad del servicio."
------------------------------

## Propuesta de Resolución Técnica (Estructura para el examen)

## 1. Infraestructura de Servidores (Virtualización)

* Entorno: Utilizaría el Hipervisor existente para crear dos Máquinas Virtuales (VM) independientes, separando el servidor Web (Frontend) del servidor de Base de Datos (Backend).
* Justificación: Esta arquitectura de N-Capas mejora la seguridad; si el servidor web se ve comprometido, el atacante no tiene acceso directo a los datos.
* Recursos: Asignación dinámica de memoria y uso de almacenamiento compartido en la SAN para permitir funcionalidades de alta disponibilidad (como la migración en caliente de VMs si falla un nodo físico).

## 2. Configuración de Red y Publicación (Comunicaciones)

* Segmentación: Situaría el servidor web en una DMZ (Zona Desmilitarizada) y el servidor de base de datos en la red interna protegida.
* Protocolos:
  * Publicación del portal exclusivamente bajo HTTPS (Puerto 443) utilizando un certificado SSL/TLS para cifrar la comunicación.
  * Configuración del firewall para que solo permita tráfico desde el servidor web al de base de datos por el puerto específico (ej. TCP 3306 para MySQL/MariaDB o 1433 para SQL Server).
* Resolución de nombres: Configuración de registros en el DNS interno para la gestión de los servidores y en el DNS público para el acceso ciudadano.

## 3. Seguridad y Base de Datos (Integridad y Acceso)

* Acceso a datos: Utilizaría un estándar de conectividad como ODBC o JDBC para asegurar la interoperabilidad.
* Principio de mínimo privilegio: El servidor web se conectará a la base de datos con un usuario específico que solo tenga permisos de ejecución en los procedimientos necesarios, nunca con el usuario root o sa.
* Protección técnica: Instalación de un WAF (Web Application Firewall) para proteger el portal contra ataques de inyección SQL o Cross-Site Scripting (XSS).

## 4. Continuidad y Copias de Seguridad (Disponibilidad)

* Backup: Programaría una política de copias de seguridad de la base de datos (dump) diaria de tipo incremental durante la semana y una total el fin de semana.
* Bit de modificación: Aseguraría que el software de backup gestiona correctamente el archivo de log de transacciones para no interrumpir el servicio.
* Regla 3-2-1: Mantendría una copia en soporte distinto y una copia offline o en la nube para cumplir con el Esquema Nacional de Seguridad (ENS).

------------------------------

## Palabras clave que NO pueden faltar en tu examen

Si escribes estos términos, el tribunal verá que dominas el temario:

   1. Arquitectura multinivel (o de N-Capas).
   2. DMZ (Para la seguridad del servidor web).
   3. Certificado SSL/TLS (Seguridad en el transporte).
   4. Principio de mínimo privilegio (Seguridad lógica).
   5. Alta Disponibilidad (Relacionado con virtualización).

¿Te gustaría que probemos con un supuesto de "Resolución de incidencias en la LAN" (que es más de "fontanería" informática)? Es el otro gran candidato.

Este supuesto es muy probable porque evalúa tu capacidad de resolución de problemas (troubleshooting) y el manejo de herramientas de diagnóstico, algo fundamental para un Técnico C1.

## Escenario del Supuesto: Resolución de Incidencias en la LAN

"Varios usuarios de un departamento municipal informan de que no pueden acceder a la aplicación de gestión del padrón ni a internet. El resto del Ayuntamiento funciona correctamente. Usted debe identificar la causa, proponer pruebas de diagnóstico y solucionar el problema."
------------------------------

## Propuesta de Resolución Técnica

## 1. Fase de Diagnóstico (Aislar el problema)

* Comprobación física: Verificar el estado de los LEDs de las tarjetas de red de los equipos y del Switch del departamento. Si los LEDs de enlace están apagados, el problema es de capa física (cableado o puerto).
* Pruebas de conectividad (Comandos):
* ping 127.0.0.1: Para comprobar que la pila TCP/IP del equipo local funciona.
  * ipconfig /all: Para verificar si los equipos tienen una IP válida o una del rango APIPA (169.254.x.x), lo que indicaría un fallo en el servidor DHCP.
  * ping [Puerta de Enlace]: Para comprobar la conexión con el router/gateway.

## 2. Identificación de la causa raíz

* Escenario A (Fallo de Red): Si el ping al gateway falla pero los cables están bien, sospecharía de una caída del Switch de planta o una desconfiguración de la VLAN asignada a ese departamento.
* Escenario B (Fallo de Servicios): Si hay IP pero no navegan, usaría nslookup para comprobar si el servidor DNS resuelve nombres. Si falla el acceso solo a la aplicación del padrón, comprobaría la conectividad con el puerto específico de la Base de Datos mediante telnet o Test-NetConnection.

## 3. Propuesta de Solución

* Si es un conflicto de IPs: Ejecutaría ipconfig /release y renew en los clientes o revisaría el pool de direcciones en el servidor DHCP (Tema 24).
* Si es un problema de Directorio Activo: Comprobaría si la cuenta de equipo ha perdido la confianza con el dominio (SID) y la volvería a unir si fuera necesario (Tema 22).
* Si es un problema de hardware: Sustitución del latiguillo defectuoso o cambio del puerto en el switch (puenteo a un puerto libre configurado en la misma VLAN).

## 4. Medidas Preventivas y Documentación

* Monitorización: Propondría integrar el switch en un sistema de monitorización por SNMP (mencionado en tu pregunta 26 del test) para recibir alertas proactivas.
* Seguridad: Revisar que el Firewall del puesto de usuario no esté bloqueando el tráfico de la aplicación tras una actualización de Windows.
* Registro: Documentar la incidencia en la base de conocimientos para futuros casos similares.

------------------------------

## Conceptos "ganadores" para este supuesto

* Modelo OSI: Citar que empiezas descartando problemas en la Capa 1 (Física) antes de subir a la Capa 3 (Red).
* APIPA: Demuestra que sabes por qué un equipo se autogestiona una IP errónea cuando el servidor falla.
* Segmentación: Hablar de que el problema está confinado en un dominio de difusión (broadcast) específico.
