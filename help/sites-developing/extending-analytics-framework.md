---
title: Personalizar Adobe Analytics Framework
description: Obtenga información sobre cómo personalizar el marco de trabajo de Adobe Analytics para Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Personalizar Adobe Analytics Framework{#customizing-the-adobe-analytics-framework}

El marco de Adobe Analytics determina la información de la que se realiza un seguimiento con Adobe Analytics. Para personalizar el marco predeterminado, utilice JavaScript para agregar un seguimiento personalizado, integrar complementos de Adobe Analytics y cambiar la configuración general dentro del marco utilizado para el seguimiento.

## Acerca del JavaScript generado para módulos {#about-the-generated-javascript-for-frameworks}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics y la página incluye [referencias al módulo de Analytics](/help/sites-administering/adobeanalytics.md), se generará automáticamente un archivo analytics.sitecatalyst.js para la página.

El JavaScript de la página crea un `s_gi`(que define la biblioteca de Adobe Analytics s_code.js) y asigna valores a sus propiedades. El nombre de la instancia de objeto es `s`. Los ejemplos de código que se presentan en esta sección hacen varias referencias a esto `s` variable.

El siguiente código de ejemplo es similar al código de un archivo analytics.sitecatalyst.js:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Cuando se utiliza código JavaScript personalizado para personalizar el marco de trabajo, se modifica el contenido de este archivo.

## Configuración de propiedades de Adobe Analytics {#configuring-adobe-analytics-properties}

Hay varias variables predefinidas en Adobe Analytics que se pueden configurar en un marco de trabajo. El **charset**, **cookieLifetime**, **currencyCode**, y **trackInlineStats** Las variables de se incluyen en **Configuración general de Analytics** lista de forma predeterminada.

![aa-22](assets/aa-22.png)

Puede agregar nombres y valores de variables a la lista. Estas variables predefinidas y cualquier variable que agregue se utilizan para configurar las propiedades del `s` en el archivo analytics.sitecatalyst.js. El siguiente ejemplo muestra cómo se agrega el elemento `prop10` propiedad de valor `CONSTANT` se representa en el código JavaScript:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

Utilice el siguiente procedimiento para añadir variables a la lista:

1. En la página del marco de trabajo de Adobe Analytics, expanda **Configuración general de Analytics** área.
1. Debajo de la lista de variables, haga clic en Agregar elemento para agregar una nueva variable a la lista.
1. En la celda de la izquierda, introduzca un nombre para la variable, por ejemplo, `prop10`.

1. En la columna derecha, introduzca un valor para la variable, por ejemplo, `CONSTANT`.

1. Para quitar una variable, haga clic en el botón (-) junto a la variable.

>[!NOTE]
>
>Al introducir variables y valores, asegúrese de que tienen el formato y la ortografía correctos, o la variable **las llamadas de no se enviarán** con el par de valor y variable correcto. Las variables y los valores mal escritos pueden incluso evitar que se produzcan llamadas.
>
>Consulte con su representante de Adobe Analytics para asegurarse de que estas variables estén configuradas correctamente.

>[!CAUTION]
>
>Algunas de las variables de esta lista son **obligatorio** para que las llamadas de Adobe Analytics funcionen correctamente (por ejemplo, **currencyCode**, **charSet**).
>
>Por lo tanto, aunque se eliminen del propio marco de trabajo, se adjuntarán con un valor predeterminado cuando se realice la llamada de Adobe Analytics.

### Agregar JavaScript personalizado a un marco de trabajo de Adobe Analytics {#adding-custom-javascript-to-an-adobe-analytics-framework}

El cuadro de diálogo libre de JavaScript en **Configuración general de Analytics** permite añadir código personalizado a un marco de trabajo de Adobe Analytics.

![aa-21](assets/aa-21.png)

El código que agregue se anexará al archivo analytics.sitecatalyst.js. Por lo tanto, puede acceder a las `s` , que es una instancia de `s_gi` Objeto JavaScript definido en `s_code.js`. Por ejemplo, añadir el siguiente código equivale a añadir una variable denominada `prop10` de valor `CONSTANT`, que es el ejemplo de la sección anterior:

`s.prop10= 'CONSTANT';`

El código de la variable [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (que incluye el contenido de Adobe Analytics) `s-code.js` ) contiene el siguiente código:

`if (s.usePlugins) s.doPlugins(s)`

El siguiente procedimiento muestra cómo utilizar el cuadro JavaScript para personalizar el seguimiento de Adobe Analytics. Si JavaScript necesita utilizar complementos de Adobe Analytics, [integrarlos](/help/sites-administering/adobeanalytics.md) AEM en el.

1. Agregue el siguiente código JavaScript al cuadro para que `s.doPlugins` se ejecuta:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Este código es necesario si desea enviar variables en una llamada de Adobe Analytics que se hayan personalizado de alguna manera que no se puedan realizar a través de la interfaz básica de arrastrar y soltar O a través de JavaScript en línea en la vista de Adobe Analytics.
   >
   >Si las variables personalizadas están fuera de la función s_doPlugins, se enviarán como *undefined *en la llamada de Adobe Analytics

1. Añada su código JavaScript en la **s_doPlugins** función.

En el siguiente ejemplo, se concatenan los datos capturados en una página en orden jerárquico, utilizando un separador común de &quot;|&quot;.

Un marco de trabajo de Adobe Analytics tiene las siguientes configuraciones:

* El `prop2` La variable de Adobe Analytics está asignada a `pagedata.sitesection` propiedad del sitio.

* El `prop3` La variable de Adobe Analytics está asignada a `pagedata.subsection` propiedad del sitio.

* El siguiente código se agrega al cuadro de diálogo Código libre de JavaScript:

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* Cuando se visita la página web que utiliza el módulo de (o, en el modo de edición, se vuelve a cargar la página o se obtiene una vista previa de ella), se realizan las llamadas a Adobe Analytics.

Por ejemplo, en Adobe Analytics se generan los siguientes valores:

![aa-20](assets/aa-20.png)

### Añadir código personalizado global para todos los marcos de Adobe Analytics {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Proporcione código JavaScript personalizado que esté integrado en todos los marcos de trabajo de Adobe Analytics. Cuando el marco de trabajo de Adobe Analytics de una página no contiene elementos personalizados [JavaScript de forma libre](/help/sites-administering/adobeanalytics.md), el JavaScript que genera el script /libs/cq/analytics/components/sitecatalyst/config.js.jsp se anexa al [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) archivo. De forma predeterminada, la secuencia de comandos no tiene efecto porque está comentada. El código también establece `s.usePlugins` hasta `false`:

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

El código del archivo analytics.sitecatalyst.js (que incluye el contenido del archivo Adobe Analytics s_code.js) contiene el siguiente código:

if (s.usePlugins) s.doPlugins

Por lo tanto, JavaScript debe establecer `s.usePlugins` hasta `true` para que cualquier código de la variable `s_doPlugins` se ejecuta. Para personalizar el código, superponga el archivo config.js.jsp con uno que utilice su propio JavaScript. Si JavaScript necesita utilizar complementos de Adobe Analytics, [integrarlos](/help/sites-administering/adobeanalytics.md) AEM en el.

>[!NOTE]
>
>No edite el archivo /libs/cq/analytics/components/sitecatalyst/config.js.jsp. AEM Ciertas tareas de actualización o mantenimiento pueden reinstalar el archivo original y eliminar los cambios.

1. En CRXDE Lite, cree la estructura de carpetas /apps/cq/analytics/components:

   1. Haga clic con el botón derecho en la carpeta /apps y haga clic en Crear > Crear carpeta.
   1. Especificar `cq` como el nombre de la carpeta y haga clic en Aceptar.
   1. Del mismo modo, cree el `analytics` y `components` carpetas.

1. Haga clic con el botón derecho en `components` que ha creado y haga clic en Crear > Crear componente. Especifique los siguientes valores de propiedad:

   * Etiqueta: `sitecatalyst`
   * Título: `sitecatalyst`
   * Supertipo: `/libs/cq/analytics/components/sitecatalyst`
   * Grupo: `hidden`

1. Haga clic repetidamente en Siguiente hasta que el botón Aceptar esté habilitado y, a continuación, haga clic en Aceptar.

   El componente de SiteCatalyst contiene el archivo sitecatalyst.jsp creado automáticamente.

1. Haga clic con el botón derecho en el archivo sitecatalyst.jsp y haga clic en Eliminar.

1. Haga clic con el botón derecho en el componente SiteCatalyst y haga clic en Crear > Crear archivo. Especifique el nombre `config.js.jsp` y, a continuación, haga clic en Aceptar.

   El archivo config.js.jsp se abre automáticamente para su edición.

1. Agregue el siguiente texto al archivo y, a continuación, haga clic en Guardar todo:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   El código JavaScript que genera el script /apps/cq/analytics/components/sitecatalyst/config.js.jsp ahora se inserta en el archivo analytics.sitecatalyst.js para todas las páginas que utilizan un marco de trabajo de Adobe Analytics.

1. Agregue el código JavaScript que desee ejecutar en la variable `s_doPlugins` y, a continuación, haga clic en Guardar todo.

>[!CAUTION]
>
>Si hay texto presente en el JavaScript de forma libre del marco de trabajo de una página (incluso solo espacio en blanco), se omite config.js.jsp.

### Uso de complementos de Adobe Analytics AEM en la {#using-adobe-analytics-plugins-in-aem}

Obtenga el código JavaScript para los complementos de Adobe Analytics e inclúyalos en su marco de trabajo de Adobe Analytics AEM en la versión de. Agregue el código a una carpeta de la biblioteca de cliente de la categoría `sitecatalyst.plugins` para que estén disponibles en el código personalizado de JavaScript.

Por ejemplo, si integra la variable `getQueryParams` , puede llamar al complemento desde el `s_doPlugins` de su JavaScript personalizado. El siguiente código de ejemplo envía la cadena de consulta en **&quot;pid&quot;** desde la dirección URL del referente como **EVAR 1**, cuando se activa una llamada de Adobe Analytics.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM instala los siguientes complementos de Adobe Analytics, de modo que estén disponibles de forma predeterminada:

* getQueryParam()
* getPreviousValue()
* split()

La carpeta de biblioteca de cliente /libs/cq/analytics/clientlibs/sitecatalyst/plugins incluye estos complementos en la categoría sitecatalyst.plugins.

>[!NOTE]
>
>Cree una carpeta de biblioteca de cliente para los complementos. No agregue complementos a `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` carpeta. Esta práctica garantiza que su contribución a la `sitecatalyst.plugins` AEM Las categorías de no se sobrescriben durante las tareas de reinstalación o actualización de la.

Utilice el siguiente procedimiento para crear la carpeta de la biblioteca de cliente para sus complementos. Solo debe realizar este procedimiento una vez. Para añadir un complemento a la carpeta de biblioteca del cliente, utilice el procedimiento siguiente.

1. En un explorador web, abra el CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Haga clic con el botón derecho en la carpeta /apps/my-app/clientlibs y haga clic en Crear > Crear nodo. Introduzca los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: un nombre para la carpeta de la biblioteca de cliente, como my-plugins

   * Tipo: cq:ClientLibraryFolder

1. Seleccione la carpeta de biblioteca de cliente que ha creado y utilice la barra de propiedades inferior derecha para agregar la siguiente propiedad:

   * Nombre: categories
   * Tipo: cadena
   * Valor: sitecatalyst.plugins
   * Múltiple: seleccionado

   Haga clic en OK en la ventana Edit para confirmar el valor de la propiedad.

1. Haga clic con el botón derecho en la carpeta de la biblioteca de cliente que ha creado y haga clic en Crear > Crear archivo. Para el nombre de archivo, escriba js.txt y haga clic en Aceptar.

1. Haga clic en Guardar todo.

AEM Utilice el siguiente procedimiento para obtener el código del complemento, almacenarlo en el repositorio de y agregarlo a la carpeta de la biblioteca de cliente.

1. Iniciar sesión en [sc.omniture.com](https://sc.omniture.com/login/) con su cuenta de Adobe Analytics.
1. En la página de aterrizaje, vaya a Ayuda > Página principal de ayuda.
1. En la tabla de contenido de la izquierda, haga clic en Complementos de implementación.
1. Haga clic en el vínculo al complemento que desee añadir y, cuando se abra la página, busque el código fuente JavaScript para el complemento y, a continuación, seleccione el código y cópielo.

1. Haga clic con el botón derecho en la carpeta de la biblioteca de cliente y haga clic en Crear > Crear archivo. Para el nombre del archivo, escriba el nombre del complemento que está integrando seguido de .js y, a continuación, haga clic en Aceptar. Por ejemplo, si está integrando el complemento getQueryParam, asigne al archivo el nombre getQueryParam.js.

   Cuando cree el archivo, se abrirá para editarlo.

1. Pegue el código JavaScript del complemento en el archivo, haga clic en Guardar todo y cierre el archivo.

1. Abra el archivo js.txt desde la carpeta de biblioteca de cliente.

1. En una línea nueva, añada el nombre del archivo que contiene el complemento, por ejemplo, getQueryParam.js. A continuación, haga clic en Guardar todo y cierre el archivo.

>[!NOTE]
>
>Cuando utilice complementos, asegúrese de integrar también cualquier complemento de soporte; de lo contrario, el complemento JavaScript no reconocerá las llamadas que realiza a las funciones del complemento de soporte. Por ejemplo, el complemento getPreviousValue() requiere que el complemento split() funcione correctamente.
>
>El nombre del complemento de asistencia debe añadirse a **js.txt** y también.
