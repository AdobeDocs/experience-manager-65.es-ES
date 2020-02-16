---
title: Personalización de Adobe Analytics Framework
seo-title: Personalización de Adobe Analytics Framework
description: nulo
seo-description: nulo
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# Personalización de Adobe Analytics Framework{#customizing-the-adobe-analytics-framework}

El marco de trabajo de Adobe Analytics determina la información que se rastrea con Adobe Analytics. Para personalizar la estructura predeterminada, utilice javascript para agregar seguimiento personalizado, integrar los complementos de Adobe Analytics y cambiar la configuración general en la estructura utilizada para el seguimiento.

## Acerca del javascript generado para marcos {#about-the-generated-javascript-for-frameworks}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics y la página incluye [referencias al módulo](/help/sites-administering/adobeanalytics.md)de Analytics, se genera automáticamente un archivo analytics.sitecatalyst.js para la página.

El javascript de la página crea un `s_gi`objeto (que define la biblioteca s_code.js de Adobe Analytics) y asigna valores a sus propiedades. El nombre de la instancia de objeto es `s`. Los ejemplos de código que se presentan en esta sección hacen varias referencias a esta `s` variable.

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

Al utilizar código personalizado de javascript para personalizar la estructura, se modifica el contenido de este archivo.

## Configuración de las propiedades de Adobe Analytics {#configuring-adobe-analytics-properties}

Adobe Analytics incluye una serie de variables predefinidas que se pueden configurar en un marco. Las variables **charset**, **cookieLifetime**, **currencyCode** y **trackInlineStats** se incluyen de forma predeterminada en la lista Configuración **** general de Analytics.

![aa-22](assets/aa-22.png)

Puede agregar nombres y valores de variables a la lista. Estas variables predefinidas y cualquier variable que agregue se utilizarán para configurar las propiedades del `s` objeto en el archivo analytics.sitecatalyst.js. El siguiente ejemplo muestra cómo se representa la propiedad `prop10` agregada del valor `CONSTANT` en el código javascript:

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

Siga el procedimiento siguiente para agregar variables a la lista:

1. En la página de marco de Adobe Analytics, expanda el área Configuración **** general de análisis.
1. Debajo de la lista de variables, haga clic en Agregar elemento para agregar una nueva variable a la lista.
1. En la celda de la izquierda, escriba un nombre para la variable, por ejemplo `prop10`.

1. En la columna de la derecha, introduzca un valor para la variable, por ejemplo `CONSTANT`.

1. Para eliminar una variable, haga clic en el botón (-) al lado de la variable.

>[!NOTE]
>
>Al introducir variables y valores, asegúrese de que tienen el formato y la ortografía correctos o de que las **llamadas no se enviarán** con el par valor/variable correcto. Los valores y las variables mal escritos pueden incluso evitar que se produzcan llamadas.
>
>Consulte con su representante de Adobe Analytics para asegurarse de que estas variables están correctamente configuradas.

>[!CAUTION]
>
>Algunas de las variables de esta lista son **obligatorias** para que las llamadas de Adobe Analytics funcionen correctamente (por ejemplo, **currencyCode**, **charSet**)
>
>Por lo tanto, aunque se eliminen del propio marco, se adjuntarán con un valor predeterminado cuando se realice la llamada de Adobe Analytics.

### Adición de javascript personalizado a un marco de Adobe Analytics {#adding-custom-javascript-to-an-adobe-analytics-framework}

El cuadro javascript gratuito del área Configuración **** general de análisis le permite agregar código personalizado a un marco de Adobe Analytics.

![aa-21](assets/aa-21.png)

El código que agregue se anexa al archivo analytics.sitecatalyst.js. Por lo tanto, puede acceder a la `s` variable, que es una instancia del objeto `s_gi` javascript definido en `s_code.js`. Por ejemplo, agregar el siguiente código equivale a agregar una variable denominada `prop10` of value `CONSTANT`, que es el ejemplo de la sección anterior:

`s.prop10= 'CONSTANT';`

