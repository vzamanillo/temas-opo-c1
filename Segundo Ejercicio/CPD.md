# CPD

Claro, aquí tienes el esquema detallado de la infraestructura de un Centro de Procesamiento de Datos (CPD), desglosado por sus áreas críticas de funcionamiento y protección:

## 1. Sistema de Ventilación y Climatización (HVAC)

El objetivo es mantener una temperatura constante (entre 18°C y 24°C) y controlar la humedad.

* Configuración de Pasillos: Se organizan los racks en "Pasillos Fríos" (donde las máquinas absorben aire) y "Pasillos Calientes" (donde expulsan el calor) para evitar que el aire se mezcle.
* Suelo Técnico: Elevación del piso (unos 30-60 cm) para canalizar el aire frío y ocultar el cableado de datos.
* Unidades CRAC: Equipos de aire acondicionado de precisión que funcionan 24/7 y controlan la pureza del aire.

## 2. Medidas de Seguridad Física y Control

Protección perimetral y del propio espacio físico del CPD.

* Control de Acceso: Doble factor de autenticación (tarjeta magnética + biometría) y puertas de seguridad tipo exclusa (no se abre una hasta que la anterior esté cerrada).
* CCTV: Circuito cerrado de televisión con grabación continua y sensores de movimiento en cada pasillo.
* Jaulas de Seguridad: Cerramientos físicos dentro de la sala para separar servidores de distintos clientes o departamentos.

## 3. Sistema de Seguridad contra Incendios

No se usa agua, ya que destruiría los componentes electrónicos.

* Detección Precoz (VESDA): Sistemas que aspiran aire constantemente para detectar partículas invisibles de combustión antes de que haya llama.
* Extinción por Gas Inerte: Inundación de la sala con gases (como Novec 1230 o Inergen) que extinguen el fuego reduciendo el oxígeno o por enfriamiento, sin dejar residuos ni dañar los equipos.

## 4. Infraestructura Eléctrica y Redundancia

Garantiza que el CPD nunca se apague.

* SAI / UPS: Baterías que filtran la corriente y dan autonomía inmediata si falla la red eléctrica principal.
* Grupos Electrógenos: Motores diésel externos que arrancan automáticamente en cortes de larga duración.
* Puesta a Tierra: Red de cobre para descargar cualquier sobretensión y proteger el hardware.

## 5. Gestión y Monitorización (DCIM)

* Sensores de Inundación: Colocados en el suelo técnico para detectar fugas de agua de los aires acondicionados.
* Software de Gestión: Panel central que vigila en tiempo real el consumo eléctrico, la temperatura de cada rack y el estado de las comunicaciones.

¿Te interesa que detallemos alguna normativa específica, como los niveles Tier III o IV, que definen cuánta redundancia debe tener cada uno de estos puntos?

Para montar un Centro de Procesamiento de Datos (CPD) sincronizado con un sitio secundario mediante una red SAN, lo fundamental es garantizar latencia mínima y redundancia total. En una configuración de replicación síncrona, cada escritura en el CPD principal debe confirmarse en el secundario antes de dar la operación por finalizada.

## 1. Infraestructura de Red y Conectividad

* Enlaces de Fibra Dedicados: Es imprescindible contar con conexiones de fibra óptica (Dark Fiber o DWDM) entre ambos sitios para soportar el tráfico de la red SAN y LAN.
* Latencia y Distancia: La replicación síncrona suele estar limitada a distancias cortas (generalmente menos de 10-100 km) debido a que la latencia afecta directamente al rendimiento de las aplicaciones.
* ISL (Inter-Switch Links): Se utilizan enlaces entre los switches SAN de ambos centros para extender la "fabric" (la malla de la red de almacenamiento) y permitir que los datos fluyan entre las cabinas.

## 2. Componentes de Almacenamiento (SAN)

