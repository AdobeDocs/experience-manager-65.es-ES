---
title: 'Administración de proyectos: lista de comprobación de prácticas recomendadas'
seo-title: Managing Projects - Best Practices Checklist
description: La administración de un proyecto para implementar Adobe Experience Manager (AEM) requiere planificación y comprensión. Las listas de comprobación de proyectos están pensadas como un conjunto de prácticas recomendadas para la entrega de proyectos. Le guían a través de todas las fases del ciclo de vida del proyecto y le proporcionan una monitorización de alto nivel de su estado actual.
seo-description: Managing a project to implement Adobe Experience Manager (AEM) requires planning and understanding. The Project Checklists are intended as a set of best practices for project delivery. They guide you through all phases of the project life cycle and provide high level monitoring of your current status.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3264'
ht-degree: 2%

---

# Administración de proyectos: lista de comprobación de prácticas recomendadas{#managing-projects-best-practices-checklist}

La administración de un proyecto para implementar Adobe Experience Manager (AEM) requiere planificación y comprensión para garantizar que es consciente de los problemas y las decisiones (relacionadas) que debe tomar (tanto antes como durante la implementación del proyecto).

Para ayudarle, las prácticas recomendadas consisten en:

* Un [lista de comprobación interactiva](/help/managing/best-practices-checklist.md) que le permite realizar un seguimiento y un seguimiento del progreso con estas prácticas recomendadas.

   * Define las entradas y los resultados según la fase, el hito y la persona.
   * Proporciona información general automatizada (calidad, salud e integridad) para indicar el progreso y el estado del proyecto.