El código del archivo [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (que incluye el contenido del `s-code.js` archivo de Adobe Analytics) contiene el siguiente código:

`if (s.usePlugins) s.doPlugins(s)`

El siguiente procedimiento muestra cómo utilizar el cuadro de javascript para personalizar el seguimiento de Adobe Analytics. Si su javascript necesita utilizar complementos de Adobe Analytics, [inclúyalos](/help/sites-administering/adobeanalytics.md) en AEM.

1. Agregue el siguiente código de javascript al cuadro para que `s.doPlugins` se ejecute:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Este código es necesario si desea enviar variables en una llamada de Adobe Analytics que se hayan personalizado de alguna manera que no se puedan realizar mediante la interfaz básica de arrastrar y soltar O mediante javascript en línea en la vista de Adobe Analytics.
   >
   >Si las variables personalizadas están fuera de la función s_doPlugins, se enviarán como *undefined *en la llamada de Adobe Analytics

1. Agregue el código de javascript en la función **s_doPlugins** .

El siguiente ejemplo concatena los datos capturados en una página en orden jerárquico, utilizando un separador común de &quot;|&quot;.

Un marco de trabajo de Adobe Analytics tiene las siguientes configuraciones:

* La variable `prop2` de Adobe Analytics se asigna a la propiedad del `pagedata.sitesection` sitio.

* La variable `prop3` de Adobe Analytics se asigna a la propiedad del `pagedata.subsection` sitio.

* El siguiente código se agrega al cuadro javascript libre:

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* Cuando se visita la página web que utiliza el marco (o, en modo de edición, se vuelve a cargar o previsualizar la página), se realizan las llamadas a Adobe Analytics.

Por ejemplo, en Adobe Analytics se generan los siguientes valores:

![aa-20](assets/aa-20.png)

### Adición de código personalizado global para todos los marcos de Adobe Analytics {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Proporcione código de JavaScript personalizado que esté integrado en todos los marcos de trabajo de Adobe Analytics. Cuando la estructura de Adobe Analytics de una página no contiene JavaScript [de forma](/help/sites-administering/adobeanalytics.md)libre personalizado, el javascript que genera la secuencia de comandos /libs/cq/analytics/components/sitecatalyst/config.js.jsp se anexa al archivo [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) . De forma predeterminada, la secuencia de comandos no tiene efecto porque está comentada. El código también se establece `s.usePlugins` en `false`:

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

El código del archivo analytics.sitecatalyst.js (que incluye el contenido del archivo s_code.js de Adobe Analytics) contiene el siguiente código:

if (s.usePlugins) s.doPlugins(s)

Por lo tanto, javascript debe configurarse `s.usePlugins` en `true` para que se ejecute cualquier código de la `s_doPlugins` función. Para personalizar el código, superponga el archivo config.js.jsp con uno que utilice su propio javascript. Si su javascript necesita utilizar complementos de Adobe Analytics, [inclúyalos](/help/sites-administering/adobeanalytics.md) en AEM.

>[!NOTE]
>
>No edite el archivo /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Algunas tareas de actualización o mantenimiento de AEM pueden volver a instalar el archivo original, eliminando los cambios.

1. En CRXDE Lite, cree la estructura de carpetas /apps/cq/analytics/components:

   1. Haga clic con el botón secundario en la carpeta /apps y, a continuación, haga clic en Crear > Crear carpeta.
   1. Especifique `cq` como nombre de la carpeta y haga clic en Aceptar.
   1. Del mismo modo, cree las `analytics` carpetas y `components` .

1. Haga clic con el botón secundario en la `components` carpeta que acaba de crear y, a continuación, haga clic en Crear > Crear componente. Especifique los siguientes valores de propiedad:

   * Etiqueta: `sitecatalyst`
   * Título: `sitecatalyst`
   * Super Type: `/libs/cq/analytics/components/sitecatalyst`
   * Agrupar: `hidden`

1. Haga clic en Siguiente varias veces hasta que el botón Aceptar esté activado y, a continuación, haga clic en Aceptar.

   El componente sitecatalyst contiene el archivo sitecatalyst.jsp creado automáticamente.

1. Haga clic con el botón secundario en el archivo sitecatalyst.jsp y, a continuación, haga clic en Eliminar.

1. Haga clic con el botón secundario en el componente de SiteCatalyst y, a continuación, haga clic en Crear > Crear archivo. Especifique el nombre `config.js.jsp` y haga clic en Aceptar.

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

   El código javascript que genera la secuencia de comandos /apps/cq/analytics/components/sitecatalyst/config.js.jsp ahora se inserta en el archivo analytics.sitecatalyst.js para todas las páginas que utilizan un marco de trabajo de Adobe Analytics.

1. Agregue el código javascript que desee ejecutar en la `s_doPlugins` función y, a continuación, haga clic en Guardar todo.

>[!CAUTION]
>
>Si hay texto presente en el JavaScript de forma libre del marco de una página (incluso solo espacios en blanco), se omite config.js.jsp.

### Uso de complementos de Adobe Analytics en AEM {#using-adobe-analytics-plugins-in-aem}

Obtenga el código de javascript para los complementos de Adobe Analytics e inclúyalo en su marco de Adobe Analytics en AEM. Agregue el código a una carpeta de la biblioteca de cliente de la categoría para que esté disponible para el código de JavaScript personalizado. `sitecatalyst.plugins`

Por ejemplo, si integra el `getQueryParams` complemento, puede llamar al complemento desde la `s_doPlugins` función de su javascript personalizado. El siguiente código de ejemplo envía la cadena de consulta en **&quot;pid&quot;** desde la dirección URL del referente como **eVar1**, cuando se activa una llamada de Adobe Analytics.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM instala los siguientes complementos de Adobe Analytics para que estén disponibles de forma predeterminada:

* getQueryParam()
* getPreviousValue()
* split()

La carpeta /libs/cq/analytics/clientlibs/sitecatalyst/plugins de la biblioteca del cliente incluye estos complementos en la categoría sitecatalyst.plugins.

>[!NOTE]
>
>Cree una nueva carpeta de biblioteca de cliente para sus complementos. No agregue complementos a la `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` carpeta. Esta práctica garantiza que su contribución a la `sitecatalyst.plugins` categoría no se sobrescriba durante las reinstalaciones o tareas de actualización de AEM.

Utilice el siguiente procedimiento para crear la carpeta de la biblioteca del cliente para sus complementos. Solo necesita realizar este procedimiento una vez. Para agregar un complemento a la carpeta de la biblioteca del cliente, utilice el procedimiento siguiente.

1. En un navegador web, abra CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Haga clic con el botón derecho en la carpeta /apps/my-app/clientlibs y, a continuación, haga clic en Crear > Crear nodo. Introduzca los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: Un nombre para la carpeta de la biblioteca de cliente, como my-plugins

   * Tipo: cq:ClientLibraryFolder

1. Seleccione la carpeta de la biblioteca de cliente que acaba de crear y utilice la barra de propiedades inferior derecha para agregar la siguiente propiedad:

   * Nombre: categorías
   * Tipo: Cadena
   * Valor: sitecatalyst.plugins
   * Múltiple: seleccionado
   Haga clic en Aceptar en la ventana Editar para confirmar el valor de la propiedad.

1. Haga clic con el botón secundario en la carpeta de la biblioteca de cliente que acaba de crear y haga clic en Crear > Crear archivo. Para el nombre de archivo, escriba js.txt y, a continuación, haga clic en Aceptar.

1. Haga clic en Guardar todo.

Utilice el procedimiento siguiente para obtener el código del complemento, almacenarlo en el repositorio de AEM y agregarlo a la carpeta de la biblioteca de cliente.

1. Inicie sesión en [sc.omniture.com](https://sc.omniture.com) con su cuenta de Adobe Analytics.
1. En la página de aterrizaje, vaya a Ayuda > Página inicial de Ayuda.
1. En la tabla de contenido del lado izquierdo, haga clic en Complementos de implementación.
1. Haga clic en el vínculo al complemento que desee agregar y, cuando se abra la página, busque el código fuente de javascript para el complemento, luego seleccione el código y cópielo.

1. Haga clic con el botón secundario en la carpeta de la biblioteca del cliente y, a continuación, haga clic en Crear > Crear archivo. Para el nombre del archivo, escriba el nombre del complemento que está integrando seguido de .js y, a continuación, haga clic en Aceptar. Por ejemplo, si está integrando el complemento getQueryParam, asigne un nombre al archivo getQueryParam.js.

   Al crear el archivo, se abre para su edición.

1. Pegue el código JavaScript del complemento en el archivo, haga clic en Guardar todo y, a continuación, cierre el archivo.

1. Abra el archivo js.txt desde la carpeta de la biblioteca del cliente.

1. En una nueva línea, agregue el nombre del archivo que contiene el complemento, por ejemplo getQueryParam.js. A continuación, haga clic en Guardar todo y cierre el archivo.

>[!NOTE]
>
>Al utilizar complementos, asegúrese de integrar también los complementos de soporte; de lo contrario, el complemento javascript no reconocerá las llamadas que realiza a las funciones del complemento de soporte. Por ejemplo, el complemento getPreviousValue() requiere que el complemento split() funcione correctamente.
>
>El nombre del complemento de soporte también debe agregarse a **js.txt** .
