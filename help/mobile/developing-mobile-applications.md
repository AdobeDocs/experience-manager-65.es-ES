---
title: Desarrollo de aplicaciones móviles en AEM
seo-title: Developing Mobile Applications in AEM
description: Siga esta página para empezar a desarrollar aplicaciones móviles en AEM con Adobe PhoneGap Enterprise.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Desarrollo de aplicaciones móviles en AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM aprovecha las soluciones de publicación de Adobe PhoneGap y Adobe, que le permiten crear y administrar aplicaciones móviles multiplataforma, tanto enriquecidas como basadas en utilidades:

* Administre todas las aplicaciones móviles de su empresa en un solo lugar.
* Revise las aplicaciones en entornos de desarrollo y ensayo sin las complejidades de los perfiles de aprovisionamiento ni el esfuerzo adicional para crear y cargar su aplicación para compartirla.
* Utilice el entorno de creación de AEM para crear y administrar contenido enriquecido para sus aplicaciones.
* Use el HTML5 con Adobe PhoneGap para crear experiencias enriquecidas con funciones nativas del dispositivo.
* Presentación de las vistas web de HTML5 a las nuevas o preexistentes **nativo** a través de Cordova WebViews.
* Cree, depure y comparta contenido multimedia enriquecido en todos los canales de envío, incluidos web, web móvil, aplicación móvil e impresión.

AEM se integra con el Adobe **[Servicio de PhoneGap Build](https://build.phonegap.com/)** para simplificar el proceso de creación e implementación de aplicaciones.

**Adobe ContentSync** permite a los usuarios descargar fácilmente actualizaciones de página y contenido de Over-the-Air (OTA) en sus dispositivos sin tener que volver a instalar la aplicación ni descargar desde la appStore, Google Play u otras fuentes de aplicaciones.

**Adobe Analytics** está totalmente integrado en AEM aplicaciones y permite un seguimiento detallado de la distribución, la geolocalización, los sistemas operativos, los dispositivos, los flujos de clics, el seguimiento de iBeacon y más.

## Creación de aplicaciones {#creating-apps}

Los desarrolladores pueden utilizar el [AEM Kit de inicio de PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) junto con los recursos adicionales que se encuentran en [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) para arrancar AEM aplicaciones con PhoneGap, incluida una aplicación nativa de referencia que ejecute Cordova Webviews.

El archivo readme del repositorio de Git del Starter Kit incluye un tutorial para utilizar el kit de inicio:

* Personalizar la marca
* Maven muestras de objetivos de compilación e implementación
* Configuración del repositorio de control de código fuente
* Instalación e implementación en instancias de AEM locales o remotas
* Desinstalar desde AEM

>[!NOTE]
>
>Puede encontrar fuentes de implementación de referencia adicionales, como laboratorios, en GitHub [here](https://github.com/adobe-marketing-cloud-apps) y, la fuente &quot;fregadero-cocina&quot; [here](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Desarrollo para hosts de IOS 9 y HTTP {#developing-for-ios-and-http-hosts}

Los desarrolladores de iOS deben tener en cuenta un problema abierto con las aplicaciones de Cordova que se ejecutan en iOS 9. Este problema impide que se realicen solicitudes en hosts inseguros (como *http://localhost:4502*). Este problema se resolverá con una próxima versión de cordova-ios (que consume la CLI de Cordova), pero mientras tanto hay dos soluciones alternativas disponibles:

1. Como solución alternativa inmediata, puede seguir utilizando cualquiera de los simuladores de iOS 8 sin problemas.
1. Si debe utilizar iOS 9, sus aplicaciones -Info.plist (se encuentran después de ejecutar `cordova platform add ios` en &quot;&lt;app root=&quot;&quot;>/plataformas/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>El archivo -Info.plist&quot;) se puede editar manualmente para incluir la siguiente propiedad:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Para obtener más información sobre &quot;App Transport Security&quot;, consulte la siguiente sección de [Documentos de la versión preliminar de iOS9 de Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) y [Discusión de desbordamiento de pila](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Desarrollo de aplicaciones móviles en AEM {#developing-mobile-applications-in-aem-1}

* [Inicio AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creación de aplicaciones móviles](/help/mobile/building-app-mobile-phonegap.md)
* [Estructura de una aplicación](/help/mobile/phonegap-structure-an-app.md)
* [Creación y edición de aplicaciones mediante la consola Aplicaciones](/help/mobile/phonegap-apps-console.md)
* [Aplicaciones de una sola página](/help/mobile/phonegap-single-page-applications.md)
* [Desarrollo de aplicaciones con la CLI de PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Acceder a las funciones de los dispositivos](/help/mobile/phonegap-access-device-features.md)
* [Seguimiento del rendimiento de la aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Añadir Adobe Analytics a la aplicación móvil](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notificaciones push](/help/mobile/phonegap-push-notifications.md)
* [Personalización de contenido de AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [La anatomía de una aplicación](/help/mobile/phonegap-apps-arch.md)
* [¿Su aplicación híbrida está lista para AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y desarrollador, consulte los siguientes recursos:

* [Creación para Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
