---
title: Configuración del Cloud Service de Adobe Mobile Services
description: Siga esta página para configurar el Cloud Service de Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Configuración del Cloud Service de Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El **mosaico de métricas móviles** del centro de comandos proporciona análisis en tiempo real para su aplicación móvil.

El SDK de [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) está disponible a través de un complemento de PhoneGap. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta este. En ese momento, los datos se insertan en Adobe Mobile Services Cloud para la realización de informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales móviles**: recopile datos completos para sus sitios web y aplicaciones móviles en todos los sistemas operativos principales.
1. **Análisis de participación móvil**: Comprenda la participación del usuario en su aplicación móvil, sitio web o vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Paneles e informes de aplicaciones móviles**: obtenga informes de uso que incluyan métricas del ciclo vital para sus aplicaciones y métricas de la tienda de aplicaciones; consulte tendencias para usuarios, inicios, duración promedio de la sesión, duración de la retención y bloqueos.
1. **Análisis de campañas móviles**: Cuantifique la eficacia de campañas específicas para móviles como SMS, anuncios de búsquedas móviles, anuncios en pantallas móviles y códigos QR.
1. **Análisis de geolocalización**: encuentre dónde inician los usuarios de su aplicación e interactúen con sus experiencias móviles mediante la ubicación GPS o puntos de interés.
1. **Análisis de rutas**: vea cómo navegan los usuarios por su aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles hacen que abandonen los usuarios.

>[!CAUTION]
>
>El mosaico **Analizar métricas** se muestra en el panel, solo si ha configurado servicios en la nube.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Mosaico de métricas del centro de comandos

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar Adobe Mobile Services Analytics, debe configurar el servicio de AEM Mobile Analytics Cloud con la información de su cuenta de Adobe Analytics.

1. Haga clic en el icono de la parte superior derecha para agregar o editar los Cloud Service del mosaico **Administrar Cloud Service** del panel de aplicaciones.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Se muestra la pantalla **Agregar o editar Cloud Service**. Seleccione **Adobe Mobile Services** y haga clic en **Siguiente**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Elija una configuración existente de **Mobile Services** o elija **Crear configuración** para crear una.

   Para obtener la nueva configuración, escribe las **Propiedades de Mobile Services** y haz clic en **Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si se verifican las credenciales, el botón **Verificar** cambiará a **Verificado**. Puede elegir una aplicación de servicio móvil de **Seleccionar un servicio de aplicación móvil**.

   Haga clic en **Enviar** para configurar la configuración.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Una vez configurada una configuración de nube, puede ver lo mismo en el panel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Una vez que hayas configurado la nube, puedes ver el mosaico **Analizar métricas** en el panel de la aplicación.

   ![chlimage_1-28](assets/chlimage_1-28.png)
