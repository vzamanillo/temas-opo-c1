El Esquema Nacional de Seguridad (ENS), regulado por el Real Decreto 311/2022, establece la política de seguridad para la protección de la información en el sector público español y sus proveedores tecnológicos. [1, 2, 3] 
Aquí tienes el resumen estructurado para tu documento:
------------------------------
## EL ESQUEMA NACIONAL DE SEGURIDAD (ENS)

## 1. ÁMBITO DE APLICACIÓN
El ENS se aplica a:

* Sector Público: Administración General del Estado, Comunidades Autónomas, Entidades Locales y organismos públicos vinculados.
* Sector Privado: Empresas que presten servicios o soluciones a las Administraciones Públicas para el manejo de información ciudadana o administrativa.
* Sistemas de Información: Todos los sistemas que procesan información en el ejercicio de competencias públicas. [4, 5, 6, 7] 

## 2. PRINCIPIOS BÁSICOS
Son las pautas que deben regir toda decisión en materia de seguridad: [8] 

   1. Seguridad como proceso integral: La seguridad debe abarcar elementos organizativos, técnicos, humanos y físicos.
   2. Gestión basada en riesgos: Las medidas se deciden tras un análisis previo.
   3. Prevención, detección, respuesta y recuperación: El sistema debe estar preparado para evitar ataques, pero también para reaccionar y restaurarse.
   4. Líneas de defensa: Estrategia de defensa en profundidad con múltiples capas de seguridad.
   5. Vigilancia continua: Evaluación periódica del estado de seguridad para detectar vulnerabilidades.
   6. Reevaluación periódica: Actualización de las medidas según cambien las amenazas. [9, 10, 11, 12, 13] 

## 3. ANÁLISIS DE RIESGOS (AR)
Es el paso previo y obligatorio. Consiste en:

* Identificar los activos (datos, hardware, personas).
* Evaluar las amenazas y las vulnerabilidades.
* Calcular el impacto y la probabilidad de que ocurra un incidente.
* El objetivo es mantener el riesgo bajo un nivel aceptable (riesgo residual). [14, 15, 16, 17, 18] 

## 4. CATEGORIZACIÓN DE LOS SISTEMAS
Los sistemas se clasifican según el impacto que tendría un incidente en la seguridad de la información (dimensiones: Confidencialidad, Integridad, Disponibilidad, Autenticidad y Trazabilidad). [19, 20, 21, 22, 23] 

* Categoría Básica: Impacto bajo.
* Categoría Media: Impacto moderado.
* Categoría Alta: Impacto grave.
* Nota: La categoría del sistema la determina la dimensión que haya obtenido el nivel más alto. [24, 25, 26, 27, 28] 

## 5. SELECCIÓN DE LAS MEDIDAS DE SEGURIDAD
Una vez categorizado el sistema, se aplican las medidas recogidas en el Anexo II del ENS, divididas en tres grupos: [29, 30] 

   1. Marco Organizativo [G]: Estrategia, política de seguridad y roles.
   2. Marco Operacional [op]: Planificación, control de accesos, explotación y protección de servicios.
   3. Medidas de Protección [mp]: Seguridad física, de las comunicaciones, del soporte de información y de las aplicaciones. [31, 32, 33, 34, 35] 

## 6. RESPUESTA A INCIDENTES DE SEGURIDAD
El ENS obliga a:

* Notificación: Los incidentes significativos deben notificarse al CCN-CERT (Centro Criptológico Nacional).
* Gestión: Disponer de procedimientos para contener el incidente, mitigar daños y erradicar la causa.
* Recuperación: Garantizar la continuidad del servicio y restaurar la información afectada.
* Lecciones aprendidas: Analizar el incidente para mejorar las medidas preventivas. [36, 37, 38, 39, 40]

## Comparativa de Categorías y Requisitos (ENS)

