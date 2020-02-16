---
title: Configuración del seguimiento de vínculos para Adobe Analytics
seo-title: Configuración del seguimiento de vínculos para Adobe Analytics
description: Obtenga información sobre la configuración del seguimiento de vínculos para SiteCatalyst.
seo-description: Obtenga información sobre la configuración del seguimiento de vínculos para SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2

---


# Configuración del seguimiento de vínculos para Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Cuando los usuarios hacen clic en los vínculos de las páginas del sitio web, puede capturar información relacionada en Adobe Analytics. Por ejemplo: utilice el seguimiento de vínculos para conocer la forma en que los usuarios interactúan con el sitio, rastrear las descargas de archivos y rastrear los vínculos de salida.

## Configuración del seguimiento de vínculos para un marco de Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Con **Navegación**, vaya a través de **Implementación**, Servicios **de** nube a la sección **Adobe Analytics** .

1. Con **Mostrar configuraciones**, abra el marco de trabajo necesario de Adobe Analytics.
1. Expanda la sección Configuración **de seguimiento de** vínculos y configúrela según sea necesario (esta página proporciona más detalles):

   ![aa-08](assets/aa-08.png)

## Seguimiento de descargas de archivos {#tracking-file-downloads}

Configure el marco de Adobe Analytics para que los archivos descargados de páginas asociadas se rastreen automáticamente como descargas en Adobe Analytics. Cuando se habilita el seguimiento de descargas, solo se realiza el seguimiento de los tipos de archivo que se especifiquen.

Las descargas de los siguientes tipos de archivo se rastrean de forma predeterminada:

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

Por ejemplo: con el seguimiento de descargas habilitado para archivos PDF, siempre que los usuarios hagan clic en vínculos a archivos PDF, se realizará un seguimiento de la descarga del PDF.

Las propiedades de seguimiento de descarga de la estructura se implementan como código en el `analytics.sitecatalyst.js` archivo que se genera para una página. El siguiente ejemplo de código representa la configuración predeterminada del seguimiento de descarga:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Para habilitar el seguimiento de descargas para el marco de Adobe Analytics:

