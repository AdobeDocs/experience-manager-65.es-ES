---
title: Prácticas recomendadas para AEM Mobile On-demand Services
description: Conozca las prácticas recomendadas y las directrices que ayudan a los desarrolladores competentes de Adobe Experience Manager AEM () para sitios que desean crear plantillas y componentes de aplicaciones móviles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---

# Prácticas recomendadas {#best-practices}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Crear una aplicación de AEM Mobile On-demand Services es diferente a crear una aplicación que se ejecute directamente en el shell de Cordova (o PhoneGap). Los desarrolladores deben estar familiarizados con lo siguiente:

* Complementos admitidos de forma predeterminada y los complementos específicos de Adobe Experience Manager AEM () Mobile.

>[!NOTE]
>
>Para obtener información detallada sobre los complementos, consulte los siguientes recursos:
>
>* [Uso de complementos de Cordova en AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Uso de complementos específicos de AEM Mobile habilitados para Cordova](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Las plantillas que utilizan la funcionalidad del complemento deben escribirse de tal manera que se puedan crear en el explorador, sin que esté presente el puente del complemento.

   * Por ejemplo, asegúrese de esperar a que *dispositivo preparado* antes de intentar acceder a la API de un complemento.

## AEM Directrices para desarrolladores de {#guidelines-for-aem-developers}

AEM Las siguientes directrices ayudan a los desarrolladores competentes de la aplicación para sitios que deseen crear plantillas y componentes de aplicaciones móviles:

**AEM Estructura de plantillas de sitios para fomentar la reutilización y la extensibilidad**

* Preferir varios archivos de script de componente sobre uno monolítico

   * Se proporcionan varios puntos de extensión vacíos, como *customheaderlibs.html* y *customfoterlibs.html*, que permiten al desarrollador cambiar la plantilla de página duplicando el menor código principal posible
   * Las plantillas se pueden ampliar y personalizar mediante las API de Sling *sling:resourceSuperType* mecanismo

* Preferir Sightly/HTL sobre JSP como idioma de creación de plantillas

   * El uso de esto promueve la separación del código del marcado, ofrece protección XSS integrada y tiene una sintaxis más familiar

**Optimización del rendimiento en el dispositivo**

* La secuencia de comandos específica del artículo y las hojas de estilo deben incluirse en la carga útil del artículo mediante la plantilla dps-article contentsync
* Las hojas de estilo y los scripts compartidos por más de un artículo se deben incluir en los recursos compartidos mediante la plantilla contentsync dps-HTMLResources
* No haga referencia a ningún script externo que bloquee el procesamiento

>[!NOTE]
>
>Puede obtener más información en detalle sobre los scripts externos que bloquean el procesamiento [aquí](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferir bibliotecas CSS y JS del lado del cliente y específicas de la aplicación sobre las específicas de la web**

* Para evitar sobrecargas en bibliotecas como jQuery Mobile para gestionar una gran cantidad de dispositivos y navegadores
* Cuando se ejecuta una plantilla en la vista web de una aplicación, usted tiene control sobre las plataformas y versiones que la aplicación va a admitir y sabe que la compatibilidad con JavaScript estará presente. Por ejemplo, prefiera Ionic (solo el CSS) sobre jQuery Mobile y la interfaz de usuario de Onsen sobre Bootstrap.

>[!NOTE]
>
>Para obtener más información detallada sobre jQuery mobile, haga clic en [aquí](https://jquerymobile.com/browser-support/1.4/).

**Preferir las microbibliotecas en lugar de la pila completa**

* El tiempo que se tarda en poner el contenido en el cristal del dispositivo se ralentiza con cada biblioteca de la que dependen los artículos. Esta ralentización se agrava cuando se utiliza una nueva vista web para procesar cada artículo, por lo que cada biblioteca debe inicializarse de nuevo desde cero
* SPA Si los artículos no están diseñados como tal (aplicaciones de una sola página), probablemente no necesite incluir una biblioteca de pila completa como Angular
* Prefiera bibliotecas de un solo uso más pequeñas que ayuden a añadir la interactividad que requiere su página, como las siguientes [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Minimizar el tamaño de la carga útil del artículo**

* Utilice los recursos más pequeños posibles que puedan cubrir eficazmente la ventanilla más grande que admita, con una resolución razonable
* Utilice una herramienta como *ImageOptim* en las imágenes para eliminar el exceso de metadatos

## Primeros pasos {#getting-ahead}

Para obtener más información sobre las otras dos funciones y responsabilidades, consulte los recursos siguientes:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