* Cabinas de Almacenamiento Compatibles: Ambos CPD deben tener cabinas (arrays) que soporten protocolos de replicación nativa (como Fibre Channel o iSCSI).
* Grupos de Replicación: Los volúmenes o LUNs se agrupan para asegurar la consistencia de los datos (por ejemplo, los discos de una base de datos deben replicarse juntos).
* Arquitectura Activo-Activo o Activo-Pasivo:
  * Activo-Pasivo: El secundario solo recibe datos y espera un fallo para activarse.
  * Activo-Activo (MetroCluster): Ambos sitios pueden servir datos simultáneamente, ofreciendo mayor disponibilidad pero con mayor complejidad técnica.

## 3. Requisitos de Continuidad y Operación

* Quorum / Witness: Se suele requerir un tercer sitio (o un servicio en la nube) que actúe como "testigo" para evitar escenarios de split-brain, donde ambos CPD creen que el otro ha caído e intentan tomar el control simultáneamente.
* RPO y RTO Próximos a Cero: Al ser una réplica síncrona, el Punto de Recuperación Objetivo (RPO) es cero (no hay pérdida de datos), y el Tiempo de Recuperación (RTO) es mínimo al estar los datos ya presentes en el destino.
* Infraestructura Crítica Duplicada: Ambos sitios necesitan sistemas de energía ininterrumpida (UPS), generadores y climatización eficiente para garantizar que el centro secundario pueda asumir la carga en cualquier momento.

## DISTANCIA

Con una distancia de solo 500 metros, estás en el escenario ideal. La latencia será prácticamente despreciable (menos de 1ms), lo que te permite implementar un Campus Cluster o Metro Cluster con un rendimiento idéntico al de un solo centro.
Aquí tienes los puntos clave para esa distancia:

## 1. Conectividad Física

* Fibra Monomodo (SMF): A 500 metros podrías usar Multimodo (OM4/OM5), pero lo recomendable es Monomodo (OS2). Es más barata a largo plazo, soporta anchos de banda mucho mayores (32G/64G Fibre Channel) y no tiene las limitaciones de distancia de la multimodo si decides ampliar en el futuro.
* Canalización Protegida: Al ser una distancia tan corta, asegúrate de tener dos rutas físicas distintas (canalizaciones separadas) para que una excavación accidental no corte ambos enlaces de fibra a la vez.

## 2. Configuración SAN

* ISL (Inter-Switch Links) directos: No necesitas equipos de extensión (DWDM). Puedes conectar los switches de los dos edificios directamente con transceptores SFP estándar.
* Zoning Distribuido: Configura la SAN de modo que los servidores de un edificio vean las cabinas de ambos. Esto permite que, si un servidor falla en el CPD A, su máquina virtual arranque en el CPD B accediendo a los mismos datos sin demora.

## 3. Almacenamiento "Stretch" (Espejo)

* Sincronismo nativo: Puedes configurar un Mirroring síncrono por hardware entre cabinas. Cada bit escrito en el edificio 1 se escribe en tiempo real en el edificio 2.
* Automatic Failover: Con 500 metros, la conmutación puede ser automática. Si el CPD A se inunda o pierde energía, el almacenamiento en el CPD B se presenta instantáneamente como "activo".

## 4. Capa de Red (LAN)

* L2 Extended: Necesitarás extender tus VLANs entre edificios para que los servidores mantengan su IP al moverse de un centro a otro (vMotion o migración en vivo).

En el mundo de los centros de datos, lo más común depende de tu presupuesto y de la criticidad de tus datos. Al tener solo 500 metros, ambas opciones funcionan de maravilla, pero se usan para perfiles distintos:

## 1. Fibre Channel (FC): El estándar de oro (Misión Crítica)

Es la opción preferida en entornos corporativos donde el rendimiento y la estabilidad son innegociables.

