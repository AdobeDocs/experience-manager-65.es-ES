---
title: Configuración del Cloud Service de Adobe Mobile Services
description: Siga esta página para configurar el Cloud Service de Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Configuración del Cloud Service de Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El **Mosaico de métricas móviles** en el centro de comandos proporciona análisis en tiempo real para su aplicación móvil.

El [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) El SDK está disponible a través de un complemento PhoneGap. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta este. En ese momento, los datos se insertan en Adobe Mobile Services Cloud para la realización de informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales móviles** - Recopile datos completos para sus sitios web y aplicaciones móviles en todos los sistemas operativos principales.
1. **Análisis de participación móvil** : Comprenda la participación del usuario en su aplicación móvil, sitio web o vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Paneles e informes de aplicaciones móviles** : Obtenga informes de uso que incluyen métricas del ciclo vital para sus aplicaciones y métricas de la tienda de aplicaciones. Consulte tendencias para usuarios, inicios, duración promedio de la sesión, duración de la retención y bloqueos.
1. **Análisis de campañas móviles** - Cuantifique la eficacia de campañas específicas para móviles como SMS, anuncios de búsqueda móviles, anuncios en pantalla móviles y códigos QR.
1. **Análisis de geolocalización** - Encuentre dónde inician los usuarios de su aplicación e interactúen con sus experiencias móviles mediante la ubicación GPS o puntos de interés.
1. **Análisis de rutas** : Consulte cómo navegan los usuarios por la aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles provocan que estos bajen.

>[!CAUTION]
>
>El **Analizar métricas** El mosaico se muestra en el panel, solo si ha configurado servicios en la nube.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Mosaico de métricas del centro de comandos

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar Adobe Mobile Services Analytics, debe configurar el servicio de AEM Mobile Analytics Cloud con la información de su cuenta de Adobe Analytics.

1. Haga clic en el icono superior derecho para añadir o editar los Cloud Service del **Administración de Cloud Service** del tablero de la aplicación.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. El **Añadir o editar Cloud Service** se muestra. Seleccionar **Adobe Mobile Services** y haga clic en **Siguiente**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Elija una configuración existente en la **Mobile Services** o elija **Crear configuración** para crear uno.

   Para la nueva configuración, introduzca la variable **Propiedades de Mobile Services** y haga clic en **Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si se verifican las credenciales, la variable **Verificar** el botón cambia a **Verificado**. Puede elegir una aplicación de servicio móvil de **Seleccione un servicio de aplicación móvil**.

   Clic **Enviar** para configurar su configuración.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Una vez configurada una configuración de nube, puede ver lo mismo en el panel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Una vez configurada la nube de, puede ver el **Analizar métricas** Mosaico en el tablero de la aplicación.

   ![chlimage_1-28](assets/chlimage_1-28.png)
