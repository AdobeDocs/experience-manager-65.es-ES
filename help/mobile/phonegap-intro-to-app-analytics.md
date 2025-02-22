---
title: Seguimiento del rendimiento de las aplicaciones con Adobe Mobile Analytics
description: Con Adobe Mobile Services, puede obtener información sobre el uso que hacen los usuarios de sus aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de dispositivos y otras métricas esenciales para sus aplicaciones móviles. Siga esta página para obtener más información.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Seguimiento del rendimiento de las aplicaciones con Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

{{ue-over-mobile}}

Desea aumentar las conversiones y la lealtad de los clientes.

Desea ofrecer experiencias relevantes y atractivas a sus clientes.

¿Qué hace su aplicación de AEM Mobile para sus campañas de marketing?

¿Cómo puede ajustar mejor sus aplicaciones móviles para proporcionar la mejor experiencia a sus usuarios?

Con Adobe Mobile Services, puede obtener información sobre el uso que hacen los usuarios de sus aplicaciones móviles mediante el seguimiento del uso, los bloqueos de aplicaciones, los detalles de dispositivos y otras métricas esenciales para sus aplicaciones móviles.

Adobe Experience Manager Mobile proporciona un vistazo a los detalles de su análisis móvil directamente desde el panel de aplicaciones de AEM Mobile. El **mosaico de métricas móviles** del panel proporciona Real-Time Analytics para su aplicación móvil, lo que permite a desarrolladores, autores y administradores obtener un vistazo rápido del estado de su aplicación móvil. En las portadas, el SDK de [Adobe Mobile Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html) se encarga de alimentar los análisis. El SDK de Adobe Mobile Analytics puede conectarse a sus aplicaciones de forma nativa o a través de un complemento de PhoneGap Bridge para visualizaciones web. Las métricas se recopilan y almacenan en caché en el dispositivo hasta que se conecta este, momento en el que los datos se insertan en Adobe Mobile Services Cloud para la realización de informes y análisis.

Adobe Mobile Analytics SDK proporciona lo siguiente:

1. **Recopilación de datos para canales móviles**: recopile datos completos para sus sitios web y aplicaciones móviles en todos los sistemas operativos principales.
1. **Análisis de participación móvil**: Comprenda la participación del usuario en su aplicación móvil, sitio web o vídeo, incluida la frecuencia con la que los consumidores inician el canal, si realizan compras en él y mucho más.
1. **Paneles e informes de aplicaciones móviles**: obtenga informes de uso que incluyan métricas del ciclo vital para sus aplicaciones y métricas de la tienda de aplicaciones; consulte tendencias para usuarios, inicios, duración promedio de la sesión, duración de la retención y bloqueos.
1. **Análisis de campañas móviles**: Cuantifique la eficacia de campañas específicas para móviles como SMS, anuncios de búsquedas móviles, anuncios en pantallas móviles y códigos QR.
1. **Análisis de geolocalización**: encuentre dónde inician los usuarios de su aplicación e interactúen con sus experiencias móviles mediante la ubicación GPS o puntos de interés.
1. **Análisis de rutas**: vea cómo navegan los usuarios por su aplicación para determinar qué pantallas y elementos de la interfaz de usuario atraen a los usuarios y cuáles hacen que abandonen los usuarios.