| Característica | Categoría BÁSICA | Categoría MEDIA | Categoría ALTA |
|---|---|---|---|
| Impacto estimado | Bajo (perjuicio limitado) | Moderado (perjuicio grave) | Muy grave (daño catastrófico) |
| Análisis de Riesgos | Puede ser simplificado. | Formal y estructurado. | Formal, detallado y revisado periódicamente. |
| Autoevaluación / Auditoría | Autoevaluación anual por el responsable. | Auditoría externa obligatoria cada 2 años. | Auditoría externa obligatoria cada 2 años. |
| Control de Accesos | Identificación y autenticación básica. | Doble factor de autenticación (2FA) recomendado. | Doble factor (2FA) obligatorio para administración. |
| Cifrado de datos | Opcional según el riesgo. | Obligatorio para datos en tránsito y soportes. | Obligatorio en tránsito, soportes y datos en reposo. |
| Registro de Actividad (Logs) | Registro de eventos críticos. | Registro detallado y protección de logs. | Registro exhaustivo, protección y correlación de eventos. |
| Continuidad | Copias de seguridad básicas. | Plan de continuidad y recuperación probado. | Centro de respaldo o alta disponibilidad garantizada. |
| Notificación al CCN-CERT | Solo incidentes muy críticos. | Obligatoria para incidentes significativos. | Obligatoria e inmediata para incidentes significativos. |

## Puntos clave para tu documento:

   1. Principio de proporcionalidad: No se aplican las mismas medidas a una web informativa (Básica) que a una base de datos de salud (Alta).
   2. Mecanismo de Selección: Para la categoría Básica, las medidas son de aplicación mínima. Para Media y Alta, se deben cumplir los refuerzos específicos detallados en el Anexo II del Real Decreto 311/2022.
   3. Certificación: Solo los sistemas de categoría Media y Alta obtienen una "Certificación de Conformidad" tras la auditoría; los de categoría Básica obtienen una "Declaración de Conformidad".

## DIMENSIONES DE SEGURIDAD (DICAT)
Para determinar la categoría de un sistema (Básica, Media o Alta), el ENS evalúa el impacto que tendría un incidente sobre estas cinco dimensiones fundamentales:

   1. Disponibilidad [D]: Garantiza que los usuarios autorizados tengan acceso a la información y a los servicios cuando lo requieran. (Ejemplo: que la sede electrónica no esté "caída").
   2. Integridad [I]: Garantiza la exactitud y completitud de la información y de sus métodos de procesamiento. Asegura que los datos no han sido modificados de forma no autorizada.
   3. Confidencialidad [C]: Garantiza que la información solo sea accesible por personas, entidades o procesos autorizados. Evita filtraciones de datos sensibles.
   4. Autenticidad [A]: Garantiza la identidad de quien genera o recibe la información. Asegura que quien dice ser el emisor es realmente quien es.
   5. Trazabilidad [T]: Garantiza que se pueda conocer en cualquier momento quién ha accedido a qué información y qué acciones ha realizado (deja un "rastro" o historial).

Nota para tu estudio/documento: La categoría final del sistema será la del nivel más alto alcanzado en cualquiera de estas dimensiones. Por ejemplo, si un sistema es de nivel Bajo en Confidencialidad pero Medio en Disponibilidad, el sistema completo se clasifica como Categoría Media.
¿Quieres que pasemos a otro tema del temario o necesitas un resumen de los roles responsables en el ENS (Responsable de Información, del Servicio, de Seguridad, etc.)?