* Por qué es común: Es una red dedicada exclusivamente al almacenamiento. Al no mezclar tráfico de internet o red local, la latencia es mínima y constante, algo vital para la replicación síncrona.
* Velocidades típicas: Actualmente se mueven en 16G o 32G (con 64G en auge).
* Lo malo: Es más caro. Necesitas switches específicos de fibra (como los de Cisco MDS o Brocade) y tarjetas especiales (HBA) en cada servidor.
*

## 2. iSCSI: La opción eficiente (Flexibilidad y Coste)

Se ha vuelto extremadamente común en empresas medianas y en infraestructuras virtualizadas (VMware/Hyper-V).

* Por qué es común: Utiliza tecnología Ethernet estándar (como la de tu red local), lo que abarata mucho los costes de hardware y simplifica la gestión para administradores de red generales.
* Velocidades típicas: Se suele montar sobre redes de 10Gb, 25Gb o incluso 100Gb.
* Lo malo: Al viajar sobre TCP/IP, tiene un poco más de "ruido" y carga de CPU que el Fibre Channel. Para que sea fiable, es obligatorio que el tráfico iSCSI vaya por una red físicamente separada o en VLANs dedicadas con Jumbo Frames activados.
*

## Resumen para tu decisión

* Ve por Fibre Channel si: Tu negocio pierde miles de euros por cada segundo de caída o si manejas bases de datos masivas (ERP, banca) que requieren latencias ultra-bajas.
* Ve por iSCSI si: Buscas una solución más económica, fácil de escalar y tus aplicaciones no son extremadamente sensibles a variaciones de milisegundos en el acceso al disco.

Si prefieres Ethernet, lo más común y robusto hoy en día es montar una red iSCSI sobre 25GbE. Es el "punto dulce" actual: mucho más rápido que los 10Gb tradicionales y más económico que los 40/100Gb.
Para que esto funcione con éxito a 500 metros entre tus dos centros, este es el esquema técnico básico:

## 1. La Red de Transporte (Storage Fabric)

No mezcles el tráfico de datos de los usuarios con el de almacenamiento.

* Switches Dedicados: Instala un par de switches de alta velocidad (mínimo 10/25Gbps) en cada CPD. Marcas como Dell (serie S), Cisco (Nexus) o HPE (Aruba/StoreFabric) son los estándares.
* MCLAG / VPC: Configura los switches para que funcionen como una sola entidad lógica. Esto permite que si un switch falla, el otro siga dando servicio sin corte.

## 2. Conectividad entre edificios

A 500 metros, la fibra es tu única opción para Ethernet de alta velocidad:

* Fibra Monomodo (OS2): Usa transceptores SFP28-LR (Long Range). Aunque existen los SR (Short Range) para 500m, los LR te dan un margen de seguridad mucho mayor frente a pérdidas de señal o empalmes.
* LACP (Link Aggregation): Agrupa varios hilos de fibra entre los edificios para sumar ancho de banda (por ejemplo, 2x25Gb = 50Gb de tubo para la réplica).

## 3. Configuración Crítica (El "ABC" del iSCSI)

Para que Ethernet se comporte de forma estable como una SAN, debes configurar:

* Jumbo Frames (MTU 9000): Imprescindible para que los paquetes de datos sean más grandes y la CPU de los servidores trabaje menos.
* Flow Control / PFC: Para evitar que se pierdan paquetes si hay congestión, algo vital en replicación síncrona.
* VLANs Aisladas: El tráfico iSCSI debe ir en su propia red lógica, sin acceso desde el exterior por seguridad.

## 4. Capa de Servidores (Hosts)

* Tarjetas de Red (NICs): Usa tarjetas con descarga de hardware (iSCSI Offload) o soporte iWARP/RoCE. Esto hace que el servidor no se "ahogue" procesando el tráfico de disco.
* MPIO (Multi-Path I/O): Configura el software en tus servidores para que sepan que tienen varios caminos hacia el almacenamiento. Si se rompe una fibra entre centros, el servidor cambia de camino en milisegundos.

