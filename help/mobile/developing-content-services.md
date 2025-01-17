---
title: Content Services
description: Aprenda a utilizar los servicios de contenido de AEM Mobile AEM para solicitar contenido administrado por los usuarios de la red de distribución de contenido (CDNs.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Content Services{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>La función Servicios de contenido está documentada únicamente con fines de vista previa.
>
>Está sujeto a cambios con el lanzamiento del paquete de servicio 1 de 6.3.

AEM Mobile AEM Content Services es una función ligera para solicitar contenido que administra el usuario de forma independiente. AEM Esto proporciona a todos los desarrolladores de aplicaciones una forma de alto rendimiento de recuperar contenido sin tener que tener conocimientos profundos sobre el repositorio de contenido (JCR) y el marco de trabajo web (Sling) de los que se dispone en la aplicación. Permite que las aplicaciones solicitantes se disocien del repositorio de contenido.

AEM AEM Content Services introduce varias construcciones de nuevas que permiten a un desarrollador acceder a contenido administrado por el usuario sin tener conocimiento de la estructura del repositorio de ese contenido.

AEM Estas construcciones son necesarias para mantener la flexibilidad y permitir la expansión futura mediante la provisión de una capa de abstracción entre el contenido administrado por el usuario y las aplicaciones móviles que consumen el contenido. AEM AEM Esto permite que los servicios de contenido de la aplicación funcione como una capa de abstracción entre los requisitos de contenido de la aplicación nativa y el repositorio de contenido de la aplicación de la aplicación de la aplicación de la que se dispone en el sitio de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de contenido.

Los servicios de contenido pueden entregar el contenido como recursos, HTML empaquetado (HTML/CSS/JS) o como contenido independiente del canal.

>[!CAUTION]
>
>**Requisitos previos:**
>
>Antes de empezar a usar los servicios de contenido, asegúrese de habilitar el indicador Servicios de contenido. Para habilitar la creación y administración de modelos en la aplicación, habilite los modelos de datos en el Explorador de configuración.
>
>Consulte **[Administración de servicios de contenido](/help/mobile/developing-content-services.md)** y la documentación de [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

![chlimage_1-143](assets/chlimage_1-143.png)

Después de establecer el indicador Servicios de contenido y de habilitar los modelos de datos en el Explorador de configuración, consulte los recursos siguientes para empezar a utilizar los servicios de contenido de AEM Mobile. Familiarícese con los Conceptos de servicios de contenido como administración de modelos, administración de entidades seguida de entrega/representación de contenido para los servicios de contenido de AEM Mobile.

* Modelos en el repositorio
* Procesamiento y entrega
