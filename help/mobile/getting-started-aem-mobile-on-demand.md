---
title: Adobe Experience Manager Mobile On-Demand
description: El inicio de una nueva experiencia de aplicación móvil de Adobe Experience Manager AEM () requiere una cohesión de funciones antes de que esté lista para la edición de contenido. AEM Siga esta página para empezar a usar los servicios móviles bajo demanda de la aplicación de la versión de.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

{{ue-over-mobile}}

>[!NOTE]
>
>Si no usa Adobe Experience Manager AEM () como fuente de administración de contenido, consulte la [Ayuda de AEM Mobile On-demand Services](https://helpx.adobe.com/es/digital-publishing-solution/topics.html).

AEM proporciona varias herramientas que le permiten integrar el contenido en aplicaciones móviles.

El diagrama siguiente ilustra cómo los distintos componentes de AEM Mobile y On-Demand Services encajan para ofrecer contenido a las aplicaciones móviles.

AEM La aplicación de comprobación preliminar se puede considerar un entorno de prueba para obtener una vista previa de la aplicación y el contenido antes de publicarla, mientras que la aplicación de AEM Mobile es la última creada para su distribución.

>[!NOTE]
>
>AEM Para obtener información detallada acerca de la aplicación Preflight, consulte [Uso de la aplicación Preflight de la aplicación Preflight](https://helpx.adobe.com/es/digital-publishing-solution/help/preflight-app.html) en la Ayuda de AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>AEM En el diagrama anterior, no se requiere la instancia de Publish para la implementación típica en AEM Mobile On-demand Services.

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

Antes de comprender las funciones y responsabilidades, el usuario debe conocer a fondo **AEM Mobile Control Center** o **Application Dashboard**. Haga clic [aquí](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener información detallada.

### Administrador de AEM {#aem-administrator}

AEM Un ***administrador de*** es responsable de agregar una aplicación al catálogo de AEM Mobile, ya sea creando una aplicación con el asistente para la creación o importando una aplicación existente. AEM Los administradores de la aplicación que crean una aplicación con el *asistente para la creación de aplicaciones* de AEM Mobile suelen seleccionar una de las plantillas de aplicaciones deseadas de las muestras de referencia listas para usar de Adobe AEM o (normalmente) una plantilla de aplicación personalizada creada por los desarrolladores de *.*

AEM Un administrador de la aplicación es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Configuración de AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuración de los usuarios y grupos de usuarios](/help/mobile/aem-mobile-configure-users.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

Para comenzar con las funciones y responsabilidades de un administrador, consulte [Administración de contenido para usar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Desarrollador de {#aem-developer}

AEM AEM Un **desarrollador de** amplía y crea plantillas web y componentes personalizados para permitir que el *Autor de la aplicación *cree experiencias móviles hermosas y atractivas. AEM Estas plantillas y componentes no solo están optimizadas para el mundo de las aplicaciones móviles, sino que se comunican tanto con el dispositivo como con el servidor de (cualquier servidor remoto) a los puntos finales de servicios omnicanal. AEM AEM *Autores de contenido* utilizan el editor de contenido integrado para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Experience Cloud.

AEM Un desarrollador de aplicaciones es responsable de las siguientes tareas al crear una aplicación mediante AEM Mobile On-demand Services:

* [Plantillas y componentes de aplicación](/help/mobile/app-templates-and-components1.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Propiedades de contenido y exportación de contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Desarrollo de AEM Mobile Content Services](/help/mobile/developing-content-services.md)

AEM Para empezar a usar las funciones y responsabilidades de Desarrollador, consulte [Desarrollo de contenido para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>AEM La función ** de desarrollador no comienza ni finaliza con el desarrollo de plantillas y componentes. AEM Un *desarrollador de* puede crear una aplicación completamente nueva en lugar de extender el ejemplo de implementación de referencia listo para usar.

## AEM Author {#aem-author}

AEM Un ***Autor de* (o *Especialista en marketing*)**&#x200B;usa las plantillas y componentes personalizados desarrollados o listos para usar para agregar y editar páginas, arrastrar y soltar componentes y agregar medios de todos los tipos desde DAM, como imágenes, vídeos y fragmentos de texto (fragmentos de contenido). AEM AEM *Autores de contenido* utilizan el editor de contenido integrado para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Experience Cloud.

AEM Un autor de la debe comprender los siguientes temas al crear una aplicación con AEM Mobile On-demand Services:

* [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Acciones de creación y configuración de aplicaciones](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuración de nube](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Información general de servicios de contenido](/help/mobile/develop-content-as-a-service.md)

AEM Para comenzar con las funciones y responsabilidades de un autor, consulte [Creación de contenido de la aplicación de AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md) para la creación de aplicaciones de la aplicación de.

>[!NOTE]
>
>AEM También es responsable de configurar la asignación de derechos, crear tarjetas y diseños y enviar notificaciones push. Además, para obtener más información sobre los métodos para crear contenido, administrar artículos y colecciones, crear titulares, tarjetas y diseños en AEM Mobile, consulte [AEM Mobile On-Demand Portal](https://helpx.adobe.com/es/digital-publishing-solution/topics.html#dynamicpod_reference_2).
