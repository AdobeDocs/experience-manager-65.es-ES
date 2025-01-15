---
title: AEM Desarrollo de aplicaciones móviles en el sector de la
description: AEM Siga esta página para empezar a desarrollar aplicaciones móviles en el uso de la de Adobe PhoneGap Enterprise.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# AEM Desarrollo de aplicaciones móviles en el sector de la {#developing-mobile-applications-in-aem}

{{ue-over-mobile}}

AEM Utiliza Adobe PhoneGap y Adobe Publishing Solutions, lo que le permite crear y administrar aplicaciones móviles multiplataforma enriquecidas en contenido y basadas en utilidades:

* Administre todas las aplicaciones móviles de su empresa en un solo lugar.
* Revise las aplicaciones en entornos de ensayo y desarrollo sin las complejidades de los perfiles de aprovisionamiento y sin el esfuerzo adicional de crear y cargar la aplicación para compartirla.
* AEM Utilice el entorno de creación de para crear y administrar contenido enriquecido para sus aplicaciones.
* Utilice HTML5 con Adobe PhoneGap para crear experiencias enriquecidas con funciones nativas del dispositivo.
* Presente las vistas web de HTML5 a las aplicaciones **nativas** nuevas o preexistentes a través de las vistas web de Cordova.
* Cree, depure y comparta contenido multimedia enriquecido en todos los canales de envío, incluidos el web, el web móvil, la aplicación móvil y la impresión.

AEM La integración de la aplicación con el servicio de Adobe PhoneGap Build (`https://build.phonegap.com/`) simplifica el proceso de generación e implementación de la aplicación.

**Adobe ContentSync** permite a los usuarios descargar fácilmente actualizaciones de páginas y de contenido por el aire (OTA) en sus dispositivos sin tener que volver a instalar la aplicación ni descargar desde AppStore, Google Play u otras fuentes de aplicaciones.

**Adobe Analytics AEM** está totalmente integrado en las aplicaciones y permite un seguimiento detallado de la distribución, geolocalización, sistemas operativos, dispositivos, flujos de clics, seguimiento de iBeacon y más.

## Creación de aplicaciones {#creating-apps}

AEM AEM Los desarrolladores pueden usar el [Kit de inicio de PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) junto con recursos adicionales que se encuentran en [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para arrancar aplicaciones de con PhoneGap, incluida una aplicación nativa de referencia que ejecuta Cordova Webviews.

El archivo léame del repositorio Git del Starter Kit incluye un tutorial para utilizar el Starter Kit:

* Personalización de la marca
* Objetivos de generación e implementación de muestra de Maven
* Configuración del repositorio de control de Source
* AEM Instalar e implementar en instancias de locales o remotas
* AEM Desinstalar desde la

>[!NOTE]
>
>Encontrará fuentes de implementación de referencia adicionales, incluidos laboratorios, en GitHub [aquí](https://github.com/adobe-marketing-cloud-apps) y en el origen del &quot;receptor de cocina&quot; [aquí](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desarrollo para hosts HTTP y IOS 9 {#developing-for-ios-and-http-hosts}

Los desarrolladores de iOS deben tener en cuenta un problema pendiente con las aplicaciones de Cordova que se ejecutan en iOS 9. Este problema evita que se realicen solicitudes a hosts no seguros (como *http://localhost:4502*). Este problema se resolverá en una próxima versión de cordova-ios (consumido por la CLI de Cordova), pero mientras tanto hay dos soluciones disponibles:

1. Como solución alternativa, puede seguir utilizando cualquiera de los simuladores de iOS 8 sin problemas.
1. Si debe usar iOS 9, sus aplicaciones -Info.plist (que se encuentra después de ejecutar `cordova platform add ios` en el archivo &quot;&lt;app root>/platform/ios/&lt;app name>/&lt;app name>-Info.plist&quot;) se pueden editar manualmente para incluir la siguiente propiedad:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obtener más información sobre &quot;App Transport Security&quot;, consulte la siguiente sección de [documentos de la versión preliminar de iOS9 de Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) y esta [discusión sobre el desbordamiento de la pila](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## AEM Desarrollo de aplicaciones móviles en el sector de la {#developing-mobile-applications-in-aem-1}

* [AEM Iniciando PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creación de aplicaciones móviles](/help/mobile/building-app-mobile-phonegap.md)
* [Estructurar una aplicación](/help/mobile/phonegap-structure-an-app.md)
* [Creación y edición de aplicaciones mediante la consola de aplicaciones](/help/mobile/phonegap-apps-console.md)
* [Aplicaciones de una sola página](/help/mobile/phonegap-single-page-applications.md)
* [Desarrollo de aplicaciones con CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Acceso a funciones de dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Seguimiento del rendimiento de las aplicaciones con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Añadir Adobe Analytics a la aplicación móvil](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificaciones push](/help/mobile/phonegap-push-notifications.md)
* [Personalización de contenido de AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [La estructura de una aplicación](/help/mobile/phonegap-apps-arch.md)
* [¿Su aplicación híbrida está lista para AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Creación para Adobe PhoneGap AEM Enterprise con](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
