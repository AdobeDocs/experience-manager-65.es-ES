---
title: Acciones de creación y configuración de aplicaciones
seo-title: Application Create and Configuration Actions
description: La creación de una aplicación suele ser el primer paso para crear y administrar el contenido bajo demanda de AEM Mobile. Siga esta página para obtener más información.
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Acciones de creación y configuración de aplicaciones{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

## Creación de una aplicación a petición {#creating-an-on-demand-application}

La creación de una aplicación suele ser el primer paso para crear y administrar el contenido bajo demanda de AEM Mobile, y a menudo se realiza en el nivel de administrador AEM. Representa un shell de contenido, visible en dispositivos móviles, listo para mostrar contenido creado por el autor, como artículos, imágenes, colecciones, etc.

Los detalles de la aplicación se pueden ver en el panel de control o en el centro de control de AEM Mobile.

>[!NOTE]
>
>El panel es una serie de útiles mosaicos que proporcionan información general sobre el contenido de la aplicación, los metadatos y el estado de conexión a AEM Mobile On-Demand.
>
>Consulte [Panel de aplicaciones de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener más información.

**Para crear una aplicación bajo demanda:**

1. Select **Móvil** del carril lateral.
1. Select **Aplicaciones** de Navegación.
1. Haga clic en **Crear** y seleccione **Aplicación** en la lista desplegable .
1. Seleccione la plantilla Aplicación móvil y haga clic en **Siguiente**.
1. Introduzca propiedades de la aplicación como **Título**, **Nombre**, **Descripción**.
1. Haga clic en **Siguiente**.
1. Si se conoce, introduzca los detalles de configuración de la nube; de lo contrario, haga clic en **Crear**.
1. Haga clic en **Listo** para ver la nueva aplicación de AEM Mobile en el catálogo.

![imagen_1](assets/chlimage_1.gif)

>[!NOTE]
>
>Este proceso le permite crear una instancia de aplicación en AEM.

## Uso de plantillas de aplicación {#using-app-templates}

Las plantillas de aplicación proporcionan una manera sencilla de aprovechar los diseños existentes creados por los desarrolladores y utilizados para la creación de nuevas aplicaciones en AEM.

¿Qué es una plantilla de aplicación? Piense en ella como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación.
Al crear una aplicación nueva basada en la plantilla de otra aplicación, obtendrá una aplicación que tenga un punto de partida representativo de la aplicación desde la que se creó.

Debe tener una plantilla de aplicación móvil existente (o una aplicación instalada que tenga una plantilla de aplicación) para poder usar esta función.

### El paso siguiente {#the-next-step}

Una vez que haya creado una aplicación a petición desde el panel de la aplicación, el paso siguiente consiste en asociar la aplicación a la configuración de la nube.

Consulte [Asociación de la aplicación a la configuración de Cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) para obtener más información.

### Cómo avanzar {#getting-ahead}

Una vez que esté familiarizado con la creación de una aplicación bajo demanda y, por lo tanto, asociarla a una configuración de nube, consulte [Acciones de administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**Acciones de administración de contenido** implica la creación y administración del siguiente contenido:

* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar Cancelar publicación de contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

Para obtener más información sobre las funciones y responsabilidades de un administrador y desarrollador, consulte los siguientes recursos:

* [Desarrollo de contenido de AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Administración de contenido para usar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
