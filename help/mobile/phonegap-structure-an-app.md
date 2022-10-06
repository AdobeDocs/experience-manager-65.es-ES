---
title: Estructura de una aplicación
seo-title: Structure an App
description: Siga esta página para obtener información sobre cómo crear una estructura de una aplicación. En esta página se describe cómo estructurar plantillas y componentes junto con información sobre JavaScript y CSS Clientlibs.
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# Estructura de una aplicación{#structure-an-app}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Un proyecto de AEM Mobile incluye un conjunto diverso de tipos de contenido, incluidas páginas, bibliotecas de cliente JavaScript y CSS, componentes de AEM reutilizables, configuraciones de sincronización de contenido y contenido del shell de la aplicación PhoneGap. Basar la nueva aplicación de AEM Mobile en [Kit de arranque](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) es una buena manera de incorporar todos los diferentes tipos de contenido en nuestra estructura recomendada para facilitar tanto la portabilidad como la capacidad de mantenimiento a largo plazo.

## Contenido de la página {#page-content}

Las páginas de su aplicación deben estar situadas debajo de /content/mobileapps para que la consola de AEM Mobile las reconozca.

![imagen_1-52](assets/chlimage_1-52.png)

Por AEM convención, la primera página de la aplicación debe ser un redireccionamiento a uno de sus elementos secundarios, que sirve como idioma predeterminado de la aplicación (&quot;en&quot; en los casos de Geometrixx y Starter Kit). La página de configuración regional de nivel superior generalmente hereda del componente base &quot;splash-page&quot; (/libs/mobileapps/components/splash-page) que se encarga de la inicialización necesaria para admitir la instalación de actualizaciones de sincronización de contenido sobre el aire (el código contentInit se puede encontrar en /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Plantillas y componentes {#templates-and-components}

La plantilla y el código de componente de la aplicación deben estar ubicados en /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. De conformidad con la convención, debe colocar la plantilla y el código de componente en /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Este patrón debe resultarle familiar a los desarrolladores que ya hayan trabajado con Site en AEM. Normalmente se sigue porque /apps/ está bloqueado para el acceso anónimo de forma predeterminada en las instancias de publicación. En consecuencia, su código JSP sin procesar está oculto frente a posibles atacantes.

Las plantillas específicas de la aplicación solo se pueden configurar para que se presenten utilizando la variable `allowedPaths` en la plantilla y estableciendo su valor en &#39;/content/mobileapps(/.&amp;ast;)?&#39; - o incluso algo más específico si la plantilla solo debería utilizarse para una sola aplicación. La variable `allowedParents` y `allowedChildren` las propiedades también se pueden aprovechar para un control muy detallado de qué plantillas estarán disponibles para un autor en función del lugar en el que se esté creando la nueva página.

Al crear un nuevo componente de página de aplicación desde cero, se recomienda establecer `sling:resourceSuperType` a &quot;mobileapps/components/angular/ng-page&quot;. Esto configurará la página para la creación y el procesamiento como una aplicación de una sola página y le permitirá superponer cualquier archivo .jsp que su componente necesite cambiar. Dado que ng-page no incluye ningún marco de interfaz de usuario, un desarrollador normalmente terminará superponiendo (al menos) &#39;template.jsp&#39; (superpuesto desde /libs/mobileapps/components/angular/ng-page/template.jsp).

Los componentes de página autorizados, que desean aprovechar AngularJS, tienen un equivalente `sling:resourceSuperType` componente ubicado en /libs/mobileapps/components/angular/ng-component que puede superponerse y personalizarse del mismo modo.

## Clientlibs de JavaScript y CSS {#javascript-and-css-clientlibs}

Cuando se trata de bibliotecas de cliente, hay algunas opciones disponibles para el desarrollador de dónde colocarlas en el repositorio. El siguiente patrón se ofrece como guía, pero no es un requisito difícil.

Si su código clientside puede mantenerse por sí solo y no está relacionado con un componente específico de su aplicación, lo que significa que puede reutilizarse en otras aplicaciones, le recomendamos que lo almacene en /etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. Por otro lado, si la clientlib es específica de una aplicación única, puede anidarla como un elemento secundario del nodo de diseño de la aplicación; /etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. La categoría de clientlib no debe ser utilizada por otras bibliotecas, y debe usarse para incrustar otras bibliotecas según sea necesario. Seguir estos patrones evita que el desarrollador tenga que agregar nuevas configuraciones de sincronización de contenido cada vez que se agrega una biblioteca de cliente a la aplicación, en lugar de actualizar simplemente la propiedad &quot;embeds&quot; de la clientlib de diseño de la aplicación. Por ejemplo, eche un vistazo al nodo de configuración de sincronización de contenido clientlibs-all en /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Si el código del lado del cliente está estrechamente vinculado a un componente específico, coloque ese código en una biblioteca de cliente anidada debajo de la ubicación del componente en /apps/ e incruste su categoría en la clientlib &quot;design&quot; de la aplicación.

## Configuración de PhoneGap {#phonegap-configuration}

Cada aplicación de AEM Mobile contiene un directorio que aloja los archivos de configuración utilizados por PhoneGap [interfaz de línea de comandos](https://github.com/phonegap/phonegap-cli) y [Compilación de PhoneGap](https://build.phonegap.com/) para convertir el contenido web en una aplicación ejecutable. En el ejemplo de Geometrixx, por ejemplo, este directorio (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) se encuentra como parte del Shell; una decisión de diseño tomada debido al hecho de que contiene solo contenido que no se puede actualizar de forma instantánea, como complementos que tratan con las API de dispositivo y la configuración de la propia aplicación.

En este directorio también encontrará una serie de [Enlaces de Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) que se puede utilizar para instalar complementos, colocar archivos de recursos en ubicaciones específicas de la plataforma y otras acciones que se deben ejecutar como parte de la compilación. Nota: como alternativa a descargar cada complemento como parte de la compilación, puede seguir el patrón de la aplicación Kitchen Sink y [incluir código fuente del complemento](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) con el resto del proyecto de la aplicación.

## Pasos siguientes {#the-next-steps}

Una vez que conozca la estructura de la aplicación, consulte [Creación y edición de aplicaciones mediante la consola de aplicación](/help/mobile/phonegap-apps-console.md).
