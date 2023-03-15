---
title: Prácticas recomendadas
seo-title: Best Practices
description: AEM Siga esta página para conocer las prácticas recomendadas y las directrices que ayudarán a los desarrolladores de sitios con experiencia en la creación de plantillas y componentes de aplicaciones móviles.
seo-description: Follow this page to  learn best practices and guidelines that will help experienced AEM developers for sites, who want to build mobile app templates and components.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Prácticas recomendadas {#best-practices}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Crear una aplicación de AEM Mobile On-demand Services es diferente a crear una aplicación que se ejecute directamente en el shell de Cordova (o PhoneGap). Los desarrolladores deben estar familiarizados con lo siguiente:

* Complementos admitidos de forma predeterminada, así como los complementos específicos de AEM Mobile.

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

AEM Las siguientes directrices ayudarán a los desarrolladores de sitios con experiencia en la creación de plantillas y componentes de aplicaciones móviles, que ya tienen experiencia en la creación de sitios:

**AEM Estructura de plantillas de sitios para fomentar la reutilización y la extensibilidad**

* Preferir varios archivos de script de componente sobre uno monolítico

   * Se proporcionan varios puntos de extensión vacíos, como *customheaderlibs.html* y *customfoterlibs.html*, que permiten al desarrollador cambiar la plantilla de página duplicando el menor código principal posible
   * Las plantillas se pueden ampliar y personalizar mediante las API de Sling *sling:resourceSuperType* mecanismo

* Preferir Sightly/HTL sobre JSP como idioma de creación de plantillas

   * El uso de esto promueve la separación del código del marcado, ofrece protección XSS integrada y tiene una sintaxis más familiar

**Optimización del rendimiento en el dispositivo**

* La secuencia de comandos específica del artículo y las hojas de estilo deben incluirse en la carga útil del artículo mediante la plantilla dps-article-contentsync
* Las secuencias de comandos y las hojas de estilo compartidas por más de un artículo se deben incluir en los recursos compartidos mediante la plantilla contentsync dps-HTMLResources
* No haga referencia a ningún script externo que bloquee el procesamiento

>[!NOTE]
>
>Puede obtener más información en detalle sobre los scripts externos que bloquean el procesamiento [aquí](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferir bibliotecas JS y CSS del lado del cliente y específicas de la aplicación sobre las específicas de la web**

* Para evitar sobrecargas en bibliotecas como jQuery Mobile para gestionar una gran cantidad de dispositivos y navegadores
* Cuando se ejecuta una plantilla en la vista web de una aplicación, usted tiene control sobre las plataformas y versiones que esa aplicación va a admitir, así como sobre la presencia de compatibilidad con JavaScript. Por ejemplo, prefiera Ionic (quizás solo el CSS) sobre jQuery Mobile y la interfaz de usuario de Onsen sobre Bootstrap.

>[!NOTE]
>
>Para obtener más información detallada sobre jQuery mobile, haga clic en [aquí](https://jquerymobile.com/browser-support/1.4/).

**Preferir las microbibliotecas en lugar de la pila completa**

* El tiempo que se tarda en poner el contenido en el cristal del dispositivo se ralentizará con cada biblioteca de la que dependan los artículos. Esta ralentización se agrava cuando se utiliza una nueva vista web para procesar cada artículo, por lo que cada biblioteca debe inicializarse de nuevo desde cero
* SPA Si los artículos no están diseñados como tal (aplicaciones de una sola página), probablemente no necesite incluir una biblioteca de pila completa como Angular
* Prefiera bibliotecas de un solo propósito más pequeñas para añadir la interactividad que requiere su página, como [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Minimizar el tamaño de la carga útil del artículo**

* Utilice los recursos más pequeños posibles que puedan cubrir eficazmente la ventanilla más grande que admita, con una resolución razonable
* Utilice una herramienta como *ImageOptim* en las imágenes para eliminar el exceso de metadatos

## Primeros pasos {#getting-ahead}

Para obtener más información sobre las otras dos funciones y responsabilidades, consulte los recursos siguientes:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
