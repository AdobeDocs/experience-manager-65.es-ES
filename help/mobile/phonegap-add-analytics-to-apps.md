---
title: Agregar Adobe Analytics a la aplicación móvil
seo-title: Agregar Adobe Analytics a la aplicación móvil
description: Siga esta página para conocer cómo puede utilizar Mobile App Analytics en sus aplicaciones AEM mediante la integración con Adobe Mobile Services.
seo-description: Siga esta página para conocer cómo puede utilizar Mobile App Analytics en sus aplicaciones AEM mediante la integración con Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Agregar Adobe Analytics a la aplicación móvil{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

¿Desea crear experiencias atractivas y relevantes para los usuarios de aplicaciones móviles? Si no utiliza el SDK de Adobe Mobile Services para supervisar y medir el ciclo de vida y el uso de las aplicaciones, ¿en qué se basan sus decisiones? ¿Dónde están sus clientes más leales? ¿Cómo puede garantizar que sigue siendo relevante y optimizando las conversiones?

¿Los usuarios están accediendo a todo el contenido? ¿Están abandonando la aplicación y, en caso afirmativo, dónde? ¿Con qué frecuencia se quedan en la aplicación y con qué frecuencia vuelven a utilizarla? ¿Qué cambios puede introducir y luego medir ese aumento de la retención? ¿Qué sucede con las tasas de bloqueo, si la aplicación se bloquea para los usuarios?

Aproveche [Mobile App Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) en sus aplicaciones AEM mediante la integración con [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Instrumente sus aplicaciones de AEM para rastrear, informar y comprender cómo los usuarios interactúan con su aplicación móvil y contenido, así como para medir métricas clave del ciclo vital como inicios, tiempo en la aplicación y tasa de bloqueo.

En esta sección se describe cómo *los desarrolladores* de AEM pueden:

* Integrar Mobile Analytics en la aplicación móvil
* Probar el seguimiento de análisis con Bloodhound

## Prerrequisitos {#prerequisties}

AEM Mobile requiere una cuenta de Adobe Analytics para recopilar y crear informes de los datos de seguimiento en la aplicación. Como parte de la configuración, el *administrador* de AEM primero deberá:

* Configure una cuenta de Adobe Analytics y cree un grupo de informes para la aplicación en Mobile Services.
* Configure un servicio de nube de AMS en Adobe Experience Manager (AEM).

## Para desarrolladores: Integrar Mobile Analytics en la aplicación {#for-developers-integrate-mobile-analytics-into-your-app}

### Configure ContentSync para extraer el archivo de configuración {#configure-contentsync-to-pull-in-configuration-file}

Una vez configurada la cuenta de Analytics, deberá crear una configuración de sincronización de contenido para extraer el contenido de la aplicación móvil.

Para obtener más información, consulte Configuración del contenido de sincronización de contenido. La configuración deberá indicar a Content Sync que coloque ADBMobileConfig en el directorio /www. Por ejemplo, en la aplicación Geometrixx Outdoors, la configuración de la sincronización de contenido se encuentra en: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. También hay una configuración para el desarrollo; sin embargo, es idéntico a la configuración de no desarrollo en el caso de Geometrixx Outdoors.

Para obtener más información sobre cómo descargar ADBMobileConfig desde el panel Aplicaciones AEM de aplicaciones móviles, consulte el archivo de configuración del SDK de Analytics - Mobile Services - Adobe Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Cada plataforma requiere que ADBMobileConfig se copie en una ubicación específica.

Si se genera con la CLI de PhoneGap, esto se puede hacer con una secuencia de comandos de enlace de compilación de cordova. Esto se puede ver en la aplicación Geometrixx Outdoors en:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para iOS, el archivo deberá copiarse en el directorio de **recursos** del proyecto XCode (p. ej. &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si la aplicación está dirigida a Android, la ruta a la que se debe copiar es &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obtener más información sobre el uso de ganchos durante la compilación de la CLI de PhoneGap, consulte [Tres enlaces que necesita](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)su proyecto de Cordova/PhoneGap.

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### Agregar el complemento AMS en la aplicación {#add-the-ams-plugin-in-the-app}

Para que la aplicación recopile los datos, es necesario incluir el complemento Adobe Mobile Services (AMS) como parte de la aplicación. Al incluir el complemento como una función en el archivo config.xml de la aplicación, se puede usar otro enlace de Cordova para agregar automáticamente el complemento durante el proceso de compilación de PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

El archivo config.xml de la aplicación Geometrixx Outdoors se encuentra en */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. El ejemplo anterior solicita una versión específica del complemento que se utilizará agregando un &#39;#&#39; y, a continuación, un valor de etiqueta después de la dirección URL del complemento. Se trata de una buena práctica a seguir para garantizar que no aparezcan problemas imprevistos debido a la adición de complementos no probados durante una compilación.

Después de realizar estos pasos, la aplicación se habilitará para informar de todas las métricas del ciclo vital proporcionadas por Adobe Analytics. Esto incluye datos como inicios, bloqueos e instalaciones. Si esa es la única información que te importa, entonces ya has terminado. Si desea recopilar datos personalizados, deberá instrumentar su código.

### Instrumente el código para el seguimiento completo de la aplicación {#instrument-your-code-for-full-app-tracking}

Existen varias API de seguimiento en la API del complemento [AMS Phonegap.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/phonegap_methods.html)

Esto le permitirá rastrear estados y acciones como dónde navegan los usuarios en la aplicación, qué controles se utilizan con mayor frecuencia. La forma más sencilla de instrumentar su aplicación para el seguimiento es utilizar las API de Analytics proporcionadas por el complemento AMS.

* ADB.trackState()
* ADB.trackAction()

Como referencia, puede consultar el código en la aplicación Geometrixx Outdoors. En la aplicación Geometrixx Outdoors, todas las navegaciones de página se rastrean mediante el método ADB.trackState(). Para obtener más información, consulte el código fuente de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Al instrumentar el código fuente con estas llamadas de método, puede recopilar métricas completas en la aplicación.

### Prueba del seguimiento de Analytics con Bloodhound {#testing-analytics-tracking-with-bloodhound}

![](do-not-localize/chlimage_1.jpeg)

De forma opcional, antes de realizar la implementación en producción, puede utilizar la herramienta de Adobe [Bloodhound](https://marketing.adobe.com/developer/gallery/bloodhound-app-measurement-qa-tool-1) para probar la configuración de análisis. Para probar la configuración de análisis, deberá editar el archivo ADBMobileConfig.json para que apunte al servidor en el que se está ejecutando Bloodhound en lugar del servidor de Analytics real. Para realizar este cambio, desde ADBMobileConfig.json cambie la siguiente entrada.

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "YOUR_TRACKING_SERVER:YOUR_TRACKING_PORT",
...
```

Cambiar para que coincida con esta entrada:

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "localhost:50000",
...
```

Esto redireccionará todos los datos recopilados por el complemento AMS a Bloodhound para que pueda ver los resultados.

#### Propiedades para la conexión a AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobilservices.impl.service.* MobileServicesHttpClientImpl expone las siguientes propiedades para conectarse a AMS:

| **Etiqueta** | **Descripción** | **Valor predeterminado** |
|---|---|---|
| Extremo de API | La dirección URL base de las API HTTP de Adobe Mobile Services | https://api.omniture.com |
| Extremo de configuración | La dirección URL utilizada para recuperar la configuración móvil de ADB para la ID de grupo de informes dada | /ams/1.0/app/config/ |
| Aplicaciones de Mobile Service | Obtener una lista de aplicaciones dentro de la empresa de usuarios | /ams/1.0/apps |

