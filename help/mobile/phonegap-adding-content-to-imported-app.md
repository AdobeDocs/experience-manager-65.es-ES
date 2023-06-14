---
title: ¿Su aplicación híbrida está lista para AEM Mobile?
description: Más información sobre las aplicaciones híbridas. Una aplicación en Experience Manager suele dividirse en dos partes. El "shell" y el "contenido" de esta página proporcionan más información sobre estos temas.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# ¿Su aplicación híbrida está lista para Adobe Experience Manager Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM Ha importado su aplicación híbrida PhoneGap o Cordova en el mercado de los teléfonos móviles, ¿y ahora qué? Es probable que quiera añadir contenido legible a su aplicación. AEM Para llevar a cabo esta tarea, necesita una comprensión general de la estructura de una aplicación de. AEM Una aplicación en la se divide comúnmente en dos partes. El &quot;shell&quot; y el &quot;content&quot;. El &quot;shell&quot; comprende las partes estáticas de la aplicación, como los archivos de configuración de PhoneGap, el marco de la aplicación y los controles de navegación. El contenido del archivo que ha importado se almacena como parte del shell. AEM En el contexto de este documento, el shell es todo el contenido no creado por el desarrollador de la aplicación Híbrida de PhoneGap que no es de autor de la aplicación.

AEM AEM El contenido hace referencia a los componentes, las plantillas y las páginas creadas en las que se crea el desarrollador de la aplicación de manera de crear el contenido de la página de la aplicación de la aplicación de la manera de crear la página de la aplicación de la. El contenido se clasifica como contenido de desarrollador o como contenido creado. Los componentes, diseños y plantillas de página se consideran contenido de desarrollo, ya que los crea un desarrollador. El contenido de autor son páginas que se han creado mediante los componentes y las plantillas. Estas páginas las suele realizar un diseñador o un especialista en marketing.

AEM AEM La adición de páginas de creadas a la aplicación híbrida requiere la coordinación entre el desarrollador de la aplicación y el desarrollador de la. En cualquier lugar de la aplicación donde desee añadir contenido creado, el desarrollador de la aplicación debe organizar estas páginas en una estructura que se pueda superponer en Experience Manager. El desarrollador de aplicaciones debe poder proporcionar al desarrollador del Experience Manager las rutas en las que se agrega el contenido creado por el Experience Manager. A continuación, proporcione una página de marcador de posición en la aplicación híbrida que se sustituya después de que el desarrollador Experience Manager haya creado el contenido de la página.

AEM Para facilitar el seguimiento de la explicación, se está utilizando el Experience Cloud de la: Referencia híbrida de AEM Mobile para explicar los conceptos. La aplicación de referencia híbrida consiste en una página de bienvenida con un menú lateral.

![chlimage_1-76](assets/chlimage_1-76.png)

En este ejemplo, se va a crear la página de bienvenida de la aplicación. Mirando a la fuente [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Observe que el desarrollador de la aplicación ha definido una página de bienvenida y ha proporcionado una plantilla para la página que la aplicación representa. AEM En esta página es donde deben coordinarse el desarrollador de aplicaciones y el desarrollador de. La ruta a la plantilla de página de bienvenida en la aplicación de referencia híbrida se define como &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. AEM AEM Esta ruta es importante porque el desarrollador de la creará su página de bienvenida en el repositorio de carpetas utilizando la misma ruta.

![chlimage_1-77](assets/chlimage_1-77.png)

AEM Es importante que la aplicación híbrida y el contenido creado por el utilicen la misma ruta porque se basa en la capacidad de superponer contenido mediante la sincronización de contenido para agregar nuevas páginas a la aplicación híbrida. AEM Cuando la aplicación híbrida se importa a la aplicación de, como parte del proceso de importación, se configuran las opciones de configuración de sincronización de contenido.

![chlimage_1-78](assets/chlimage_1-78.png)

Al &quot;Descargar origen&quot; desde el panel de aplicaciones, estos scripts de ContentSync se ejecutan para montar un archivo de la aplicación híbrida.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync primero extrae el &quot;shell&quot; de la aplicación, que es donde se almacena todo el contenido desarrollado por la aplicación híbrida. A continuación, extrae el &quot;contenido&quot; de la aplicación. Ahora, si hay páginas en el &quot;shell&quot; que tienen la misma ruta que en el &quot;content&quot;, las páginas bajo el &quot;shell&quot; se (reemplazan) por las páginas bajo el &quot;content&quot;. AEM Por lo tanto, en el ejemplo de la aplicación de referencia híbrida, si se crea una página en que tiene la misma ruta que &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;, cuando se ejecuta ContentSync, se superpone a la página que formaba parte de la aplicación de referencia híbrida. AEM Se superpone con lo que haya en la ubicación de la que se haya en la parte de la pantalla de la pantalla de la pantalla de la pantalla de la pantalla de la ubicación. AEM ContentSync se encarga de la superposición, por lo que para alguien que esté utilizando la aplicación, las actualizaciones de la aplicación con contenido creado por el autor se ven sin problemas y no requieren una reconstrucción de la aplicación. Como resultado, al ejecutar la aplicación, la página de bienvenida aparece de la siguiente manera:

![chlimage_1-80](assets/chlimage_1-80.png)
