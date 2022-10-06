---
title: Añadir Adobe Analytics a la aplicación móvil
seo-title: Add Adobe Analytics to your Mobile Application
description: Siga esta página para obtener información sobre cómo puede utilizar Mobile App Analytics en sus aplicaciones AEM mediante la integración con Adobe Mobile Services.
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Añadir Adobe Analytics a la aplicación móvil{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

¿Quiere crear experiencias atractivas y relevantes para los usuarios de su aplicación móvil? Si no utiliza el SDK de Adobe Mobile Services para supervisar y medir el ciclo de vida y el uso de las aplicaciones, ¿en qué basa sus decisiones? ¿Dónde están sus clientes más fieles? ¿Cómo puede garantizar que sigue siendo relevante y optimizando las conversiones?

¿Los usuarios acceden a todo el contenido? ¿Están abandonando la aplicación y, en caso afirmativo, dónde? ¿Con qué frecuencia permanecen en la aplicación y con qué frecuencia vuelven para usar la aplicación? ¿Qué cambios puede introducir y luego medir ese aumento de la retención? ¿Qué sucede con las tasas de bloqueo, si su aplicación se bloquea para sus usuarios?

Aproveche [Análisis de aplicaciones móviles](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) en sus aplicaciones AEM integrando con [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Instrumente sus aplicaciones AEM para realizar un seguimiento, informar y comprender cómo los usuarios interactúan con su aplicación móvil y contenido, y para medir métricas clave del ciclo vital como inicios, tiempo en la aplicación y tasa de bloqueo.

Esta sección describe cómo AEM *Desarrolladores* puede:

* Integrar Mobile Analytics en la aplicación móvil
* Pruebe el seguimiento de análisis con Bloodhound

## Requisitos previos {#prerequisties}

AEM Mobile requiere una cuenta de Adobe Analytics para recopilar datos de seguimiento y crear informes de ellos en la aplicación. Como parte de la configuración, la AEM *Administrador* primero tendrá que :

* Configure una cuenta de Adobe Analytics y cree un grupo de informes para la aplicación en Mobile Services.
* Configuración de un Cloud Service de AMS en Adobe Experience Manager (AEM).

## Para desarrolladores: Integre Mobile Analytics en su aplicación {#for-developers-integrate-mobile-analytics-into-your-app}

### Configure ContentSync para extraer el archivo de configuración {#configure-contentsync-to-pull-in-configuration-file}

Una vez configurada la cuenta de Analytics, deberá crear una configuración de sincronización de contenido para extraer el contenido en la aplicación móvil.

Para obtener más información, consulte Configuración del contenido de sincronización de contenido . La configuración deberá indicar a Content Sync que coloque ADBMobileConfig en el directorio /www. Por ejemplo, en la aplicación de Geometrixx Outdoors, la configuración de sincronización de contenido se encuentra en: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. También hay una configuración para el desarrollo; sin embargo, es idéntico a la configuración que no es de desarrollo en el caso de los Geometrixx Outdoors.

Para obtener más información sobre cómo descargar ADBMobileConfig desde el panel Aplicaciones AEM móviles, consulte Analytics - Mobile Services - Archivo de configuración del SDK de Adobe Mobile Services.

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

Si se crea con la CLI de PhoneGap, esto se puede hacer con un script de enlace de compilación de cordova. Esto se puede ver en la aplicación Geometrixx Outdoors en:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para iOS, el archivo deberá copiarse en el proyecto XCode **Recursos** directorio (p. ej. &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si la aplicación está dirigida a Android, la ruta a la que copiar es &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obtener más información sobre el uso de los enlaces durante la compilación de la CLI de PhoneGap, consulte [Tres enlaces a las necesidades del proyecto Cordova/PhoneGap](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

### Añadir el complemento de AMS en la aplicación {#add-the-ams-plugin-in-the-app}

Para que la aplicación recopile los datos, el complemento de Adobe Mobile Services (AMS) debe incluirse como parte de la aplicación. Al incluir el complemento como una función en el archivo config.xml de la aplicación, se puede utilizar otro vínculo de Cordova para agregar automáticamente el complemento durante el proceso de compilación de PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

El archivo Geometrixx Outdoors App config.xml se encuentra en */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. El ejemplo anterior solicita una versión específica del complemento para utilizarlo añadiendo un &#39;#&#39; y, a continuación, un valor de etiqueta después de la dirección URL del complemento. Esta es una buena práctica a seguir para garantizar que no aparezcan problemas no previstos debido a que los complementos no probados se agregan durante una compilación.

Después de realizar estos pasos, su aplicación estará habilitada para informar de todas las métricas del ciclo vital proporcionadas por Adobe Analytics. Esto incluye datos como inicios, bloqueos e instalaciones. Si esos son los únicos datos que les importan, entonces ya están hechos. Si desea recopilar datos personalizados, deberá instrumentar el código.

### Instrumente su código para el seguimiento completo de la aplicación {#instrument-your-code-for-full-app-tracking}

Hay varias API de seguimiento proporcionadas en la variable [API del complemento AMS Phonegap.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Esto le permitirá realizar el seguimiento de estados y acciones, como por ejemplo hacia dónde navegan los usuarios en la aplicación, a qué controles se utilizan más. La forma más sencilla de instrumentar su aplicación para el seguimiento es utilizar las API de Analytics proporcionadas por el complemento de AMS.

* ADB.trackState()
* ADB.trackAction()

Como referencia, puede consultar el código en la aplicación de Geometrixx Outdoors. En la aplicación de Geometrixx Outdoors, se realiza un seguimiento de todas las navegaciones de página mediante el método ADB.trackState() . Para obtener más información, consulte el código fuente de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Al instrumentar el código fuente con estas llamadas de método, puede recopilar métricas completas para su aplicación.

#### Propiedades para conectarse a AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileserservices.impl.service.MobileServicesHttpClientImp* l expone las siguientes propiedades para conectarse a AMS:

| **Etiqueta** | **Descripción** | **Predeterminado** |
|---|---|---|
| Punto final de API | La URL base de las API HTTP de Adobe Mobile Services | https://api.omniture.com |
| Punto final de configuración | La URL utilizada para recuperar la configuración móvil de ADB para el ID del grupo de informes determinado | /ams/1.0/app/config/ |
| Aplicaciones de Mobile Services | Obtener una lista de aplicaciones dentro de la empresa de usuarios | /ams/1.0/apps |