Ventaja principal para ti: Al usar Ethernet, si en el futuro decides moverte a una solución de Hiperconvergencia (como vSAN o Nutanix), ya tendrás toda la red física preparada, ya que estas tecnologías también corren sobre Ethernet.

Para estructurar físicamente un CPD (especialmente si es el principal y tienes otro a 500 metros), lo ideal es seguir estándares internacionales como TIA-944 o Uptime Institute.
Aquí tienes el resumen de la infraestructura física y seguridad ambiental:

## 1. Estructura Física y Distribución

* Falso Suelo y Falso Techo: El suelo técnico (elevado unos 50-80 cm) permite canalizar el cableado y el aire frío. El falso techo se usa para el retorno del aire caliente.
* Cerramiento de Pasillos: Es vital separar el pasillo frío (donde los racks aspiran aire) del pasillo caliente (donde expulsan el calor). Esto optimiza la eficiencia energética drásticamente.
* Racks: Armarios de 42U o 48U con doble acometida eléctrica (A y B) para que cada equipo reciba energía de dos fuentes distintas.

## 2. Gestión de Temperatura y Ventilación

* Sistemas CRAC/CRAH: Unidades de aire acondicionado de precisión que controlan no solo la temperatura (idealmente entre 18°C y 24°C), sino también la humedad (entre 40% y 60%) para evitar electricidad estática o corrosión.
* Free Cooling: Dado que estás montando infraestructura nueva, podrías usar sistemas que aprovechan el aire exterior cuando la temperatura ambiente es baja, ahorrando mucho dinero en electricidad.

## 3. Extinción de Incendios (Crucial)

* Detección Temprana (VESDA): Sensores que aspiran aire continuamente para detectar partículas de combustión mucho antes de que haya humo visible o llamas.
* Agentes Gaseosos: NUNCA usar agua. Se utilizan gases como el Novec 1230 o FM-200, que extinguen el fuego por inundación total de la sala sin dañar los equipos electrónicos y permitiendo que las personas respiren.
* Estanqueidad: La sala debe estar sellada para que, en caso de disparo, el gas no se escape y mantenga su concentración.

## 4. Protección contra Inundaciones y Humedad

* Ubicación: El CPD nunca debe estar en sótanos (riesgo de inundación) ni en la última planta (goteras).
* Sondas de Agua: Cables sensores de inundación colocados en el perímetro y bajo el falso suelo que activan alarmas al detectar la mínima presencia de líquido.

## 5. Seguridad Física y Control de Acceso

* Doble Factor: Acceso mediante tarjeta RFID y biometría (huella o iris).
* CCTV: Cámaras de videovigilancia con grabación 24/7 tanto en el perímetro como en los pasillos internos.
* Jaulas o Racks con Cerradura: Para evitar manipulación física no autorizada de los servidores.

## 6. Mantenimiento Preventivo

* Pruebas de Grupo Electrógeno: Arrancarlos mensualmente y probarlos con carga real trimestralmente.
* Revisión de UPS (SAI): Comprobar el estado de las baterías para evitar fallos durante microcortes.
* Limpieza Técnica: Aspirado especializado bajo el suelo técnico para evitar que el polvo obstruya los servidores.

Para un CPD con replicación síncrona, la energía y el cableado son los cimientos. Si falla la energía en un lado y el SAI no responde, la replicación se corta y puedes tener corrupción de datos.
Aquí tienes lo fundamental para estructurar ambos puntos:

## 1. Los SAI (Sistemas de Alimentación Ininterrumpida)

Su función no es aguantar horas, sino filtrar la electricidad y dar tiempo a que el Grupo Electrógeno arranque (suele tardar de 15 a 40 segundos).