* Documentación basada directamente en la variable [lista de comprobación](/help/managing/best-practices-checklist.md), que detalla lo siguiente:

   * [Latido del proyecto](#projectheartbeat) análisis.
   * [Estado por función](#status-by-role) información general.
   * [Fases e hitos](#phases-and-milestones).
   * [Persona clave](#persona) y su participación en cada fase (pertinente).
   * A [Glosario](/help/managing/best-practices-glossary.md) del [Documentos y entregables requeridos](#required-documents-and-deliverables).

* [Referencia adicional](/help/managing/best-practices-further-reference.md) material para proporcionar más detalles sobre áreas específicas.

## Panel de latidos del proyecto {#project-heartbeat-dashboard}

La variable **Latido del proyecto** la hoja de cálculo ofrece información general gráfica de las métricas críticas del proyecto:

* **Calidad de fase**

   * Indica la calidad de la variable [Documentos y entregables requeridos](#required-documents-and-deliverables) en todo el proyecto.

* **Fase de salud**

   * Un indicador de estado de alto nivel para el proyecto; útil para destacar áreas que pueden estar en riesgo.

* **Finalización de la fase**

   * En cualquier momento durante el proyecto, esto indica cuánto se ha completado para cada fase del proyecto.

## Estado por función {#status-by-role}

La variable **Estado por función** la hoja de cálculo muestra el desglose detallado de [**Salud**, **Calidad** y **Complejidad**](#projectheartbeat) por **[Fase](#phases-and-milestones)** y **[Persona](#persona)**.

## Fases e hitos {#phases-and-milestones}

El plan del proyecto se desglosa en distintas fases (de alto nivel).

Cada fase contiene sus propios hitos. Para cada [personaje](#persona) (o función), se enumeran los hitos relevantes, junto con los documentos necesarios para producir los entregables definidos.

>[!NOTE]
>
>No existe una relación directa 1:1 entre los documentos individuales requeridos y los entregables.

### Preparación {#preparation}

La preparación del proyecto forma la base de todo el proyecto. Debe definir requisitos clave junto con objetivos y expectativas claros para:

* **Justificación empresarial**

   * Las razones fundamentales y la justificación para llevar a cabo el proyecto.

* **Ámbito y programa**

   * Debe disponerse de un alcance básico y de un calendario aproximado para definir lo que es necesario y en qué plazo; si ayuda a aclarar la situación, también puede definir qué queda fuera del ámbito.

La forma en que prepare, planifique y ejecute el proyecto e implemente su solución se verá afectada por las restricciones que esté utilizando, por ejemplo, en el presupuesto fijo, la cronología fija, la cantidad de contenido y la calidad requerida.

Como siempre, ajustar cualquiera de los factores afectará a los demás. Por ejemplo, si se reduce el tiempo, pero se requiere el mismo nivel de calidad, probablemente se aumente el precio y se reduzca la cantidad de contenido que se puede satisfacer. El presupuesto es a menudo un factor clave, por lo que tales relaciones no se pueden olvidar.

Los Cuatro Factores:

![projectfases_fourfases](assets/projectphases_fourphases.png)

#### Hitos {#milestones}

* **Validación**

   En esta fase, debe validar y confirmar los objetivos del proyecto; por ejemplo:

   * ¿Qué desea obtener/proporcionar?
   * ¿Quién se beneficiará?
   * ¿Cuál es el alcance?

      * Si ayuda a aclarar la situación, también puede definir lo que queda fuera del ámbito.
   * ¿Cómo definirá el éxito?
   * ¿Cómo medirá el éxito?
   * ¿Cuáles son los requisitos, empresariales y técnicos?
   * ¿Hay sistemas heredados que reemplazar y, en caso afirmativo, hay datos que migrar?
   * ¿Quién estará involucrado?
   * ¿Cómo medirá el progreso?
   * ¿Con qué frecuencia revisará el progreso durante la vida del proyecto?


* **Presupuesto**

   Antes de comenzar cualquier proyecto, necesita una estimación fiable y realista de lo que costará implementar:

   * Utilice la información del hito de validación como base para las estimaciones.
   * Sea realista en sus estimaciones.
   * Considere y respete cualquier guía de cliente, proceso o restricción a la que el cliente pueda estar sujeto.
   * Considerar los procesos de contingencia y revisión si se requiere una revisión o perfeccionamiento del presupuesto en una etapa posterior.
   * Recuerde que los costes se presentan de muchas formas; compras, uso de recursos y tarifas, entre otros.

### Planificación {#planning}

Al planificar el proyecto, se consolida la preparación. Aquí tiene que empezar a convertir los objetivos y expectativas en una hoja de ruta bien definida que consista en tareas concretas, sujetas a una comunicación clara, con revisiones rigurosas para medir el progreso.

#### Hitos {#milestones-1}

* **Gestión**

   Un traspaso limpio garantiza que las personas o grupos adecuados sean conscientes de sus responsabilidades dentro del proyecto.

   Deben facilitarse o generarse detalles completos para garantizar que comprenden plenamente todos los aspectos pertinentes, incluidos el plan de trabajo, el alcance, los objetivos, los requisitos y los indicadores clave de rendimiento.

* **Evaluación de riesgos**

   Para evitar sorpresas desagradables, utilice la evaluación del riesgo para identificar y cuantificar cualquier riesgo potencial junto con su impacto y probabilidad.

   Esto debe hacerse al principio del ciclo de vida del proyecto para garantizar que se identifiquen y evalúen todas las vulnerabilidades. En función de las conclusiones, puede informar a las partes interesadas sobre si se pueden implementar todos los requisitos y, si es necesario, si es posible planificar las acciones adecuadas que se deben llevar a cabo y realizar un seguimiento.

* **Comunicación**

   La comunicación es siempre clave para el éxito de cualquier proyecto. Debe comunicarse de forma clara y eficaz para asegurarse de que todos:

   * Trabajar en pos de los mismos objetivos básicos
   * Desde la misma base de información
   * Con los mismos canales

* **Inicio**

   La reunión de Kick Off se usa para crear conciencia de que el proyecto está comenzando. Es una buena oportunidad para:

   * Invitar a todas las partes interesadas (o al menos a los representantes de los grupos).
   * Presente hechos clave sobre el proyecto.
   * Responda preguntas.
   * Garantizar que todos tengan la misma base de conocimiento.
   * Obtenga el compromiso de todos los que participarán: esto tendrá que ganarse.

      * Al involucrar a los principales jugadores (incluidos los posibles autores) al comienzo del proyecto, incrementas tus posibilidades de conseguir su compromiso con el proyecto.

### Preparación para el desarrollo {#development-preparation}

La planificación del desarrollo es clave para garantizar que el proyecto se construya sobre un diseño sólido por parte de un equipo que tenga los conocimientos necesarios.

#### Hitos {#milestones-2}

* **Personal y capacitación del equipo de desarrollo**

   Antes de comenzar cualquier proyecto, debe asegurarse de que su equipo de desarrollo cuente con el personal adecuado y de que todos los integrantes del equipo estén formados para la tarea en cuestión.

* **Arquitectura de contenido**

   La arquitectura de contenido define y describe la arquitectura futura del contenido; incluido:

   * El árbol de contenido; incluir activos
   * Estructuras básicas; incluir campañas, etc.
   * Estructuras de varios sitios y varios idiomas (MSM, traducción, etc.)
   * Contenido compatible (incluidas etiquetas y conceptos de etiquetado)
   * Estrategias de almacenamiento en caché y reutilización de contenido

* **Arquitectura del sistema**

   La arquitectura del sistema define la vista conceptual de su sistema; incluido (entre otros datos):

   * [Estructura del sistema](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) para todos los entornos necesarios
   * Subsistemas
   * Sistemas de terceros
   * Interfaces; hardware, software e interacción humana
   * Servidores para cada entorno; consulte la [Requisitos técnicos](/help/sites-deploying/technical-requirements.md) y [Pautas para el tamaño del hardware](/help/managing/hardware-sizing-guidelines.md)

   * Procesos para cada entorno; por ejemplo, los requisitos de implementación y mantenimiento
   * Actividades de mantenimiento (Datastore GC, optimización de TarPM, etc.)
   * [](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)Almacenamiento en caché de Dispatcher
   * [Clustering](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) Publicar/Autorcompartir
   * Rendimiento del lado del cliente (minify de JS, concat, sprites css, número total de solicitudes http y otras)

* **Arquitectura de aplicaciones**

   La arquitectura de la aplicación define y describe el comportamiento de las aplicaciones propuestas.

   Se centra en:

   * Cómo interactuarán entre ellos y con los usuarios.
   * Los datos que deben ser consumidos y producidos por las aplicaciones, en lugar de su estructura interna.

   Las definiciones deberían abarcar:

   * Estructura básica del código para el proyecto
   * Artefactos de código (paquetes, paquetes, etc.)
   * Desgloses de las plantillas/componentes y sus relaciones
   * Detalles de alto nivel de las personalizaciones necesarias (a continuación se superponen determinadas opciones)
   * Diseño de los flujos de trabajo requeridos por la solución (por ejemplo, creación de contenido, aprobación, publicación, transformaciones, importaciones, exportaciones, etc.)
   * Consideración especial para cualquier módulo complejo, como MSM, Commerce, integración de terceros


* **Integración del sistema**

   La integración del sistema requiere que planifique (e implemente):

   * Cómo todos los subsistemas y [integraciones de soluciones](/help/sites-administering/integration.md) se reunirán para funcionar como un sistema coherente
   * ¿Cómo se integrarán los sistemas de terceros? junto con cualquier consideración especial, como offline/online, client-side/browser o gestión de devoluciones cuando un sistema de terceros está inactivo

* **Concepto de prueba**

   Antes de comenzar el desarrollo, debe elaborar un concepto exhaustivo y completo de todos [prueba](/help/sites-developing/planning.md) requisitos del proyecto.

   Esto debería incluir (entre otros):

   * Detalles de todas las pruebas que deben realizarse
   * Preparación de cualquier contenido necesario para estas pruebas
   * Información sobre las herramientas de prueba que deben utilizarse
   * Indicación de alto nivel de quién participará en las pruebas; especialmente grupos fuera del equipo de control de calidad
   * Detalles de la automatización de las pruebas; por ejemplo, con el modo de desarrollador de Selenium o AEM

* **Diseño de experiencias**

   El diseño de experiencia (XD) implica diseñar la experiencia del usuario para su solución.

   La experiencia del usuario debe analizarse y desarrollarse tanto para los autores como para los usuarios finales del sitio web.

* **Configuración de asistencia**

   Antes del desarrollo, se deben configurar todos los procesos de soporte necesarios para implementar, publicar, probar e informar sobre problemas.

   Consulte también la [Portal de soporte de Adobe](https://helpx.adobe.com/es/marketing-cloud/contact-support.html).

### Planificación de operaciones y operaciones {#operations-planning-and-operations}

De forma similar, las operaciones deben planificarse correctamente para garantizar que dispone de los entornos necesarios para todas las etapas del ciclo de vida del proyecto. También necesita los procesos adecuados para mantenerlos.

#### Hitos {#milestones-3}

* **Permisos**

   Debe planificar y luego implementar un Concepto de funciones y derechos para todos los usuarios/grupos que utilicen la solución.

   Por ejemplo:

   * Una lista de funciones (es decir, grupos) con `read`/ `write` definiciones de acceso para cada

   * Definición del uso de privilegios que afectan al entorno de publicación; por ejemplo, `replicate`
   * Para los usuarios con privilegios mínimos, los flujos de trabajo deben definirse
   * Los usuarios de `editor` El grupo no debe tener `admin` ni formar parte de `administrators` grupo

   Para obtener más información, consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

* **Supervisión y mantenimiento**

   La supervisión y el mantenimiento son aspectos clave para garantizar el correcto funcionamiento de su solución una vez que se ponga en marcha. Para ello, debe definir:

   * Qué necesita monitorización
   * Tareas de mantenimiento; tanto ordinarios como especiales

   Consulte también [Supervisión y mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md) para obtener más información.

* **Migración**

   Cualquier contenido del sistema heredado debe revisarse y validarse para su migración.

* **Plan de recuperación**

   Asegúrese de que dispone de un plan de recuperación. En una situación de emergencia, esto debe estar disponible para asegurar el uso de la producción de AEM. Esto debería cubrir situaciones como backup, restore, falllover y otras.

### Desarrollo {#development}

El desarrollo es una fase crucial que requiere algo más que simplemente codificación.

#### Hitos {#milestones-4}

* **Entorno de desarrollo**

   Planifique y documente su entorno de desarrollo, lo que incluye:

   * Arquitectura
   * [Herramientas de desarrollo](/help/sites-developing/dev-tools.md)

      * Un entorno típico consta de:

         * un sistema de seguimiento de problemas; como Jira
         * un IDE; como Eclipse
         * un instrumento de gestión de la compilación; como Maven
         * un instrumento para la integración continua; como Jenkins
         * una herramienta para el control de versiones; como GIT/SVN
         * un administrador de repositorios de artefactos de compilación; como Archiva/Nexus
   * Integración/dependencias de software de terceros
   * [Integración y dependencias de la solución](/help/sites-administering/integration.md)
   * cadencia de implementación


* **Sistema de pruebas**

   Planifique y documente el entorno de prueba, lo que incluye:

   * Arquitectura
   * Dependencias de las bases del desarrollo; incluir compilaciones por la noche
   * Las posibilidades o limitaciones de probar la integración/dependencias de software de terceros
   * Herramientas de prueba
   * Estrategia de prueba automatizada

* **Sistema de producción**

   Planifique y documente su entorno de producción, lo que incluye:

   * Arquitectura
   * cadencia de implementación
   * Integración/dependencias de software de terceros
   * Configuración de seguridad
   * El rendimiento de línea de base verificado ejecutando el [Pruebas de día duro](/help/sites-developing/tough-day.md) en la configuración de producción
   * Requisitos para las pruebas de rendimiento; see [Prácticas recomendadas para garantizar la calidad](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integración**

   Planificar, documentar y probar todos los aspectos del sistema y [integración de soluciones](/help/sites-administering/integration.md), incluido:

   * Una estrategia de pruebas automatizada
   * Procesos automatizados para [mover aplicaciones de desarrollo a prueba y luego producción](/help/managing/enterprise-devops.md#code-movement)
   * Procesos automatizados para [mover contenido de producción a prueba y desarrollo](/help/managing/enterprise-devops.md#content-movement)

* **Migración**

   Planificar, documentar y probar todos los aspectos de la migración de contenido; incluido:

   * Arquitectura de contenido
   * Estrategia de migración

* **Comunicación**

   Asegúrese de que todos los integrantes del equipo y el perfil del proyecto estén actualizados según sea necesario.

* **Documentación**.

   Documentar completamente la solución; incluido:

   * Manual de operaciones
   * Cualquier personalización que pueda afectar a las actualizaciones
   * Notas de versión

### Rendimiento y pruebas {#performance-and-testing}

Una vez que la nueva aplicación esté disponible, deberá someterse a pruebas rigurosas, tanto para la funcionalidad como para la [rendimiento](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Se debe permitir que cualquier equipo de prueba permanezca neutral y ofrezca los resultados de la prueba.
>
>Corresponde al Administrador del proyecto evaluar las consecuencias de los resultados y decidir las medidas apropiadas.

#### Hitos {#milestones-5}

* **Prueba de aceptación del usuario final**

   [Pruebas de aceptación del usuario](/help/sites-developing/acceptance-signoff.md) (UAT) es crucial para garantizar que:

   * La solución cumple los requisitos del usuario y del cliente
   * El cliente o los usuarios aceptan la solución (función, diseño y rendimiento)

   Debe haber una lista de comprobación formalizada para la entrega de clientes; lo ideal es automatizarlo y ejecutarlo todas las noches en función de una instantánea. Los resultados deben enviarse al administrador del proyecto y al equipo de desarrollo

* **Pruebas de rendimiento y carga**

   Las pruebas de rendimiento y carga se utilizan para garantizar que la solución cumpla los niveles de rendimiento requeridos, en cargas medias y máximas.

   Para obtener más información sobre las pruebas de rendimiento, consulte:

   * [Pruebas de rendimiento](/help/sites-deploying/configuring-performance.md)
   * [Cómo planificar y ejecutar pruebas](/help/sites-developing/planning.md)

   * [Directrices básicas de rendimiento](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >Este proceso tendrá que continuar durante el uso normal de AEM, pero estas etapas iniciales son las más cruciales.

### Despliegue {#rollout}

El despliegue de la nueva aplicación necesita una planificación cuidadosa para garantizar un lanzamiento suave. Esto incluye confirmar un alto nivel de seguridad, capacitar a todos los usuarios potenciales y realizar varias simulaciones para confirmar que se han tratado todos los problemas.

#### Hitos {#milestones-6}

* **Preparación**

   La preparación y la planificación ayudarán a garantizar un despliegue sin problemas.

* **Capacitación**

   Asegurar que todo el personal involucrado haya sido capacitado.

   Consulte [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) en el catálogo de cursos.

* **Administradores formados**

   Asegúrese de que los administradores de soluciones tengan:

   * Recibido formación
   * Se ha recibido el material de formación adecuado
   * Se ha recibido la documentación apropiada

* **Usuarios formados**

   Asegúrese de que los autores tengan:

   * Recibido formación
   * Se ha recibido el material de formación adecuado
   * Recibió la documentación apropiada; por ejemplo, la Guía del usuario

* **Pruebas de penetración**

   Las pruebas de penetración simulan un ataque a un sistema informático para identificar posibles deficiencias de seguridad.

* **Pruebas de penetración/seguridad**

   Para garantizar la seguridad de su solución, realice pruebas de penetración específicas, junto con una gama más amplia de pruebas de seguridad.

   Consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para obtener más información.

### Lanzamiento {#go-live}

Quieres que tu Go Live sea lo más suave posible. Una vez más, los pasos finales necesitan planificación para una ejecución limpia.

#### Hitos {#milestones-7}

* **Preparación**

   La preparación y la planificación ayudarán a garantizar un lanzamiento sin problemas.

* **Seguridad**

   Confirme la seguridad de la solución para usuarios internos y externos y su contenido.

* **Abandono**

   Asegúrese de que todos los sistemas, procedimientos y mecanismos necesarios para la reserva estén establecidos antes de la entrada en funcionamiento.

* **Asistencia**

   Asegúrese de que los servicios de soporte estén listos y en su lugar.

* **Transición**

   Planifique y ejecute la transición al entorno de producción y a los usuarios.

* **Desplegar**

   Prepare y ejecute sus pruebas de humo.

## Grupo de usuarios {#persona}

Las listas de comprobación están diseñadas por persona. Estas son las funciones que tienen una participación significativa en el ciclo de vida del proyecto.

También hay algunas [otra persona](#other-persona) que participan en tareas específicas.

### Patrocinador del proyecto {#project-sponsor}

El patrocinador del proyecto es:

* Responsable de proporcionar/presentar el caso empresarial del proyecto.
* La clave para definir y definir el ámbito del proyecto; incluido:

   * la definición y los criterios del éxito
   * los KPI principales

* Proporcione los hitos principales basados en la hoja de ruta del cliente.

### Gestor de proyectos {#project-manager}

El administrador de proyectos es:

* Responsable de la ejecución general del proyecto en función de los requisitos (por ejemplo, ámbito, KPI, criterios de éxito y definición) proporcionados por el patrocinador del proyecto.
* Responsable de definir el presupuesto y de dotar al proyecto de recursos basados en dicho presupuesto.
* El principal punto de comunicación para toda persona involucrada en el proyecto.

### Arquitecto {#architect}

El arquitecto de soluciones:

* Es responsable del diseño de alto nivel de la solución y del sistema.
* Ayuda a definir la estrategia de implementación para AEM. Por ejemplo, si se debe implementar una instalación en clúster, o una espera en frío, o cuando se necesita una red de entrega de contenido (CDN).
* Defina también la arquitectura de la solución AEM en función de los requisitos del cliente. Esto puede incluir el concepto de funciones de usuario (con derechos relacionados), la relación entre plantillas y componentes, o cuándo utilizar la administración de varios sitios.

### Analista empresarial {#business-analyst}

El analista empresarial:

* Es el responsable principal de reunir y analizar los requisitos de alto nivel, transformándolos luego en especificaciones:

   * para que el administrador de proyectos lo utilice al planificar el desarrollo
   * para que el equipo de desarrollo trabaje durante el diseño y el desarrollo.

* Trabaja estrechamente con el cliente para analizar los requisitos. Coinciden con:

   * La definición del éxito.
   * Los criterios de éxito.
   * KPI (basados tanto en el negocio como en el rendimiento).

### Plomo de desarrollo {#development-lead}

El líder de desarrollo:

* Es responsable de la entrega técnica del proyecto.
* Es responsable de seleccionar una metodología de desarrollo que cumpla con los requisitos del cliente.
* Elabora la estrategia de desarrollo:

   * garantizar que esté alineado con los KPI de negocio y rendimiento
   * teniendo en cuenta los criterios y la definición de éxito

* Trabaja estrechamente con el arquitecto (especialmente al elaborar la estrategia de desarrollo para AEM) para definir aspectos como la relación entre plantillas y componentes, la estrategia de integración para aplicaciones de terceros y cualquier funcionalidad especializada.

### Plomo de calidad {#quality-lead}

El nivel de calidad:

* Es responsable de la calidad de la entrega; garantizar que cumpla los criterios de éxito y cualquier KPI definido por el cliente.
* Define las métricas de calidad, se alinea con todas las partes interesadas, elabora los planes de prueba y garantiza que se ejecuten.
* Crea y envía informes a las partes interesadas del proyecto.

### Ingeniero de sistemas {#system-engineer}

El ingeniero del sistema:

* Es responsable de supervisar la infraestructura del proyecto.
* Es responsable de:

   * la configuración de entornos de prueba y desarrollo internos
   * para hacer coincidir esos sistemas con los sistemas cliente

* Proporciona recomendaciones de hardware, supervisa las distintas implementaciones y proporciona soporte para las operaciones tanto antes de su lanzamiento como después.

### Jefe de seguridad {#security-lead}

El posible cliente de seguridad:

* Es responsable del concepto general de seguridad de la solución, asegurándose de que esté alineado con cualquier requerimiento y política del cliente.
* Ofrece un concepto de seguridad, operaciones de seguridad y recomendaciones para cualquier concepto de seguridad basado en hardware; como zonas y cortafuegos.

### Otras personas {#other-persona}

* Partes interesadas

   * Personas (a menudo de la empresa) que tienen interés (en) en el éxito del proyecto. A menudo contribuyen al presupuesto.

* Oficio

   * Se requiere asesoramiento jurídico al negociar contratos.

* Formadores

   * En función de la escala y la naturaleza del proyecto, se pueden utilizar instructores especializados para preparar y presentar sesiones de capacitación para los grupos pertinentes.

* Escritores técnicos

   * En función de la escala y la naturaleza del proyecto, se pueden utilizar escritores técnicos especializados para redactar directrices y manuales para grupos específicos; Por ejemplo, un manual de mantenimiento para administradores del sistema o una guía del usuario para los autores.

* Administradores del sistema

   * Responsable del funcionamiento en curso del sistema.

* Autores y usuarios finales

   * Personas que utilizarán el sistema para crear y mantener el contenido del sitio web.

## Documentos y entregables requeridos {#required-documents-and-deliverables}

Las listas de comprobación cubren el **Documentos requeridos** y **Deliverables** para cada hito.

* No existe una relación 1:1 entre estas; por ejemplo, un grupo de documentos necesarios puede resultar en una única entrega.
* Un envío de una persona puede ser un documento requerido para otra persona durante el mismo hito.

### Documentos requeridos {#required-documents}

La variable **Documentos requeridos** son necesarios para el perfil adecuado al producir sus entregables.

Para cada **Documento requerido** la persona debe indicar:

* **Y/N**: si se ha recibido.
* **1-3**: una indicación de la calidad del documento recibido.

### Deliverables {#deliverables}

Para cada hito, la persona apropiada es responsable de entregar documentos específicos y, por lo tanto, cumplir con sus responsabilidades para un hito específico.

Para cada **Entrega** la persona debe indicar:

* **Y/N**: si se ha completado.

Los entregables a menudo se utilizan como **Documentos requeridos** para el hito actual o posterior.

## Prácticas recomendadas relacionadas {#related-best-practices}

Para conocer las prácticas recomendadas sobre la implementación, administración, desarrollo o creación, consulte lo siguiente:

* Otras prácticas recomendadas y directrices relacionadas con la administración de un proyecto de AEM:
   * [Pautas para configurar el tamaño del hardware ](/help/managing/hardware-sizing-guidelines.md)
   * [Operaciones de desarrollo empresarial ](/help/managing/enterprise-devops.md)
   * [Recomendaciones para la administración de direcciones URL y SEO ](/help/managing/seo-and-url-management.md)
   * [AEM y las directrices de accesibilidad web ](/help/managing/web-accessibility.md)
   * [Reglamento general de protección de datos](/help/managing/data-protection-and-privacy.md)* [Implementación y mantenimiento de las prácticas recomendadas](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas sobre administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas sobre desarrollo](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas sobre la creación](/help/sites-authoring/best-practices.md)

## Áreas de documentación clave {#key-documentation-areas}

* AEM Documentación Además, las siguientes secciones de AEM documentación revisten especial interés (sin embargo, esta lista no es exhaustiva):

   * [Seguridad](/help/sites-developing/security.md)
   * [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
   * [Operaciones de desarrollo empresarial ](/help/managing/enterprise-devops.md)
   * [Tamaño del hardware](/help/managing/hardware-sizing-guidelines.md)
   * Conceptos de AEM:

      * [Desarrollo: conceptos básicos](/help/sites-developing/the-basics.md)
      * [Conceptos de MSM](/help/sites-administering/msm.md)
      * [Idioma de plantilla del HTML (HTL)](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html)

* Documentación relacionada

   * Adobe Experience Cloud - [Planificación de Adobe Experience Cloud](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
