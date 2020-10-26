---
title: Content Services
seo-title: Content Services
description: nulo
seo-description: nulo
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La función Servicios de contenido está documentada únicamente para fines de previsualización.
>
>Está sujeto a cambios con la versión de 6.3 GA Service Pack 1.

AEM Mobile Content Services es una función ligera para solicitar contenido administrado por AEM. Esto proporciona a todos los desarrolladores de aplicaciones una manera de alto rendimiento de recuperar contenido sin tener que tener un profundo conocimiento del repositorio de contenido (JCR) y del marco de trabajo web (Sling) de AEM. Permite que las aplicaciones que solicitan se desvinculen del repositorio de contenido.

Content Services introduce varias construcciones de AEM nuevas que permiten a los desarrolladores acceder a AEM contenido administrado sin tener conocimiento de la estructura de repositorio de dicho contenido.

Estas construcciones son necesarias para mantener la flexibilidad y permitir una futura expansión proporcionando una capa de abstracción entre el contenido administrado AEM y las aplicaciones móviles que consumen el contenido. Esto permite que AEM Content Services funcione como una capa de abstracción entre los requisitos de contenido de la aplicación nativa y el repositorio de contenido AEM.

Content Services puede entregar el contenido como recursos, HTML empaquetado (HTML/CSS/JS) o como contenido independiente de canal.

>[!CAUTION]
>
>**Requisitos previos:**
>
>Antes de empezar a usar los servicios de contenido, asegúrese de activar el indicador de los servicios de contenido. Para habilitar la creación y la administración de modelos en la aplicación, debe activar los modelos de datos en el navegador de configuración.
>
>Consulte **[Administración de servicios](/help/mobile/developing-content-services.md)** de contenido y la documentación [del navegador](/help/sites-administering/configurations.md) de configuración para obtener más información.

![chlimage_1-143](assets/chlimage_1-143.png)

Una vez que haya establecido el indicador de Content Services y habilitado los modelos de datos en el navegador de configuración, consulte los recursos siguientes para empezar a usar AEM Mobile Content Services, familiarizarse con los conceptos de Content Services como administración de modelos, administración de entidades seguida de envío/procesamiento de contenido para AEM Mobile Content Services.

* Modelos en el repositorio
* Procesamiento y Envío
