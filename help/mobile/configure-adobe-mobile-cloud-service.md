---
title: Configuración del Cloud Service de Adobe Mobile Services
seo-title: Configuración del Cloud Service de Adobe Mobile Services
description: Siga esta página para configurar el Cloud Service de Adobe Mobile Services.
seo-description: Siga esta página para configurar el Cloud Service de Adobe Mobile Services.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Configure el Cloud Service de Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El **Mosaico de métricas móviles** del centro de comandos proporciona análisis en tiempo real para la aplicación móvil.

El SDK de [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) está disponible mediante un complemento de PhoneGap. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta el dispositivo, momento en el que los datos se insertan en Adobe Mobile Services Cloud para sistema de informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales**  móviles: recopile datos completos para sus aplicaciones y sitios web móviles en todos los principales sistemas operativos.
1. **Análisis**  de participación móvil: comprenda la participación del usuario en la aplicación móvil, el sitio web o el vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Paneles e informes**  de aplicaciones móviles: obtenga informes de uso que incluyan métricas del ciclo vital para sus aplicaciones y métricas del almacén de aplicaciones: consulte las tendencias de los usuarios, inicios, duración media de la sesión, duración de la retención y bloqueos.
1. **Análisis**  de campaña móvil: Cuantifique la efectividad de campañas específicas de dispositivos móviles como SMS, anuncios de búsqueda móvil, anuncios en pantalla móviles y códigos QR.
1. **Análisis**  de geolocalización: busque dónde inician e interactúan los usuarios con sus experiencias móviles mediante la ubicación GPS o los puntos de interés.
1. **Análisis**  de rutas: consulte cómo navegan los usuarios por la aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles provocan que éstos abandonen la aplicación.

>[!CAUTION]
>
>El icono **Analizar métricas** se muestra en el panel, solo si ha configurado los servicios en la nube.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaico de métricas del centro de comandos de AEM

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar Adobe Mobile Services Analytics, debe configurar el servicio Analytics Cloud de AEM Mobile con la información de su cuenta de Adobe Analytics.

1. Haga clic en el icono de la parte superior derecha para agregar o editar los Cloud Services desde el mosaico **Administrar Cloud Services** del panel de la aplicación.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Se abre la pantalla **Añadir o editar Cloud Services**. Seleccione **Adobe Mobile Services** y haga clic en **Siguiente**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Elija una configuración existente en **Mobile Services** o elija **Crear configuración** para crear una nueva.

   Para obtener una nueva configuración, introduzca las **Propiedades de Mobile Services** y haga clic en **Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si se verifican las credenciales, el botón **Verificar** cambia a **Verificado**. Puede elegir una aplicación de servicio móvil desde **Seleccionar un servicio de aplicación móvil**.

   Haga clic en **Enviar** para configurar la configuración.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Una vez configurada la configuración de nube, puede realizar la misma vista en el panel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Una vez configurada la configuración de nube, puede realizar la vista del icono **Analizar métricas** en el panel de la aplicación.

   ![chlimage_1-28](assets/chlimage_1-28.png)