[1] [https://www.audidat.com](https://www.audidat.com/blog/esquema-nacional-de-seguridad/auditoria-esquema-nacional-de-seguridad/#:~:text=Para%20entender%20la%20auditor%C3%ADa%2C%20primero%20hay%20que,de%20las%20Administraciones%20P%C3%BAblicas%20y%20sus%20proveedores.)
[2] [https://blog.grupocfi.es](https://blog.grupocfi.es/es/formacion-requerida-ens-iso27001#:~:text=El%20Real%20Decreto%20311/2022%2C%20de%203%20de,las%20funciones%20y%20responsabilidades%20de%20cada%20rol.)
[3] [https://certificacionglobal.com](https://certificacionglobal.com/ens.html#:~:text=%C2%BFQu%C3%A9%20es%20el%20ENS%20%28%20Esquema%20Nacional,por%20las%20entidades%20del%20sector%20p%C3%BAblico%20espa%C3%B1ol.)
[4] [https://iveconsultores.com](https://iveconsultores.com/esquema-nacional-de-seguridad/#:~:text=El%20sector%20p%C3%BAblico:%20La%20Administraci%C3%B3n%20General%20del,vinculados%20o%20dependientes%20a%20las%20Administraciones%20P%C3%BAblicas.)
[5] [https://www.neotica.net](https://www.neotica.net/concienciacion-en-ciberseguridad/el-ens-como-columna-vertebral-de-la-confianza-digital-guia-completa-y-actualidad/#:~:text=1.%20Sector%20P%C3%BAblico%20%28Obligatoriedad%20Directa%29%20Todas%20las,Aut%C3%B3nomas%2C%20Ayuntamientos%2C%20Universidades%20P%C3%BAblicas%20y%20Colegios%20Profesionales.)
[6] [https://www.intedya.com](https://www.intedya.com/internacional/244/consultoria-ens-esquema-nacional-de-seguridad.html#:~:text=Sectores%20de%20APLICACI%C3%93N%20La%20Administraci%C3%B3n%20General%20del,p%C3%BAblico%20vinculadas%20o%20dependientes%20de%20la%20Administraci%C3%B3n)
[7] [https://www.teenvio.com](https://www.teenvio.com/blog/por-que-es-obligatorio-el-esquema-nacional-de-seguridad/#:~:text=Sector%20privado:%20Tambi%C3%A9n%20es%20obligatorio%20para%20empresas,software%20que%20maneje%20informaci%C3%B3n%20sensible%20de%20ciudadanos.)
[8] [https://solucionesqes.com](https://solucionesqes.com/sectores/ens-medicina/#:~:text=Esquema%20Nacional%20de%20Seguridad:%20Medicina%20La%20naturaleza,se%20tomen%20deben%20de%20seguir%20estos%20requisitos.)
[9] [https://iveconsultores.com](https://iveconsultores.com/principios-del-esquema-nacional-de-seguridad/#:~:text=Principio:%20Seguridad%20como%20un%20Proceso%20Integral%20Elementos,como%20firewalls%2C%20antivirus%2C%20sistemas%20de%20cifrado%2C%20etc.)
[10] [https://libisec.com](https://libisec.com/esquema-nacional-de-seguridad-ens/#:~:text=Principios%20del%20Esquema%20ENS%20Seguridad%20integral:%20La,y%20gesti%C3%B3n%20de%20riesgos%20de%20forma%20continua.)
[11] [https://www.audidat.com](https://www.audidat.com/blog/esquema-nacional-de-seguridad/auditoria-esquema-nacional-de-seguridad/#:~:text=Gesti%C3%B3n%20de%20Riesgos:%20El%20coraz%C3%B3n%20del%20ENS.,justificada%20por%20un%20an%C3%A1lisis%20de%20riesgos%20previo.)
[12] [https://www.secureit.es](https://www.secureit.es/cumplimiento/esquema-nacional-de-seguridad/#:~:text=Esquema%20Nacional%20de%20Seguridad%20%28ENS%29%20Elaborar%20una,para%20poder%20determinar%20la%20categor%C3%ADa%20del%20sistema.)
[13] [https://www.cci-es.org](https://www.cci-es.org/plan-de-respuesta-a-incidentes-de-ciberseguridad/#:~:text=Recuperaci%C3%B3n%20Despu%C3%A9s%20de%20que%20la%20amenaza%20se,que%20el%20negocio%20se%20vea%20m%C3%ADnimamente%20afectado.)
[14] [https://www.impconsultores.com](https://www.impconsultores.com/seguridad-de-la-informacion-iso-27001/#:~:text=El%20An%C3%A1lisis%20de%20Riesgos%20consiste%20en%20la,a%20las%20amenazas%20y%20vulnerabilidades%20los%20rodean.)
[15] [https://s2grupo.es](https://s2grupo.es/el-esquema-nacional-de-seguridad-ens/#:~:text=Metodolog%C3%ADa%20de%20adecuaci%C3%B3n:%20An%C3%A1lisis%20de%20situaci%C3%B3n:%20Evaluamos,del%20ENS:%20Plan%20de%20adecuaci%C3%B3n%20al%20ENS:)
[16] [https://www.pozuelodealarcon.org](https://www.pozuelodealarcon.org/sites/default/files/2023-09/Glosario%20del%20Esquema%20Nacional%20de%20Seguridad.pdf#:~:text=%E2%80%95%20An%C3%A1lisis%20de%20riesgos:%20estudio%20de%20las,funciones%29%20y%20la%20probabilidad%20de%20que%20ocurra.)
[17] [https://www.administraciondejusticia.gob.es](https://www.administraciondejusticia.gob.es/documents/7557301/7558194/CTEAJE-+Gu%C3%ADa+de+criterios+de+valoraci%C3%B3n+de+referencia+de+seguridad_GV1.0.pdf/2dfaae21-6371-af79-4ab8-63bea4331f81?t=1734953165793&download=true#:~:text=Para%20efectuar%20las%20valoraciones%20de%20las%20dimensiones,servicios%20prestados%20para:%20a%29%20Alcanzar%20sus%20objetivos.)
[18] [https://www.itdo.com](https://www.itdo.com/blog/el-esquema-nacional-de-seguridad-ens-como-marco-para-garantizar-la-seguridad-en-organizaciones-publicas-y-privadas/#:~:text=Requiere%20medidas%20razonables%20y%20controles%20fundamentales%20como,y%20mantener%20un%20umbral%20de%20seguridad%20aceptable.)
[19] [https://ayudaleyprotecciondatos.es](https://ayudaleyprotecciondatos.es/2020/11/19/esquema-nacional-de-seguridad-ens/#:~:text=La%20siguiente%20fase%20se%20dedicar%C3%A1%20a%20hacer,informaci%C3%B3n%20o%20de%20los%20sistemas%2C%20atendiendo%20a:)
[20] [https://www.audidat.com](https://www.audidat.com/blog/esquema-nacional-de-seguridad/auditoria-esquema-nacional-de-seguridad/#:~:text=Requisito%20previo:%20La%20categorizaci%C3%B3n%20del%20sistema%20Identificar,Integridad%2C%20Disponibilidad%2C%20Autenticidad%2C%20Trazabilidad%29%20para%20esos%20servicios.)
[21] [https://minciencias.gov.co](https://minciencias.gov.co/sites/default/files/ckeditor_files/D103PR03%20Gesti%C3%B3n%20de%20Incidente%20de%20seguridad%20de%20la%20Informaci%C3%B3n%20V01.pdf#:~:text=Integridad:%20Propiedad%20de%20la%20informaci%C3%B3n%20relativa%20a,a%20la%20informaci%C3%B3n.%20Riesgo%20de%20seguridad%20inform%C3%A1tica:)
[22] [https://www.fundaciondiagrama.es](https://www.fundaciondiagrama.es/sites/default/files/archivos/politica_de_seguridad_informacion.pdf#:~:text=Trazabilidad:%20propiedad%20o%20caracter%C3%ADstica%20con%2D%20sistente%20en,de%20la%20informaci%C3%B3n%20como%20un%20proceso%20integral.)
[23] [https://asocex.es](https://asocex.es/wp-content/uploads/2022/01/GPF-OCEX-5312_Glosario_de_Ciberseguridad4308.pdf#:~:text=La%20confidencialidad%20de%20la%20informaci%C3%B3n%20constituye%20la,dimensiones%20de%20la%20seguridad%20de%20la%20informaci%C3%B3n.)
[24] [https://www.neotica.net](https://www.neotica.net/concienciacion-en-ciberseguridad/el-ens-como-columna-vertebral-de-la-confianza-digital-guia-completa-y-actualidad/#:~:text=Categor%C3%ADa%20B%C3%A1sica:%20Se%20aplica%20a%20sistemas%20cuyo,el%20punto%20de%20partida%20para%20muchas%20PYMES.)
[25] [https://forlopd.es](https://forlopd.es/preguntas-frecuentes-sobre-esquema-nacional-de-seguridad/#:~:text=%C2%BFQu%C3%A9%20son%20los%20niveles%20de%20seguridad%20del,Media:%20Para%20sistemas%20con%20un%20impacto%20moderado.)
[26] [https://femp.femp.es](http://femp.femp.es/files/3580-2716-fichero/ENS%20-%20Lecciones%20Aprendidas.pdf)
[27] [https://www.applicalia.com](https://www.applicalia.com/esquema-nacional-de-seguridad-ens-preguntas-y-respuestas-para-entender-donde-estas-y-que-te-queda-por-hacer/#:~:text=A%20cada%20una%20se%20le%20asigna%20un,menos%20una%20dimensi%C3%B3n%20alcanza%20el%20nivel%20medio.)
[28] [https://administracionelectronica.gob.es](https://administracionelectronica.gob.es/ctt/resources/Soluciones/766/Descargas/Cl-ve-Niveles%20de%20Seguridad-v2-0.pdf?idIniciativa=766&idElemento=7186#:~:text=El%20ENS%20%28%20ESQUEMA%20NACIONAL%20DE%20SEGURIDAD,de%20todas%20las%20dimensiones.%201.%20Nivel%20BAJO.)
[29] [https://www.grupoacms.com](https://www.grupoacms.com/esquema-nacional-de-seguridad-ens-ambito-de-aplicacion-y-objetivos#:~:text=Existen%20diversas%20medidas%20de%20seguridad%20recogidas%20en,grupos%20%28Anexo%20II%20del%20Real%20Decreto%20311/2022%29:)
[30] [https://ens.ccn.cni.es](https://ens.ccn.cni.es/es/que-es-el-ens/faq#:~:text=%C2%BFQu%C3%A9%20es%20una%20Declaraci%C3%B3n%20de%20Aplicabilidad?%20En,que%20se%20trate%2C%20conforme%20a%20su%20categor%C3%ADa.)
[31] [https://iveconsultores.com](https://iveconsultores.com/medidas-de-seguridad-segun-el-esquema-nacional-de-seguridad/#:~:text=Medidas%20de%20seguridad%20del%20Esquema%20Nacional%20de,explotaci%C3%B3n%20de%20los%20servicios%20de%20una%20organizaci%C3%B3n.)
[32] [https://www.audidat.com](https://www.audidat.com/blog/esquema-nacional-de-seguridad/auditoria-esquema-nacional-de-seguridad/#:~:text=Requisito%20t%C3%A9cnico:%20La%20implementaci%C3%B3n%20de%20las%20medidas,de%20las%20operaciones.%20Marco%20de%20Protecci%C3%B3n%20%5Bmp%5D:)
[33] [https://aixacorpore.es](https://aixacorpore.es/ens-esquema-nacional-de-seguridad/)
[34] [https://www.leasba.com](https://www.leasba.com/esquema-nacional-de-seguridad/#:~:text=2%29%20Marco%20operacional%20Planificaci%C3%B3n:%20por%20medio%20de,externos:%20Continuidad%20del%20servicio:%20Monitorizaci%C3%B3n%20del%20sistema:)
[35] [https://www.um.es](https://www.um.es/web/atica/servicios/seguridad/ens)
[36] [https://www.applicalia.com](https://www.applicalia.com/esquema-nacional-de-seguridad-ens-preguntas-y-respuestas-para-entender-donde-estas-y-que-te-queda-por-hacer/#:~:text=%C2%BFQu%C3%A9%20ocurre%20cuando%20se%20produce%20un%20incidente,como%20el%20centro%20de%20respuesta%20t%C3%A9cnica%20nacional.)
[37] [https://www.idep.edu.co](https://www.idep.edu.co/sites/default/files/2023-05/GU-GT-12-01%20GU%C3%8DA%20PARA%20LA%20GESTI%C3%93N%20DE%20INCIDENTES%20DE%20SEGURIDAD%20DE%20LA%20INFORMACION.pdf)
[38] [https://protege.la](https://protege.la/guias-contenido/diseno-politicas-protocolos-lineamientos/)
[39] [https://level4.es](https://level4.es/es/como-responder-eficazmente-a-una-brecha-de-seguridad/#:~:text=Una%20vez%20que%20se%20comprende%20la%20naturaleza,acci%C3%B3n%20para%20contenerlo%20y%20mitigar%20los%20da%C3%B1os.)
[40] [https://www.kiteworks.com](https://www.kiteworks.com/es/glosario-riesgo-cumplimiento/respuesta-a-incidentes/#:~:text=Recuperaci%C3%B3n:%20Restaurar%20Operaciones%20La%20etapa%20de%20recuperaci%C3%B3n,procedimiento%20afectado%20est%C3%A9%20de%20nuevo%20en%20l%C3%ADnea.)
