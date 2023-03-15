---
title: Información general de AEM Communities
seo-title: AEM Communities Overview
description: Información general sobre las funciones y la configuración de AEM Communities
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 4%

---

# Información general de AEM Communities {#aem-communities-overview}

Las comunidades de Adobe Experience Manager (AEM) ofrecen la posibilidad de crear rápidamente un sitio de comunidad local que tenga un rendimiento y una gestión mejorados, y que anime a los visitantes a convertirse en miembros valiosos de la comunidad.

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Características de Communities {#communities-features}

AEM Communities permite desarrollar una relación con los visitantes del sitio que:

* **Informa** a través de blogs, preguntas y respuestas y calendarios de eventos,
* While **obtención de perspectivas** a través de foros, comentarios y otros contenidos de la comunidad, a menudo denominados contenido generado por el usuario (UGC).
* Permite **moderación** por miembros de confianza en el entorno de publicación,
* **Inicio de sesión social** con Twitter y Facebook,
* **Traducción en línea** del contenido de la comunidad,
* **Creación de grupos de comunidad** del sitio de la comunidad publicado,
* **Puntuación** para otorgar insignias,
* **Uso compartido de archivos**,
* **Notificaciones** y **flujos de actividad**,
* Permite **etiquetado** (@mention) otros miembros registrados en Contenido generado por el usuario, para llamar su atención.
* Admite **navegación mediante el teclado** en componentes de habilitación (por ejemplo, Reproducción de catálogos y cursos, Asignaciones, Biblioteca de archivos) .

Las funciones de las comunidades se pueden mostrar utilizando la variable [AEM Máquina de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible públicamente en GitHub.com o con la nueva implementación de referencia de We.Retail.

## Sitios de la comunidad {#community-sites}

AEM Un sitio de la comunidad es un sitio de la comunidad creado mediante un asistente simple que da como resultado un sitio web con muchas funciones comunes precableadas en el sitio.

El [asistente de creación de sitios](/help/communities/sites-console.md):

* Agrupa las características del sitio según el sitio seleccionado [plantilla del sitio de la comunidad](/help/communities/sites.md) que es:

   * compilado desde [funciones de comunidad](#community-functions)
   * opcional [grupos comunitarios](#communitygroups) característica

* Utiliza la configuración para configurar:

   * moderación
   * login
   * traducción

* Proporciona funciones esenciales:

   * Diseño interactivo: usos [Temas del Bootstrap de twitter](https://getbootstrap.com)

   * Inicio de sesión : registro automático, [inicio de sesión social](/help/communities/social-login.md), perfiles de usuario

      * Notificaciones: los miembros ven eventos de relevancia para ellos y el contenido generado por el usuario donde se encuentran [@mentioned](/help/communities/overview.md#mentionssupport).

      * Mensajes: los miembros pueden enviar o recibir mensajes dentro del sitio de la comunidad.
      * Buscar: capacidad de buscar en el sitio de la comunidad.
      * Cambio de idioma: capacidad para seleccionar un idioma para una [sitio multilingüe](/help/sites-administering/translation.md).

      * Administración: acceso para miembros autorizados a moderar y administrar usuarios dentro del sitio de la comunidad.

* Elimina muchos pasos de la creación en el nivel de página:

   * Personalización de marca: carga opcional de una imagen de titular para mostrarla en todas las páginas del sitio de la comunidad.
   * Menú de navegación: se proporcionan vínculos de navegación para las funciones incluidas en la plantilla del sitio de la comunidad.

Para experimentar la facilidad de crear rápidamente un nuevo sitio de comunidad, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

## Persistencia del contenido de comunidad {#community-content-persistence}

Para mejorar el rendimiento y la sincronización del contenido de la comunidad, AEM Communities AEM requiere un almacén común específico para el contenido generado por el usuario (UGC) compartido entre todas las instancias (de autor y publicación) de la.

Se puede acceder fácilmente al contenido de la comunidad a través del proveedor de recursos de almacenamiento (SRP), que proporciona una capa para separar el acceso de la topología subyacente y admite un almacén común para UGC.

Para obtener más información acerca de la persistencia del contenido de la comunidad y las implementaciones recomendadas, consulte:

* [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md), que analiza las opciones de almacenamiento SRP disponibles para UGC.
* [Topologías recomendadas](/help/communities/topologies.md), que analiza topologías basadas en casos de uso y opciones de SRP.
* [AEM Actualización a comunidades de 6.5](/help/communities/upgrade.md)AEM , que proporciona información útil sobre UGC al pasar a la versión 6.5 del.

## Consolas de Communities {#communities-consoles}

En el entorno de creación, la consola de navegación global proporciona acceso a [Consola Communities](/help/communities/consoles.md), que contiene:

* consola [Sitios](/help/communities/sites-console.md)

   * Creación del sitio
   * Edición del sitio
   * Administración del sitio
   * [Grupos de comunidad](/help/communities/groups.md) consolar

* [Moderación](/help/communities/moderation.md) consolar

   * IU de moderación masiva común para entornos de creación y publicación.
   * Nuevos criterios de filtrado.

* [Miembros y grupos](/help/communities/members.md) consolas de administración

   * Proporciona la capacidad de crear y administrar usuarios (miembros) de publicación desde el entorno de creación.
   * Proporciona la capacidad de prohibir miembros.
   * Proporciona la capacidad de crear y administrar grupos de usuarios del lado de la publicación (grupos de miembros) desde el entorno de creación.

* [Informes](/help/communities/reports.md) consolar

   * Proporciona la capacidad de generar informes sobre asignaciones, entradas y vistas.

* [Recursos](/help/communities/resources.md) consolar

   * Proporciona la capacidad de crear recursos de habilitación y rutas de aprendizaje.
   * Proporciona acceso a informes sobre recursos de habilitación y rutas de aprendizaje.

La consola de herramientas globales proporciona acceso a las siguientes herramientas de Communities:

* [Plantillas de sitio](/help/communities/tools.md#sitetemplatesconsole) consolar

   * Cree y administre plantillas de sitios de la comunidad.

* [Plantillas de grupo](/help/communities/tools.md#grouptemplatesconsole) consolar

   * Cree y administre plantillas de grupos de la comunidad.

* [Funciones de comunidad](/help/communities/tools.md#communityfunctionsconsole) consolar

   * Crear y administrar funciones de la comunidad.

* [Configuración de almacenamiento](/help/communities/tools.md#storageconfiguratonconsole) consolar

   * Seleccione y configure el [almacén común](/help/communities/working-with-srp.md) para el sitio.

* [Guía de componentes](/help/communities/components-guide.md)

   * Un sitio de muestra, [Componentes de la comunidad](https://localhost:4502/editor.html/content/community-components/en.html), que proporciona una muestra de todos los componentes de Communities con su configuración predeterminada y la capacidad de experimentar con ellos.

## Plantillas de sitio de la comunidad {#community-site-templates}

La creación del sitio de la comunidad se basa en la selección de una plantilla de sitio de la comunidad para configurar rápidamente un sitio de la comunidad que sea independiente de cualquier sitio de muestra.

Una plantilla de sitio de comunidad, compuesta por funciones de comunidad y plantillas de grupo de comunidad, proporciona la estructura para un sitio de comunidad, incluidos el inicio de sesión, los perfiles de usuario, los mensajes, el menú del sitio, las funciones de búsqueda, establecimiento de temas y promoción de la marca.

Consulte la [Consola Plantillas del sitio](/help/communities/sites.md).

## Funciones de comunidad {#community-functions}

Las características que se esperan de una experiencia de comunidad son bien conocidas. Con AEM Communities, estas funciones están disponibles como componentes básicos, conocidos como funciones de la comunidad.

AEM Las funciones de la comunidad son páginas normales, ya que incluyen componentes conectados entre sí en una función que se incorpora fácilmente en una plantilla de sitio de la comunidad.

Consulte la [Consola de funciones de comunidad](/help/communities/functions.md).

## Grupos de la comunidad y plantillas de grupo {#community-groups-and-group-templates}

La función de grupos de comunidad permite que usuarios autorizados y miembros de la comunidad creen dinámicamente una subcomunidad dentro de un sitio de comunidad, tanto desde el entorno de creación como de publicación.

Desde el entorno de creación, los grupos de comunidad (subcomunidades) pueden crearse dentro de un sitio de comunidad existente o anidarse dentro de un grupo existente, cuando la estructura de la plantilla contenga la variable [Función Grupos](/help/communities/functions.md#groups-function).

La creación de un grupo de comunidad requiere la selección de una plantilla de grupo de comunidad que proporcione el diseño de las páginas de grupo de comunidad. Cuando se agrega una función Grupos a una estructura de plantilla, se configura para especificar una plantilla de grupo o para proporcionar una opción de plantillas en el momento en que se crea un nuevo grupo de comunidad.

Consulte también lo siguiente:

* [Consola Grupos de sitio](/help/communities/groups.md) para crear subcomunidades en el entorno de creación.
* [Consola de plantillas de grupo](/help/communities/tools-groups.md) para crear la estructura del sitio para grupos.
* [Introducción a AEM Communities](/help/communities/getting-started.md) para ver un tutorial que le ayudará a crear rápidamente un sitio de comunidad que incluya grupos anidados.

## Componentes de la comunidad {#community-components}

El [componentes de la comunidad](/help/communities/author-communities.md) AEM desde el cual se crea un sitio de la comunidad puede utilizarse para agregar características de Communities a cualquier Sitio de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad de la comunidad.

El [guía de componentes de la comunidad](/help/communities/components-guide.md) está disponible para la exploración interactiva de los componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidad de participación {#engagement-community}

Una comunidad de participación es un sitio de la comunidad centrado en atraer clientes para informar, solicitar comentarios y permitir que los clientes interactúen como miembros de la comunidad.

Las funciones de una comunidad de participación pueden incluir:

* Inicio de sesión
* Mensajes
* Foros
* Comentarios
* Críticas
* Clasificaciones
* Votación
* Blogs
* Grupos
* Calendarios
* Traducción
* Moderación
* Notificaciones
* Puntuación y distintivos
* Informes de Analytics

Para experimentar la facilidad de crear rápidamente una nueva comunidad de participación, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

### Comunidad de habilitación {#enablement-community}

Una comunidad de habilitación es un sitio de la comunidad que incluye funciones para aprendizaje en línea.

Las funciones de una comunidad de habilitación pueden incluir:

* Todas las características de un [comunidad de participación](#engagement-community).
* capacidad para asignar contenido y aprendizaje. recursos para miembros y grupos de miembros.
* Admite contenido SCORM, como cuestionarios y pruebas.
* Seguimiento de la finalización de asignaciones.
* Acceso a informes y análisis.
* La capacidad de mantener una conversación sobre un recurso de aprendizaje a través de foros, mensajes, comentarios y valoraciones.

Se puede crear una comunidad de habilitación cuando la variable [Se ha configurado el complemento de habilitación](/help/communities/enablement.md), que requiere licencias adicionales para su uso en entornos de producción. Un sitio de comunidad de habilitación incluirá lo siguiente [función asignaciones](#community-functions).

Para experimentar la facilidad de crear una nueva comunidad de habilitación, visite [Introducción a AEM Communities para la habilitación](/help/communities/getting-started-enablement.md).

## AEM Máquina de demostración {#aem-demo-machine}

El [AEM Máquina de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM gestiona y ejecuta demostraciones para la creación de informes de [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicaciones](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) y [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que a menudo requieren más configuración que simplemente iniciar una instancia de QuickStart. AEM La máquina de demostración de la configurará más [infraestructura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) como MongoDB, Solr, MySQL, FFmpeg y servidores de correo electrónico.

AEM La máquina de demostración de la incluye:

* A [interfaz gráfica de usuario](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts ANT de Apache con configuración [propiedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) y [objetivos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Paquetes para instalar.

AEM AEM AEM AEM AEM AEM La máquina de demostración de la se probó con éxito con CQ 5.5, CQ 5.6.1, 6.0, 6.1, 6.2, 6.3 y 6.4 en Windows, MacOS y Linux.

AEM AEM La máquina de demostración de la requiere una licencia válida de la misma.

>[!NOTE]
>
>Ver una [presentación de vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) AEM a la máquina de demostración de la (13:26).

## Documentación de AEM Communities {#aem-communities-documentation}

* Visita [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas.
* Visita [Administración de sitios de Communities](administer-landing.md) para obtener información sobre la creación de un sitio de comunidad, la adición de grupos de comunidad, la configuración de plantillas de sitios de comunidad, la moderación del contenido de la comunidad, la administración de miembros, el etiquetado, las notificaciones, la puntuación y las insignias.
* Visita [Desarrollo de comunidades](communities.md) para obtener más información sobre el marco de trabajo de componentes sociales (SCF) y personalizar los componentes y las funciones de las Comunidades.
* Visita [Componentes de comunidades de creación](author-communities.md) para aprender a crear y configurar componentes de Communities.
