# ESQUEMA

Este es un esquema técnico de Arquitectura de N-Capas diseñado para cumplir con los estándares de un examen de oposición y las exigencias del ENS. El diseño se centra en la segmentación física/lógica y la protección del dato.

## Etiquetas Técnicas Imprescindibles para el Dibujo

   1. DMZ (Zona Desmilitarizada): Aísla el servidor web de la red interna. Si el portal es hackeado, el atacante sigue atrapado en este segmento.
   2. Arquitectura de N-Capas: Separación de la capa de Presentación (Web) y la capa de Datos (DB).
   3. Firewalling Diferenciado: Un firewall perimetral (externo) con WAF y un firewall interno que solo permite la comunicación entre el servidor Web y la DB por su puerto específico.
   4. Almacenamiento SAN + HA: El uso de una SAN permite que si un nodo físico del hipervisor muere, la VM se reinicie automáticamente en otro nodo (Alta Disponibilidad).
   5. Principio de Mínimo Privilegio: Etiquetar que la conexión Web -> DB no se hace como admin, sino con un usuario con permisos limitados.
   6. Regla 3-2-1 de Backup: 3 copias, 2 soportes, 1 fuera de línea (exigencia directa del ENS).

Para que el esquema sea técnicamente impecable en un examen, debemos añadir la capa física y de conmutación. En un entorno de Alta Disponibilidad (HA), la electrónica de red debe estar duplicada para evitar el "punto único de fallo" (Single Point of Failure).
Aquí tienes el esquema actualizado incluyendo Switches, VLANs y los Enlaces Troncales:

## Conceptos de electrónica de red añadidos

   1. Switches en Stack (Redundancia L3): No ponemos un solo switch, sino dos conectados entre sí. Si uno falla, el tráfico sigue fluyendo por el otro.
   2. VLANs (Virtual LAN): Es fundamental mencionar que el aislamiento entre la Web (DMZ) y la DB (Interna) se hace mediante VLANs distintas a nivel de switch.
   3. Etiquetado 802.1Q (Trunking): Los enlaces que van desde los switches hacia los servidores virtualizados son "Trunks". Esto permite que una sola tarjeta de red física transporte varias VLANs hacia las máquinas virtuales.
   4. Balanceo de Carga / FW: El Firewall actúa como la "puerta de enlace" (Default Gateway) de las VLANs para filtrar el tráfico que salta de una a otra (Inter-VLAN routing).
   5. Red SAN Dedicada: Nota que los switches de almacenamiento son independientes de la red de datos. Esto evita que un pico de tráfico de usuarios ralentice el acceso a los discos.

Para que el esquema sea de nivel experto en un examen, el direccionamiento IP debe seguir una lógica de segmentación estricta (usualmente usando el rango privado 10.0.0.0/8 o 172.16.0.0/12).

Aquí tienes el esquema final con el mapa de red detallado:

Aquí tienes el Diagrama de Arquitectura Técnica Final. Este esquema es el más complejo y completo posible: incluye la segmentación por VLANs, el direccionamiento IP, la electrónica de red redundante, el almacenamiento SAN con RAID 10, el servidor NAS de archivos y el sistema de Backup, además de la capa de usuarios.

## Puntos clave del esquema

   1. VLAN 40 (Usuarios): Segmento aislado para equipos municipales. El acceso al portal o al NAS está filtrado por el Firewall interno para cumplir con el principio de mínimo privilegio.
   2. Servidor NAS (VLAN 20): Almacenamiento de archivos (PDFs, imágenes) accesible por el Servidor Web. Separado de la SAN (VLAN 100), que se reserva para el tráfico de bloques de baja latencia de la base de datos.
   3. RAID 10: Configuración de discos en la cabina que garantiza que, ante el fallo de un disco, la base de datos del Ayuntamiento siga operativa con rendimiento máximo.
   4. Servidor de Backup (VLAN 30): Orquesta la regla 3-2-1. Copia datos de la DB y del NAS, almacenándolos en un repositorio que puede ser el propio NAS o un soporte offline.
   5. Alta Disponibilidad: Todos los flujos críticos (Web, DB, SAN) están duplicados mediante clústeres, stacks y multipathing (MPIO).

## Por qué esta SAN cumple con el "Sobresaliente"

   1. Red de Almacenamiento Aislada: He usado el rango 192.168.100.x. Es una red que no tiene salida a Internet ni se cruza con los usuarios. Esto garantiza que nadie pueda atacar los discos directamente.
   2. MPIO (MultiPath I/O): Fíjate en las flechas cruzadas. Cada servidor tiene al menos dos caminos para llegar a los datos. Si un switch SAN o un cable se rompe, el portal del ciudadano no se cae.
   3. LUNs Compartidas: El almacenamiento no está "dentro" de los servidores, sino en la cabina. Esto permite que la VM de la Base de Datos pueda saltar del Host A al Host B en tiempo real (vMotion/Live Migration) si hay mantenimiento.
   4. Controladoras Redundantes: La cabina tiene dos IPs de gestión, cumpliendo con la Alta Disponibilidad mecánica que pide el supuesto.

Para cumplir con el ENS, el diseño debe seguir un enfoque de "Defensa en Profundidad". Aquí tienes el esquema final integrado con la electrónica de red, el direccionamiento IP y los puertos específicos:

## Esquema Detallado: Arquitectura Portal del Ciudadano (Cumplimiento ENS)

