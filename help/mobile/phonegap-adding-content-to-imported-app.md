---
title: ¿Su aplicación híbrida está lista para AEM Mobile?
seo-title: ¿Su aplicación híbrida está lista para AEM Mobile?
description: Siga esta página para conocer las aplicaciones híbridas. Las aplicaciones de AEM se suelen dividir en dos partes. El 'shell' y el 'contenido' y esta página proporciona más información sobre estos temas.
seo-description: Siga esta página para conocer las aplicaciones híbridas. Las aplicaciones de AEM se suelen dividir en dos partes. El 'shell' y el 'contenido' y esta página proporciona más información sobre estos temas.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ¿Su aplicación híbrida está lista para AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Así que ha importado su aplicación híbrida PhoneGap o Cordova en AEM, ¿ahora qué? Es probable que quiera añadir contenido de creación a su aplicación. Para llevar a cabo esta tarea, necesitará una comprensión general de la estructura de una aplicación de AEM. Las aplicaciones de AEM se suelen dividir en dos partes. El &#39;shell&#39; y el &#39;contenido&#39;. El &quot;shell&quot; está formado por las partes estáticas de la aplicación; como los archivos de configuración de PhoneGap, el marco de la aplicación y los controles de navegación. El contenido del archivo importado se almacena como parte del shell. En el contexto de este documento, el shell es todo el contenido no creado por AEM de la aplicación Híbrido PhoneGap creada por el desarrollador de la aplicación.

El contenido hace referencia a los componentes, las plantillas y las páginas creadas por AEM creadas por el desarrollador de AEM. El contenido se clasifica como contenido para desarrolladores o como contenido creado. Los componentes, diseños y plantillas de página se consideran contenido de desarrollo, ya que son creados por un desarrollador. author-content son páginas que se han creado con los componentes y las plantillas. Normalmente, los realiza un diseñador o un especialista en marketing.

La adición de páginas de AEM creadas en la aplicación híbrida requiere la coordinación entre el desarrollador de la aplicación y el desarrollador de AEM. En cualquier parte de la aplicación en la que desee añadir contenido de creación, el desarrollador de la aplicación debe organizar estas páginas en una estructura que se pueda superponer en AEM. El desarrollador de la aplicación debe poder proporcionar al desarrollador de AEM las rutas a las que se añadirá el contenido creado por AEM y, a continuación, proporcionar una página de marcador de posición en la aplicación híbrida que se sustituirá después de que el desarrollador de AEM haya creado el contenido de la página.

Para facilitar el seguimiento de la explicación, se utilizará AEM Marketing Cloud: Referencia híbrida de AEM Mobile para explicar los conceptos. La aplicación de referencia híbrida consta de una página de bienvenida con un menú lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

En este ejemplo vamos a crear la página de bienvenida de la aplicación. Eche un vistazo a la fuente [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Vemos que el desarrollador de la aplicación ha definido una página de bienvenida y ha proporcionado una plantilla para la página representada por la aplicación. Aquí es donde el desarrollador de la aplicación y el desarrollador de AEM deben coordinarse. La ruta a la plantilla de página de bienvenida en la aplicación de referencia híbrida se define como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Esta ruta es extremadamente importante porque el desarrollador de AEM creará su página de bienvenida en el repositorio de AEM utilizando la misma ruta.

![chlimage_1-77](assets/chlimage_1-77.png)

Es importante que la aplicación híbrida y el contenido creado por AEM utilicen la misma ruta porque confiamos en la capacidad de superponer contenido mediante la sincronización de contenido para añadir nuevas páginas a la aplicación híbrida. Cuando la aplicación híbrida se importa en AEM como parte del proceso de importación, se configuran las configuraciones de sincronización de contenido.

![chlimage_1-78](assets/chlimage_1-78.png)

Al &#39;Descargar fuente&#39; desde el tablero de la aplicación, estos scripts de ContentSync se ejecutan para compilar un archivo de la aplicación híbrida.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync primero extrae &#39;shell&#39; de la aplicación, que es donde se almacena todo el contenido desarrollado por la aplicación de la aplicación híbrida y, a continuación, extrae el &#39;contenido&#39; de la aplicación. Ahora, si hay páginas en el &quot;shell&quot; que tienen la misma ruta que en &#39;content&#39;, las páginas debajo de &#39;shell&#39; serán (reemplazadas) por las páginas debajo de &#39;content&#39;. En otras palabras, en el ejemplo de la aplicación de referencia híbrida, si creamos una página en AEM que tenga la misma ruta que &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39; cuando se ejecuta ContentSync, se superpondrá a la página que formaba parte de la aplicación de referencia híbrida con lo que esté en AEM en esa ubicación. ContentSync se encarga de la superposición, por lo que para las personas que utilicen la aplicación, las actualizaciones de la aplicación con contenido creado en AEM tendrán un aspecto perfecto y no requerirán una reconstrucción de la aplicación. Como resultado, al ejecutar la aplicación, la página de bienvenida aparecerá de la siguiente manera:

![chlimage_1-80](assets/chlimage_1-80.png)
