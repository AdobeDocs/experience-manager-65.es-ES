---
title: ¿Su aplicación híbrida está lista para AEM Mobile?
seo-title: Is your hybrid app ready for AEM Mobile?
description: Siga esta página para obtener más información sobre las aplicaciones híbridas. Una aplicación de AEM se divide comúnmente en dos partes. El "shell" y el "contenido" y esta página proporcionan más información sobre estos temas.
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# ¿Su aplicación híbrida está lista para AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Así que ha importado su aplicación híbrida PhoneGap o Cordova en AEM, ¿ahora qué? Es probable que desee agregar contenido de autoría a su aplicación. Para llevar a cabo esta tarea, necesitará una comprensión general de la estructura de una aplicación AEM. Una aplicación de AEM se divide comúnmente en dos partes. El &quot;shell&quot; y el &quot;contenido&quot;. El &quot;shell&quot; consta de las partes estáticas de la aplicación; como los archivos de configuración de PhoneGap, el marco de aplicación y los controles de navegación. El contenido del archivo que ha importado se almacena como parte del shell. En el contexto de este documento, el shell es todo el contenido no AEM creado por el desarrollador de la aplicación de PhoneGap híbrido.

El contenido hace referencia a los componentes, las plantillas y las páginas creadas en AEM creadas por el desarrollador de AEM. El contenido se clasifica como contenido para desarrolladores o como contenido creado. Los componentes, diseños y plantillas de página se consideran contenido de desarrollo, ya que los crea un desarrollador. author-content son páginas que se han creado utilizando los componentes y las plantillas. Generalmente, los realiza un diseñador o un especialista en marketing.

La adición de páginas de AEM creadas en la aplicación híbrida requiere una coordinación entre el desarrollador de la aplicación y el desarrollador de AEM. En cualquier parte de la aplicación en la que quiera añadir contenido creado, el desarrollador de la aplicación debe organizar estas páginas en una estructura que se pueda superponer en AEM. El desarrollador de la aplicación debe poder proporcionar al desarrollador de la AEM las rutas a las que se agregará el contenido creado por el AEM y, a continuación, proporcionar una página de marcador de posición en la aplicación híbrida que se sustituirá después de que el desarrollador de la AEM haya creado el contenido de la página.

Para que la explicación sea más fácil de seguir, usaremos el Marketing Cloud AEM: Referencia híbrida de AEM Mobile para explicar los conceptos. La aplicación de referencia híbrida consiste en una página de bienvenida con un menú lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

En este ejemplo vamos a crear la página de bienvenida de la aplicación. Mirar la fuente [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Vemos que el desarrollador de la aplicación ha definido una página de bienvenida y proporcionado una plantilla para la página representada por la aplicación. Aquí es donde el desarrollador de la aplicación y el desarrollador de AEM deben coordinarse. La ruta a la plantilla de página de bienvenida en la aplicación de referencia híbrida se define como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Esta ruta es extremadamente importante porque el desarrollador de AEM creará su página de bienvenida en el repositorio de AEM usando la misma ruta.

![chlimage_1-77](assets/chlimage_1-77.png)

Es importante que la aplicación híbrida y el contenido creado AEM utilicen la misma ruta, ya que confiamos en la capacidad de superponer contenido mediante la sincronización de contenido para añadir nuevas páginas a la aplicación híbrida. Cuando la aplicación híbrida se importa en AEM como parte del proceso de importación, se configuran las configuraciones de sincronización de contenido.

![chlimage_1-78](assets/chlimage_1-78.png)

Cuando descarga Fuente desde el panel de la aplicación, estos scripts de ContentSync se ejecutan para ensamblar un archivo de la aplicación híbrida.

![chlimage_1-79](assets/chlimage_1-79.png)

En primer lugar, ContentSync extrae &quot;shell&quot; de la aplicación, que es donde se almacena todo el contenido de la aplicación desarrollada por la aplicación híbrida y, a continuación, extrae el &quot;contenido&quot; de la aplicación. Ahora, si hay páginas en el &quot;shell&quot; que tienen la misma ruta que en &quot;contenido&quot;, las páginas en &quot;shell&quot; serán (reemplazadas) por las páginas en &quot;contenido&quot;. En otras palabras, en el ejemplo de la aplicación de referencia híbrida, si creamos una página en AEM que tenga la misma ruta que &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot; cuando se ejecute ContentSync, se superpondrá la página que formaba parte de la aplicación de referencia híbrida con lo que esté en AEM en esa ubicación. ContentSync se encarga de la superposición, por lo que para alguien que utilice la aplicación, las actualizaciones de la aplicación con AEM contenido creado se verán perfectamente y no requerirán una reconstrucción de la aplicación. Como resultado, cuando ejecute la aplicación, la página de bienvenida aparecerá de la siguiente manera:

![chlimage_1-80](assets/chlimage_1-80.png)
