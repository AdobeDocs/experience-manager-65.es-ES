---
title: Seguimiento del rendimiento de las aplicaciones con Adobe Mobile Analytics
seo-title: Track App Performance with Adobe Mobile Analytics
description: Con Adobe Mobile Services, puede obtener información sobre cómo utilizan sus usuarios las aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de los dispositivos y otras muchas métricas esenciales para sus aplicaciones móviles. Siga esta página para obtener más información.
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

# Seguimiento del rendimiento de las aplicaciones con Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Desea aumentar las conversiones y la lealtad de los clientes.

Desea ofrecer experiencias relevantes y atractivas a sus clientes.

¿Qué hace su aplicación de AEM Mobile para sus campañas de marketing?

¿Cómo puede ajustar mejor sus aplicaciones móviles para proporcionar la mejor experiencia a sus usuarios?

Con Adobe Mobile Services, puede obtener información sobre cómo utilizan sus usuarios las aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de los dispositivos y otras muchas métricas esenciales para sus aplicaciones móviles.

Adobe Experience Manager Mobile proporciona un vistazo a los detalles de su análisis móvil directamente desde el panel de aplicaciones de AEM Mobile. El **Mosaico de métricas móviles** en el tablero proporciona análisis en tiempo real para su aplicación móvil, lo que permite a desarrolladores, autores y administradores obtener un vistazo rápido del estado de su aplicación móvil. Bajo las cubiertas que alimentan el análisis se encuentra la [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. El SDK de Adobe Mobile Analytics se puede conectar a sus aplicaciones de forma nativa o a través de un complemento de PhoneGap Bridge para vistas web. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta este, momento en el que los datos se insertan en Adobe Mobile Services Cloud para la realización de informes y análisis.

El SDK de Adobe Mobile Analytics proporciona lo siguiente:

1. **Recopilación de datos para canales móviles** - Recopile datos completos para sus sitios web y aplicaciones móviles en todos los sistemas operativos principales.
1. **Análisis de participación móvil** : Comprenda la participación del usuario en su aplicación móvil, sitio web o vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Paneles e informes de aplicaciones móviles** : Obtenga informes de uso que incluyen métricas del ciclo vital para sus aplicaciones y métricas de la tienda de aplicaciones. Consulte tendencias para usuarios, inicios, duración promedio de la sesión, duración de la retención y bloqueos.
1. **Análisis de campañas móviles** - Cuantifique la eficacia de campañas específicas para móviles como SMS, anuncios de búsqueda móviles, anuncios en pantalla móviles y códigos QR.
1. **Análisis de geolocalización** - Encuentre dónde inician los usuarios de su aplicación e interactúen con sus experiencias móviles mediante la ubicación GPS o puntos de interés.
1. **Análisis de rutas** : Consulte cómo navegan los usuarios por la aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles provocan que estos bajen.

Esta sección describe cómo [AEM Desarrolladores de](#developers) A continuación, puede aprender a instrumentar aplicaciones de AEM Mobile con el seguimiento de analytics.

Finalmente, [AEM Administradores de](#administrators) aprenda a:

* crear un servicio en la nube para Adobe Mobile Services
* crear una configuración de mobile service y asociar un grupo de informes
* asociar la configuración de mobile service a una aplicación móvil.
* AEM visualización de métricas a través del Centro de comandos de aplicaciones para la aplicación de
* asigne la configuración del SDK de AMS a su aplicación móvil

## Para desarrolladores: Integración de Analytics en la aplicación {#for-developers-integrate-analytics-into-your-app}

**Requisito previo:** AEM Los administradores de deben configurar la configuración de nube de Adobe Mobile Services, [como se discute a continuación](#amscloudserviceconfig).

Los desarrolladores son responsables de [adición de analytics a una aplicación de AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) según sea necesario para realizar el seguimiento, informar y comprender cómo los usuarios interactúan con el contenido de su aplicación móvil y para medir métricas clave del ciclo vital como inicios, tiempo en la aplicación y tasa de bloqueo.

## Para administradores: Configuración del Cloud Service de Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aprovechar Adobe AEM Mobile Services, debe configurar el Cloud Service de Adobe Mobile Services con la información de la cuenta de Adobe Analytics para que se pueda configurar de forma correcta. El Centro de comandos de aplicaciones proporciona un **Analizar métricas** mosaico en el que puede crear y asociar el servicio en la nube con su aplicación móvil.

Para configurar el servicio en la nube en la aplicación móvil, comience por hacer clic en el icono de engranaje situado en el mosaico Analizar métricas.

![chlimage_1-125](assets/chlimage_1-125.png)

Al hacer clic en el icono del engranaje en el mosaico Analizar métricas, se abrirá el cuadro de diálogo modal &quot;Configurar análisis de Mobile Services&quot;. Seleccione la configuración en la lista desplegable &quot;Seleccionar una configuración de Mobile Services&quot;. Si necesita crear una nueva configuración, haga clic en el botón de la llave inglesa.

Para crear un servicio en la nube de Adobe Mobile Service, hay que seguir dos pasos: la conexión al servicio y seleccionar qué grupo de informes asignar a la configuración.

Para empezar, haga clic en el botón &quot;+&quot; en el mosaico Administrar Cloud Services del panel.

![chlimage_1-126](assets/chlimage_1-126.png)

Al hacer clic en &#39;**+**&#39;, el botón **Añadir Cloud Service** se mostrará el asistente.

![chlimage_1-127](assets/chlimage_1-127.png)

Seleccione o cree una nueva configuración de Mobile Services rellenando los campos obligatorios como se muestra a continuación. AEM El administrador de la aplicación necesitará esta información para crear correctamente la conexión con Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Una vez completada la Configuración de cuenta de Mobile Services, se le pedirá que seleccione una aplicación. Al hacerlo, se conectan los informes de análisis de Adobe Mobile Services a esa aplicación.

Seleccione el servicio móvil deseado y haga clic en &quot;Actualizar&quot; para asignar la configuración del servicio móvil y cerrar el cuadro de diálogo.

Ahora que ha asociado la configuración del servicio móvil a la aplicación de AEM Mobile, el mosaico empezará a recuperar los datos de la métrica y a generar informes.

![chlimage_1-129](assets/chlimage_1-129.png)

### Archivo de configuración del SDK de Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

En este punto, la aplicación móvil está asociada a un servicio en la nube, pero la aplicación móvil aún no sabe cómo volver a comunicar las métricas móviles recopiladas a Adobe Analytics. Para conectar la aplicación móvil a Adobe Analytics, es necesario agregar el archivo de configuración del SDK de Adobe Mobile Services a Adobe Experience Manager.

En el mosaico Analizar métricas, haga clic en el icono de flecha para mostrar las entradas de menú Descargar/Cargar configuración del SDK de AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

El primer paso es obtener la configuración del SDK desde Adobe Mobile Services. Al hacer clic en &quot;Descargar configuración del SDK de AMS&quot;, se le redirigirá al sitio web de Adobe Mobile Services desde el que puede descargar el archivo de configuración. AEM Una vez que haya obtenido el archivo ADBMobileConfig.json, haga clic en &quot;Cargar configuración del SDK de AMS&quot; para cargar el archivo de configuración en el archivo de configuración de la interfaz de usuario de la aplicación de ADBMobileConfig.json.

![chlimage_1-131](assets/chlimage_1-131.png)

Adobe Haga clic en el botón &quot;Cargar configuración de la aplicación de Mobile Services&quot; y busque el archivo ADBMobileConfig.json; a continuación, haga clic en &quot;Cargar&quot;.

Ahora que la aplicación móvil tiene acceso al archivo ADBMobileConfig.json, tiene conocimientos sobre cómo volver a comunicarse con Adobe Analytics y comenzar a crear informes sobre esos importantes valores de métricas que ayudarán a impulsar la eficacia de sus aplicaciones.

## Siguientes pasos? {#what-s-next}

1. [Iniciar la experiencia de mi aplicación de AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Administrar el contenido de mi aplicación](/help/mobile/phonegap-manage-app-content.md)
1. [Generar mi aplicación](/help/mobile/building-app-mobile-phonegap.md)
1. [Realizar un seguimiento del rendimiento de mi aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofrezca una experiencia de aplicación personalizada con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensajes importantes a mis usuarios](/help/mobile/phonegap-push-notifications.md)
