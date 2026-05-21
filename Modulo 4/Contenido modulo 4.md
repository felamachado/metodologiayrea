

```
# Guía Integral de los Recursos Educativos Abiertos (REA): Fundamentos, Estructura y Creación Inclusiva

## 1. Introducción al Ecosistema de lo Abierto: Hacia la Democratización del Saber

La emergencia de los Recursos Educativos Abiertos (REA) trasciende la mera disponibilidad de materiales gratuitos; representa una transformación estructural hacia la democratización del conocimiento y el empoderamiento de la comunidad académica. En este paradigma, los REA no son objetos estáticos, sino catalizadores de un modelo de participación activa donde el docente y el estudiante asumen la co-autoría de su proceso formativo. Esta apertura no solo mitiga la brecha económica de acceso, sino que potencia la calidad educativa a través de la **inteligencia colectiva**, permitiendo que los recursos evolucionen mediante procesos de mejora continua similares a los observados en el desarrollo de software libre.

Fundamentados en las directrices de la UNESCO y las definiciones de David Wiley, los REA comprenden materiales de enseñanza, aprendizaje e investigación en cualquier soporte —digital o físico— que residen en el dominio público o han sido publicados bajo licencias abiertas. La naturaleza de lo "abierto" se manifiesta en una dualidad técnica y legal: mientras que lo técnico garantiza la interoperabilidad entre plataformas, lo legal otorga permisos explícitos para ejercer las **"4R"** definidas por Wiley:

*   **Revisar (Revise):** Adaptar y mejorar el recurso según necesidades específicas.
*   **Combinar (Remix):** Mezclar materiales diversos para generar obras originales.
*   **Reusar (Reuse):** Utilizar el recurso en múltiples contextos y formatos.
*   **Redistribuir (Redistribute):** Compartir copias de la obra original o sus derivadas.

Desde una perspectiva teórica profunda, los REA se alinean con el **Conectivismo** (Siemens, 2005), donde el aprendizaje reside en la capacidad de navegar y nutrir redes de información. Asimismo, bajo el prisma del **Constructivismo Sociocultural de Vygotsky**, estos recursos actúan como instrumentos de **mediación simbólica**. En la **Zona de Desarrollo Próximo (ZDP)**, el REA funciona como un andamio que permite al estudiante alcanzar niveles superiores de competencia, incluso en entornos asincrónicos, facilitando una interacción significativa con el objeto de conocimiento.

## 2. Licenciamiento Abierto: Seguridad Jurídica y la Herramienta Yabalá

El licenciamiento abierto constituye el andamiaje legal que permite transitar del restrictivo "todos los derechos reservados" al flexible "algunos derechos reservados". La infraestructura de Creative Commons (CC) proporciona la seguridad jurídica necesaria para que la reutilización no infrinja la propiedad intelectual, respetando siempre la autoría original.

Para ser considerados genuinamente REA, los materiales deben permitir obras derivadas. La siguiente tabla clasifica las licencias según este criterio esencial:

| Licencia | Siglas | Permite Derivadas | Estatus REA | Condición Principal |
| :--- | :--- | :--- | :--- | :--- |
| **Atribución** | CC BY | Sí | **Sí** | Reconocimiento de autoría. |
| **CompartirIgual** | CC BY-SA | Sí | **Sí** | Derivadas con misma licencia. |
| **NoComercial** | CC BY-NC | Sí | **Sí** | Prohibición de fines de lucro. |
| **NC-CompartirIgual** | CC BY-NC-SA | Sí | **Sí** | No comercial y misma licencia. |
| **SinDerivadas** | CC BY-ND | No | **No** | Solo copias literales. |
| **NC-SinDerivadas** | CC BY-NC-ND | No | **No** | Restricción comercial y literal. |
| **Dominio Público** | CC0 / PD | Sí | **Sí** | Sin restricciones legales. |

### Gestión de Compatibilidad y el Módulo Yabalá

El "remix" de recursos con licencias distintas suele generar conflictos de compatibilidad (ej. entre restricciones *SA* y *NC*). Para resolver estos dilemas técnicos, el módulo de software **Yabalá** y su aplicación Calculator ofrecen una solución experta. A diferencia de un buscador genérico, esta herramienta identifica automáticamente la licencia resultante (mostrando opciones más y menos restrictivas) y genera productos de atribución profesional. Entre sus funciones críticas destaca la creación de **URLs permanentes** para créditos en formato HTML y la generación de **códigos QR** que vinculan directamente a la información de autoría, asegurando que el recurso sea trazable y legalmente íntegro en cualquier entorno digital o físico.

## 3. Arquitectura de los REA: Metadatos y Repositorios

La preservación y recuperación de los REA dependen de una descripción técnica rigurosa. Sin metadatos estandarizados, el recurso permanece invisible para los sistemas de búsqueda global.

### Estándares: Dublin Core y LOM

Mientras que **Dublin Core** ofrece una semántica universal de 15 elementos para la interoperabilidad básica, el estándar **LOM (Learning Object Metadata)** profundiza en la dimensión pedagógica. No obstante, para optimizar el flujo de trabajo docente y evitar la fatiga administrativa, la evidencia sugiere un enfoque pragmático. Según el marco de calidad del repositorio Ceibal 4.1, se establecen solo **dos descriptores LOM como obligatorios**:

1. **Tipo de recurso (learningResourceType):** Define la naturaleza didáctica (ej. simulación, experimento, cuestionario).
2. **Palabras clave (keyword):** Descriptores semánticos que facilitan la indexación temática.

### Jerarquía Técnica en Repositorios (DSpace)

Un repositorio institucional robusto organiza el conocimiento mediante una jerarquía de Comunidades y Colecciones. En el nivel de **Ítem** (objeto básico de archivo), la arquitectura técnica se desglosa en **Bundles** (paquetes) que contienen los **Bitstreams**. Estos últimos son los flujos de datos reales (archivos de imagen, texto o código) que conforman el recurso. La calidad del repositorio no reside solo en su almacenamiento, sino en la precisión con la que estos bitstreams son descritos y vinculados a sus metadatos pedagógicos.

## 4. Metodología de Creación Inclusiva: Modelo CO-CREARIA

La co-creación es una estrategia que integra la diversidad como un componente nativo del diseño, no como un parche posterior. El modelo **CO-CREARIA** adapta el ciclo ADDIE para garantizar que los principios del **Diseño Universal para el Aprendizaje (DUA/UDL)** guíen cada fase del desarrollo.

### Fases y Productos del Modelo

*   **Análisis:** Definición de roles y análisis del perfil poblacional.
    *   *Producto:* Reporte de perfil de población según UDL y análisis de ambiente.
*   **Diseño:** Creación de guiones y detección de barreras potenciales.
    *   *Producto:* Diseño de métodos/materiales y reporte de análisis de barreras.
*   **Desarrollo:** Producción mediante herramientas de autoría accesibles (ej. ATutor).
    *   *Producto:* REA disponible y documento descriptivo de desarrollo.
*   **Evaluación:** Validación técnica, de accesibilidad web y pedagógica.
    *   *Producto:* Reportes de calidad, accesibilidad y cumplimiento de principios UDL.
*   **Implementación:** Despliegue en escenarios reales con retroalimentación del usuario.
    *   *Producto:* Resultados del despliegue y reporte de ejecución.

### Evidencia de Aplicación: El Caso UPB

El rigor del modelo se evidencia en proyectos como **"Cuida tu ambiente con TIC"** (Universidad Pontificia Bolivariana). En este caso, el equipo de co-creación (docentes, psicopedagogos y padres) utilizó CO-CREARIA para diseñar materiales específicos para estudiantes con **baja visión** y diagnósticos de **hiperactividad**. Mediante la mediación virtual y metodologías como el **Aprendizaje Basado en Proyectos (ABP)** y el **Aula Invertida**, se transformó el contenido en experiencias multimodales que eliminaron las barreras de acceso tradicionales.

## 5. Evaluación de Calidad, Accesibilidad y Recomendación

La efectividad de un REA se mide por su capacidad para eliminar barreras sensoriales, cognitivas y tecnológicas. La evaluación no debe ser un proceso aislado, sino apoyarse en el **Crowdsourcing**. Estellés y González definen esta práctica como una actividad participativa en línea donde una multitud aporta conocimiento y experiencia para cumplir una tarea de beneficio mutuo; en este contexto, las valoraciones docentes filtran y elevan la calidad del repositorio.

### Checklist de Calidad REA para el Usuario

Para validar si un recurso cumple con los estándares de un REA de alta calidad, aplique los siguientes criterios:

*   **Licenciamiento Abierto:** ¿Permite explícitamente el remix y la creación de obras derivadas (4R)?
*   **Atribución Técnica:** ¿Incluye créditos claros o URLs permanentes/QR generados por herramientas como Yabalá?
*   **Interoperabilidad de Formato:** ¿Se ofrece en formatos editables y abiertos (ej. ODT) para facilitar la revisión, en lugar de formatos cerrados o solo lectura (ej. PDF)?
*   **Accesibilidad DUA:** ¿Existen alternativas textuales para imágenes y subtítulos para videos?
*   **Rigor de Metadatos:** ¿Están presentes los campos obligatorios de LOM (Tipo y Palabras Clave)?
*   **Navegabilidad:** ¿La estructura de títulos es coherente para lectores de pantalla?

## 6. Bibliografía Consultada

1. Wiley, D., “Connecting Learning Objects to Instructional Design Theory: A definition, a metaphor, and a taxonomy”, in D. A. Wiley (ed.) Instructional Use of Learning Objects. Editorial Association for Instructional Technology, 2002.
2. Sitio Web de la UNESCO. Recursos Educativos Abiertos. http://www.unesco.org/new/es/communication-and-information/access-to-knowledge/open-educational-resources/.
3. Budapest Open Access Initiative. (2002). La Iniciativa de Acceso Abierto de Budapest. http://www.geotropico.org/1_1_Documentos_BOAI.html.
4. Wiley, D. (2010). Openness as catalyst for an educational reformation. Educause Review, 45 (4), 15-20. http://www.educause.edu/EDUCAUSE+Review/EDUCAUSEReviewMagazineVolume45/OpennessasCatalystforanEducati/209246.
5. CONGRESO MUNDIAL SOBRE LOS RECURSOS EDUCATIVOS ABIERTOS (REA) UNESCO, PARÍS, 20-22 DE JUNIO DE 2012. http://www.unesco.org/new/fileadmin/MULTIMEDIA/HQ/CI/WPFD2009/Spanish_Declaration.html.
6. Paul G. West & Lorraine Victor. (2011). Background and action paper on OER. http://www.paulwest.org/public/Background_and_action_paper_on_OER.pdf.
7. Estellés-Arolas, E., & González-Ladrón-De-Guevara, F. (2012). Towards an integrated crowdsourcing definition. Journal of Information science, 38(2), 189-200.
9. Licencias Creative Commons y contenidos abiertos. http://es.wikiversity.org/wiki/Licencias_Creative_Commons_y_contenidos_abiertos.
10. Creative Commons Org. Frequently Asked Questions. https://creativecommons.org/faq/#can-i-combine-material-under-different-creative-commons-licenses-in-my-work.
12. Baldiris, S., Avila, C., et. al. (2015). CO-CREARIA: Modelo de Co-Creación de REA Inclusivos y Accesibles. Ingeniería e Innovación, Vol 3(2).
13. Carrero Romero, O. D. (2025). Educación y Mediación Virtual: Estrategias para el Aprendizaje en Entornos Digitales. Ibero Ciencias, Vol 4(2). https://doi.org/10.63371/ic.v4.n2.a68.
20. Wiley, D., “OER: Relieving the Pressure.” TEDxSANDY, 2014.
```

