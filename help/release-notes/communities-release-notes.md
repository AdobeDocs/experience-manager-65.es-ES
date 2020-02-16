---
title: Notas de versión de AEM Communities
description: Notas de versión específicas de Adobe Experience Manager 6.5 Communities.
uuid: 1b436959-581c-4b34-b2df-cccc5727da59
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: c3505807-1550-491a-8619-e87839afca4f
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# Notas de versión de AEM Communities{#aem-communities-release-notes}

Continúe leyendo para conocer las mejoras en AEM Communities desde la versión 6.4. Para obtener más información sobre las nuevas funciones con mayor detalle, consulte la [Guía del usuario de AEM 6.5 Communities](https://helpx.adobe.com/experience-manager/6-4/communities/user-guide.html).

To obtain the latest release, see the [Deploying Communities](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases) section of the documentation.

## Mejoras importantes {#major-enhancements}

### Mejoras en el compromiso de la comunidad {#enhancements-to-community-engagement}

**@Mentions admite** que las comunidades AEM ahora permiten a los usuarios registrados etiquetar (mencionar) otros miembros registrados para atraer su atención, en Contenido generado por el usuario. A continuación, se notificará a los miembros etiquetados (mencionados) con una vinculación profunda al contenido que creó el usuario correspondiente. Sin embargo, los usuarios pueden optar por activar o desactivar las notificaciones web y de correo electrónico.

![Compatibilidad con menciones](assets/at-mentions.png)

Los usuarios de la comunidad no necesitan buscar su nombre, apellido o nombre de usuario para ver si alguien los ha contactado o si necesita su atención. Además, permite que los autores de UGC busquen respuestas de usuarios específicos registrados que pueden abordar el problema y añadir entradas.

Los administradores de la comunidad deben **Activar mención **en los componentes de la comunidad para permitir que los usuarios registrados utilicen la funcionalidad en dichos componentes.

**Mensajería de grupo**

Los miembros registrados de la comunidad ahora pueden enviar mensajes masivos directos a los grupos mediante una sola composición de correo electrónico, en lugar de enviar el mismo mensaje individualmente a los miembros del grupo. To allow [group messaging](/help/communities/configure-messaging.md), enable both the instances of [Messaging Operations Service](/help/communities/messaging.md#group-messaging).

![Mensajería de grupo](assets/group-messaging.png)

### Mejoras de la moderación masiva {#enhancements-to-bulk-moderation}

Filtros personalizados en moderación masiva

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

**Compatibilidad con la navegación por teclado en los componentes de habilitación**Los componentes de habilitación (por ejemplo, Reproducción de catálogo y curso, Asignaciones, Biblioteca de archivos) en Comunidades AEM admiten la navegación mediante el teclado para mejorar la accesibilidad.

### Otras mejoras {#other-enhancements}

* **Compatibilidad con Solr 7**AEM 6.5 Communities es compatible con la versión Apache Solr 7.0 de la plataforma de búsqueda al configurar MSRP y DSRP.
