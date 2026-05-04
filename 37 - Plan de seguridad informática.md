Este es el último bloque de contenido para tu documento, enfocado en la continuidad del negocio y la protección preventiva. Estos planes son el núcleo operativo de lo que exige el ENS.
## PLANIFICACIÓN DE LA SEGURIDAD Y CONTINUIDAD

## 1. PLAN DE SEGURIDAD INFORMÁTICA
Es el documento estratégico que define la hoja de ruta de una organización para proteger sus activos.

* Contenido: Definición de objetivos, análisis de riesgos, roles y responsabilidades, y el marco normativo (cumplimiento del ENS/RGPD).
* Fase operativa: Establece qué se quiere proteger y cuántos recursos se van a invertir.

## 2. PLAN DE CONTINGENCIAS (PC)
Es el conjunto de medidas preventivas y reactivas diseñadas para que la organización pueda seguir funcionando tras un incidente, aunque sea en "modo degradado".

* Objetivo: Minimizar la interrupción del servicio.
* Componentes:
* Plan de Respaldo: Medidas preventivas (antes del fallo).
   * Plan de Emergencia: Medidas durante el fallo para contener el daño.
   * Plan de Recuperación: Medidas después del fallo.

## 3. PLAN DE RECUPERACIÓN (Disaster Recovery Plan - DRP)
Es una parte específica del Plan de Contingencias centrada exclusivamente en la restauración de los sistemas críticos tras una catástrofe.

* Métricas Clave:
* RPO (Recovery Point Objective): Cuánta información estamos dispuestos a perder (tiempo desde la última copia de seguridad).
   * RTO (Recovery Time Objective): Cuánto tiempo podemos estar sin servicio hasta restaurarlo.
* Acciones: Restauración de backups, activación de servidores espejo o centros de respaldo (CPD alternativo).

## 4. POLÍTICAS DE SALVAGUARDA
Son las acciones técnicas y organizativas concretas que se aplican para mitigar los riesgos identificados. Se dividen en:

* Salvaguardas Técnicas:
* Copias de seguridad (Backups): Deben cumplir la regla 3-2-1 (3 copias, 2 soportes distintos, 1 fuera de línea/offline).
   * Cifrado: Protección de datos en reposo y tránsito.
   * Sistemas redundantes: Equipos duplicados para evitar puntos únicos de fallo.
* Salvaguardas Organizativas:
* Formación y concienciación: Entrenar al personal contra el phishing.
   * Control de accesos: Principio de "mínimo privilegio" (cada usuario solo accede a lo que necesita).
   * Gestión de parches: Mantener todo el software actualizado para cerrar vulnerabilidades.

Aquí tienes un ejemplo práctico de cómo se definen estas métricas en un Plan de Recuperación. Estas tablas son fundamentales para priorizar qué sistemas se arreglan primero tras un desastre.

## Ejemplo de Métricas de Continuidad (RTO y RPO)

| Servicio / Sistema | Nivel de Criticidad | RPO (Pérdida de datos máxima) | RTO (Tiempo de recuperación máximo) | Estrategia de Salvaguarda |
|---|---|---|---|---|
| Sede Electrónica / Web | Crítico | 1 hora | 4 horas | Servidores en Alta Disponibilidad (clúster). |
| Base de Datos de Usuarios | Crítico | 15 minutos | 2 horas | Replicación en tiempo real y backups incrementales. |
| Correo Electrónico | Medio | 4 horas | 24 horas | Backup diario y archivado en la nube. |
| Gestión Interna (RRHH/Nóminas) | Bajo | 24 horas | 48 - 72 horas | Backup diario nocturno (fuera de línea). |
| Archivo Histórico | Muy Bajo | 1 semana | 15 días | Almacenamiento en frío (Cold Storage). |

## Conceptos clave para recordar:

* RPO (Punto de recuperación): Responde a la pregunta: "¿Desde cuándo es nuestra copia de seguridad?". Si el RPO es de 1 hora, significa que, como máximo, perderemos los últimos 60 minutos de trabajo.
* RTO (Tiempo de recuperación): Responde a la pregunta: "¿Cuánto tardamos en volver a estar operativos?". Si el RTO es de 4 horas, el servicio debe estar funcionando de nuevo antes de que pase ese tiempo desde la caída.

## Resumen de la Regla de Oro del Backup (3-2-1):
Para asegurar estas métricas, se suele incluir en el documento la política 3-2-1:

   1. 3 copias de seguridad de cada dato.
   2. 2 soportes diferentes (ej. disco duro y cinta, o disco y nube).
   3. 1 copia fuera de la oficina (off-site) para protegernos contra incendios o robos en el edificio principal.

