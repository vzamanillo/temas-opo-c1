# CONCEPTOS FUNDAMENTALES DE SEGURIDAD INFORMÁTICA

La seguridad informática busca proteger el triángulo de la seguridad (Confidencialidad, Integridad y Disponibilidad). Para ello, se divide en dos grandes áreas:

## 1. SEGURIDAD FÍSICA VS. SEGURIDAD LÓGICA

* Seguridad Física: Conjunto de medidas destinadas a proteger el hardware y el entorno del sistema frente a amenazas tangibles.
  * Ejemplos: Vigilantes, cámaras (CCTV), control de acceso biométrico, sistemas contra incendios, climatización y SAIs.
* Seguridad Lógica: Aplicación de barreras y procedimientos que resguardan el acceso a los datos y programas dentro del sistema.
  * Ejemplos: Contraseñas, cifrado, firewalls, antivirus, permisos de usuario y firmas digitales.

## 2. AMENAZAS Y VULNERABILIDADES

Es crucial no confundir estos dos términos:

* Vulnerabilidad: Es una debilidad o fallo en un sistema (un "agujero") que puede ser aprovechado.
  * Ejemplo: Un sistema operativo sin actualizar o una puerta de un CPD sin cerradura.
* Amenaza: Es un evento o acción externa que puede causar un daño aprovechando una vulnerabilidad.
  * Tipos:
    * Humanas: Intencionadas (hackers, sabotaje) o accidentales (errores de empleados).
    * Naturales: Inundaciones, rayos, terremotos.
    * Técnicas: Malware, fallos de hardware, picos de tensión.

## 3. EL RIESGO

El Riesgo es la probabilidad de que una amenaza se materialice aprovechando una vulnerabilidad, causando un impacto negativo.

* Fórmula conceptual: $Riesgo = Amenaza \times Vulnerabilidad$
* Gestión del riesgo: El objetivo no es eliminar el riesgo (es imposible), sino llevarlo a un nivel aceptable (Riesgo Residual) mediante la aplicación de medidas de seguridad.

## 4. MEDIDAS DE SEGURIDAD (SALVAGUARDAS)

Son las acciones o tecnologías que se implementan para mitigar el riesgo. Se clasifican según su función:

   1. Preventivas: Actúan antes de que ocurra el incidente (ej. un firewall o la formación del personal).
   2. Detectivas: Identifican el ataque cuando está ocurriendo o justo después (ej. un sistema de detección de intrusos IDS o alarmas).
   3. Correctivas: Entran en juego para reparar el daño y volver a la normalidad (ej. restaurar una copia de seguridad).
