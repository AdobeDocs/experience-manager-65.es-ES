---
title: Configurar el servicio de nube de Adobe Mobile Services
seo-title: Configurar el servicio de nube de Adobe Mobile Services
description: Siga esta página para configurar el servicio de nube de Adobe Mobile Services.
seo-description: Siga esta página para configurar el servicio de nube de Adobe Mobile Services.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar el servicio de nube de Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El icono **Métricas** móviles del centro de comandos proporciona análisis en tiempo real de la aplicación móvil.

El SDK de [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) está disponible mediante un complemento PhoneGap. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que éste se conecta, momento en el que los datos se envían a Adobe Mobile Services Cloud para informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales** móviles: recopile datos completos para sus aplicaciones y sitios web móviles en todos los sistemas operativos principales.
1. **Análisis** de participación móvil: comprenda la participación del usuario en la aplicación móvil, el sitio web o el vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Tableros e informes** de aplicaciones móviles: obtenga informes de uso que incluyan métricas del ciclo vital para sus aplicaciones y métricas del almacén de aplicaciones: consulte las tendencias de los usuarios, inicios, duración media de la sesión, duración de la retención y bloqueos.
1. **Análisis** de campañas móviles: cuantifique la eficacia de campañas específicas para dispositivos móviles como SMS, anuncios de búsqueda móvil, anuncios en pantalla para dispositivos móviles y códigos QR.
1. **Análisis** de geolocalización: busque dónde inician e interactúan los usuarios con sus experiencias móviles mediante la ubicación GPS o puntos de interés.
1. **Análisis** de rutas: vea cómo los usuarios navegan por la aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles provocan que éstos abandonen la aplicación.

>[!CAUTION]
>
>El icono **Analizar métricas** se muestra en el tablero, solo si ha configurado los servicios en la nube.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaico de métricas del centro de comandos de AEM

## Configuración del servicio de nube {#configuring-the-cloud-service}

Para aprovechar Adobe Mobile Services Analytics, debe configurar el servicio de nube de AEM Mobile Analytics con la información de cuenta de Adobe Analytics.

1. Haga clic en el icono superior derecho del lado para añadir o editar los servicios de nube desde el mosaico **Administrar servicios** de nube del panel de la aplicación.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Aparece la pantalla **Agregar o editar servicios** de nube. Seleccione **Adobe Mobile Services** y haga clic en **Siguiente**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Elija una configuración existente en **Mobile Services** o elija **Crear configuración** para crear una nueva.

   Para obtener una nueva configuración, introduzca las Propiedades de **Mobile Services** y haga clic **en Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si se verifican las credenciales, el botón **Verificar** cambia a **Verificado**. Puede elegir una aplicación de servicio móvil en **Seleccionar un servicio** de aplicaciones móviles.

   Haga clic en **Enviar** para configurar la configuración.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Una vez configurada la configuración de nube, puede ver lo mismo en el tablero.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Una vez configurada la configuración de nube, puede ver el icono **Analizar métricas** en el tablero de la aplicación.

   ![chlimage_1-28](assets/chlimage_1-28.png)