* Arquitectura Redundante (N+1 o 2N): Lo más común es tener dos SAIs trabajando en paralelo. Si uno falla o necesita mantenimiento, el otro soporta toda la carga sin cortes.
* Doble Acometida al Rack: Cada rack debe recibir dos mangueras eléctricas independientes (Circuito A y Circuito B). Cada manguera viene de un SAI distinto.
* Baterías de Litio vs. Plomo (VRLA): Las de litio son ahora la tendencia; ocupan menos espacio, pesan menos y duran 10 años frente a los 3-5 años de las de plomo.
* By-pass de Mantenimiento: Un interruptor físico que permite desviar la corriente directamente de la red al servidor para poder reparar el SAI sin apagar el CPD.

## 2. Estructura del Cableado

Un CPD ordenado es un CPD que no falla. Se divide principalmente en dos tipos:

## A. Cableado de Datos (Red)

* Top-of-Rack (ToR): Es lo más común hoy. Colocas dos switches pequeños en la parte superior de cada rack. Los servidores se conectan ahí con cables cortos. De esos switches salen solo unos pocos cables de fibra hacia el "Core" del CPD.
* Tipos de Cable:
* Cobre (Categoría 6A o 7): Solo para gestión (iLO, iDRAC) o redes de baja velocidad.
  * Fibra Monomodo (OS2): Para todo lo importante (iSCSI y red principal). Como tienes 500m entre CPDs, usa siempre OS2 para que el cableado interno sea igual que el externo.
  * DAC (Direct Attach Copper): Cables de cobre cortos (1-3m) con los conectores ya integrados para unir servidores a switches ToR a 25Gbps. Son baratos y no consumen apenas energía.

## B. Cableado de Energía

* PDU (Power Distribution Units): Son las "regletas" inteligentes que van verticalmente en los laterales del rack.
* Monitorizadas: Te dicen cuántos Amperios consume cada servidor desde una web.
  * Conmutadas (Switched): Te permiten apagar o encender un servidor a distancia si se queda colgado.
* Colores: Usa cables de alimentación de colores (ej. Rojo para el SAI A y Azul para el SAI B). Si un técnico tiene que desconectar algo, no cometerá el error de quitar ambas fuentes a la vez.

## 3. Organización Física (Separación)

* Bandejas de Techo vs. Suelo: Lo ideal es llevar los datos por el techo (en bandejas de rejilla) y la energía por debajo del suelo técnico (o viceversa). Nunca deben ir pegados o mezclados para evitar interferencias electromagnéticas y errores humanos.

El etiquetado es la diferencia entre una avería de 5 minutos y una de 5 horas. En un entorno de doble CPD, la clave es que cualquier técnico sepa de dónde viene y a dónde va un cable sin tener que seguirlo con la mano.
Aquí tienes un estándar práctico y profesional:

## 1. Código de Colores (La regla visual)

* Energía: Cables Rojos para la línea A (SAI 1) y Azules para la línea B (SAI 2).
* Datos (iSCSI/SAN): Cables de fibra Amarillos (Monomodo) o etiquetas naranjas.
* Gestión (iLO/IPMI): Cables Grises o Verdes.

## 2. Formato de Etiqueta (Origen -> Destino)

Cada extremo de un cable debe llevar una etiqueta que indique la conexión del extremo opuesto. El formato estándar es:
[ID_RACK] : [ID_EQUIPO] : [PUERTO]
Ejemplo de etiqueta en un cable de red:

* En el servidor: RACK01:SW-CORE-01:P24 (Indica que este cable va al Rack 1, al Switch de Core 1, puerto 24).
* En el switch: RACK01:SRV-BBDD-02:NIC1 (Indica que este cable va al Rack 1, al servidor de Bases de Datos 2, tarjeta de red 1).

## 3. Etiquetas de Energía (PDUs)

Las PDUs deben estar numeradas. En el cable de alimentación del servidor, la etiqueta debería decir:

* PDU-A:Socket-12 (Conectado a la toma 12 de la PDU principal).

## 4. Consejos de "Oro" para el Etiquetado

