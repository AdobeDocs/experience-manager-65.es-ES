---
title: Añadir Adobe Analytics a la aplicación móvil
description: Siga esta página para obtener más información sobre cómo puede utilizar el análisis de aplicaciones móviles en sus aplicaciones Adobe Experience Manager mediante la integración con Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Añadir Adobe Analytics a la aplicación móvil{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

¿Quiere crear experiencias atractivas y relevantes para los usuarios de sus aplicaciones móviles? Si no utiliza el SDK de Adobe Mobile Services para monitorizar y medir el ciclo vital y el uso de las aplicaciones, ¿en qué basa sus decisiones? ¿Dónde están sus clientes más fieles? ¿Cómo puede garantizar que sigue siendo relevante y que optimiza las conversiones?

¿Los usuarios están accediendo a todo el contenido? ¿Están abandonando la aplicación y, si es así, dónde? ¿Con qué frecuencia permanecen en la aplicación y con qué frecuencia regresan para utilizarla? ¿Qué cambios puede introducir y luego medir ese aumento de la retención? ¿Qué sucede con las tasas de bloqueo? ¿Se bloquea la aplicación para los usuarios?

Aproveche las ventajas de [Análisis de aplicaciones móviles](https://business.adobe.com/products/analytics/mobile-marketing.html) en sus aplicaciones de Adobe Experience Manager AEM () mediante la integración con [Adobe Mobile Services](https://business.adobe.com/products/campaign/mobile-marketing.html).

AEM Instrumente sus aplicaciones móviles para realizar un seguimiento, generar informes y comprender cómo los usuarios interactúan con el contenido y la aplicación móvil, así como para medir métricas clave del ciclo vital como inicios, tiempo en la aplicación y tasa de bloqueo.

AEM En esta sección se describe cómo se realiza la *Desarrolladores* puede:

* Integración de Mobile Analytics en la aplicación móvil
* Pruebe el seguimiento de análisis con Bloodhound

## Requisitos previos {#prerequisties}

AEM Mobile requiere una cuenta de Adobe Analytics para recopilar y crear informes con los datos de seguimiento en la aplicación. AEM Como parte de la configuración de, la opción de configuración de la opción de configuración de la *Administrador* primero debe:

* Configure una cuenta de Adobe Analytics y cree un grupo de informes para su aplicación en Mobile Services.
* Configuración de un Cloud Service de AMS en Adobe Experience Manager AEM ().

## Para desarrolladores: Integración de Mobile Analytics en la aplicación {#for-developers-integrate-mobile-analytics-into-your-app}

### Configurar ContentSync para extraer el archivo de configuración {#configure-contentsync-to-pull-in-configuration-file}

Una vez creada la cuenta de Analytics, cree una configuración de sincronización de contenido para extraer el contenido en la aplicación móvil.

Para obtener más información, consulte Configuración del contenido de sincronización de contenido. La configuración debe indicar a Content Sync que coloque ADBMobileConfig en el directorio /www. Por ejemplo, en la aplicación de Geometrixx Outdoors, la configuración de sincronización de contenido se encuentra en: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. También hay una configuración para desarrollo; sin embargo, es idéntica a la configuración de no desarrollo en el caso de los Geometrixx Outdoors.

AEM Para obtener más información sobre cómo descargar ADBMobileConfig desde el panel de aplicaciones de la aplicación móvil, consulte Analytics: Mobile Services: archivo de configuración del SDK de Adobe Mobile Services.

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

Si se genera con la CLI de PhoneGap, esto se puede hacer con una compilación de cordova de scripts de gancho. Esto se puede ver en la aplicación Geometrixx Outdoors en:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Para iOS, el archivo debe copiarse en el del proyecto XCode. **Recursos** (por ejemplo, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si el destino de la aplicación es Android™, la ruta a la que se copiará es &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Para obtener más información sobre el uso de vínculos durante la compilación de la CLI de PhoneGap, consulte [Tres enlaces que necesita su proyecto Cordova/PhoneGap](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

Para que la aplicación recopile los datos, es necesario incluir el complemento Adobe Mobile Services (AMS) como parte de la aplicación. Al incluir el complemento como una característica en el config.xml de la aplicación, se puede utilizar otro gancho de Cordova para agregar automáticamente el complemento durante el proceso de PhoneGap Build.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

El archivo config.xml de la aplicación para Geometrixx Outdoors se encuentra en */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. El ejemplo anterior solicita una versión específica del complemento para utilizarla agregando &quot;#&quot; y un valor de etiqueta después de la dirección URL del complemento. Se trata de una práctica recomendada a seguir para garantizar que no aparezcan problemas no anticipados debido a que se agregan complementos no probados durante una compilación.

Después de realizar estos pasos, la aplicación podrá crear informes de todas las métricas del ciclo vital proporcionadas por Adobe Analytics. Esto incluye datos como lanzamientos, bloqueos e instalaciones. Si esos son los únicos datos que te importan, entonces ya está. Si desea recopilar datos personalizados, debe instrumentar el código.

### Instrumente su código para el seguimiento completo de la aplicación {#instrument-your-code-for-full-app-tracking}

Hay varias API de seguimiento en la variable [API de complemento de PhoneGap de AMS.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

Esto le permitirá realizar un seguimiento de estados y acciones, como adónde van los usuarios a las páginas en la aplicación y qué controles se utilizan más. La forma más sencilla de instrumentar la aplicación para el seguimiento es utilizar las API de Analytics proporcionadas por el complemento de AMS.

* ADB.trackState()
* ADB.trackAction()

Como referencia, consulte el código en la aplicación de Geometrixx Outdoors. En la aplicación de los Geometrixx Outdoors, se realiza un seguimiento de toda la navegación por páginas mediante el método ADB.trackState(). Para obtener más información, consulte el código fuente de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Al instrumentar el código fuente con estas llamadas al método, puede recopilar métricas completas para la aplicación.

#### Propiedades para conectarse a AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l expone las siguientes propiedades para conectarse a AMS:

| **Etiqueta** | **Descripción** | **Predeterminado** |
|---|---|---|
| Punto final de API | La URL base de las API HTTP de Adobe Mobile Services | https://api.omniture.com |
| Extremo de configuración | La URL utilizada para recuperar la configuración de ADB Mobile para el ID de grupo de informes determinado | /ams/1.0/app/config/ |
| Aplicaciones de Mobile Services | Obtener una lista de aplicaciones dentro de la compañía de los usuarios | /ams/1.0/apps |
