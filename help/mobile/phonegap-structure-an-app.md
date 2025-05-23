---
title: Estructurar una aplicación
description: Siga esta página para obtener más información sobre cómo crear la estructura de una aplicación. En esta página se describe cómo estructurar plantillas y componentes junto con información sobre JavaScript y CSS Clientlibs.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Estructurar una aplicación{#structure-an-app}

{{ue-over-mobile}}

Un proyecto de AEM Mobile incluye un conjunto diverso de tipos de contenido, como páginas, bibliotecas de cliente JavaScript AEM y CSS, componentes de la aplicación reutilizables, configuraciones de sincronización de contenido y contenido del shell de la aplicación PhoneGap. Basar tu nueva aplicación de AEM Mobile en el [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) es una buena manera de incorporar los distintos tipos de contenido en nuestra estructura recomendada para facilitar tanto la portabilidad como la capacidad de mantenimiento a largo plazo.

## Contenido de página {#page-content}

Todas las páginas de la aplicación deben encontrarse debajo de /content/mobileapps para que la consola de AEM Mobile las reconozca.

![chlimage_1-52](assets/chlimage_1-52.png)

AEM Por convención, la primera página de la aplicación debe ser una redirección a uno de sus elementos secundarios, que sirve como idioma predeterminado de la aplicación (&quot;en&quot; en los casos de Geometrixx y Starter Kit). La página de configuración regional de nivel superior generalmente hereda del componente &quot;splash-page&quot; base (/libs/mobileapps/components/splash-page), que se encarga de la inicialización necesaria para admitir la instalación de actualizaciones de sincronización de contenido por aire (el código contentInit se encuentra en /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Plantillas y componentes {#templates-and-components}

La plantilla y el código de componente de la aplicación deben estar en /apps/&lt;brand name>/&lt;app name>. De conformidad con la convención, debe colocar la plantilla y el código del componente en /apps/&lt;brand name>/&lt;app name>. AEM Este patrón debería resultarles familiar a los desarrolladores que ya han trabajado con Site en el mundo de la. Suele ir seguido de /apps/, que está bloqueado para el acceso anónimo de forma predeterminada en instancias de publicación. Por lo tanto, su código JSP sin procesar se oculta de los atacantes potenciales.

Las plantillas específicas de la aplicación se pueden configurar para que solo se presenten mediante el nodo de propiedad `allowedPaths` en la propia plantilla y estableciendo su valor en &#39;/content/mobileapps(/.&ast;)?&#39; : o incluso algo más específico si la plantilla solo debe utilizarse para una sola aplicación. Las propiedades `allowedParents` y `allowedChildren` también se pueden usar para el control detallado de las plantillas disponibles para un autor en función de dónde se esté creando la nueva página.

Al crear un componente de página de aplicación desde cero, se recomienda establecer su propiedad `sling:resourceSuperType` en &quot;mobileapps/components/angular/ng-page&quot;. Esto configura la página para la creación y el procesamiento como una aplicación de una sola página y permite superponer los archivos .jsp que el componente pueda necesitar cambiar. Dado que ng-page no incluye ningún marco de interfaz de usuario, un desarrollador suele terminar superponiendo (al menos) &quot;template.jsp&quot; (superpuesto desde /libs/mobileapps/components/angular/ng-page/template.jsp).

Los componentes de página con autorización que desean utilizar AngularJS, tienen un componente `sling:resourceSuperType` equivalente en /libs/mobileapps/components/angular/ng-component, que se puede superponer y personalizar del mismo modo.

## JavaScript y clientes CSS {#javascript-and-css-clientlibs}

En las bibliotecas de cliente, hay algunas opciones disponibles para el desarrollador de dónde colocarlas en el repositorio. El siguiente patrón se ofrece como guía, pero no es un requisito difícil.

Si el código de cliente puede funcionar por sí solo y no está relacionado con un componente específico de la aplicación (lo que significa que puede reutilizarse en otras aplicaciones), Adobe recomienda almacenarlo en /etc/clientlibs/&lt;brand name>/&lt;lib name>. Por otro lado, si la clientlib es específica de una sola aplicación, puede anidarla como un elemento secundario del nodo de diseño de la aplicación; /etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs. No utilice la categoría de esta clientlib con otras bibliotecas; en su lugar, incruste otras bibliotecas según sea necesario. Seguir este patrón evita que el desarrollador tenga que añadir nuevas configuraciones de sincronización de contenido cada vez que se añade una biblioteca de cliente a la aplicación, en lugar de actualizar simplemente la propiedad &quot;embeds&quot; de la clientlib de diseño de la aplicación. Por ejemplo, observe el nodo de configuración Geometrixx clientlibs-all Content Sync en /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Si el código del lado del cliente está perfectamente acoplado a un componente específico, colóquelo en una biblioteca de cliente anidada debajo de la ubicación del componente en /apps/ e incruste su categoría en la clientlib de &quot;diseño&quot; de la aplicación.

## Configuración de PhoneGap {#phonegap-configuration}

Cada aplicación de AEM Mobile contiene un directorio que aloja los archivos de configuración utilizados por la [interfaz de línea de comandos](https://github.com/phonegap/phonegap-cli) de PhoneGap y PhoneGap Build en `https://build.phonegap.com/` para convertir el contenido web en una aplicación ejecutable. En el ejemplo de Geometrixx, por ejemplo, este directorio (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) se encuentra como parte del shell; una decisión de diseño hecha porque contiene solo contenido que no se puede actualizar por el aire, como complementos que tratan con las API de dispositivos y la configuración de la propia aplicación.

En este directorio, también encontrará algunos [enlaces de Cordova](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) que se pueden usar para instalar complementos, colocar archivos de recursos en sus ubicaciones específicas de la plataforma y otras acciones que se deben ejecutar como parte de la compilación. Nota: como alternativa a descargar cada complemento como parte de la compilación, puede seguir el patrón de la aplicación Fregadero de cocina e incluir el código fuente del complemento <!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> con el resto del proyecto de la aplicación.

## Pasos siguientes {#the-next-steps}

Después de obtener información sobre la estructura de la aplicación, consulte [Creación y edición de las aplicaciones mediante la consola de la aplicación](/help/mobile/phonegap-apps-console.md).
