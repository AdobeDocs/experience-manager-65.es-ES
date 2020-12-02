---
title: Información general de AEM Communities
seo-title: Información general de AEM Communities
description: Información general sobre las funciones y la configuración de AEM Communities
seo-description: Información general sobre las funciones y la configuración de AEM Communities
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 4533fa42fa3fa9f157d5ca8fee1251005b1d587e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---


# Información general de AEM Communities {#aem-communities-overview}

Las comunidades de Adobe Experience Manager (AEM) ofrecen la posibilidad de crear rápidamente un sitio de comunidad local que tenga un rendimiento y una gestión mejorados, y que anime a los visitantes a convertirse en miembros valiosos de la comunidad.

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Funciones de comunidades {#communities-features}

AEM Communities permite el desarrollo de una relación con los visitantes del sitio, que:

* **** Información a través de blogs, preguntas y respuestas y calendarios de evento,
* Mientras que **obtiene perspectivas** a través de foros, comentarios y otro contenido de la comunidad, generalmente denominado contenido generado por el usuario (UGC).
* Permite **moderación** por miembros de confianza en el entorno de publicación,
* **Inicio** de sesión social con Twitter y Facebook,
* **Traducción** en línea del contenido de la comunidad,
* **Creación** de grupos comunitarios a partir del sitio de la comunidad publicado,
* **Puntuación** para asignar distintivos,
* **Uso compartido** de archivos,
* **** Notificaciones y flujos **** de actividad,
* Permite **etiquetado** (@mención) a otros miembros registrados en Contenido generado por el usuario, para atraer su atención.
* Admite **navegación mediante el teclado** en componentes de habilitación (por ejemplo, Reproducción de catálogo y curso, Asignaciones, Biblioteca de archivos).

Las características de las comunidades se pueden demostrar con la [AEM máquina de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible públicamente en GitHub.com o con la nueva implementación de referencia de We.Retail.

## Sitios de la comunidad {#community-sites}

Un sitio de comunidad es un sitio AEM creado con un simple asistente que resulta en un sitio web con muchas características comunes preprogramadas en el sitio.

El [asistente para la creación del sitio](/help/communities/sites-console.md):

* Ensamble las características del sitio, en base a la [plantilla de sitio de comunidad](/help/communities/sites.md) seleccionada, que es:

   * creado a partir de [funciones de comunidad](#community-functions)
   * función opcional [grupos de comunidad](#communitygroups)

* Utiliza la configuración para configurar:

   * moderación
   * login
   * traducción

* Proporciona funciones esenciales:

   * Diseño adaptable: usa [temáticas de Bootstrap de Twitter](https://getbootstrap.com)

   * Inicio de sesión: autorregistro, [inicio de sesión social](/help/communities/social-login.md), perfiles de usuario

      * Notificaciones:
los miembros ven eventos de relevancia para ellos y contenido generado por el usuario donde se [@han](/help/communities/overview.md#mentionssupport).

      * Mensajería: los miembros pueden enviar o recibir mensajes dentro del sitio de la comunidad.
      * Buscar: capacidad para realizar búsquedas dentro del sitio de la comunidad.
      * Cambio de idioma: capacidad para seleccionar un idioma para un [sitio multilingüe](/help/sites-administering/translation.md).

      * Administración: acceso para miembros autorizados a moderar y administrar usuarios dentro del sitio de la comunidad.

* Elimina muchos pasos de creación a nivel de página:

   * Marca: carga opcional de una imagen de pancarta para mostrarla en todas las páginas del sitio de la comunidad
   * Menú de navegación: se proporcionan vínculos de navegación para las funciones incluidas en la plantilla de sitio de la comunidad.

Para experimentar la facilidad de crear rápidamente un nuevo sitio de comunidad, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

## Persistencia del contenido de la comunidad {#community-content-persistence}

Para mejorar el rendimiento y la sincronización del contenido de la comunidad, AEM Communities requiere un almacén común específico para el contenido generado por el usuario (UGC) compartido entre todas las instancias de AEM (autor y publicación).

Se puede acceder fácilmente al contenido de la comunidad a través del proveedor de recursos de almacenamiento (SRP), que proporciona una capa para separar el acceso de la topología subyacente y admite un almacén común para UGC.

Para obtener más información sobre la persistencia del contenido de la comunidad y las implementaciones recomendadas, consulte:

* [Community Content Almacenamiento](/help/communities/working-with-srp.md), que analiza las opciones de almacenamiento de SRP disponibles para UGC.
* [Topologías](/help/communities/topologies.md) recomendadas, que analiza las topologías basadas en el caso de uso y la elección de SRP.
* [Actualización a AEM comunidades](/help/communities/upgrade.md) 6.5, que proporciona información útil con respecto a UGC al pasar a AEM 6.5.

## Consolas de comunidades {#communities-consoles}

En el entorno de creación, la consola de navegación global proporciona acceso a la consola [Communities](/help/communities/consoles.md), que contiene:

* consola [Sitios](/help/communities/sites-console.md)

   * Creación de sitios
   * Edición del sitio
   * Administración de sitios
   * [Community ](/help/communities/groups.md) Groupsconsole

* [](/help/communities/moderation.md) Moderationconsole

   * IU común de moderación masiva para entornos de creación y publicación.
   * Nuevos criterios de filtrado.

* [Consolas de administración de miembros y ](/help/communities/members.md) grupos

   * Proporciona la capacidad de crear y administrar usuarios de publicación (miembros) desde el entorno de creación.
   * Permite prohibir miembros.
   * Proporciona la capacidad de crear y administrar grupos de usuarios del lado de la publicación (grupos de miembros) desde el entorno de creación.

* [](/help/communities/reports.md) Reportsconsole

   * Proporciona la capacidad de generar informes sobre asignaciones, publicaciones y vistas.

* [](/help/communities/resources.md) Resourcesconsole

   * Proporciona la capacidad de crear recursos de habilitación y rutas de aprendizaje.
   * Proporciona acceso a informes sobre recursos de habilitación y rutas de aprendizaje.

La consola de herramientas globales proporciona acceso a las siguientes herramientas de Comunidades:

* [Site ](/help/communities/tools.md#sitetemplatesconsole) Templatesconsole

   * Cree y administre plantillas de sitio de comunidad.

* [Consola de ](/help/communities/tools.md#grouptemplatesconsole) plantillas de grupo

   * Cree y administre plantillas de grupo de comunidad.

* [Community ](/help/communities/tools.md#communityfunctionsconsole) Functionsconsole

   * Cree y administre funciones de comunidad.

* [Almacenamiento ](/help/communities/tools.md#storageconfiguratonconsole) Configurationconsole

   * Seleccione y configure el [almacén común](/help/communities/working-with-srp.md) para el sitio.

* [Guía de componentes](/help/communities/components-guide.md)

   * Un sitio de muestra, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), que proporciona una muestra de todos los componentes de Communities con su configuración predeterminada y la capacidad de experimentar con ellos.

## Plantillas de sitio de la comunidad {#community-site-templates}

La creación del sitio de la comunidad se basa en la selección de una plantilla del sitio de la comunidad para configurar rápidamente un sitio de la comunidad que sea independiente de cualquier sitio de muestra.

Una plantilla de sitio de comunidad, compuesta de funciones de comunidad y plantillas de grupo de comunidad, proporciona la estructura de un sitio de comunidad, incluyendo inicio de sesión, perfiles de usuario, mensajes, menú del sitio, búsqueda, tema y características de marca.

Consulte la consola [Plantillas de sitio](/help/communities/sites.md).

## Funciones de comunidad {#community-functions}

Las características que se esperan de una experiencia comunitaria son bien conocidas. Con AEM Communities, estas funciones están disponibles como componentes básicos, conocidas como funciones de la comunidad.

Las funciones de la comunidad son normales AEM las páginas incluyen componentes conectados en una función que se incorpora fácilmente a una plantilla de sitio de la comunidad.

Consulte la consola [Funciones de comunidad](/help/communities/functions.md).

## Grupos de la comunidad y plantillas de grupo {#community-groups-and-group-templates}

La función de grupos de comunidad es la capacidad para que una subcomunidad sea creada dinámicamente dentro de un sitio de comunidad por usuarios autorizados y miembros de la comunidad desde los entornos de creación y publicación.

Desde el entorno de creación, se pueden crear grupos de comunidad (subcomunidades) dentro de un sitio de comunidad existente o anidados dentro de un grupo existente, cuando la estructura de la plantilla contenga la función [Grupos](/help/communities/functions.md#groups-function).

La creación de un grupo de comunidad requiere la selección de una plantilla de grupo de comunidad que proporcione el diseño de las páginas de grupo de la comunidad. Cuando se agrega una función Grupos a una estructura de plantilla, se configura para especificar una plantilla de grupo o para proporcionar una selección de plantillas en el momento en que se crea un nuevo grupo de comunidad.

Consulte también:

* [Grupos del sitio ](/help/communities/groups.md) se conforman para crear subcomunidades en el entorno de creación.
* [Plantillas de grupo ](/help/communities/tools-groups.md) consolas para crear la estructura del sitio para grupos.
* [Introducción a AEM ](/help/communities/getting-started.md) comunidades para ver un tutorial que permite crear rápidamente un sitio de comunidad que incluye grupos anidados.

## Componentes de comunidad {#community-components}

Los [componentes de comunidad](/help/communities/author-communities.md) desde los que se crea un sitio de comunidad pueden utilizarse para agregar características de Communities a cualquier sitio AEM.

La [guía de componentes de comunidad](/help/communities/components-guide.md) está disponible para la exploración interactiva de los componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidad de participación {#engagement-community}

Una comunidad de participación es un sitio de la comunidad dedicado a atraer clientes para que informen, soliciten comentarios y permitan a los clientes interactuar como miembros de la comunidad.

Las características de una comunidad de participación pueden incluir:

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
* Sistema de informes de Analytics

Para experimentar la facilidad de crear rápidamente una nueva comunidad de participación, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

### Comunidad de habilitación {#enablement-community}

Una comunidad de habilitación es un sitio de la comunidad que incluye funciones para el aprendizaje en línea.

Las características de una comunidad de habilitación pueden incluir:

* Todas las características de una [comunidad de participación](#engagement-community).
* capacidad para asignar contenido y aprendizaje. recursos para miembros y grupos miembros.
* Admite contenido SCORM, como cuestionarios y pruebas.
* Seguimiento de la finalización de asignaciones.
* Acceso a sistema de informes y análisis.
* La capacidad de tener una conversación sobre un recurso de aprendizaje a través de foros, mensajes, comentarios y valoraciones.

Se puede crear una comunidad de habilitación cuando se configura el complemento [Habilitación](/help/communities/enablement.md), que requiere licencias adicionales para su uso en un entorno de producción. Un sitio de comunidad de habilitación incluirá la función [asignaciones](#community-functions).

Para experimentar la facilidad de crear una nueva comunidad de habilitación, visite [Introducción a AEM Communities para habilitación](/help/communities/getting-started-enablement.md).

## Máquina de demostración de AEM {#aem-demo-machine}

La [AEM Máquina de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) administra y ejecuta demostraciones para AEM [Sitios](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Recursos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicaciones](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) y [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que a menudo requieren más configuración que simplemente iniciar un inicio rápido instancia. AEM Demo Machine configurará una [infraestructura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional como MongoDB, Solr, MySQL, FFmpeg y servidores de correo electrónico.

La AEM Demo Machine incluye:

* Una [interfaz gráfica de usuario](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Secuencias de comandos Apache ANT con [propiedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) y [destinatarios](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configurables.

* Paquetes para instalar.

La AEM Demo Machine se probó correctamente con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 y AEM 6.4 en Windows, MacOS y Linux.

La AEM Demo Machine requiere una licencia de AEM válida.

>[!NOTE]
>
>Vista de una [introducción de vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) en el equipo de demostración de AEM (13:26).

## Documentación de AEM Communities {#aem-communities-documentation}

* Visite [Implementación de comunidades](deploy-communities.md) para conocer las implementaciones recomendadas.
* Visite [Administración de sitios de comunidades](administer-landing.md) para obtener información sobre cómo crear un sitio de comunidad, agregar grupos de comunidades, configurar plantillas de sitio de comunidad, moderar contenido de comunidad, administrar miembros, etiquetado, notificaciones, puntuación y distintivos.
* Visite [Desarrollar comunidades](communities.md) para conocer el marco de componentes sociales (SCF) y personalizar componentes y características de Communities.
* Visite [Creación de componentes de comunidades](author-communities.md) para obtener información sobre cómo crear y configurar componentes de comunidades.

