---
title: Configuración de Seguimiento de vínculos para Adobe Analytics
seo-title: Configuring Link Tracking for Adobe Analytics
description: Obtenga más información sobre la configuración del seguimiento de vínculos para SiteCatalyst.
seo-description: Learn about configuring link tracking for SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 1%

---

# Configuración de Seguimiento de vínculos para Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Cuando los usuarios hacen clic en los vínculos de las páginas de su sitio web, puede capturar información relacionada con Adobe Analytics. Por ejemplo, utilice el seguimiento de vínculos para conocer cómo interactúan los usuarios con el sitio, realizar un seguimiento de las descargas de archivos y rastrear los vínculos de salida.

## Configuración del seguimiento de vínculos para un marco de Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Uso **Navegación**, vaya a **Implementación**, **Cloud Services** a **Adobe Analytics** para obtener más información.

1. Uso **Mostrar configuraciones**, abra el marco de Adobe Analytics requerido.
1. Expanda el **Configuración del seguimiento de vínculos** y configúrelo según sea necesario (esta página proporciona más detalles):

   ![aa-08](assets/aa-08.png)

## Seguimiento de descargas de archivos {#tracking-file-downloads}

Configure el marco de Adobe Analytics para que los archivos descargados de páginas asociadas se rastreen automáticamente como descargas en Adobe Analytics. Al habilitar el seguimiento de descargas, solo se realiza el seguimiento de los tipos de archivo especificados.

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

Por ejemplo, con el seguimiento de descargas habilitado para archivos PDF, siempre que los usuarios hagan clic en vínculos a archivos PDF, se realizará un seguimiento de la descarga del PDF.

Las propiedades de seguimiento de descargas de la infraestructura se implementan como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente ejemplo de código representa la configuración de seguimiento de descarga predeterminada:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Para habilitar el seguimiento de descargas para la infraestructura de Adobe Analytics:

