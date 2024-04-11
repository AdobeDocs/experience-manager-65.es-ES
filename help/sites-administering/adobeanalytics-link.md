---
title: Configuración del seguimiento de vínculos para Adobe Analytics
description: Obtenga información acerca de la configuración del seguimiento de vínculos para el SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# Configuración del seguimiento de vínculos para Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Cuando los usuarios hacen clic en vínculos en páginas del sitio web, puede capturar información relacionada en Adobe Analytics. Por ejemplo, utilice el seguimiento de vínculos para conocer cómo interactúan los usuarios con el sitio, realizar un seguimiento de las descargas de archivos y realizar un seguimiento de los vínculos de salida.

## Configuración del seguimiento de vínculos para un módulo de Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. Uso de **Navegación**, vaya a **Implementación**, **Cloud Service** a la **Adobe Analytics** sección.

1. Uso de **Mostrar configuraciones**, abra el marco de trabajo de Adobe Analytics necesario.
1. Expanda el **Configuración de seguimiento de vínculos** y configúrelo según sea necesario (esta página proporciona más detalles):

   ![Marco de Analytics](assets/aa-08.png)

## Descargas de archivos de seguimiento {#tracking-file-downloads}

Configure el marco de Adobe Analytics para que los archivos descargados de páginas asociadas se rastreen automáticamente como descargas en Adobe Analytics. Al habilitar el seguimiento de descargas, solo se realiza el seguimiento de los tipos de archivo especificados.

De forma predeterminada, se realiza un seguimiento de las descargas de los siguientes tipos de archivos:

* exe
* zip
* ondular
* mp3
* mover
* mpg
* avi
* wmv
* doc
* pdf
* xls

Por ejemplo, con el seguimiento de descargas habilitado para archivos de PDF, cada vez que los usuarios hacen clic en vínculos a archivos de PDF, se realiza un seguimiento de la descarga del PDF.

Las propiedades de seguimiento de descargas del marco de trabajo se implementan como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente ejemplo de código representa la configuración de seguimiento de descarga predeterminada:

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Para habilitar el seguimiento de descargas en el marco de trabajo de Adobe Analytics:

