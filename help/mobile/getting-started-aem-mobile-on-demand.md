---
title: Adobe Experience Manager Mobile On Demand
description: El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Siga esta página para empezar a utilizar AEM servicios móviles bajo demanda.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# AEM Mobile On Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si no utiliza AEM como fuente de administración de contenido, consulte [Ayuda de AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM proporciona varias herramientas que le permiten integrar su contenido en aplicaciones móviles.

El diagrama siguiente ilustra cómo se ajustan los distintos componentes de AEM Mobile y los servicios bajo demanda para ofrecer contenido a las aplicaciones móviles.

AEM aplicación Preflight puede considerarse un entorno de prueba para previsualizar la aplicación y el contenido antes de la publicación; mientras que la aplicación de AEM Mobile es la aplicación final que se ha creado para su distribución.

>[!NOTE]
>
>Para obtener información detallada sobre la aplicación Preflight, consulte [Uso de la aplicación AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) en la Ayuda de AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>En el diagrama anterior, la instancia de AEM Publish no es necesaria para un escenario de implementación típico en AEM Mobile On-demand Services.

## Inicio de una nueva aplicación móvil {#starting-a-new-mobile-app}

AEM Mobile es solo un pilar que constituye la plataforma AEM completa.

El inicio de una nueva experiencia de aplicación de AEM Mobile requiere una cohesión de funciones antes de que esté lista para la edición de contenido. Las funciones siguientes proporcionan un punto de partida para crear una nueva aplicación de AEM Mobile:

* **Administrador**
* **Desarrollador**
* **Autor**

>[!NOTE]
>
>Antes de trabajar con AEM Mobile y seguir los pasos de esta guía de introducción, los usuarios deben estar familiarizados con AEM. Conozca los conceptos básicos de AEM [here](/help/sites-deploying/deploy.md).

### Explicación del panel de aplicaciones de AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Antes de comprender las funciones y responsabilidades, el usuario debe tener un conocimiento profundo de **Centro de control de AEM Mobile** o **Panel de aplicaciones**. Haga clic en [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para una comprensión más detallada.

### Administrador de AEM {#aem-administrator}

Un ***administrador de AEM*** es responsable de agregar una nueva aplicación al catálogo de AEM Mobile, ya sea creando una nueva aplicación con el asistente de creación o importando una aplicación existente. AEM administradores que crean una aplicación nueva con AEM Mobile *asistente de creación* normalmente, seleccione una de las plantillas de aplicación que desee entre nuestras muestras de referencia predeterminadas o (en la mayoría de los casos) una plantilla de aplicación personalizada creada por *AEM desarrolladores.*

Un administrador de AEM es responsable de las siguientes tareas al crear una aplicación con AEM Mobile On-demand Services:

* [Configuración de AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuración de los grupos de usuarios y usuarios](/help/mobile/aem-mobile-configure-users.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

Para empezar a utilizar las funciones y responsabilidades de un administrador, consulte [Administración de contenido para usar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Desarrollador de AEM {#aem-developer}

Un **AEM desarrollador** amplía y crea plantillas y componentes web personalizados para permitir que *AEM Author *cree experiencias móviles hermosas y atractivas. Estas plantillas y componentes no solo están optimizados para el mundo de las aplicaciones móviles; pero comuníquese tanto con el dispositivo como con el servidor AEM (cualquier servidor remoto) a los puntos finales del servicio omnicanal. AEM editor de contenido integrado es utilizado por *Autores de AEM* para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Marketing Cloud.

Un desarrollador de AEM es responsable de las siguientes tareas mientras crea una aplicación con AEM Mobile On-demand Services:

* [Plantillas y componentes de aplicación](/help/mobile/app-templates-and-components1.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Propiedades de contenido y exportación de contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Desarrollo de los servicios de contenido de AEM Mobile](/help/mobile/developing-content-services.md)

Para empezar a utilizar las funciones y responsabilidades del desarrollador, consulte [Desarrollo de contenido de AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un *AEM del desarrollador* no comienza ni finaliza con el desarrollo de plantillas y componentes. Un *AEM desarrollador* puede crear una aplicación completamente nueva en lugar de simplemente ampliar el ejemplo de implementación de referencia predeterminada.

## AEM Author {#aem-author}

Un ***Autor de AEM* (o *Especialista en marketing*)**utiliza las plantillas y componentes desarrollados o listos para usar para agregar y editar páginas, arrastrar y soltar componentes y añadir medios de todo tipo desde DAM, incluidas imágenes, vídeos y fragmentos de texto (fragmentos de contenido). AEM editor de contenido integrado lo utiliza *Autores de AEM* para crear experiencias enriquecidas y relevantes dentro de la aplicación, incluida la integración con el resto de Adobe Marketing Cloud.

Un autor AEM debe comprender los siguientes temas al crear una aplicación con AEM Mobile On-demand Services:

* [Panel de aplicaciones de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Acciones de creación y configuración de aplicaciones](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuración de nube](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Información general de los servicios de contenido](/help/mobile/develop-content-as-a-service.md)

Para empezar a utilizar las funciones y responsabilidades de un autor, consulte [Creación de contenido AEM para aplicaciones de AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un autor de AEM también es responsable de configurar la asignación de derechos, crear tarjetas y diseños y enviar notificaciones push. Además, para obtener más información sobre métodos para crear contenido; administrar artículos y colecciones; creación de titulares, tarjetas y diseños en AEM Mobile, consulte [Portal bajo demanda de AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