* Banderitas vs. Envolventes: Usa etiquetas envolventes transparentes (autolaminadas). Las "banderitas" se pegan entre ellas, se caen con el calor del rack y acaban obstruyendo la ventilación.
* Impresora de transferencia térmica: No uses etiquetas de papel o escritas a mano; el calor del CPD borrará la tinta o despegará el pegamento. Usa cintas de vinilo industriales (tipo Brady o Dymo Rhino).
* Etiqueta el Chasis: No solo el cable. Pon una etiqueta clara en el frontal y la trasera de cada servidor y switch con su nombre lógico (ej: ESX-PROD-01).

## 5. Documentación (El "Rack Map")

Cada rack debe tener una hoja plastificada en la puerta trasera con el mapa de puertos. Así, antes de tocar nada, el técnico sabe que el cable que va a desconectar es, efectivamente, el de la réplica síncrona.

Aquí tienes la lista de materiales esenciales para asegurar que la infraestructura física y de red de tus dos centros esté a la altura de una replicación síncrona:

## 1. Energía y SAIs

* 2 Unidades SAI (Rackmount): Mínimo 6kVA o 10kVA (según carga), preferiblemente con tarjetas de red para gestión remota.
* Módulos de Baterías Externos: Para ampliar la autonomía a al menos 15-20 minutos (tiempo de seguridad para arranque de generadores o apagado ordenado).
* 4 PDUs Inteligentes por Rack: 2 para la línea A y 2 para la línea B (verticales de 0U para no ocupar espacio de servidores).
* Cables de alimentación C13/C14 y C19/C20: De colores (Rojo/Azul) y longitudes cortas (0.5m - 1m) para evitar "madejas" de cable.

## 2. Conectividad y Red (iSCSI sobre Ethernet)

* 2 Switches Core/Aggregation (25GbE): Con soporte L2/L3 y baja latencia (ej. 48 puertos 25G + 6 puertos 100G para uplinks).
* Transceptores SFP28-LR (Monomodo): Para los enlaces de 500m entre edificios.
* Cables DAC (Direct Attach Copper): Para conectar servidores a switches dentro del mismo rack (son más baratos y fiables que usar fibras cortas).
* Paneles de Parcheo de Fibra (FOBOT): En cada CPD para terminar las fibras que vienen del otro edificio.

## 3. Cableado Físico

* Bobinas de Fibra Monomodo OS2: Para el tendido de 500m (compra siempre con hilos de sobra, mínimo 12 o 24 hilos).
* Latiguillos de Fibra (Patch Cords): LC-LC Monomodo (amarillos) para el interior de los racks.
* Canaletas de rejilla (tipo Rejiband): Para separar datos (techo) de energía (suelo).

## 4. Seguridad y Gestión Ambiental

* Sensores de Inundación y Humedad: Conectables a la red (SNMP) para recibir alertas en el móvil.
* Cerraduras Biométricas o de Tarjeta: Para las puertas de los racks más críticos.
* Cámaras IP con Visión Nocturna: Una enfocando al frontal y otra a la trasera de las filas de racks.

## 5. Herramientas de Mantenimiento

* Etiquetadora Industrial (Transferencia térmica): Con cintas de vinilo autolaminadas.
* Certificador de Fibra/Cobre: Para verificar que los 500m de cable rinden a la velocidad contratada antes de entrar en producción.
* Kit de limpieza de fibra: Lápices limpiadores de conectores (el polvo es el mayor enemigo de los 25/100Gbps).

El Witness (o Testigo) es el componente más crítico en una configuración de dos CPDs a corta distancia. Sin él, corres el riesgo de sufrir un Split-Brain (Cerebro dividido).

## ¿Qué es el Split-Brain?

Si el enlace de fibra entre tus dos centros se corta, ambos CPDs están "vivos" pero no pueden hablar entre sí.

