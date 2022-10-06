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

## Funciones de Communities {#communities-features}

AEM Communities permite el desarrollo de una relación con los visitantes del sitio, que:

* **Informaciones** a través de blogs, preguntas y respuestas y calendarios de eventos,
* While **obtención de información** a través de foros, comentarios y otro contenido de la comunidad, denominado a menudo contenido generado por el usuario (UGC).
* Permite **moderación** por miembros de confianza en el entorno de publicación,
* **Inicio de sesión social** con Twitter y Facebook,
* **Traducción en línea** del contenido de la comunidad,
* **Creación de grupos de la comunidad** del sitio de la comunidad publicado,
* **Puntuación** para conceder distintivos,
* **Uso compartido de archivos**,
* **Notificaciones** y **flujos de actividad**,
* Permite **etiquetado** (@mention) otros miembros registrados en Contenido generado por el usuario, para llamar su atención.
* Admite **navegación mediante el teclado** sobre los componentes de habilitación (por ejemplo, Catálogo y Reproducción de cursos, Asignaciones, Biblioteca de archivos) .

Las características de las comunidades se pueden mostrar utilizando la variable [AEM de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible públicamente en GitHub.com o con la nueva implementación de referencia de We.Retail.

## Sitios de la comunidad {#community-sites}

Un sitio de comunidad es un sitio AEM creado con un simple asistente que resulta en un sitio web con muchas funciones comunes preprogramadas en el sitio.

La variable [asistente de creación de sitios](/help/communities/sites-console.md):

* Ensamble las características del sitio, según la selección [plantilla del sitio de la comunidad](/help/communities/sites.md) que es:

   * creado desde [funciones de la comunidad](#community-functions)
   * opcional [grupos de la comunidad](#communitygroups) función

* Utiliza la configuración para configurar:

   * moderación
   * inicio de sesión
   * traducción

* Proporciona características esenciales:

   * Diseño interactivo: uses [Temas del Bootstrap de twitter](https://getbootstrap.com)

   * Iniciar sesión : autoregistro, [inicio de sesión social](/help/communities/social-login.md), perfiles de usuario

      * Notificaciones: los miembros ven eventos de importancia para ellos y contenido generado por el usuario donde se encuentran [@mention](/help/communities/overview.md#mentionssupport).

      * Mensajería: los miembros pueden enviar o recibir mensajes dentro del sitio de la comunidad.
      * Buscar: capacidad para buscar dentro del sitio de la comunidad.
      * Cambio de idioma: capacidad para seleccionar un idioma para un [sitio multilingüe](/help/sites-administering/translation.md).

      * Administración: acceso para miembros autorizados para moderar y administrar usuarios dentro del sitio de la comunidad.

* Elimina muchos pasos de creación a nivel de página:

   * Marcas: carga opcional de una imagen de banner para mostrarla en todas las páginas del sitio de la comunidad
   * Menú de navegación: se proporcionan vínculos de navegación para las funciones incluidas en la plantilla de sitio de la comunidad.

Para experimentar la facilidad de crear rápidamente un nuevo sitio de comunidad, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

## Persistencia de contenido de la comunidad {#community-content-persistence}

Para mejorar el rendimiento y la sincronización del contenido de la comunidad, AEM Communities requiere un almacén común específico para el contenido generado por el usuario (UGC) compartido entre todas las instancias de AEM (autor y publicación).

Se puede acceder fácilmente al contenido de la comunidad a través del proveedor de recursos de almacenamiento (SRP), que proporciona una capa para separar el acceso de la topología subyacente y soporta un almacén común para UGC.

Para obtener más información sobre la persistencia del contenido de la comunidad y las implementaciones recomendadas, consulte:

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md), que analiza las opciones de almacenamiento SRP disponibles para UGC.
* [Topologías recomendadas](/help/communities/topologies.md), que analiza topologías basadas en casos de uso y elección de SRP.
* [Actualización a AEM 6.5 Communities](/help/communities/upgrade.md), que proporciona información útil sobre UGC al pasar a AEM 6.5.

## Consolas de comunidades {#communities-consoles}

En el entorno de creación, la consola de navegación global proporciona acceso al [Consola Comunidades](/help/communities/consoles.md), que contiene:

* consola [Sitios](/help/communities/sites-console.md)

   * Creación de sitios
   * Edición del sitio
   * Administración del sitio
   * [Grupos de la comunidad](/help/communities/groups.md) consola

* [Moderación](/help/communities/moderation.md) consola

   * Interfaz de usuario de moderación masiva común para entornos de creación y publicación.
   * Nuevos criterios de filtrado.

* [Miembros y grupos](/help/communities/members.md) consolas de administración

   * Proporciona la capacidad de crear y administrar usuarios del lado de publicación (miembros) desde el entorno de creación.
   * Permite prohibir miembros.
   * Proporciona la capacidad de crear y administrar grupos de usuarios del lado de publicación (grupos de miembros) desde el entorno de creación.

* [Informes](/help/communities/reports.md) consola

   * Proporciona la capacidad de generar informes sobre asignaciones, publicaciones y vistas.

* [Recursos](/help/communities/resources.md) consola

   * Proporciona la capacidad de crear recursos de habilitación y rutas de aprendizaje.
   * Proporciona acceso a informes sobre recursos de habilitación y rutas de aprendizaje.

La consola de herramientas globales proporciona acceso a las siguientes herramientas de Communities:

* [Plantillas de sitio](/help/communities/tools.md#sitetemplatesconsole) consola

   * Cree y administre plantillas de sitio de la comunidad.

* [Plantillas de grupo](/help/communities/tools.md#grouptemplatesconsole) consola

   * Cree y administre plantillas de grupo de la comunidad.

* [Funciones de la comunidad](/help/communities/tools.md#communityfunctionsconsole) consola

   * Cree y administre funciones de la comunidad.

* [Configuración de almacenamiento](/help/communities/tools.md#storageconfiguratonconsole) consola

   * Seleccione y configure el [tienda común](/help/communities/working-with-srp.md) para el sitio.

* [Guía de componentes](/help/communities/components-guide.md)

   * Un sitio de muestra, [Componentes de comunidad](https://localhost:4502/editor.html/content/community-components/en.html), que proporciona un ejemplo de todos los componentes de Communities con su configuración predeterminada y la capacidad de experimentar con ellos.

## Plantillas de sitio de la comunidad {#community-site-templates}

La creación del sitio de la comunidad se basa en la selección de una plantilla del sitio de la comunidad para configurar rápidamente un sitio de la comunidad que sea independiente de cualquier sitio de muestra.

Una plantilla de sitio de la comunidad, compuesta de funciones de la comunidad y plantillas de grupos de la comunidad, proporciona la estructura de un sitio de la comunidad, que incluye: inicio de sesión, perfiles de usuario, mensajería, menú del sitio, búsqueda, tema y funciones de marca.

Consulte la [Consola Plantillas de sitio](/help/communities/sites.md).

## Funciones de comunidad {#community-functions}

Las características que se esperan de una experiencia comunitaria son bien conocidas. Con AEM Communities, estas funciones están disponibles como componentes básicos, conocidos como funciones de la comunidad.

Las funciones de comunidad son normales AEM las páginas incluyen componentes conectados en una función que se incorpora fácilmente en una plantilla de sitio de la comunidad.

Consulte la [Consola de funciones de comunidad](/help/communities/functions.md).

## Grupos de la comunidad y plantillas de grupo {#community-groups-and-group-templates}

La función de grupos de comunidad es la capacidad de los usuarios autorizados y los miembros de la comunidad de crear dinámicamente una subcomunidad dentro de un sitio de comunidad desde los entornos de autor y publicación.

Desde el entorno de creación, se pueden crear grupos de comunidad (subcomunidades) dentro de un sitio de comunidad existente o anidados dentro de un grupo existente, cuando la estructura de la plantilla contiene la variable [Función de grupos](/help/communities/functions.md#groups-function).

La creación de un grupo de comunidad requiere la selección de una plantilla de grupo de comunidad que proporcione el diseño de las páginas de grupo de la comunidad. Cuando se agrega una función Grupos a una estructura de plantilla, se configura para especificar una plantilla de grupo o para proporcionar una selección de plantillas al crear un nuevo grupo de comunidad.

Consulte también lo siguiente:

* [Consola Grupos de sitios](/help/communities/groups.md) para crear subcomunidades en el entorno de creación.
* [Consola Plantillas de grupo](/help/communities/tools-groups.md) para crear la estructura del sitio para grupos.
* [Introducción a AEM Communities](/help/communities/getting-started.md) para el tutorial sobre la creación rápida de un sitio de comunidad que incluya grupos anidados.

## Componentes de comunidad {#community-components}

La variable [componentes de la comunidad](/help/communities/author-communities.md) desde el cual se crea un sitio de comunidad puede utilizarse para agregar características de Communities a cualquier sitio AEM.

La variable [guía de componentes de comunidad](/help/communities/components-guide.md) está disponible para la exploración interactiva de los componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidad de participación {#engagement-community}

Una comunidad de participación es un sitio de la comunidad que se centra en atraer clientes para que informen, soliciten comentarios y permitan a los clientes interactuar como miembros de la comunidad.

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
* Informes de Analytics

Para experimentar la facilidad de crear rápidamente una nueva comunidad de participación, visite [Introducción a AEM Communities](/help/communities/getting-started.md).

### Comunidad de habilitación {#enablement-community}

Una comunidad de habilitación es un sitio de la comunidad que incluye características para el aprendizaje en línea.

Las características de una comunidad de habilitación pueden incluir:

* Todas las características de un [comunidad de participación](#engagement-community).
* capacidad para asignar contenido y aprendizaje. recursos para miembros y grupos de miembros.
* Admite contenido SCORM, como cuestionarios y pruebas.
* Seguimiento de la finalización de asignaciones.
* Acceso a informes y análisis.
* La capacidad de tener una conversación sobre un recurso de aprendizaje a través de foros, mensajes, comentarios y clasificaciones.

Se puede crear una comunidad de habilitación cuando el [El complemento de habilitación está configurado](/help/communities/enablement.md), que requiere licencias adicionales para su uso en un entorno de producción. Un sitio de la comunidad de habilitación incluirá el [asignar, función](#community-functions).

Para experimentar la facilidad de crear una nueva comunidad de habilitación, visite [Introducción a AEM Communities para la activación](/help/communities/getting-started-enablement.md).

## AEM de demostración {#aem-demo-machine}

La variable [AEM de demostración](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) administra y ejecuta demostraciones para AEM [Sitios](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Recursos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicaciones](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) y [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que a menudo requieren más configuración que simplemente iniciar una instancia de QuickStart. El equipo de demostración de AEM configurará más [infraestructura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) como MongoDB, Solr, MySQL, FFmpeg y servidores de correo electrónico.

La AEM Demo Machine incluye:

* A [interfaz gráfica de usuario](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Secuencias de comandos de Apache ANT con configuración [propiedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) y [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Paquetes para instalar.

AEM Demo Machine se probó correctamente con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 y AEM 6.4 en Windows, MacOS y Linux.

AEM Demo Machine requiere una licencia de AEM válida.

>[!NOTE]
>
>Ver un [introducción de vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) a la máquina de demostración de AEM (13:26).

## Documentación de AEM Communities {#aem-communities-documentation}

* Visita [Implementación de comunidades](deploy-communities.md) para obtener más información sobre las implementaciones recomendadas.
* Visita [Administración de sitios de comunidades](administer-landing.md) para obtener información sobre la creación de un sitio de comunidad, la adición de grupos de comunidad, la configuración de plantillas de sitio de comunidad, la moderación del contenido de la comunidad, la administración de miembros, el etiquetado, las notificaciones, la puntuación y los distintivos.
* Visita [Desarrollo de comunidades](communities.md) para obtener información sobre el marco de componentes sociales (SCF) y la personalización de componentes y funciones de Communities.
* Visita [Creación de componentes de Communities](author-communities.md) para aprender a crear con y configurar componentes de Communities.