AEM En esta sección se describe cómo [desarrolladores](#developers) pueden aprender a instrumentar las aplicaciones de AEM Mobile con el seguimiento de análisis.

AEM Por último, [Administradores de](#administrators) aprenden a:

* crear un servicio en la nube para Adobe Mobile Services
* crear una configuración de mobile service y asociar un grupo de informes
* asociar la configuración de mobile service a una aplicación móvil.
* AEM visualización de métricas a través del Centro de comandos de aplicaciones para la aplicación de
* asigne la configuración de SDK de AMS a su aplicación móvil

## Para desarrolladores: Integración de Analytics en la aplicación {#for-developers-integrate-analytics-into-your-app}

AEM **Requisito previo:** los administradores de la deben configurar la configuración de nube de Adobe Mobile Services, [como se describe a continuación](#amscloudserviceconfig).

Los desarrolladores son responsables de [agregar análisis a una aplicación de AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) según sea necesario para realizar el seguimiento, generar informes y comprender cómo los usuarios interactúan con el contenido de la aplicación móvil, así como para medir métricas clave del ciclo vital como inicios, tiempo en la aplicación y tasa de bloqueo.

## Para administradores: Configuración del Cloud Service de Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aprovechar Adobe AEM Mobile Services, debe configurar el Cloud Service de Adobe Mobile Services con la información de la cuenta de Adobe Analytics. El Centro de comandos de aplicaciones proporciona un mosaico **Analizar métricas** en el que puede crear y asociar el servicio en la nube con su aplicación móvil.

Para configurar el servicio en la nube en la aplicación móvil, comience por hacer clic en el icono de engranaje en el mosaico Analizar métricas.

![chlimage_1-125](assets/chlimage_1-125.png)

Al hacer clic en el icono de engranaje en el mosaico Analizar métricas, se abre el cuadro de diálogo modal &quot;Configurar Analytics de Mobile Services&quot;. Seleccione la configuración en la lista desplegable &quot;Seleccionar una configuración de Mobile Services&quot;. Si debe crear una configuración, haga clic en el botón de la llave inglesa.

Para crear un servicio en la nube de Adobe Mobile Service, hay que seguir dos pasos: la conexión al servicio y seleccionar qué grupo de informes asignar a la configuración.

Para empezar, haga clic en el botón &quot;+&quot; en el mosaico Administrar Cloud Service del panel.

![chlimage_1-126](assets/chlimage_1-126.png)

Después de hacer clic en el botón &#39;**+**&#39;, se muestra el asistente **Agregar Cloud Service**.

![chlimage_1-127](assets/chlimage_1-127.png)

Seleccione o cree una configuración de Mobile Services rellenando los campos obligatorios como se muestra a continuación. AEM El administrador de la aplicación requiere esta información para crear correctamente la conexión con Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Una vez completada la Configuración de cuenta de Mobile Services, se le pedirá que seleccione una aplicación. Al hacerlo, se conectan los informes de análisis de Adobe Mobile Services a esa aplicación.

Seleccione el servicio móvil deseado y haga clic en &quot;Actualizar&quot; para asignar la configuración del servicio móvil y cerrar el cuadro de diálogo.

Ahora que ha asociado la configuración del servicio móvil a la aplicación de AEM Mobile, el mosaico empieza a recuperar los datos de la métrica y a generar informes.

![chlimage_1-129](assets/chlimage_1-129.png)

### Archivo de configuración de SDK de Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

En este punto, la aplicación móvil está asociada a un servicio en la nube, pero la aplicación móvil aún no sabe cómo devolver a Adobe Analytics las métricas móviles recopiladas. Para conectar la aplicación móvil a Adobe Analytics, se debe añadir el archivo de configuración de SDK de Adobe Mobile Services a Adobe Experience Manager.

En el mosaico Analizar métricas, haga clic en el icono de flecha para mostrar las entradas de menú Descargar/Cargar configuración de SDK de AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

El primer paso es obtener la configuración de SDK desde Adobe Mobile Services. Haga clic en &quot;Descargar configuración de SDK de AMS&quot; para que se le redirija al sitio web de Adobe Mobile Services, desde donde puede descargar el archivo de configuración. Una vez obtenido el archivo ADBMobileConfig.json, haga clic en &quot;Cargar configuración de SDK AEM de AMS&quot; para cargar el archivo de configuración en el archivo de configuración de la aplicación de configuración de la aplicación de configuración de la aplicación de configuración de la plataforma de almacenamiento de datos de Adobe (ADBMobileConfig.json).

![chlimage_1-131](assets/chlimage_1-131.png)

Adobe Haga clic en el botón &quot;Cargar configuración de la aplicación de Mobile Services&quot; y busque el archivo ADBMobileConfig.json; a continuación, haga clic en &quot;Cargar&quot;.

Ahora que la aplicación móvil tiene acceso al archivo ADBMobileConfig.json, tiene los conocimientos sobre cómo volver a comunicarse con Adobe Analytics y comenzar a crear informes sobre esos valores de métricas importantes que ayudan a impulsar la eficacia de sus aplicaciones.

## ¿Qué sigue? {#what-s-next}

1. [Iniciar la experiencia de mi aplicación de AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Administrar el contenido de mi aplicación](/help/mobile/phonegap-manage-app-content.md)
1. [Generar mi aplicación](/help/mobile/building-app-mobile-phonegap.md)
1. [Realizar un seguimiento del rendimiento de mi aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofrezca una experiencia de aplicación personalizada con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensajes importantes a mis usuarios](/help/mobile/phonegap-push-notifications.md)