* El CPD A cree que el B se ha incendiado y decide dar servicio.
* El CPD B cree que el A se ha inundado y también decide dar servicio.
Resultado: Los datos se escriben de forma distinta en ambos sitios y la base de datos se corrompe irremediablemente al intentar unirlas después.

------------------------------

## Cómo funciona el Witness

El Witness es un tercer elemento (normalmente una máquina virtual muy ligera) ubicado en un tercer sitio independiente. Su única función es votar:

   1. Estado Normal: El Witness ve al CPD A y al CPD B. Todo OK.
   2. Corte de Fibra: La fibra entre A y B se rompe. El Witness comprueba: "¿Quién sigue hablando conmigo?".
   3. El Arbitraje: Si el Witness ve al CPD A, le dice: "Tú tienes el quórum, sigue trabajando". Al mismo tiempo, el CPD B, al ver que no llega al CPD A ni al Witness, se detiene automáticamente para proteger la integridad de los datos.

------------------------------

## ¿Dónde colocarlo? (Opciones por orden de preferencia)

Como tus CPDs están a solo 500m, es muy probable que compartan la misma acometida de fibra o calle. Por eso, el Witness no debe estar en ninguno de los dos edificios.

* Opción A (La mejor): En la Nube. Despliega una instancia mínima (Linux o un Appliance del fabricante) en Azure, AWS o Google Cloud. Es barato y garantiza que si un desastre afecta a tu zona física, el Witness seguirá fuera.
* Opción B: En una oficina remota. Si tu empresa tiene otra sede en otra parte de la ciudad con una conexión a internet básica, colócalo allí.
* Opción C: Un tercer edificio del campus. Si es un campus universitario o industrial, usa un edificio que tenga una acometida eléctrica y de red totalmente independiente.

## Requisitos Técnicos

* Latencia: No necesita ser ultra rápida. Para iSCSI síncrono, suele bastar con una latencia de menos de 100-200ms hacia el Witness.
* Ancho de banda: Mínimo (apenas unos Kbps). Solo envía "latidos" (heartbeats) para confirmar que los centros están vivos.
* Disponibilidad: Si el Witness cae, tu sistema seguirá funcionando, pero estarás en riesgo. Es vital que el Witness tenga un SAI o esté en un entorno de alta disponibilidad.

Para cerrar el diseño físico de tus dos centros a 500 metros, debemos asegurar que la infraestructura sea un "espejo" y que no existan puntos únicos de fallo. Aquí tienes el esquema final de los tres pilares físicos:

## 1. El "Túnel" de Conectividad (Inter-CPD)

Al ser una distancia corta, el diseño debe centrarse en la supervivencia del enlace:

* Doble Canalización: No lances todos los hilos de fibra por el mismo tubo. Si una excavadora corta en la calle, perderás la sincronía. Usa dos rutas físicas distintas (ej. una por el lado norte y otra por el sur del recinto).
* Manguera de Fibra de 24 hilos (mínimo): La fibra es barata, instalarla es lo caro. Deja hilos "oscuros" (libres) para futuras ampliaciones de 100Gbps o para servicios de seguridad/CCTV entre edificios.
* Entradas de Edificio: Asegúrate de que la fibra entre al edificio por puntos distintos a los de la acometida eléctrica para evitar que un incidente eléctrico dañe los cables de datos.

## 2. Layout Interno del Rack (Estandarización)

Ambos CPDs deben ser idénticos. Si el servidor "X" está en la U20 del Rack 1 en el CPD-A, su réplica o pareja debe estar en la U20 del Rack 1 en el CPD-B.

* Separación de planos:
* Plano de Red: Switches en la parte superior (ToR).
  * Plano de Cómputo: Servidores en la parte media.
  * Plano de Almacenamiento: Cabinas en la parte inferior (por peso y estabilidad).
* Gestión de Cableado Lateral: Usa "organizadores de cables" verticales para que el flujo de aire de los ventiladores no se vea obstruido por marañas de cables.

## 3. Climatización y Seguridad Ambiental