1. [Abra el marco de Adobe Analytics y expanda la sección Configuración del seguimiento de vínculos .](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Habilitar **Seguimiento de descargas**.
1. En el **Descargar tipos de archivo** , escriba las extensiones de nombre de archivo para los tipos de archivos que desea rastrear.

## Seguimiento de vínculos externos {#tracking-external-links}

Puede rastrear los clics de los vínculos externos (vínculos de salida) en las páginas.

Para rastrear vínculos externos para su marco de Adobe Analytics:

1. [Abra el marco de Adobe Analytics y amplíe el **Configuración del seguimiento de vínculos** sección](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para el seguimiento cuando se hace clic en vínculos externos:

* **Seguimiento externo**
Habilita el seguimiento de vínculos externos.

* **Filtros externos**
(Opcional) Define filtros para buscar coincidencias con las direcciones URL externas de los destinos de vínculo. Cuando los objetivos del vínculo coinciden con el filtro, se realiza un seguimiento del vínculo. Los filtros externos son útiles para rastrear solo algunos de los vínculos externos de las páginas.

   Para especificar los vínculos externos para rastrear, escriba la dirección URL completa o parte de la dirección URL del destino del vínculo. Separe varios filtros con una coma. Incluir literales de cadena entre comillas simples. Ningún valor (el valor predeterminado de `''`, dos comillas simples) hace que se rastreen todos los vínculos externos.

* **Filtros internos**
Define filtros para buscar coincidencias con las direcciones URL de los vínculos internos. Cuando el vínculo está dirigido a direcciones URL que coinciden con este filtro, no se realiza un seguimiento del vínculo. El valor predeterminado es un comando javascript que devuelve el nombre de host de la dirección URL de la ventana actual.

   Para especificar los vínculos internos de los que no se realiza un seguimiento, escriba toda o parte de la dirección URL interna del destino del vínculo. Separe varios filtros con una coma. Incluir literales de cadena entre comillas simples.

   El valor predeterminado es `'javascript:,'+window.location.hostname`

* **Dejar cadena de consulta**
Incluye parámetros de URL al evaluar coincidencias con filtros internos y externos.

   Habilite para incluir parámetros de URL al evaluar direcciones URL de destino de vínculos con filtros externos e internos.

Las propiedades de seguimiento de vínculos externos se implementan como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente código de ejemplo se genera para una página asociada con un marco que ha habilitado el seguimiento de vínculos externos con la siguiente configuración:

* El filtro externo es `'google.com'`
* El filtro interno es el valor predeterminado de `'javascript:,'+window.location.hostname`
* Las cadenas de consulta no se incluyen al evaluar el destino del vínculo con filtros.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Envío de datos de variable con clics en vínculos {#sending-variable-data-with-link-clicks}

Puede configurar AEM para enviar datos de variables y eventos a Adobe Analytics cuando un usuario haga clic en un vínculo. La variable **Configuración del seguimiento de vínculos** las propiedades permiten especificar los eventos y las variables de Adobe Analytics que se rastrearán cuando se produzcan clics en vínculos.

Las asignaciones de marco determinan los valores de evento y variable. Puede asignar variables de Adobe Analytics a las variables de los componentes de contenido que almacenan los datos que desea rastrear cuando se hace clic en los vínculos.

Para enviar datos variables con clics en vínculos:

1. [Abra el marco de Adobe Analytics y expanda la sección Configuración del seguimiento de vínculos .](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para enviar datos variables con clics en vínculos:

* **Vínculo de seguimiento de eventos**
Introduzca las variables de evento de Adobe Analytics que desee utilizar para contar los clics en vínculos.

   Separe los nombres de varias variables con una coma.

   El valor predeterminado de `None` no provoca un seguimiento de eventos.

* **Vars de seguimiento de vínculos**
Introduzca las variables de Adobe Analytics que desea enviar a Adobe Analytics cuando haga clic en los vínculos. Separe los nombres de varias variables con una coma.

   El valor predeterminado de `None` no hace que se envíen datos de variables.

Cuando especifica los eventos y las variables que se van a enviar, la configuración se implementa como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente código de ejemplo se genera para una página cuando el marco rastrea el `event10` y `prop4` propiedad:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Ejemplo de configuración del seguimiento de vínculos {#example-link-tracking-configuration}

Realice los siguientes procedimientos para explorar el comportamiento de seguimiento de vínculos de la integración de Adobe Analytics. Los procedimientos muestran los resultados de [Adobe Marketing Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

### Configuración general {#general-configuration}

Este ejemplo ilustra cómo funciona la asignación en el contexto del seguimiento y el depurador:

1. Abra la infraestructura asociada a una página web.
1. Arrastre el **Página** al área de asignaciones del marco. La variable **Página** pertenece al **General** grupo de componentes en la barra de tareas.

   >[!NOTE]
   >
   >El componente que debe utilizar en un escenario de vida real depende del componente heredado de (si es que lo hace).
   >
   >Si no es así, debe tener su propio componente expuesto (definiendo un subnodo de analytics en su componente de página).

   Configure la asignación según la tabla siguiente, arrastrando la variable de Analytics (SiteCatalyst) desde el panel lateral izquierdo:

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrada en el explorador de variables<br /> </th>
   <th>Variable Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>eVar personalizado 1 (eVar 1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizado 1 (evento1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Arrastre el componente Buscar al área de asignaciones del marco. El componente Búsqueda pertenece al grupo de componentes General de la barra de tareas. Configure la asignación según la tabla siguiente, arrastrando la variable de Analytics (SiteCatalyst) desde el panel lateral izquierdo:

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrada en el explorador de variables</th>
   <th>Variable Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>eVar personalizado 2 (eVar 2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>eVar personalizado 3 (eVar 3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizado 2 (evento 2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configuración del seguimiento de vínculos externos {#configure-external-link-tracking}

1. En el marco, expanda el **Configuración del seguimiento de vínculos** .
1. Anular selección **Seguimiento de descargas**.

1. Select **Seguimiento externo**.
1. Anular selección **Dejar cadena de consulta**.
1. Utilice el siguiente valor para la variable **Filtros externos** para identificarlo como una URL externa:

   `‘yahoo.com’`

1. Agregue el siguiente valor al **Vínculo de seguimiento de eventos** campo:

   ```
       event1,event2
   ```

1. Agregue el siguiente valor al **Variables de seguimiento de vínculos** campo:

   ```
       eVar1,eVar2
   ```

1. En la página asociada a la estructura, agregue una **Texto** componente. Dentro de **Texto** , agregue un hipervínculo que señale a la siguiente dirección:

   `https://search.yahoo.com/?p=this`

1. Cambie a **Modo de vista previa** y haga clic en el vínculo .

La llamada realizada tendrá este aspecto cuando se visualice con Adobe Marketing Cloud Debugger:

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>La dirección URL no contiene la cadena de consulta: `?p=this`

### Incluir el parámetro de URL {#include-the-url-parameter}

1. En el marco, expanda la **Configuración del seguimiento de vínculos** .
1. Habilitar **Dejar cadena de consulta**.
1. Vuelva a cargar la vista previa de la página y haga clic en el vínculo .

Los detalles de llamada que aparecen en Adobe Marketing Cloud Debugger son similares al siguiente ejemplo:

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Esta vez la dirección URL contiene la cadena de consulta: `?p=this`

## Seguimiento de vínculos específicos {#ad-hoc-link-tracking}

El seguimiento de vínculos específicos permite a los autores de contenido configurar el seguimiento de vínculos de un componente. La configuración del componente anula el **Configuración del seguimiento de vínculos** del marco, por ejemplo, en las páginas asociadas al marco, **Texto** se pueden configurar para el seguimiento de vínculos de direcciones URL.

El seguimiento de vínculos específicos permite rastrear vínculos de descarga y vínculos externos, así como datos de variables y eventos.

Para habilitar el seguimiento de vínculos ad hoc debe:

* [Asocie la página que contiene la variable **Texto** con el marco](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configuración del marco de Adobe Analytics para habilitar el seguimiento de vínculos ad hoc](#enabling-ad-hoc-link-tracking).
* [Configuración del seguimiento de vínculos para un componente de texto](#configuring-link-tracking-for-a-text-component).

### Activación del seguimiento de vínculos específicos {#enabling-ad-hoc-link-tracking}

Configure el marco de Adobe Analytics para habilitar el seguimiento de vínculos ad-hoc.

1. Abra el marco de Adobe Analytics y amplíe el **Configuración del seguimiento de vínculos** para obtener más información.

1. Habilitar **Seguimiento de vínculos específicos**.

   >[!NOTE]
   >
   >No todos los tipos de usuarios tienen acceso a esta casilla de verificación. Póngase en contacto con el administrador del sitio si necesita acceder.

>[!NOTE]
>
>La configuración XSS Antisamy ahora está en SLING en la ruta **/libs/sling/xss.config.xml** y es necesario agregar las siguientes reglas a para que funcione la vinculación ad hoc:

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

Antes de configurar el seguimiento de vínculos específicos para **Texto** , las siguientes configuraciones ya deben haberse implementado:

* La variable [El marco de Adobe Analytics está configurado para habilitar el seguimiento de vínculos ad hoc](#enabling-ad-hoc-link-tracking).
* La variable [página que contiene el **Texto** el componente está asociado con el marco](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Utilice el siguiente procedimiento para configurar el seguimiento de vínculos para un **Texto** componente:

1. Abra la página en modo de edición y edite la **Texto** componente.

1. Seleccione el texto que desee utilizar como hipertexto y haga clic en el botón Hipervínculo .

   ![](do-not-localize/chlimage_1.png)

1. Agregue la dirección URL de destino en el cuadro Vincular a y expanda el área Seguimiento de vínculos .

   >[!NOTE]
   >
   >El seguimiento de vínculos personalizados se puede ver como una acción independiente junto a la acción Vincular/Desvincular (icono de Analytics).
   >
   >Solo se activará si ha seleccionado un vínculo válido en RTE.

   ![aa-17](assets/aa-17.png)

1. Habilitar **Seguimiento de vínculos personalizados** para anular la configuración de seguimiento de vínculos de la infraestructura de Adobe Analytics y habilitar el seguimiento de vínculos para el vínculo actual.

1. (Opcional) Para rastrear eventos con el clic en vínculo, agregue nombres de eventos de Adobe Analytics en la variable **Incluir variables de Adobe Analytics** campo . Separe varios nombres de evento con comas, por ejemplo

   `event1, event22`.

1. (Opcional) Para rastrear datos variables con el clic en vínculo, agregue variables de Adobe Analytics en la variable **Incluir variables de Adobe Analytics** campo . Utilice cualquiera de los siguientes formatos:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*

   Los siguientes ejemplos ilustran cada formato:

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   Separe los distintos valores con una coma.

1. Select **OK**.