## Justificación Técnica para el Examen

   1. Capa de Acceso (Perímetro): El tráfico entra por el puerto 443 (HTTPS). El Firewall/WAF realiza la terminación SSL y aplica reglas de seguridad antes de pasar el tráfico a la DMZ.
   2. Capa de Distribución (Electrónica): Los Switches Core gestionan el Inter-VLAN Routing. Solo se permite el tráfico entre VLANs que haya sido explícitamente autorizado en el firewall.
   3. Capa de Aplicación (DMZ): El servidor web tiene una IP en la VLAN 10 (10.0.1.x). No tiene acceso directo a la red interna, solo al puerto de la DB.
   4. Capa de Datos (Interna): La base de datos reside en la VLAN 20 (10.0.2.x). Solo escucha en el puerto 3306 y solo acepta peticiones de la IP del servidor web (Mínimo Privilegio).
   5. Capa de Almacenamiento (SAN): Red aislada en la VLAN 100 (192.168.100.x). El tráfico viaja por el puerto 3260 (iSCSI). Al ser una red no enrutable, se garantiza que un ataque a la web jamás pueda comprometer la integridad de la cabina de discos.

Este esquema cubre las dimensiones de Confidencialidad (cifrado), Integridad (aislamiento de SAN) y Disponibilidad (electrónica redundante y SAN).

He seleccionado un Switch de Capa 3 (L3) para el núcleo (Core) de la red por tres razones críticas que el tribunal de un examen técnico valorará positivamente, especialmente bajo el marco del ENS:

   1. Enrutamiento Inter-VLAN de alto rendimiento: Un switch L3 realiza el enrutamiento entre las diferentes VLANs (Usuarios, DMZ, Backend, Gestión) mediante hardware especializado (ASICs). Esto es mucho más rápido que enviar todo el tráfico interno a un router o firewall externo (técnica conocida como router-on-a-stick), lo que evita cuellos de botella.
   2. Segmentación y Seguridad Lógica: Permite definir las Interfaces Virtuales de Red (SVI) que sirven como "puerta de enlace" (Gateway) para cada segmento. Al tener capacidades de Capa 3, podemos aplicar ACLs (Listas de Control de Acceso) directamente en el switch para filtrar tráfico antes incluso de que llegue al firewall perimetral.
   3. Disponibilidad y Escalabilidad: Los switches L3 permiten protocolos de redundancia como HSRP o VRRP, y facilitan el Stacking (apilamiento físico). Esto garantiza que si un switch del Core falla, el otro asume el enrutamiento de todas las VLANs de forma casi instantánea, cumpliendo con los requisitos de disponibilidad del ENS.

En resumen, el switch L3 actúa como el "cerebro" que distribuye el tráfico interno con eficiencia, dejando que el Firewall se concentre exclusivamente en la inspección profunda de seguridad y el tráfico con el exterior.

Para configurar el Stacking (apilamiento) entre los dos switches L3 del esquema y que funcionen como una sola entidad lógica (un único "cerebro"), seguiríamos estos pasos técnicos:

## 1. Conexión Física (Stack Cables)

Se conectan los switches mediante puertos dedicados de alta velocidad (StackPorts) en la parte trasera, normalmente en una topología de anillo (Ring).

* Por qué: Si un cable se rompe, el anillo se convierte en línea y la comunicación no se corta.

## 2. Configuración Lógica (Roles)

Aunque actúan como uno solo, internamente se reparten el trabajo:

* Switch Maestro (Active): Gestiona el plano de control (decide por dónde van los datos) y la configuración.
* Switch Esclavo (Standby): Sincroniza la configuración en tiempo real. Si el Maestro falla, el Esclavo asume el control en milisegundos sin que el Portal del Ciudadano pierda conexión.

## 3. Configuración de Enlaces (EtherChannel / LACP)

Para aprovechar que tenemos dos switches, conectamos los servidores y el firewall a ambos a la vez:

* Usamos LACP (802.3ad) para crear un "agregado de enlaces".
* Si el Switch A falla, el tráfico sigue fluyendo por el cable conectado al Switch B automáticamente.

## Esquema del Stack y Conectividad HA## Ventajas para el ENS

* Disponibilidad: El tiempo de recuperación ante fallos es casi cero.
* Simplicidad: Gestionas una sola IP para configurar ambos switches (una única tabla de rutas y ACLs).
* Rendimiento: Duplicas el ancho de banda disponible para los servidores.

La presencia de dos hosts ESXi es el pilar fundamental para garantizar la Alta Disponibilidad (HA) y la Continuidad del Negocio, requisitos indispensables para cumplir con el ENS en un sistema que ofrece servicios al ciudadano.
Aquí tienes los tres motivos técnicos por los que no se puede diseñar con uno solo:

   1. Evitar el Punto Único de Fallo (SPOF): Si solo tuvieras un servidor físico (host) y su placa base, fuente de alimentación o CPU fallara, todas las máquinas virtuales (Web y Base de Datos) se apagarían. Con dos hosts, si el "Host A" muere, el "Host B" detecta la caída y reinicia automáticamente las máquinas virtuales.
   2. VMware HA (High Availability): Es la tecnología que orquesta este proceso. Al estar ambos hosts conectados a la misma SAN (almacenamiento compartido), el Host B puede "ver" los archivos de las máquinas virtuales que estaban en el Host A y arrancarlas de inmediato.
   3. Mantenimiento sin Paradas (vMotion): Si necesitas actualizar el hardware o el software del Host A, puedes mover las máquinas virtuales "en caliente" (encendidas y funcionando) al Host B. El ciudadano que está usando el portal en ese momento no nota absolutamente nada.

## Esquema del Funcionamiento del Cluster HA

En resumen: El segundo host es el seguro de vida del sistema. Sin él, cualquier fallo de hardware significa la interrupción total del servicio público.