1. [Abra el marco de Adobe Analytics y expanda la sección Configuración del seguimiento de vínculos](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Activar **Descargas de seguimiento**.
1. En el **Descargar tipos de archivo** , escriba las extensiones de nombre de archivo para los tipos de archivos de los que desea realizar un seguimiento.

## Seguimiento de vínculos externos {#tracking-external-links}

Puede realizar un seguimiento de los clics en vínculos externos (vínculos de salida) en las páginas.

Para realizar un seguimiento de los vínculos externos del marco de trabajo de Adobe Analytics:

1. [Abra el marco de Adobe Analytics y expanda **Configuración de seguimiento de vínculos** sección](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para el seguimiento de cuándo se hace clic en vínculos externos:

* **Seguimiento externo**
Habilita el seguimiento de vínculos externos.

* **Filtros externos**
(Opcional) Define filtros para hacer coincidir las direcciones URL externas de los destinos del vínculo. Cuando los destinos del vínculo coinciden con el filtro, se realiza el seguimiento del vínculo. Los filtros externos solo son útiles para rastrear algunos de los vínculos externos de las páginas.

  Para especificar los vínculos externos que se van a rastrear, escriba la dirección URL del destino del vínculo o parte de ella. Separe varios filtros con una coma. Escriba los literales de cadena entre comillas simples. Sin valor (el valor predeterminado de `''`, dos comillas simples) hace que se rastreen todos los vínculos externos.

* **Filtros internos**
Define filtros para hacer coincidir las direcciones URL de los vínculos internos. Cuando el vínculo se dirige a direcciones URL que coinciden con este filtro, no se realiza el seguimiento del vínculo. El valor predeterminado es un comando de javascript que devuelve el nombre de host de la dirección URL de la dirección de la ventana actual.

  Para especificar los vínculos internos de los que no se realiza un seguimiento, escriba la dirección URL interna del destino del vínculo o parte de ella. Separe varios filtros con una coma. Escriba los literales de cadena entre comillas simples.

  El valor predeterminado es `'javascript:,'+window.location.hostname`

* **Dejar cadena de consulta**
Incluye parámetros de URL al evaluar coincidencias con filtros internos y externos.

  Habilite la opción si desea incluir parámetros de URL al evaluar direcciones URL de destino de vínculo con filtros externos e internos.

Las propiedades de seguimiento de vínculos externos se implementan como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente código de ejemplo se genera para una página asociada a un marco de trabajo que ha habilitado el seguimiento de vínculos externos con la siguiente configuración:

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

AEM Puede configurar los datos para enviar datos de eventos y variables a Adobe Analytics cuando un usuario haga clic en un vínculo. El **Configuración de seguimiento de vínculos** las propiedades permiten especificar los eventos y las variables de Adobe Analytics que se van a rastrear cuando se producen clics en vínculos.

Las asignaciones de marco de trabajo determinan los valores de evento y de variable. Puede asignar variables de Adobe Analytics a las variables de los componentes de contenido que almacenan los datos de los que desea hacer un seguimiento cuando se hace clic en los vínculos.

Para enviar datos variables con clics en vínculos:

1. [Abra el marco de Adobe Analytics y expanda la sección Configuración del seguimiento de vínculos](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configure las siguientes propiedades según sus necesidades.

Propiedades para enviar datos de variables con clics en vínculos:

* **Eventos de seguimiento de vínculos**
Introduzca las variables de evento de Adobe Analytics que desee utilizar para contar los clics en vínculos.

  Separe los nombres de varias variables con una coma.

  El valor predeterminado de `None` no provoca ningún seguimiento de eventos.

* **Variables de seguimiento de vínculos**
Introduzca las variables de Adobe Analytics que desee enviar a Adobe Analytics cuando se haga clic en un vínculo. Separe los nombres de varias variables con una coma.

  El valor predeterminado de `None` no hace que se envíen datos de variables.

Cuando especifica los eventos y las variables que se van a enviar, la configuración se implementa como código en la variable `analytics.sitecatalyst.js` que se genera para una página. El siguiente código de ejemplo se genera para una página cuando el marco de trabajo realiza el seguimiento de `event10` y el `prop4` propiedad:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Ejemplo de configuración de seguimiento de vínculos {#example-link-tracking-configuration}

Realice los siguientes procedimientos para explorar el comportamiento de seguimiento de vínculos de la integración de Adobe Analytics. Los procedimientos muestran los resultados de [Adobe Marketing Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

### Configuración general {#general-configuration}

Este ejemplo ilustra cómo funciona la asignación en el contexto del seguimiento y el depurador:

1. Abra el marco de trabajo asociado a una página web.
1. Arrastre el **Página** al área de asignaciones del marco de trabajo. El **Página** El componente pertenece a **General** grupo de componentes en el Sidekick.

   >[!NOTE]
   >
   >El componente que debe utilizarse en un escenario en tiempo real depende del componente heredado de (si es que lo es).
   >
   >Si no es así, debe tener su propio componente expuesto allí (definiendo un subnodo de Analytics en su componente de página).

   Configure la asignación según la tabla siguiente arrastrando la variable de Analytics (SiteCatalyst) desde el panel lateral izquierdo:

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrada en el explorador de variables<br /> </th>
   <th>Variable de Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>EVar personalizado 1 (eVar 1)</td>
   <td>EVAR 1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personalizado 1 (evento1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Arrastre el componente Buscar al área de asignaciones del marco de trabajo. El componente Buscar pertenece al grupo de componentes General de Sidekick. Configure la asignación según la tabla siguiente arrastrando la variable de Analytics (SiteCatalyst) desde el panel lateral izquierdo:

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrada en el explorador de variables</th>
   <th>Variable de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>EVar personalizado 2 (eVar 2)</td>
   <td>EVAR 2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>EVar personalizado 3 (eVar 3)</td>
   <td>EVAR 3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personalizado 2 (evento2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configuración del seguimiento de vínculos externos {#configure-external-link-tracking}

1. En el marco de trabajo, expanda **Configuración del seguimiento de vínculos** área.
1. Anular selección **Descargas de seguimiento**.

1. Seleccionar **Seguimiento externo**.
1. Anular selección **Dejar cadena de consulta**.
1. Utilice el siguiente valor para **Filtros externos** para identificarla como URL externa:

   `'yahoo.com'`

1. Añada el siguiente valor a **Eventos de seguimiento de vínculos** campo:

   ```
       event1,event2
   ```

1. Añada el siguiente valor a **Variables de seguimiento de vínculos** campo:

   ```
       eVar1,eVar2
   ```

1. En la página asociada al marco de trabajo, añada un **Texto** componente. Dentro de **Texto** , agregue un hipervínculo que apunte a la siguiente dirección:

   `https://search.yahoo.com/?p=this`

1. Cambiar a **Modo de previsualización** y haga clic en el vínculo.

La llamada realizada tendrá este aspecto cuando se visualice con Adobe Marketing Cloud Debugger:

![Adobe Marketing Cloud Debugger](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>La dirección URL no contiene la cadena de consulta: `?p=this`

### Incluya el parámetro de URL {#include-the-url-parameter}

1. En el marco de trabajo, expanda **Configuración de seguimiento de vínculos** área.
1. Activar **Dejar cadena de consulta**.
1. Vuelva a cargar la vista previa de la página y haga clic en el vínculo.

Los detalles de la llamada que aparecen en Adobe Marketing Cloud Debugger son similares al siguiente ejemplo:

![Adobe Marketing Cloud Debugger de nuevo](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Esta vez, la dirección URL no contiene la cadena de consulta: `?p=this`

## Seguimiento de vínculos ad hoc {#ad-hoc-link-tracking}

El seguimiento de vínculos ad hoc permite a los autores de contenido configurar el seguimiento de vínculos para un componente. La configuración del componente anula la variable **Configuración de seguimiento de vínculos** del marco de trabajo, por ejemplo, en las páginas asociadas al marco de trabajo, **Texto** Los componentes de se pueden configurar para el seguimiento de vínculos de direcciones URL.

El seguimiento de vínculos ad hoc permite rastrear vínculos de descarga y vínculos externos, así como datos de eventos y variables.

Para habilitar el seguimiento de vínculos ad hoc, debe hacer lo siguiente:

* [Asocie la página que contiene el **Texto** componente con el marco](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configure el marco de Adobe Analytics para habilitar el seguimiento de vínculos ad hoc](#enabling-ad-hoc-link-tracking).
* [Configuración del seguimiento de vínculos para un componente de texto](#configuring-link-tracking-for-a-text-component).

### Activación del seguimiento de vínculos ad hoc {#enabling-ad-hoc-link-tracking}

Configure el marco de Adobe Analytics para habilitar el seguimiento de vínculos ad hoc.

1. Abra el marco de Adobe Analytics y expanda **Configuración de seguimiento de vínculos** sección.

1. Activar **Seguimiento de vínculos ad hoc**.

   >[!NOTE]
   >
   >No todos los tipos de usuarios tienen acceso a esta casilla de verificación. Póngase en contacto con el administrador del sitio si necesita acceso.

>[!NOTE]
>
>La configuración XSS Antisamy ahora está en SLING en la ruta **/libs/sling/xss.config.xml** y es necesario añadir las siguientes reglas a para que funcione la vinculación ad hoc:

#### Extensión de regla de etiqueta de anclaje {#anchor-tag-rule-extension}

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

Antes de configurar el seguimiento de vínculos ad hoc para **Texto** componentes en sí, ya deben haberse implementado las siguientes configuraciones:

* El [El marco de Adobe Analytics está configurado para habilitar el seguimiento de vínculos ad hoc](#enabling-ad-hoc-link-tracking).
* El [página que contiene el **Texto** el componente está asociado al marco de trabajo](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Utilice el siguiente procedimiento para configurar el seguimiento de vínculos para una **Texto** componente:

1. Abra la página en modo de edición y edite el **Texto** componente.

1. Seleccione el texto que desee utilizar como hipertexto y haga clic en el botón Hipervínculo.

   ![Icono de vínculo](do-not-localize/chlimage_1.png)

1. Añada la dirección URL de destino en el cuadro Vincular a y, a continuación, expanda el área Seguimiento de vínculos.

   >[!NOTE]
   >
   >El seguimiento de vínculos personalizados se puede ver como una acción independiente, junto a la acción Vincular/Desvincular (icono de Analytics).
   >
   >Solo se activará cuando haya seleccionado un vínculo válido en RTE.

   ![Habilitación del seguimiento de vínculos](assets/aa-17.png)

1. Activar **Seguimiento de vínculos personalizados** para anular la configuración de seguimiento de vínculos del marco de trabajo de Adobe Analytics y habilitar el seguimiento de vínculos para el vínculo actual.

1. (Opcional) Para realizar un seguimiento de los eventos con el clic en el vínculo, agregue nombres de eventos de Adobe Analytics en la variable **Incluir variables de Adobe Analytics** field. Separe los distintos nombres de eventos con comas, por ejemplo

   `event1, event22`.

1. (Opcional) Para realizar un seguimiento de los datos de las variables con el clic en el vínculo, agregue variables de Adobe Analytics en la variable **Incluir variables de Adobe Analytics** field. Utilice cualquiera de los siguientes formatos:

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`'CONSTANT'`*

   Los siguientes ejemplos ilustran cada formato:

   * `eVar10:pagedata.title`
   * `prop1: 'Aubergine'`

   Separe los distintos valores con una coma.

1. Seleccionar **OK**.