1. [Abra el marco de trabajo de Adobe Analytics y expanda la sección](#configuring-link-tracking-for-an-adobe-analytics-framework)Configuración del seguimiento de vínculos.
1. Habilite **Rastrear descargas**.
1. En el cuadro **Descargar tipos** de archivo, escriba las extensiones de nombre de archivo para los tipos de archivos que desee rastrear.

## Seguimiento de vínculos externos {#tracking-external-links}

Puede rastrear los clics de los vínculos externos (vínculos de salida) en las páginas.

Para rastrear vínculos externos para su marco de trabajo de Adobe Analytics:

1. [Abra el marco de trabajo de Adobe Analytics y expanda la sección Configuración **de seguimiento de** vínculos](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para el seguimiento cuando se hace clic en vínculos externos:

* **Seguimiento externo** Habilita el seguimiento de vínculos externos.

* **Filtros** externos (opcional) Define filtros para que coincidan con las direcciones URL externas de los destinos de vínculo. Cuando los destinos de vínculo coinciden con el filtro, se realiza el seguimiento del vínculo. Los filtros externos son útiles para rastrear solo algunos de los vínculos externos de las páginas.

   Para especificar los vínculos externos para rastrear, escriba la dirección URL completa o parte de la dirección URL del destino del vínculo. Separe varios filtros con una coma. Escriba literales de cadena entre comillas simples. Ningún valor (el valor predeterminado de `''`, dos comillas simples) hace que se rastreen todos los vínculos externos.

* **Filtros** internos Define filtros para que coincidan con las direcciones URL de los vínculos internos. Cuando el vínculo está dirigido a direcciones URL que coinciden con este filtro, no se realiza el seguimiento del vínculo. El valor predeterminado es un comando javascript que devuelve el nombre de host de la URL de la dirección de la ventana actual.

   Para especificar los vínculos internos que no se rastrean, escriba la dirección URL interna completa o parte de ella del destino del vínculo. Separe varios filtros con una coma. Escriba literales de cadena entre comillas simples.

   El valor predeterminado es `'javascript:,'+window.location.hostname`

* **Dejar cadena** de consultaIncluye parámetros de URL al evaluar coincidencias con filtros internos y externos.

   Active esta opción para incluir parámetros de URL al evaluar las direcciones URL de destino de vínculos con filtros externos e internos.

Las propiedades de seguimiento de vínculos externos se implementan como código en el `analytics.sitecatalyst.js` archivo que se genera para una página. El siguiente código de ejemplo se genera para una página asociada a un marco que ha habilitado el seguimiento de vínculos externos con la siguiente configuración:

* El filtro externo es `'google.com'`
* El filtro interno es el valor predeterminado de `'javascript:,'+window.location.hostname`
* Las cadenas de consulta no se incluyen al evaluar el destino del vínculo con los filtros.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Envío de datos de variables con clics en vínculos {#sending-variable-data-with-link-clicks}

Puede configurar AEM para que envíe datos de eventos y variables a Adobe Analytics cuando un usuario haga clic en un vínculo. Las propiedades de configuración **de seguimiento de** vínculos le permiten especificar los eventos y las variables de Adobe Analytics para rastrear cuándo se producen clics en vínculos.

Las asignaciones de marco determinan los valores de evento y variable. Puede asignar variables de Adobe Analytics a las variables de los componentes de contenido que almacenan los datos que desea rastrear cuando se hace clic en los vínculos.

Para enviar datos de variables con clics en vínculos:

1. [Abra el marco de trabajo de Adobe Analytics y expanda la sección](#configuring-link-tracking-for-an-adobe-analytics-framework)Configuración del seguimiento de vínculos.
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para enviar datos de variables con clics en vínculos:

* **Vínculo de eventos** de seguimiento Introduzca las variables de eventos de Adobe Analytics que desea utilizar para contar los clics en vínculos.

   Separe los nombres de varias variables con una coma.

   El valor predeterminado de `None` no provoca el seguimiento de eventos.

* **Vars** de seguimiento de vínculos Introduzca las variables de Adobe Analytics que desea enviar a Adobe Analytics cuando se hace clic en los vínculos. Separe los nombres de varias variables con una coma.

   El valor predeterminado de `None` hace que no se envíen datos de variables.

Cuando se especifican los eventos y las variables que se van a enviar, la configuración se implementa como código en el `analytics.sitecatalyst.js` archivo que se genera para una página. El siguiente código de ejemplo se genera para una página cuando la estructura rastrea el `event10` evento y la `prop4` propiedad:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Ejemplo de configuración del seguimiento de vínculos {#example-link-tracking-configuration}

Realice los siguientes procedimientos para explorar el comportamiento de seguimiento de vínculos de la integración de Adobe Analytics. Los procedimientos muestran los resultados de [Adobe Marketing Cloud Debugger](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html).

### General configuration {#general-configuration}

Este ejemplo ilustra cómo funciona la asignación en el contexto del seguimiento y el depurador:

1. Abra el marco que se ha asociado con una página web.
1. Arrastre el componente **Página** al área de asignaciones del marco. El componente **Página** pertenece al grupo de componentes **General** en la barra de tareas.

   >[!NOTE]
   >
   >El componente que debe utilizar en un escenario de vida real depende del componente heredado (si es que lo hace).
   >
   >Si no es así, debería tener su propio componente expuesto allí (definiendo un subnodo de análisis en su componente de página).

   Configure la asignación según la tabla siguiente, arrastrando la variable de Analytics (SiteCatalyst) desde el panel izquierdo:

<table>
 <tbody>
  <tr>
   <th>CQ Variable<br /> </th>
   <th>Entrada en el explorador de variables<br /> </th>
   <th>Variable de Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>eVar personalizada 1 (eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizado 1 (evento1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Arrastre el componente Buscar al área de asignaciones del marco. El componente Buscar pertenece al grupo de componentes General de la barra de tareas. Configure la asignación según la tabla siguiente, arrastrando la variable de Analytics (SiteCatalyst) desde el panel izquierdo:

<table>
 <tbody>
  <tr>
   <th>CQ Variable<br /> </th>
   <th>Entrada en el explorador de variables</th>
   <th>Variable de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>eVar personalizada 2 (eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>eVar personalizada 3 (eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizado 2 (evento2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurar el seguimiento de vínculos externos {#configure-external-link-tracking}

1. En su marco de trabajo, expanda el área Configuración **de seguimiento de** vínculos.
1. Anule la selección de **Seguimiento de descargas**.

1. Seleccione **Rastrear externo**.
1. Anule la selección de **Dejar cadena** de consulta.
1. Utilice el siguiente valor para la lista Filtros **** externos para identificarla como una URL externa:

   `‘yahoo.com’`

1. Agregue el siguiente valor al campo **Vincular eventos** de seguimiento:

   ```
       event1,event2
   ```

1. Agregue el siguiente valor al campo **Vincular variables** de seguimiento:

   ```
       eVar1,eVar2
   ```

1. En la página asociada al marco, agregue un componente **Texto** . Dentro del componente **Texto** , agregue un hipervínculo que señale a la siguiente dirección:

   `https://search.yahoo.com/?p=this`

1. Cambie al modo **** Vista previa y haga clic en el vínculo.

La llamada realizada tendrá este aspecto cuando se visualice con Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>La dirección URL no contiene la cadena de consulta: `?p=this`

### Incluir el parámetro de URL {#include-the-url-parameter}

1. En el marco, expanda el área Configuración **de seguimiento de** vínculos.
1. Habilitar **dejar cadena** de consulta.
1. Vuelva a cargar la vista previa de la página y haga clic en el vínculo.

Los detalles de la llamada que aparecen en Adobe Marketing Cloud Debugger son similares al siguiente ejemplo:

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Esta vez la dirección URL contiene la cadena de consulta: `?p=this`

## Ad-Hoc Link Tracking {#ad-hoc-link-tracking}

El seguimiento de vínculos específicos permite a los autores de contenido configurar el seguimiento de vínculos para un componente. La configuración del componente anula la configuración **de seguimiento de** vínculos del marco, por lo que en las páginas asociadas con el marco se pueden configurar componentes de **texto** para el seguimiento de vínculos de direcciones URL.

El seguimiento de vínculos ad-hoc le permite rastrear vínculos de descarga, vínculos externos, junto con datos de variables y eventos.

Para habilitar el seguimiento de vínculos ad-hoc debe:

* [Asocie la página que contiene el componente **Texto** con el marco](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configure el marco de trabajo de Adobe Analytics para habilitar el seguimiento](#enabling-ad-hoc-link-tracking)de vínculos ad-hoc.
* [Configuración del seguimiento de vínculos para un componente](#configuring-link-tracking-for-a-text-component)de texto.

### Activación del seguimiento de vínculos específicos {#enabling-ad-hoc-link-tracking}

Configure el marco de Adobe Analytics para habilitar el seguimiento de vínculos ad-hoc.

1. Abra el marco de Adobe Analytics y expanda la sección Configuración **del seguimiento de** vínculos.

1. Habilite el seguimiento **de vínculos específicos**.

   >[!NOTE]
   >
   >No todos los tipos de usuarios tienen acceso a esta casilla. Póngase en contacto con el administrador del sitio si necesita acceso.

>[!NOTE]
>
>La configuración XSS Antisamy ahora está en SLING en la ruta **/libs/sling/xss.config.xml** y es necesario agregar las siguientes reglas para que funcione la vinculación ad-hoc:

#### Extensión de regla de etiqueta delimitadora {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### Configuración del seguimiento de vínculos para un componente de texto {#configuring-link-tracking-for-a-text-component}

Para poder configurar el seguimiento de vínculos ad-hoc para los propios componentes de **texto** , las siguientes configuraciones ya deben haberse implementado:

* El marco de trabajo de [Adobe Analytics está configurado para habilitar el seguimiento](#enabling-ad-hoc-link-tracking)de vínculos ad-hoc.
* La [página que contiene el componente **Texto** está asociada al marco](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Utilice el procedimiento siguiente para configurar el seguimiento de vínculos para un componente **Texto** :

1. Abra la página en modo de edición y edite el componente **Texto** .

1. Seleccione el texto que desee utilizar como hipertexto y haga clic en el botón Hipervínculo.

   ![](do-not-localize/chlimage_1.png)

1. Agregue la dirección URL de destino en el cuadro Vincular a y expanda el área Seguimiento de vínculos.

   >[!NOTE]
   >
   >El seguimiento de vínculos personalizados está visible como una acción independiente, junto a la acción Vincular/Desvincular (icono de Analytics).
   >
   >Solo se activará cuando haya seleccionado un vínculo válido en RTE.

   ![aa-17](assets/aa-17.png)

1. Active el seguimiento **de vínculos** personalizados para anular la configuración del seguimiento de vínculos del marco de Adobe Analytics y habilitar el seguimiento de vínculos para el vínculo actual.

1. (Opcional) Para rastrear eventos con el clic en el vínculo, agregue los nombres de eventos de Adobe Analytics en el campo **Incluir variables** de Adobe Analytics. Separe el nombre de varios eventos con comas, por ejemplo

   `event1, event22`.

1. (Opcional) Para rastrear datos de variables con el clic en el vínculo, agregue variables de Adobe Analytics en el campo **Incluir variables** de Adobe Analytics. Utilice cualquiera de los formatos siguientes:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*
   Los siguientes ejemplos ilustran cada formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`
   Separe varios valores con una coma.

1. Seleccione **Aceptar**.

