---
title: Adobe Experience Manager Mobile On-Demand
description: El inicio de una nueva experiencia de aplicación móvil de Adobe Experience Manager AEM () requiere una cohesión de funciones antes de que esté lista para la edición de contenido. AEM Siga esta página para empezar a usar los servicios móviles bajo demanda de la aplicación de la versión de.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si no utiliza Adobe Experience Manager AEM () como fuente de administración de contenido, consulte [Ayuda de AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM proporciona varias herramientas que le permiten integrar el contenido en aplicaciones móviles.

El diagrama siguiente ilustra cómo los distintos componentes de AEM Mobile y On-Demand Services encajan para ofrecer contenido a las aplicaciones móviles.

AEM La aplicación de comprobación preliminar se puede considerar un entorno de prueba para obtener una vista previa de la aplicación y el contenido antes de publicarla, mientras que la aplicación de AEM Mobile es la última creada para su distribución.

>[!NOTE]
>
>Para obtener información detallada sobre la aplicación de comprobaciones, consulte [AEM Uso de la aplicación de comprobación preliminar de](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) en la Ayuda de AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>En el diagrama anterior, la instancia de publicación de AEM no es necesaria para un escenario de implementación típico en AEM Mobile On-demand Services.

## Inicio de una nueva aplicación móvil {#starting-a-new-mobile-app}

AEM Mobile AEM es solo uno de los pilares que conforman la plataforma completa de la.

El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Las siguientes funciones proporcionan un punto de partida para crear una aplicación de AEM Mobile:

* **Administrador**
* **Desarrollador**
* **Autor**

>[!NOTE]
>
>Antes de trabajar con AEM Mobile AEM y seguir los pasos de esta guía de introducción, los usuarios deben estar familiarizados con el uso de las funciones de la interfaz de usuario de. AEM Conozca los conceptos básicos de la [aquí](/help/sites-deploying/deploy.md).

### Explicación del panel de aplicaciones de AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de comprender las funciones y responsabilidades, el usuario debe tener un conocimiento exhaustivo de **Centro de control de AEM Mobile** o el **Tablero de aplicación**. Clic [aquí](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para una comprensión exhaustiva.

### Administrador de AEM {#aem-administrator}

Un ***AEM administrador de*** es responsable de añadir una aplicación al catálogo de AEM Mobile, ya sea creando una aplicación con el asistente de creación o importando una aplicación existente. AEM administradores de que crean una aplicación con el de AEM Mobile *asistente de creación* normalmente, seleccione una de las plantillas de aplicación que desee entre las muestras de referencia predeterminadas de Adobe o (normalmente) una plantilla de aplicación personalizada creada por *AEM desarrolladores de.*

AEM Un administrador de la aplicación es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Configuración de AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuración de los usuarios y grupos de usuarios](/help/mobile/aem-mobile-configure-users.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

Para empezar con las funciones y responsabilidades de un administrador, consulte [Administración de contenido para utilizar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Desarrollador de {#aem-developer}

Un **AEM desarrollador de** amplía y crea plantillas web y componentes personalizados para permitir que *AEM Author *cree experiencias móviles hermosas y atractivas. AEM Estas plantillas y componentes no solo están optimizadas para el mundo de las aplicaciones móviles, sino que se comunican tanto con el dispositivo como con el servidor de (cualquier servidor remoto) a los puntos finales de servicios omnicanal. AEM El editor de contenido integrado de la lo utiliza *Autores AEM* para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Experience Cloud.

AEM Un desarrollador de aplicaciones es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Plantillas y componentes de aplicación](/help/mobile/app-templates-and-components1.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Propiedades de contenido y exportación de contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Desarrollo de AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Para empezar a usar las funciones y responsabilidades de desarrollador, consulte [AEM Desarrollo de contenido para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un *AEM de desarrollador de* Esta función no comienza ni finaliza con el desarrollo de plantillas y componentes. Un *AEM desarrollador de* puede crear una aplicación completamente nueva en lugar de simplemente ampliar el ejemplo de implementación de referencia listo para usar.

## AEM Author {#aem-author}

Un ***AEM Author* (o *Especialista en marketing*)**utiliza las plantillas y los componentes desarrollados o predeterminados para añadir y editar páginas, arrastrar y soltar componentes y añadir medios de todos los tipos desde DAM, incluidas imágenes, vídeos y fragmentos de texto (fragmentos de contenido). AEM A continuación, utiliza el editor de contenido integrado de la *Autores AEM* para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Experience Cloud.

AEM Un autor de la debe comprender los siguientes temas al crear una aplicación con AEM Mobile On-demand Services:

* [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Acciones de creación y configuración de aplicaciones](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuración de nube](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Información general de servicios de contenido](/help/mobile/develop-content-as-a-service.md)

Para empezar con las funciones y responsabilidades de un autor, consulte [AEM Creación de contenido de la aplicación de para AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un autor de AEM también es responsable de configurar el derecho, crear tarjetas y diseños y enviar notificaciones push. Además, para obtener más información sobre los métodos para crear contenido, administrar artículos y colecciones, crear titulares, tarjetas y diseños en AEM Mobile, consulte [Portal de AEM Mobile On-Demand](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
