---
title: Información general sobre comunidades AEM
seo-title: Información general sobre comunidades AEM
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
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Información general sobre comunidades AEM{#aem-communities-overview}

Las comunidades de Adobe Experience Manager (AEM) ofrecen la posibilidad de crear rápidamente un sitio de comunidad local que tenga un rendimiento y una gestión mejorados, y que anime a los visitantes a convertirse en miembros valiosos de la comunidad.

Póngase en contacto con el representante de cuentas para obtener información sobre las licencias de AEM Communities, así como licencias adicionales para funciones de habilitación y Adobe Analytics.

## Funciones de comunidades {#communities-features}

Las comunidades AEM permiten el desarrollo de una relación con los visitantes del sitio, que:

* **información** a través de blogs, preguntas y respuestas y calendarios de eventos,
* mientras que **obtener perspectivas **a través de foros, comentarios y otro contenido de la comunidad, a menudo denominado contenido generado por el usuario (UGC).
* Permite** moderación **por miembros de confianza en el entorno de publicación,
* **inicio de sesión social **con Twitter y Facebook,
* **traducción** en línea del contenido de la comunidad,
* **creación de grupos comunitarios **desde el sitio comunitario publicado,
* **anotar **conceder insignias,
* **uso compartido** de archivos,
* **notificaciones **y flujos **de** actividad,

* permite **etiquetar** (@mención) a otros miembros registrados en Contenido generado por el usuario, para atraer su atención.
* Admite la navegación **mediante** teclado en componentes de habilitación (por ejemplo, Reproducción de catálogo y curso, Asignaciones, Biblioteca de archivos).

Las características de las comunidades se pueden demostrar con la [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible públicamente en GitHub.com o con la nueva implementación de referencia de We.Retail.

## Sitios de la comunidad {#community-sites}

Un sitio de comunidad es un sitio de AEM creado mediante un sencillo asistente que resulta en un sitio web con muchas funciones comunes preprogramadas en el sitio.

Asistente para la creación [del sitio](/help/communities/sites-console.md):

* ensambla las características del sitio, según la plantilla [del sitio de](/help/communities/sites.md) comunidad seleccionada, que es:

   * creado a partir de funciones [comunitarias](#community-functions)
   * función opcional de grupos [de](#communitygroups) comunidad

* utiliza la configuración:

   * moderación
   * login
   * traducción

* proporciona funciones esenciales:

   * diseño interactivo:
usa temas de [Twitter Bootstrap](https://getbootstrap.com)

   * login :
autorregistro, inicio de sesión [](/help/communities/social-login.md)social, perfiles de usuario

   * notificaciones:
los miembros ven los eventos que les interesan y el contenido generado por el usuario donde se [@mencionan](/help/communities/overview.md#mentionssupport).

   * mensajería:
los miembros pueden enviar o recibir mensajes dentro del sitio de la comunidad
   * search:
capacidad de búsqueda dentro del sitio de la comunidad
   * cambio de idioma:
capacidad para seleccionar un idioma para un sitio [multilingüe](/help/sites-administering/translation.md)

   * administración:
acceso para miembros autorizados a moderar y administrar usuarios dentro del sitio de la comunidad

* elimina muchos pasos de creación a nivel de página:

   * marca:
carga opcional de una imagen de pancarta para mostrarla en todas las páginas del sitio de la comunidad
   * menú de navegación:
se proporcionan vínculos de navegación para las funciones incluidas en la plantilla de sitio de comunidad

Para disfrutar de la facilidad de crear rápidamente un nuevo sitio de comunidad, visite [Introducción a las comunidades](/help/communities/getting-started.md)de AEM.

## Persistencia del contenido de la comunidad {#community-content-persistence}

Para mejorar el rendimiento y la sincronización del contenido de la comunidad, AEM Communities necesita un almacén común específico para el contenido generado por el usuario (UGC) compartido entre todas las instancias de AEM (autor y publicación).

Se puede acceder fácilmente al contenido de la comunidad a través del proveedor de recursos de almacenamiento (SRP), que proporciona una capa para separar el acceso de la topología subyacente y admite un almacén común para UGC.

Para obtener más información sobre la persistencia del contenido de la comunidad y las implementaciones recomendadas, consulte:

* [Almacenamiento](/help/communities/working-with-srp.md)de contenido de comunidad, que analiza las opciones de almacenamiento SRP disponibles para UGC.
* [Topologías](/help/communities/topologies.md)recomendadas, que analiza las topologías basadas en el caso de uso y la elección de SRP.
* [Actualización a AEM 6.5 Communities](/help/communities/upgrade.md), que proporciona información útil sobre UGC al pasar a AEM 6.5.

## Consolas de comunidades {#communities-consoles}

En el entorno de creación, la consola de navegación global proporciona acceso a la consola [](/help/communities/consoles.md)Comunidades, que contiene:

* [Consola Sitios](/help/communities/sites-console.md)

   * creación de sitios
   * edición del sitio
   * administración del sitio
   * [Consola de grupos](/help/communities/groups.md) de comunidad

* [Consola de moderación](/help/communities/moderation.md)

   * IU de moderación masiva común para entornos de creación y publicación
   * nuevos criterios de filtrado

* [Consolas de administración de miembros y grupos](/help/communities/members.md)

   * permite crear y administrar usuarios de publicación (miembros) desde el entorno de creación
   * permite prohibir miembros
   * permite crear y administrar grupos de usuarios del lado de la publicación (grupos de miembros) desde el entorno de creación

* [Consola de informes](/help/communities/reports.md)

   * permite generar informes sobre asignaciones, anuncios y vistas

* [Consola de recursos](/help/communities/resources.md)

   * permite crear recursos de habilitación y rutas de aprendizaje
   * proporciona acceso a informes sobre recursos de habilitación y rutas de aprendizaje

La consola de herramientas globales proporciona acceso a las siguientes herramientas de Communities:

* [Consola Plantillas](/help/communities/tools.md#sitetemplatesconsole) de sitio

   * crear y administrar plantillas de sitio de comunidad

* [Consola Plantillas](/help/communities/tools.md#grouptemplatesconsole) de grupo

   * crear y administrar plantillas de grupo de comunidad

* [Consola de funciones](/help/communities/tools.md#communityfunctionsconsole) de comunidad

   * crear y administrar funciones de comunidad

* [Consola de configuración](/help/communities/tools.md#storageconfiguratonconsole) de almacenamiento

   * seleccionar y configurar el almacén [](/help/communities/working-with-srp.md) común para el sitio

* [Guía de componentes](/help/communities/components-guide.md)

   * un sitio de muestra, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), que proporciona una muestra de todos los componentes de Communities con su configuración predeterminada y la capacidad de experimentar con ellos

## Plantillas de sitio de la comunidad {#community-site-templates}

La creación del sitio de la comunidad se basa en la selección de una plantilla del sitio de la comunidad para configurar rápidamente un sitio de la comunidad que sea independiente de cualquier sitio de muestra.

Una plantilla de sitio de comunidad, compuesta de funciones de comunidad y plantillas de grupo de comunidad, proporciona la estructura de un sitio de comunidad, incluyendo inicio de sesión, perfiles de usuario, mensajes, menú del sitio, búsqueda, tema y características de marca.

Consulte la consola [Plantillas](/help/communities/sites.md)del sitio.

## Funciones de comunidad {#community-functions}

Las características que se esperan de una experiencia comunitaria son bien conocidas. Con AEM Communities, estas funciones están disponibles como elementos básicos, conocidos como funciones de comunidad.

Las funciones de la comunidad son páginas normales de AEM que incluyen componentes conectados en una función que se incorpora fácilmente a una plantilla de sitio de la comunidad.

Consulte la consola [Funciones de](/help/communities/functions.md)comunidad.

## Grupos de la comunidad y plantillas de grupo {#community-groups-and-group-templates}

La función de grupos de comunidad es la capacidad para que una subcomunidad sea creada dinámicamente dentro de un sitio de comunidad por usuarios autorizados y miembros de la comunidad desde los entornos de creación y publicación.

Desde el entorno de creación, los grupos de comunidad (subcomunidades) pueden crearse dentro de un sitio de comunidad existente o anidarse dentro de un grupo existente, cuando la estructura de la plantilla contenga la función [](/help/communities/functions.md#groups-function)Grupos.

La creación de un grupo de comunidad requiere la selección de una plantilla de grupo de comunidad que proporcione el diseño de las páginas de grupo de la comunidad. Cuando se agrega una función Grupos a una estructura de plantilla, se configura para especificar una plantilla de grupo o para proporcionar una selección de plantillas en el momento en que se crea un nuevo grupo de comunidad.

Consulte también:

* [Consola](/help/communities/groups.md) Grupos del sitio para crear subcomunidades en el entorno de creación
* [Consola](/help/communities/tools-groups.md) Plantillas de grupo para crear la estructura de sitio para grupos
* [Introducción a Comunidades](/help/communities/getting-started.md) AEM para ver un tutorial sobre la creación rápida de un sitio de comunidad que incluya grupos anidados

## Componentes de comunidad {#community-components}

Los componentes [de](/help/communities/author-communities.md) comunidad a partir de los cuales se crea un sitio de comunidad pueden utilizarse para agregar funciones de comunidades a cualquier sitio de AEM.

La guía [de componentes de](/help/communities/components-guide.md) comunidad está disponible para la exploración interactiva de los componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidad de participación {#engagement-community}

Una comunidad de participación es un sitio de la comunidad dedicado a atraer clientes para que informen, soliciten comentarios y permitan a los clientes interactuar como miembros de la comunidad.

Las características de una comunidad de participación pueden incluir:

* login
* mensajería
* foros
* comentarios
* críticas
* clasificaciones
* votación
* blogs
* grupos
* calendarios
* traducción
* moderación
* notificaciones
* puntuación y distintivos
* informes de análisis

Para disfrutar de la facilidad de crear rápidamente una nueva comunidad de participación, visite [Introducción a las comunidades](/help/communities/getting-started.md)de AEM.

### Comunidad de habilitación {#enablement-community}

Una comunidad de habilitación es un sitio de la comunidad que incluye funciones para el aprendizaje en línea.

Las características de una comunidad de habilitación pueden incluir:

* todas las características de una comunidad de [participación](#engagement-community)
* capacidad para asignar contenido y recursos de aprendizaje a miembros y grupos de miembros
* admite contenido SCORM, como cuestionarios y pruebas
* seguimiento de la finalización de asignaciones
* acceso a informes y análisis
* la capacidad de tener una conversación sobre un recurso de aprendizaje a través de foros, mensajes, comentarios y valoraciones

Se puede crear una comunidad de habilitación cuando se configura [el complemento](/help/communities/enablement.md)Habilitación, que requiere licencias adicionales para su uso en un entorno de producción. Un sitio de comunidad de habilitación incluirá la función [](#community-functions)asignaciones.

Para disfrutar de la facilidad de crear una nueva comunidad de habilitación, visite [Introducción a Comunidades de AEM para la habilitación](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

El equipo [de demostración de](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM administra y ejecuta demostraciones para [sitios](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)de AEM, [recursos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [aplicaciones](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)y formularios, que a menudo requieren más configuración que simplemente iniciar una instancia de QuickStart. AEM Demo Machine configurará [infraestructura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional como MongoDB, Solr, MySQL, FFmpeg y servidores de correo electrónico.

AEM Demo Machine incluye:

* una interfaz de usuario [gráfica](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Secuencias de comandos Apache ANT con [propiedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) y [destinos configurables](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* paquetes para instalar

AEM Demo Machine se probó correctamente con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 y AEM 6.4 en Windows, MacOS y Linux.

AEM Demo Machine requiere una licencia de AEM válida.

>[!NOTE]
>
>Vea una introducción [en](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) vídeo a AEM Demo Machine (13:26).

## Documentación de AEM Communities {#aem-communities-documentation}

* Visite [Implementar comunidades](/help/communities/deploy-communities.md) para conocer las implementaciones recomendadas.
* Visite [Administración de sitios](/help/communities/administer-landing.md) de comunidades para obtener información sobre cómo crear un sitio de comunidad, agregar grupos de la comunidad, configurar plantillas de sitio de la comunidad, moderar contenido de la comunidad, administrar miembros, etiquetado, notificaciones, puntuación y distintivos.
* Visite [Desarrollar comunidades](/help/communities/communities.md) para conocer el marco de componentes sociales (SCF) y personalizar componentes y características de Comunidades.
* Visite [Creación de componentes](/help/communities/author-communities.md) de comunidades para obtener información sobre cómo crear y configurar componentes de comunidades.

