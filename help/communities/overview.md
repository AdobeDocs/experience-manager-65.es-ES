---
title: Información general de AEM Communities
description: Obtenga información acerca de los aspectos básicos de las funciones y configuración de las comunidades de Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Información general de AEM Communities {#aem-communities-overview}

Las comunidades de Adobe Experience Manager AEM () le permiten crear rápidamente un sitio de comunidad local que mejore el rendimiento, la administración del sitio y fomente la conversión de los visitantes del sitio en miembros valiosos de la comunidad.

## Características de Communities {#communities-features}

AEM Communities permite desarrollar una relación con los visitantes del sitio que:

* **Informa** a través de blogs, preguntas y respuestas y calendarios de eventos,
* Mientras **obtiene perspectivas** a través de foros, comentarios y otro contenido de la comunidad, a menudo se denomina contenido generado por el usuario (UGC).
* Permite la **moderación** por miembros de confianza en el entorno de Publish,
* **Inicio de sesión social** con Twitter y Facebook,
* **Traducción en línea** del contenido de la comunidad,
* **Creación de grupos de comunidad** a partir del sitio de comunidad publicado,
* **Puntuación** para otorgar insignias,
* **Uso compartido de archivos**,
* **Notificaciones** y **flujos de actividad**,
* Permite que **etiqueten** (@mention) otros miembros registrados en el contenido generado por el usuario para llamar su atención.

AEM Las características de las comunidades se pueden demostrar usando la máquina de demostración [disponible públicamente en GitHub.com o con la nueva implementación de referencia de `We.Retail`.](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)

## Sitios de la comunidad {#community-sites}

AEM Un sitio de la comunidad es un sitio de la comunidad creado mediante un asistente simple que da como resultado un sitio web con muchas funciones comunes precableadas en el sitio.

El [asistente para la creación de sitios](/help/communities/sites-console.md):

* Ensambla características del sitio, basándose en la [plantilla del sitio de la comunidad](/help/communities/sites.md) seleccionada, que es:

   * se creó a partir de [funciones de la comunidad](#community-functions)
   * característica [grupos de la comunidad](#communitygroups) opcional

* Utiliza la configuración para configurar:

   * moderación
   * login
   * traducción

* Proporciona funciones esenciales:

   * Diseño interactivo: utiliza [temas de Bootstrap de Twitter](https://getbootstrap.com)

   * Iniciar sesión : autorregistro, [inicio de sesión en redes sociales](/help/communities/social-login.md), perfiles de usuario

      * Notificaciones:
los miembros ven eventos de relevancia para ellos y contenido generado por el usuario donde están [@mentioned](/help/communities/overview.md#mentionssupport).

      * Mensajes: los miembros pueden enviar o recibir mensajes dentro del sitio de la comunidad.
      * Buscar: capacidad de buscar en el sitio de la comunidad.
      * Cambio de idioma: capacidad para seleccionar un idioma para un [sitio multilingüe](/help/sites-administering/translation.md).

      * Administración: acceso para miembros autorizados a moderar y administrar usuarios dentro del sitio de la comunidad.

* Elimina muchos pasos de la creación en el nivel de página:

   * Personalización de marca: carga opcional de una imagen de titular para mostrarla en todas las páginas del sitio de la comunidad.
   * Menú de navegación: se proporcionan vínculos de navegación para las funciones incluidas en la plantilla del sitio de la comunidad.

Para experimentar la facilidad de crear rápidamente un sitio de la comunidad, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

## Persistencia del contenido de comunidad {#community-content-persistence}

Para mejorar el rendimiento y la sincronización del contenido de la comunidad, AEM Communities AEM requiere un almacén común específico para el contenido generado por el usuario (UGC) compartido entre todas las instancias (de autor y publicación) de los.

Se puede acceder fácilmente al contenido de la comunidad a través del proveedor de recursos de almacenamiento (SRP), que proporciona una capa para separar el acceso de la topología subyacente y admite un almacén común para UGC.

Para obtener más información acerca de la persistencia del contenido de la comunidad y las implementaciones recomendadas, consulte:

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md)—analiza las opciones de almacenamiento SRP disponibles para UGC.
* [Topologías recomendadas](/help/communities/topologies.md): analiza las topologías en función del caso de uso y la opción de SRP.
* AEM AEM [Actualización a comunidades de la versión 6.5 de la versión de la versión &#x200B;](/help/communities/upgrade.md): proporciona información útil acerca de UGC cuando se pasa a la versión 6.5 de la versión de la versión de la versión de la versión 6.5.

## Consolas de Communities {#communities-consoles}

En el entorno de creación, la consola de navegación global proporciona acceso a [Consola de Communities](/help/communities/consoles.md), que contiene:

* consola [Sitios](/help/communities/sites-console.md)

   * Creación del sitio
   * Edición del sitio
   * Administración del sitio
   * Consola de [grupos de la comunidad](/help/communities/groups.md)

* Consola [moderación](/help/communities/moderation.md)

   * IU de moderación masiva común para los entornos de Autor y Publish.
   * Nuevos criterios de filtrado.

* [Miembros y grupos](/help/communities/members.md) consolas de administración

   * Permite crear y administrar usuarios (miembros) de publicación desde el entorno de creación.
   * Le permite prohibir miembros.
   * Permite crear y administrar grupos de usuarios del lado de la publicación (grupos de miembros) desde el entorno de creación.

* Consola [Informes](/help/communities/reports.md)

   * Permite generar informes sobre asignaciones, publicaciones y vistas.

La consola de herramientas globales proporciona acceso a las siguientes herramientas de Communities:

* Consola [Plantillas de sitio](/help/communities/tools.md#sitetemplatesconsole)

   * Cree y administre plantillas de sitios de la comunidad.

* [Plantillas de grupo](/help/communities/tools.md#grouptemplatesconsole) consola

   * Cree y administre plantillas de grupos de la comunidad.

* [Funciones de la comunidad](/help/communities/tools.md#communityfunctionsconsole) consola

   * Crear y administrar funciones de la comunidad.

* Consola [Configuración de almacenamiento](/help/communities/tools.md#storageconfiguratonconsole)

   * Seleccione y configure [almacén común](/help/communities/working-with-srp.md) para el sitio.

* [Guía de componentes](/help/communities/components-guide.md)

   * Un sitio de muestra, [Componentes de la comunidad](https://localhost:4502/editor.html/content/community-components/en.html), proporciona una muestra de todos los componentes de la comunidad con su configuración predeterminada y la capacidad de experimentar con ellos.

## Plantillas de sitio de la comunidad {#community-site-templates}

La creación del sitio de la comunidad se basa en la selección de una plantilla de sitio de la comunidad para configurar rápidamente un sitio de la comunidad que sea independiente de cualquier sitio de muestra.

Una plantilla de sitio de comunidad, compuesta por funciones de comunidad y plantillas de grupo de comunidad, proporciona la estructura para un sitio de comunidad. Incluye funciones de inicio de sesión, perfiles de usuario, mensajería, menú del sitio, búsqueda, establecimiento de temas y promoción de la marca.

Consulte la [consola Plantillas de sitio](/help/communities/sites.md).

## Funciones de la comunidad {#community-functions}

Las características que se esperan de una experiencia de comunidad son bien conocidas. Con AEM Communities, estas funciones están disponibles como componentes básicos, conocidos como funciones de la comunidad.

AEM Las funciones de la comunidad son páginas normales, ya que incluyen componentes conectados entre sí en una función que se incorpora fácilmente en una plantilla de sitio de la comunidad.

Consulte la [consola de funciones de la comunidad](/help/communities/functions.md).

## Grupos de la comunidad y plantillas de grupo {#community-groups-and-group-templates}

La función de grupos de comunidad permite que usuarios autorizados y miembros de la comunidad creen dinámicamente una subcomunidad dentro de un sitio de comunidad, tanto desde el entorno de creación como de publicación.

Desde el entorno de creación, los grupos de comunidad (subcomunidades) pueden crearse dentro de un sitio de comunidad existente o anidarse dentro de un grupo existente, cuando la estructura de la plantilla contiene la función [Grupos](/help/communities/functions.md#groups-function).

La creación de un grupo de comunidad requiere la selección de una plantilla de grupo de comunidad que proporcione el diseño de las páginas del grupo de comunidad. Cuando se agrega una función Grupos a una estructura de plantilla, se configura para especificar una plantilla de grupo o para proporcionar una opción de plantillas en el momento en que se crea un nuevo grupo de comunidad.

Consulte también lo siguiente:

* [Consola de grupos de sitio](/help/communities/groups.md) para crear subcomunidades en el entorno de creación.
* [Consola de plantillas de grupo](/help/communities/tools-groups.md) para crear estructuras de sitio para grupos.
* [Introducción a AEM Communities](/help/communities/getting-started.md) para ver el tutorial que permite crear rápidamente un sitio de comunidad que incluya grupos anidados.

## Componentes de la comunidad {#community-components}

AEM Los [componentes de la comunidad](/help/communities/author-communities.md) a partir de los cuales se ha creado un sitio de la comunidad se pueden usar para agregar características de Communities a cualquier sitio de la comunidad de.

La [guía de componentes de la comunidad](/help/communities/components-guide.md) está disponible para la exploración interactiva de los componentes.

## Comunidad de participación {#engagement-community}

Una comunidad de participación es un sitio de la comunidad centrado en atraer clientes para informar, solicitar comentarios y permitir que los clientes interactúen como miembros de la comunidad.

Las funciones de una comunidad de participación pueden incluir:

* Inicio de sesión
* Mensajes
* Foros
* Comentarios
* Repasos
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

Para experimentar la facilidad de crear rápidamente una comunidad de participación, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

## AEM Máquina de demostración {#aem-demo-machine}

AEM AEM La máquina de demostración [&#128279;](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) administra y ejecuta demostraciones para los sitios [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) y [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que a menudo requieren más configuración que simplemente iniciar una instancia de QuickStart. AEM El equipo de demostración de la máquina de la máquina de la máquina de la demostración configura [Infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional como MongoDB, Solr, MySQL, FFmpeg, y servidores de correo electrónico.

AEM La máquina de demostración de la incluye:

* Una [interfaz gráfica de usuario](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts ANT de Apache con [properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) y [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) que se pueden configurar.

* Paquetes para instalar.

AEM AEM AEM AEM AEM AEM La máquina de demostración de la se probó con éxito con CQ 5.5, CQ 5.6.1, 6.0, 6.1, 6.2, 6.3 y 6.4 en Windows, macOS y Linux®.

AEM AEM La máquina de demostración de la requiere una licencia de uso válida de la misma.

>[!NOTE]
>
>AEM Vea un [vídeo introductorio](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) a la máquina de demostración de la (13:26).

## Documentación de AEM Communities {#aem-communities-documentation}

* Visite [Implementación de comunidades](deploy-communities.md), donde podrá obtener información sobre las implementaciones recomendadas.
* Visite [Sitios de administración de comunidades](administer-landing.md), donde podrá obtener información sobre cómo crear un sitio de comunidad, agregar grupos de comunidad, configurar plantillas de sitios de comunidad, moderar el contenido de la comunidad, administrar miembros, etiquetar, notificar, puntuar e insignias.
* Visite [Desarrollo de comunidades](communities.md), donde podrá obtener información acerca del marco de componentes sociales (SCF) y la personalización de componentes y características de las comunidades.
* Visite [Creación de componentes de comunidades](author-communities.md), donde aprenderá a crear y configurar componentes de comunidades.
