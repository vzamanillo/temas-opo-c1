# INFRAESTRUCTURA Y PROTECCIÓN FÍSICA (CPD)

## 1. EL CENTRO DE PROCESO DE DATOS (CPD)

Es la ubicación física donde se concentran los recursos necesarios para el procesamiento de la información.

## Acondicionamiento y Equipamiento

* Ubicación: Debe ser un lugar seguro, alejado de zonas de riesgo (inundaciones, vibraciones) y sin ventanas al exterior.
* Climatización: Control estricto de temperatura (entre 18°C y 24°C) y humedad para evitar condensación o electricidad estática. Se suelen usar configuraciones de pasillos fríos y pasillos calientes para optimizar el flujo de aire.
* Falso suelo y falso techo: Permiten canalizar el cableado y el aire acondicionado de forma ordenada y protegida.
* Protección contra incendios: Sistemas de detección temprana (humo) y extinción mediante gases inertes (que no dañan los equipos electrónicos al desplazar el oxígeno).

## 2. SISTEMAS DE ALIMENTACIÓN ININTERRUMPIDA (SAI/UPS)

Garantizan la continuidad eléctrica ante fallos en el suministro de la red pública.

* SAI (UPS): Dispositivos con baterías que filtran picos de tensión y proporcionan energía inmediata si hay un apagón, permitiendo que los sistemas sigan activos o se apaguen de forma ordenada.
* Grupos Electrógenos: Generadores de combustible (diésel) que entran en funcionamiento si el corte eléctrico se prolonga más allá de la capacidad de las baterías del SAI.

## 3. SISTEMAS TOLERANTES A FALLOS

La tolerancia a fallos busca que el sistema siga operativo a pesar de la avería de alguno de sus componentes.

* RAID (Redundant Array of Independent Disks): Combinación de varios discos duros para que, si uno falla, no se pierdan los datos (ej. RAID 1 o RAID 5).
* Fuentes de alimentación redundantes: Servidores con dos o más fuentes conectadas a líneas eléctricas distintas.
* Clusterización: Grupo de servidores que trabajan como uno solo; si uno cae, otro asume su carga automáticamente.

## 4. PREVISIÓN DE CATÁSTROFES Y RESPALDO

Estrategias para enfrentar desastres totales (incendio, terremoto, inundación):

* Centro de Respaldo (Disaster Recovery Center): Un segundo CPD ubicado en una localización geográfica distinta. Puede ser:
  * Hot Site (Sede Caliente): Réplica exacta en tiempo real, lista para funcionar al instante.
  * Warm Site (Sede Templada): Equipos disponibles pero requieren cargar copias de seguridad.
  * Cold Site (Sede Fría): Solo tiene la infraestructura básica (luz, aire); el hardware debe ser instalado tras el desastre.

## 5. PROCEDIMIENTOS DE COPIAS DE SEGURIDAD (BACKUP)

Tipos de ejecución según el volumen de datos:

   1. Completa: Copia de todos los datos. Es lenta pero la recuperación es la más sencilla.
   2. Incremental: Solo copia lo que ha cambiado desde la última copia (ya sea completa o incremental). Rápida de hacer, lenta de restaurar.
   3. Diferencial: Copia lo que ha cambiado desde la última copia completa. Equilibrio entre velocidad de copia y restauración.

Gestión de Soportes: Las copias deben estar cifradas y, al menos una de ellas, almacenada fuera de las instalaciones (custodia de soportes).
