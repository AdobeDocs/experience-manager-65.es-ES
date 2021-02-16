---
title: 'Prácticas recomendadas  '
seo-title: 'Prácticas recomendadas  '
description: Siga esta página para conocer las prácticas recomendadas y las directrices que ayudarán a los desarrolladores AEM experimentados de los sitios que deseen crear plantillas y componentes de aplicaciones móviles.
seo-description: Siga esta página para conocer las prácticas recomendadas y las directrices que ayudarán a los desarrolladores AEM experimentados de los sitios que deseen crear plantillas y componentes de aplicaciones móviles.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Prácticas recomendadas   {#best-practices}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La creación de una aplicación de AEM Mobile On-demand Services es diferente a la creación de una aplicación que se ejecuta directamente en el shell de Cordova (o PhoneGap). Los desarrolladores deben estar familiarizados con:

* Los complementos que se admiten de forma predeterminada, así como los complementos específicos de AEM Mobile.

>[!NOTE]
>
>Para obtener información detallada sobre los complementos, consulte los siguientes recursos:
>
>* [Uso de complementos de Cordova en AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Uso de complementos específicos de AEM Mobile adaptados para Cordova](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* Las plantillas que utilizan la funcionalidad de complemento deben escribirse de tal manera que sigan siendo autorizadas en el navegador, sin que el puente de complemento esté presente.

   * Por ejemplo, asegúrese de esperar a la función *deviceready* antes de intentar acceder a la API de un complemento.

## Directrices para desarrolladores de AEM {#guidelines-for-aem-developers}

Las siguientes directrices ayudarán a los desarrolladores experimentados de AEM para sitios que deseen crear plantillas y componentes de aplicaciones móviles:

**Estructurar plantillas de sitios AEM para fomentar la reutilización y la extensibilidad**

* Preferir varios archivos de secuencias de comandos de componentes sobre uno solo y monolítico

   * Se proporcionan varios puntos de extensión vacíos, como *customheaderlibs.html* y *customfoterlibs.html*, que permiten al programador cambiar la plantilla de página al mismo tiempo que se duplica el menor código principal posible
   * Las plantillas se pueden ampliar y personalizar mediante el mecanismo *sling:resourceSuperType* de Sling

* Preferir Sightly/HTL sobre JSP como idioma de plantilla

   * El uso de esto fomenta la separación del código del marcado, ofertas integradas en la protección XSS y tiene una sintaxis más familiar

**Optimizar el rendimiento en el dispositivo**

* La secuencia de comandos y las hojas de estilo específicas del artículo deben incluirse en la carga útil del artículo, mediante la plantilla dps-article contentsync
* Las hojas de estilo y las secuencias de comandos compartidas por más de un artículo deben incluirse en los recursos compartidos, mediante la plantilla dps-HTMLResources contentsync
* No haga referencia a secuencias de comandos externas que bloqueen el procesamiento

>[!NOTE]
>
>Aquí](https://developers.google.com/speed/docs/insights/BlockingJS) puede obtener más información detallada sobre secuencias de comandos externas de bloqueo de procesamiento.[

**Prefiere las bibliotecas JS y CSS de cliente específicas de la aplicación en lugar de las bibliotecas específicas de la web**

* Para evitar sobrecargas en bibliotecas como jQuery Mobile con el fin de gestionar una gran variedad de dispositivos y exploradores
* Cuando una plantilla se está ejecutando en la vista web de una aplicación, tiene control sobre las plataformas y versiones que la aplicación va a admitir, así como el conocimiento de que estará presente la compatibilidad con JavaScript. Por ejemplo, prefiera Iónico (quizás solo CSS) sobre jQuery Mobile y la interfaz de usuario de Onsen en lugar de Bootstrap.

>[!NOTE]
>
>Para obtener más información sobre jQuery Mobile, haga clic [aquí](https://jquerymobile.com/browser-support/1.4/).

**Prefiere las microbibliotecas en lugar de las pilas completas**

* Cada biblioteca de la que dependan los artículos ralentizará el tiempo necesario para que el contenido pase a la copa del dispositivo. Esta ralentización se agrava cuando se utiliza una nueva vista de web para procesar todos los artículos, por lo que cada biblioteca debe inicializarse de nuevo desde cero
* Si los artículos no se crean como SPA (aplicaciones de una sola página), probablemente no necesite incluir una biblioteca de pilas completa como Angular
* Prefiera bibliotecas más pequeñas y de un solo propósito para ayudar a agregar la interactividad que requiere su página, como [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Minimizar el tamaño de la carga útil del artículo**

* Utilice los recursos más pequeños posibles que cubran eficazmente la ventanilla más grande que admita, con una resolución razonable
* Utilice una herramienta como *ImageOptim* en las imágenes para eliminar cualquier exceso de metadatos

## Cómo avanzar {#getting-ahead}

Para obtener más información sobre las otras dos funciones y responsabilidades, consulte los recursos siguientes:

* [Administrador](/help/mobile/aem-mobile.md)
* [Autor](/help/mobile/aem-mobile-on-demand.md)
