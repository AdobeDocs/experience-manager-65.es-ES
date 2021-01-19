---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté listo para la edición de contenido. Siga esta página para empezar a usar AEM servicios bajo demanda para dispositivos móviles.
seo-description: El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté listo para la edición de contenido. Siga esta página para empezar a usar AEM servicios bajo demanda para dispositivos móviles.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a876a1a8d4aeb9e9a94c93a16742a4058307b0a8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si no utiliza AEM como fuente de administración de contenido, consulte [Ayuda de AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM ofrece varias herramientas que le permiten integrar su contenido en aplicaciones móviles.

En el diagrama siguiente se muestra cómo se ajustan los distintos componentes de AEM Mobile y On-Demand Services para distribuir contenido a las aplicaciones móviles.

AEM aplicación Preflight puede considerarse un entorno de prueba para realizar la previsualización de la aplicación y el contenido antes de la publicación; mientras que la aplicación de AEM Mobile es la aplicación final que se crea para su distribución.

>[!NOTE]
>
>Para obtener más información sobre la aplicación Preflight, consulte [Uso de la aplicación AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) en la Ayuda de AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>En el diagrama anterior, la instancia de AEM Publish no es necesaria para un escenario de implementación típico en AEM Mobile On-demand Services.

## Inicio de una nueva aplicación móvil {#starting-a-new-mobile-app}

AEM Mobile es sólo un pilar que constituye la plataforma AEM completa.

El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté listo para la edición de contenido. Las siguientes funciones proporcionan un punto de partida para crear una nueva aplicación de AEM Mobile:

* **Administrador**
* **Desarrollador**
* **Autor**

>[!NOTE]
>
>Antes de trabajar con AEM Mobile y seguir los pasos de esta guía de introducción, los usuarios deben estar familiarizados con AEM. Conozca los conceptos básicos de AEM [aquí](/help/sites-deploying/deploy.md).

### Explicación del Panel de aplicaciones de AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de comprender las funciones y responsabilidades, el usuario debe tener un conocimiento profundo de **AEM Mobile Control Center** o del **Panel de la aplicación**. Haga clic [aquí](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener información detallada.

### Administrador de AEM {#aem-administrator}

Un ***administrador de AEM*** es responsable de agregar una nueva aplicación al catálogo de AEM Mobile, ya sea creando una aplicación nueva mediante el asistente de creación o importando una aplicación existente. Los administradores de AEM que crean una aplicación nueva mediante el *asistente para la creación* de AEM Mobile suelen seleccionar una de las plantillas de aplicación deseadas, ya sea de nuestros ejemplos de referencia predeterminados o (en la mayoría de los casos) de una plantilla de aplicación personalizada creada por *desarrolladores de AEM.*

Un administrador de AEM es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Configuración de AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuración de los grupos de usuarios y usuarios](/help/mobile/aem-mobile-configure-users.md)
* [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

Para comenzar con las funciones y responsabilidades de un administrador, consulte [Administración de contenido para usar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Desarrollador de AEM {#aem-developer}

Un **desarrollador de AEM** amplía y crea plantillas web y componentes personalizados para permitir que *AEM Author *cree experiencias móviles hermosas y atractivas. Estas plantillas y componentes no solo están optimizados para el mundo de las aplicaciones móviles; pero comuníquese tanto con el dispositivo como con el servidor AEM (cualquier servidor remoto) a los puntos finales del servicio omni-canal. AEM editor de contenido integrado lo utilizan *AEM Authors* para crear experiencias ricas y relevantes dentro de la aplicación, incluida la integración con el resto del Adobe Marketing Cloud.

Un desarrollador de AEM es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Plantillas y componentes de aplicación](/help/mobile/app-templates-and-components1.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Propiedades de contenido y exportación de contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Desarrollo de AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Para comenzar con las funciones y responsabilidades de desarrollador, consulte [Desarrollo de contenido AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Una función *de desarrollador de AEM* no inicio ni termina con el desarrollo de plantillas y componentes. Un *desarrollador de AEM* puede crear una aplicación completamente nueva en lugar de simplemente ampliar el ejemplo de implementación de referencia lista para usar.

## AEM Author {#aem-author}

Una ***AEM Author* (o *Marketer*)**utiliza plantillas y componentes desarrollados o listos para usar personalizados para agregar y editar páginas, arrastrar y soltar componentes y agregar medios de todos los tipos desde DAM, incluidas imágenes, videos y fragmentos de texto (fragmentos de contenido). A continuación, *AEM Authors* utiliza AEM editor de contenido integrado para crear experiencias ricas y relevantes dentro de la aplicación, incluida la integración con el resto del Adobe Marketing Cloud.

Un autor AEM debe comprender los siguientes temas al crear una aplicación con AEM Mobile On-demand Services:

* [AEM Mobile Application Panel](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Acciones de creación y configuración de aplicaciones](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuración de nube](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Información general de Content Services](/help/mobile/develop-content-as-a-service.md)

Para comenzar con las funciones y responsabilidades de un autor, consulte [Creación de contenido AEM para la aplicación AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM Author también se encarga de configurar la asignación de derechos, crear tarjetas y diseños y enviar notificaciones push. Asimismo, para obtener más información sobre los métodos de creación de contenido; gestión de artículos y colecciones; creación de pancartas, tarjetas y diseños en AEM Mobile, consulte [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

