---
title: Desarrollo de aplicaciones móviles en AEM
seo-title: Desarrollo de aplicaciones móviles en AEM
description: Siga esta página para desarrollar inicio aplicaciones móviles en AEM con Adobe PhoneGap Enterprise.
seo-description: Siga esta página para desarrollar inicio aplicaciones móviles en AEM con Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Desarrollo de aplicaciones móviles en AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM aprovecha las soluciones de publicación de Adobe PhoneGap y Adobe, lo que le permite crear y administrar aplicaciones móviles multiplataforma, tanto enriquecidas con contenido como basadas en utilidades:

* Administre todas las aplicaciones móviles de compañías en un solo lugar.
* Revise las aplicaciones en entornos de desarrollo y ensayo sin las complejidades de los perfiles de aprovisionamiento ni el esfuerzo adicional de crear y cargar la aplicación para compartirla.
* Utilice el entorno de creación de AEM para crear y administrar contenido enriquecido para sus aplicaciones.
* Utilice HTML5 con Adobe PhoneGap para crear experiencias enriquecidas con funciones nativas del dispositivo.
* Presente las vistas web de HTML5 a aplicaciones **nativas** nuevas o preexistentes a través de las vistas web de Cordova.
* Cree, depure y comparta contenido multimedia enriquecido en todos los canales de envío, incluidos los de web, web móvil, aplicación móvil e impresión.

AEM se integra con el Adobe **[servicio de PhoneGap Build](https://build.phonegap.com/)** para simplificar el proceso de implementación y compilación de aplicaciones.

**Adobe** ContentSyncenable permite a los usuarios descargar fácilmente las actualizaciones de página y contenido de Over-the-Air (OTA) en sus dispositivos sin tener que volver a instalar la aplicación ni descargar desde AppStore, Google Play u otras fuentes de la aplicación.

**Adobe** Analytics está totalmente integrado en AEM aplicaciones y permite un seguimiento detallado de la distribución, la geolocalización, los sistemas operativos, los dispositivos, los flujos de clics, el seguimiento de iBeacon y mucho más.

## Creación de aplicaciones {#creating-apps}

Los desarrolladores pueden utilizar el [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) junto con los recursos adicionales que se encuentran en [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para arrancar aplicaciones de AEM con PhoneGap, incluida una aplicación nativa de referencia que ejecute Cordova Webviews.

El archivo léame del repositorio de Starter Kit Git incluye un tutorial para utilizar el kit de arranque:

* Personalización de la marca
* Destinatarios de implementación y compilación de muestra de Maven
* Configuración del repositorio de control de código fuente
* Instalación e implementación en instancias de AEM locales o remotas
* Desinstalar desde AEM

>[!NOTE]
>
>Encontrará fuentes de implementación de referencia adicionales, incluyendo laboratorios, en GitHub [aquí](https://github.com/adobe-marketing-cloud-apps) y, la fuente de &quot;fregadero-cocina&quot; [aquí](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desarrollo para hosts de IOS 9 y HTTP {#developing-for-ios-and-http-hosts}

Los desarrolladores de IOS deben tener en cuenta un problema abierto con las aplicaciones de Cordova que se ejecutan en iOS 9. Este problema impide que las solicitudes se realicen en hosts inseguros (como *http://localhost:4502*). Este problema se resolverá con una próxima versión de cordova-ios (consumida por la CLI de Cordova), pero mientras tanto hay dos soluciones alternativas disponibles:

1. Como solución alternativa inmediata, puede seguir utilizando cualquiera de los simuladores de iOS 8 sin problemas.
1. Si debe utilizar iOS 9, el archivo de aplicaciones -Info.plist (que se encuentra después de ejecutar `cordova platform add ios` en &quot;&lt;app root>/platform/ios/&lt;app name>/&lt;app name>-Info.plist&quot;) se puede editar manualmente para incluir la siguiente propiedad:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obtener más información sobre &quot;App Transport Security&quot;, consulte la siguiente sección de [documentos de evaluación de iOS9 de Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) y este [análisis de desbordamiento de pila](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Desarrollo de aplicaciones móviles en AEM {#developing-mobile-applications-in-aem-1}

* [Inicio AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creación de aplicaciones móviles](/help/mobile/building-app-mobile-phonegap.md)
* [Estructurar una aplicación](/help/mobile/phonegap-structure-an-app.md)
* [Creación y edición de aplicaciones con la consola Aplicaciones](/help/mobile/phonegap-apps-console.md)
* [Aplicaciones de una sola página](/help/mobile/phonegap-single-page-applications.md)
* [Desarrollo de aplicaciones con la CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Acceder a las funciones del dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Seguimiento del rendimiento de la aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Añadir Adobe Analytics a su aplicación móvil](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificaciones push](/help/mobile/phonegap-push-notifications.md)
* [Personalización de contenido de AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [La anatomía de una aplicación](/help/mobile/phonegap-apps-arch.md)
* [¿Su aplicación híbrida está lista para AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Creación para Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
