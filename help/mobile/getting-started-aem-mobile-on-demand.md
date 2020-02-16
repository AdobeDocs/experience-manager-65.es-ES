---
title: On-Demand de AEM Mobile
seo-title: On-Demand de AEM Mobile
description: El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Siga esta página para empezar a utilizar los servicios On-Demand Services de AEM Mobile.
seo-description: El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Siga esta página para empezar a utilizar los servicios On-Demand Services de AEM Mobile.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# On-Demand de AEM Mobile{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si no utiliza AEM como fuente de administración de contenido, consulte la Ayuda [de On-Demand Services de](https://helpx.adobe.com/digital-publishing-solution/topics.html)AEM Mobile.

AEM proporciona varias herramientas que le permiten integrar su contenido en aplicaciones móviles.

En el diagrama siguiente se muestra cómo los distintos componentes de AEM Mobile y On-Demand Services se ajustan para distribuir contenido a las aplicaciones móviles.

La aplicación AEM Preflight puede considerarse un entorno de prueba para obtener una vista previa de la aplicación y el contenido antes de la publicación; mientras que la aplicación de AEM Mobile es la aplicación final que se ha creado para su distribución.

>[!NOTE]
>
>Para obtener más información sobre la aplicación Preflight, consulte [Uso de la aplicación](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) AEM Preflight en la Ayuda de On-Demand Services de AEM Mobile.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>En el diagrama anterior, la instancia de AEM Publish no es necesaria para un escenario de implementación típico en los servicios bajo demanda de AEM Mobile.

## Inicio de una nueva aplicación móvil {#starting-a-new-mobile-app}

AEM Mobile es solo un pilar que constituye la plataforma completa de AEM.

El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Las siguientes funciones proporcionan un punto de partida para crear una nueva aplicación de AEM Mobile:

* **Administrador**
* **Desarrollador**
* **Creación**

>[!NOTE]
>
>Antes de trabajar con AEM Mobile y seguir los pasos de esta guía de introducción, los usuarios deben estar familiarizados con AEM. Learn the basics of AEM [here](/help/sites-deploying/deploy.md).

### Explicación del panel de aplicaciones de AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de comprender las funciones y responsabilidades, el usuario debe tener un conocimiento profundo del Centro **de control de** AEM Mobile o del Panel **de** aplicación. Haga clic [aquí](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener una comprensión detallada.

### Administrador de AEM {#aem-administrator}

Un administrador ***de*** AEM es responsable de añadir una nueva aplicación al catálogo de AEM Mobile, ya sea creando una aplicación nueva con el asistente para la creación o importando una existente. Los administradores de AEM que crean una aplicación nueva mediante el asistente *de* creación de AEM Mobile suelen seleccionar una de las plantillas de aplicación deseadas, ya sea de nuestros ejemplos de referencia predeterminados o, en la mayoría de los casos, de una plantilla de aplicación personalizada creada por los desarrolladores de *AEM.*

Un administrador de AEM es responsable de las siguientes tareas al crear una aplicación mediante los servicios bajo demanda de AEM Mobile:

* [Configuración de AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuración de los grupos de usuarios y usuarios](/help/mobile/aem-mobile-configure-users.md)
* [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

Para empezar a usar las funciones y responsabilidades de un administrador, consulte [Administración de contenido para utilizar los servicios](/help/mobile/aem-mobile.md)bajo demanda de AEM Mobile.

## Desarrollador de AEM {#aem-developer}

Un desarrollador **de** AEM amplía y crea plantillas web y componentes personalizados para permitir que *AEM Author *cree unas experiencias móviles atractivas y hermosas. Estas plantillas y componentes no solo están optimizados para el mundo de las aplicaciones móviles; pero comuníquese tanto con el dispositivo como con el servidor AEM (cualquier servidor remoto) a los puntos finales del servicio de canal omnio. El editor de contenido integrado de AEM lo utilizan los autores *de* AEM para crear experiencias ricas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Marketing Cloud.

Un desarrollador de AEM es responsable de las siguientes tareas al crear una aplicación mediante los servicios bajo demanda de AEM Mobile:

* [Plantillas y componentes de aplicación](/help/mobile/app-templates-and-components1.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Propiedades de contenido y exportación de contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Desarrollo de AEM Mobile Content Services](//help/mobile/developing-content-services.md)

Para empezar a usar las funciones y responsabilidades de desarrollador, consulte [Desarrollo de contenido de AEM para los servicios](/help/mobile/aem-mobile-on-demand.md)bajo demanda de AEM Mobile.

>[!NOTE]
>
>La función de desarrollador de *AEM* no comienza ni termina con el desarrollo de plantillas y componentes. Un desarrollador *de* AEM puede crear una aplicación completamente nueva en lugar de simplemente ampliar el ejemplo de implementación de referencia lista para usar.

## AEM Author {#aem-author}

Un ***AEM Author *(o*Marketer *)**utiliza plantillas y componentes desarrollados o listos para usar personalizados para añadir y editar páginas, arrastrar y soltar componentes y añadir medios de todo tipo desde DAM, incluidas imágenes, vídeos y fragmentos de texto (fragmentos de contenido). A continuación, los autores de*AEM *utilizan el editor de contenido integrado de AEM para crear experiencias ricas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Marketing Cloud.

Un autor de AEM debe comprender los siguientes temas al crear una aplicación mediante los servicios bajo demanda de AEM Mobile:

* [Panel de aplicaciones de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Acciones de creación y configuración de aplicaciones](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuración de nube](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Información general de Content Services](/help/mobile/develop-content-as-a-service.md)

Para empezar a usar las funciones y responsabilidades de un autor, consulte [Creación de contenido de AEM para la aplicación](/help/mobile/mobile-apps-ondemand.md)On-Demand Services de AEM Mobile.

>[!NOTE]
>
>AEM Author también se encarga de configurar la asignación de derechos, crear tarjetas y diseños y enviar notificaciones push. Asimismo, para obtener más información sobre los métodos de creación de contenido; gestión de artículos y colecciones; creación de pancartas, tarjetas y diseños en AEM Mobile, consulte [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

