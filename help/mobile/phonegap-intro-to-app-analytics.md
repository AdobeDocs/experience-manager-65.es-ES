---
title: Seguimiento del rendimiento de la aplicación con Adobe Mobile Analytics
seo-title: Track App Performance with Adobe Mobile Analytics
description: Con Adobe Mobile Services, puede obtener información sobre cómo los usuarios utilizan sus aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de dispositivos y muchas otras métricas críticas de sus aplicaciones móviles. Siga esta página para obtener más información.
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# Seguimiento del rendimiento de la aplicación con Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Desea aumentar las conversiones y la lealtad de los clientes.

Desea ofrecer experiencias relevantes y atractivas a sus clientes.

¿Qué está haciendo la aplicación de AEM Mobile para sus campañas de marketing?

¿Cómo puede ajustar sus aplicaciones móviles para proporcionar la mejor experiencia para sus usuarios?

Con Adobe Mobile Services, puede obtener información sobre cómo los usuarios utilizan sus aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de dispositivos y muchas otras métricas críticas de sus aplicaciones móviles.

Adobe Experience Manager Mobile proporciona un vistazo a los detalles de su análisis móvil directamente desde el panel de aplicaciones de AEM Mobile. La variable **Mosaico de métricas móviles** en el panel de control proporciona análisis en tiempo real para su aplicación móvil, lo que permite a los desarrolladores, autores y administradores obtener un vistazo rápido al estado de su aplicación móvil. En las portadas que alimentan el análisis se muestra la variable [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. El SDK de Adobe Mobile Analytics se puede conectar a sus aplicaciones de forma nativa o a través de un complemento puente PhoneGap para las vistas web. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta el dispositivo, momento en el que los datos se envían a Adobe Mobile Services Cloud para su sistema de informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales móviles** : recopile datos completos para sus sitios web y aplicaciones móviles en todos los sistemas operativos principales.
1. **Análisis de participación móvil** : Comprenda la participación del usuario en su aplicación móvil, sitio web o vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Tableros e informes de aplicaciones móviles** : obtenga informes de uso que incluyan métricas del ciclo vital para sus aplicaciones y métricas del almacén de aplicaciones; consulte tendencias para usuarios, lanzamientos, longitud promedio de sesión, duración de retención y bloqueos.
1. **Análisis de campañas móviles** : Cuantifique la eficacia de campañas específicas para móviles como SMS, anuncios de búsqueda móvil, anuncios en pantalla para móviles y códigos QR.
1. **Análisis de geolocalización** : Descubra dónde se inician los usuarios de la aplicación e interactúan con sus experiencias móviles mediante la ubicación GPS o los puntos de interés.
1. **Análisis de rutas** : Vea cómo navegan los usuarios a través de la aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y qué causan que abandonen la aplicación.

Esta sección describe cómo [Desarrolladores de AEM](#developers) A continuación, puede aprender a instrumentar aplicaciones de AEM Mobile con el seguimiento de análisis.

Finalmente, [Administradores de AEM](#administrators) aprenda a:

* crear un servicio en la nube en Adobe Mobile Services
* crear una configuración de servicio móvil y asociar un grupo de informes
* asociar la configuración del servicio móvil a una aplicación móvil
* ver métricas a través del Centro de comandos de las aplicaciones AEM
* asignar la configuración del SDK de AMS a la aplicación móvil

## Para desarrolladores: Integre Analytics en su aplicación {#for-developers-integrate-analytics-into-your-app}

**Requisito previo:** Los administradores de AEM necesitan configurar la configuración de nube de Adobe Mobile Services, [como se describe a continuación](#amscloudserviceconfig).

Los desarrolladores son responsables de [adición de analytics a una aplicación de AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) cuando sea necesario para realizar un seguimiento, crear informes y comprender cómo los usuarios interactúan con el contenido de su aplicación móvil, así como para medir métricas clave del ciclo vital, como inicios, tiempo en la aplicación y tasa de bloqueo.

## Para administradores: Configuración del Cloud Service de Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aprovechar las ventajas de Adobe Mobile Services, debe configurar el Cloud Service de Adobe AEM Mobile Services con la información de su cuenta de Adobe Analytics. El Centro de comandos de las aplicaciones proporciona un **Analizar métricas** mosaico en el que puede crear y asociar el servicio de nube con su aplicación móvil.

Para configurar el servicio de nube en la aplicación móvil, haga clic en el icono de engranaje situado en el mosaico Analizar métricas .

![chlimage_1-125](assets/chlimage_1-125.png)

Si hace clic en el icono de engranaje del mosaico Analizar métricas , se abrirá el cuadro de diálogo modal &quot;Configurar análisis de Mobile Services&quot;. Seleccione la configuración en la lista desplegable &quot;Seleccionar una configuración de Mobile Service&quot;. Si necesita crear una configuración nueva, haga clic en el botón de la llave inglesa.

Para crear un servicio en la nube de Adobe Mobile Service, hay que seguir dos pasos: la conexión con el servicio y seleccionar qué grupo de informes asignar a la configuración.

Para empezar, haga clic en el botón &quot;+&quot; del mosaico Administrar Cloud Services del tablero.

![chlimage_1-126](assets/chlimage_1-126.png)

Al hacer clic en el botón **+** botón &#39;, la variable **Agregar Cloud Service** se mostrará el asistente.

![chlimage_1-127](assets/chlimage_1-127.png)

Seleccione o cree una nueva configuración de servicio móvil rellenando los campos obligatorios, como se muestra a continuación. El administrador de AEM necesitará esta información para crear correctamente la conexión a Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Una vez que haya completado la Configuración de cuenta de Mobile Services, se le pedirá que seleccione una aplicación. Al hacerlo, se conecta el informe de análisis de Adobe Mobile Service a esa aplicación.

Seleccione el servicio móvil deseado y haga clic en &quot;Actualizar&quot; para asignar la configuración del servicio móvil y cerrar el cuadro de diálogo.

Ahora que ha asociado la configuración del servicio móvil a la aplicación de AEM Mobile, el mosaico empezará a recuperar los datos de la métrica y a comenzar a generar informes.

![chlimage_1-129](assets/chlimage_1-129.png)

### Archivo de configuración del SDK de Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

En este punto, la aplicación móvil está asociada a un servicio en la nube, pero la aplicación móvil aún no sabe cómo volver a comunicar a Adobe Analytics las métricas móviles recopiladas. Para conectar la aplicación móvil a Adobe Analytics, es necesario agregar el archivo de configuración del SDK de Adobe Mobile Services a Adobe Experience Manager.

En el mosaico Analizar métricas , haga clic en el icono de flecha para mostrar las entradas del menú Descargar / Cargar configuración del SDK de AMS .

![chlimage_1-130](assets/chlimage_1-130.png)

El primer paso es obtener la configuración del SDK desde Adobe Mobile Services. Si hace clic en Descargar configuración del SDK de AMS, se le redirigirá al sitio web de Adobe Mobile Services, desde donde podrá descargar el archivo de configuración. Una vez que haya obtenido el archivo ADBMobileConfig.json , haga clic en &quot;Cargar la configuración del SDK de AMS&quot; para cargar el archivo de configuración en AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Haga clic en el botón &quot;Cargar configuración de aplicación de Adobe Mobile Services&quot;, busque el archivo ADBMobileConfig.json y, a continuación, haga clic en &quot;Cargar&quot;.

Ahora que la aplicación móvil tiene acceso al archivo ADBMobileConfig.json , tiene conocimientos sobre cómo comunicarse con Adobe Analytics y empezar a generar informes sobre el valor de las métricas importantes que le ayudarán a mejorar el éxito de sus aplicaciones.

## Siguientes pasos? {#what-s-next}

1. [Iniciar mi experiencia en la aplicación de AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Administrar el contenido de mi aplicación](/help/mobile/phonegap-manage-app-content.md)
1. [Generar mi aplicación](/help/mobile/building-app-mobile-phonegap.md)
1. [Seguimiento del rendimiento de mi aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofrecer una experiencia de aplicación personalizada con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensajes importantes a mis usuarios](/help/mobile/phonegap-push-notifications.md)