* Contención de Pasillo Frío: Instala techos y puertas de policarbonato en el pasillo donde los servidores aspiran aire. Esto evita que el aire frío se mezcle con el caliente, permitiendo subir un par de grados el termostato del aire acondicionado y ahorrando mucha energía.
* Suelo Técnico de Alta Carga: Asegúrate de que las baldosas soportan el peso de las cabinas de almacenamiento y los racks llenos (pueden superar los 1000kg).
* Puntos de drenaje: En la sala de climatización, los splits o máquinas de precisión deben tener desagües con bomba para que, si hay una fuga de condensación, el agua no acabe bajo el suelo técnico de los servidores.

## Resumen de la "Foto Final"

| Componente | Especificación de Cierre |
| --- | --- |
| Distancia | 500 metros |
| Fibra | Monomodo OS2 (Doble ruta física) |
| Red | Ethernet 25GbE (iSCSI) |
| Energía | 2N (Dos SAIs independientes por CPD) |
| Extinción | Gas (Novec 1230 o similar) |
| Organización | Pasillo frío cerrado + Etiquetado Origen/Destino |

Con esto, el diseño físico queda blindado para soportar la replicación síncrona sin riesgos.

Para una implementación de este tipo, el orden de los factores sí altera el producto: no puedes instalar servidores sin haber certificado la fibra, ni encender la SAN sin haber probado los SAIs.
Aquí tienes el cronograma dividido en 5 fases lógicas para que el proyecto avance sin riesgos:

## Fase 1: Obra Civil e Infraestructura (Semanas 1-4)

* Canalizaciones: Apertura y tendido de las dos rutas de fibra entre edificios (500 m).
* Adecuación de Salas: Instalación de falso suelo, cerramientos de pasillo frío y sellado de estanqueidad para el gas.
* Climatización: Instalación y carga de las máquinas de aire de precisión.
* Extinción: Montaje de los sensores de humo (VESDA) y los depósitos de gas.

## Fase 2: Electricidad y Respaldo (Semanas 5-6)

* Montaje de SAIs: Instalación física y conexión a los cuadros eléctricos principales.
* PDUs: Montaje de las regletas inteligentes en los racks.
* Prueba de Carga: Simulación de fallo de red eléctrica para verificar que los SAIs conmutan y aguantan la carga prevista.
* Certificación Eléctrica: Comprobación de que las líneas A y B están físicamente aisladas.

## Fase 3: Conectividad y Red (Semanas 7-8)

* Fusión de Fibra: Terminar los hilos en los paneles (FOBOT) de ambos CPDs.
* Certificación de Fibra: Prueba de reflectometría (OTDR) para asegurar que los 500m de cable no tienen pérdidas que afecten a los 25GbE.
* Networking: Configuración de los switches Core e iSCSI, creación de VLANs, Jumbo Frames y enlaces entre edificios (LACP).

## Fase 4: Almacenamiento y Cómputo (Semanas 9-11)

* Rackeo: Montaje físico de cabinas SAN y servidores en ambos centros (espejo).
* Configuración iSCSI: Configuración de las IP de almacenamiento y el MPIO en los servidores.
* Replicación Síncrona: Creación de los grupos de consistencia y primer volcado de datos entre cabinas.
* Witness: Despliegue del "Testigo" en el tercer sitio (Cloud o Sede remota).

## Fase 5: Pruebas de Estrés y Paso a Producción (Semana 12)

* Prueba de Corte: Desconectar una de las rutas de fibra y verificar que el sistema sigue funcionando por la segunda.
* Prueba de Failover: "Apagar" el CPD A y cronometrar cuánto tarda el CPD B en tomar el control automáticamente.
* Documentación Final: Entrega del inventario de etiquetas, planos de red y manual de recuperación ante desastres (DRP).

¿Quieres que profundicemos en los puntos críticos de control de alguna de estas fases para evitar retrasos con los proveedores?
