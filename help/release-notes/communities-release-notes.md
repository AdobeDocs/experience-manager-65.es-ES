---
title: Notas de versión de AEM Communities
description: Notas de versión específicas de Adobe Experience Manager 6.5 Communities.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 66%

---


# AEM Communities release notes {#aem-communities-release-notes}

Continúe leyendo para conocer las mejoras en AEM Communities desde la versión 6.4. Para obtener más información sobre las nuevas funciones con mayor detalle, consulte la [Guía del usuario de AEM 6.5 Communities](https://helpx.adobe.com/es/experience-manager/6-4/communities/user-guide.html).

To obtain the latest release, see the [Deploying Communities](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases) section of the documentation.

## Mejoras importantes {#major-enhancements}

### Mejoras en el compromiso de la comunidad {#enhancements-to-community-engagement}

**@Mentions ahora permite a los usuarios registrados etiquetar (mencionar) otros miembros registrados para atraer su atención en Contenido generado por el usuario**. A continuación, se notificará a los miembros etiquetados (mencionados) con una vinculación profunda al contenido que creó el usuario correspondiente. Sin embargo, los usuarios pueden optar por activar o desactivar las notificaciones web y de correo electrónico.

![Compatibilidad con menciones](assets/at-mentions.png)

Los usuarios de la comunidad no necesitan buscar su nombre, apellido o nombre de usuario para ver si alguien los ha contactado o si necesita su atención. Además, permite que los autores de UGC busquen respuestas de usuarios específicos registrados que pueden abordar el problema y añadir entradas.

The community administrators need to **Enable Mention** on community components to allow registered users use the functionality on those components.

**Mensajería de grupo**

Los miembros registrados de la comunidad ahora pueden enviar mensajes masivos directos a los grupos mediante una sola composición de correo electrónico, en lugar de enviar el mismo mensaje individualmente a los miembros del grupo. To allow [group messaging](/help/communities/configure-messaging.md), enable both the instances of [Messaging Operations Service](/help/communities/messaging.md#group-messaging).

![Mensajería de grupo](assets/group-messaging.png)

### Mejoras de la moderación masiva {#enhancements-to-bulk-moderation}

filtros personalizados en moderación masiva

[Los filtros](/help/communities/moderation.md#custom-filters) personalizados ahora se pueden desarrollar y agregar a la IU de moderación masiva.

En [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) encontrará un [proyecto de muestra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) del filtrado mediante etiquetas. Este proyecto se puede utilizar como base para desarrollar filtros personalizados similares.

![Filtros personalizados](assets/custom-tag-filter.png)

**Vista de lista en la moderación masiva**

Se ha proporcionado una nueva vista de lista con una interfaz de usuario mejorada con la moderación masiva, para mostrar las entradas del contenido que haya creado el usuario.

![Moderación masiva en la vista de lista](assets/list-view-moderation.png)

### Mejoras en la administración del sitio y del grupo {#enhancements-to-site-and-group-management}

**Autor del sitio y administradores del grupo**

Communities, AEM 6.5 y otras versiones posteriores le permiten realizar operaciones con la administración (y gestión) descentralizada de distintos sitios de comunidad y grupos anidados. Las organizaciones que alojan varios sitios de comunidad y grupos anidados ahora pueden seleccionar miembros para funciones de administrador del lado de autor en el momento de la creación del sitio (y del grupo).

![Administrador del sitio](assets/site-admin.png)

Los administradores del sitio pueden crear un grupo en cualquier nivel de jerarquía y convertirse en administradores predeterminados. Estos administradores pueden ser eliminados posteriormente por otros administradores de grupos. Los administradores del grupo pueden administrar su grupo G1 y crear un subgrupo anidado en G1.

### Mejoras en la activación {#enhancements-to-enablement}

**Compatibilidad con SCORM 2017.1**

The enablement functionality of AEM 6.5 Communities support Shareable Content Object Reference Model [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.

* Compatibilidad con la navegación por teclado en los componentes de habilitación
* Los componentes de habilitación (por ejemplo, Catálogo y Reproducción de cursos, Asignaciones, Biblioteca de archivos) de los AEM Communities admiten la navegación mediante el teclado para mejorar la accesibilidad.

### Otras mejoras {#other-enhancements}

* Compatibilidad con Solr 7
* AEM 6.5 Communities es compatible con la versión Apache Solr 7.0 de la plataforma de búsqueda al configurar MSRP y DSRP.
