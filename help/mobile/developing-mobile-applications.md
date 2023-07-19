---
title: AEM Desarrollo de aplicaciones móviles en el sector de la
seo-title: Developing Mobile Applications in AEM
description: AEM Siga esta página para empezar a desarrollar aplicaciones móviles en el uso de la de Adobe PhoneGap Enterprise.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# AEM Desarrollo de aplicaciones móviles en el sector de la {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM aprovecha Adobe PhoneGap y las soluciones de publicación de Adobe, lo que le permite crear y administrar aplicaciones móviles multiplataforma enriquecidas en contenido y basadas en utilidades:

* Administre todas las aplicaciones móviles de su empresa en un solo lugar.
* Revise las aplicaciones en entornos de ensayo y desarrollo sin las complejidades de los perfiles de aprovisionamiento y sin el esfuerzo adicional de crear y cargar la aplicación para compartirla.
* AEM Utilice el entorno de creación de para crear y administrar contenido enriquecido para sus aplicaciones.
* Utilice HTML5 con Adobe PhoneGap para crear experiencias enriquecidas con funciones nativas del dispositivo.
* Introducción de las vistas web de HTML5 a las nuevas o preexistentes **nativo** aplicaciones a través de Cordova WebViews.
* Cree, depure y comparta contenido multimedia enriquecido en todos los canales de envío, incluidos el web, el web móvil, la aplicación móvil y la impresión.

AEM Se integra con el servicio de Adobe PhoneGap Build (`https://build.phonegap.com/`) para simplificar el proceso de generación e implementación de la aplicación.

**Adobe ContentSync** permite a los usuarios descargar fácilmente actualizaciones de páginas y contenido por el aire (OTA) en sus dispositivos sin tener que volver a instalar la aplicación ni descargar desde la AppStore, Google Play u otras fuentes de aplicaciones.

**Adobe Analytics** AEM está totalmente integrado en aplicaciones de y permite un seguimiento detallado de la distribución, geolocalización, sistemas operativos, dispositivos, flujos de clics, seguimiento de iBeacon y mucho más.

## Creación de aplicaciones {#creating-apps}

Los desarrolladores pueden utilizar el [AEM Kit de inicio de PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) junto con recursos adicionales que se encuentran en [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) AEM para arrancar aplicaciones de con PhoneGap, incluida una aplicación nativa de referencia que ejecuta Cordova Webviews.

El archivo léame del repositorio Git del Starter Kit incluye un tutorial para utilizar el Starter Kit:

* Personalización de la marca
* Objetivos de generación e implementación de muestra de Maven
* Configuración del repositorio de control de origen
* AEM Instalar e implementar en instancias de locales o remotas
* AEM Desinstalar desde la

>[!NOTE]
>
>En GitHub, se pueden encontrar fuentes de implementación de referencia adicionales, incluidos laboratorios [aquí](https://github.com/adobe-marketing-cloud-apps) y, la fuente &quot;fregadero-cocina&quot; [aquí](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desarrollo para hosts HTTP y IOS 9 {#developing-for-ios-and-http-hosts}

Los desarrolladores de iOS deben tener en cuenta un problema pendiente con las aplicaciones de Cordova que se ejecutan en iOS 9. Este problema evita que se realicen solicitudes a hosts no seguros (como *http://localhost:4502*). Este problema se resolverá en una próxima versión de cordova-ios (consumido por la CLI de Cordova), pero mientras tanto hay dos soluciones disponibles:

1. Como solución alternativa, puede seguir utilizando cualquiera de los simuladores de iOS 8 sin problemas.
1. Si debe utilizar iOS 9, sus aplicaciones -Info.plist (que se encuentra después de ejecutar `cordova platform add ios` en &quot;&lt;app root=&quot;&quot;>/platform/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;) se puede editar manualmente para incluir la siguiente propiedad:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obtener más información sobre &quot;App Transport Security&quot;, consulte la siguiente sección de [Documentos de la versión preliminar de iOS9 de Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) y esto [Discusión de desbordamiento de pila](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

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
