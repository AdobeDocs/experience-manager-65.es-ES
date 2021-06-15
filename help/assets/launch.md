---
title: Integración de visores de Dynamic Media con Adobe Analytics y Experience Platform Launch
description: La extensión de visores de Dynamic Media para Experience Platform Launch, junto con visores de Dynamic Media 5.13, permite a los clientes de Adobe Analytics y a los Platforms launch utilizar eventos y datos específicos para los visualizadores de Dynamic Media en su configuración de Platform launch.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Visores
role: Business Practitioner, Administrator,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: 22a181e77a563ee3590cd661507f4dfeaf9d14da
workflow-type: tm+mt
source-wordcount: '6616'
ht-degree: 8%

---

# Integración de visores de Dynamic Media con Adobe Analytics y el Experience Platform Launch {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## ¿Qué es la integración de los visualizadores de Dynamic Media con Adobe Analytics y Experience Platform Launch? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

La nueva extensión *Dynamic Media Viewers* para Platform launch y visores de Dynamic Media 5.13 permite a los clientes de Adobe Analytics y de Platform launch utilizar eventos y datos específicos para los visualizadores en su configuración de Platform launch.

Esta integración significa que puede realizar un seguimiento del uso de los visualizadores de Dynamic Media en su sitio web con Adobe Analytics. Al mismo tiempo, puede utilizar los eventos y datos expuestos por los visualizadores con cualquier otra extensión de Experience Platform Launch que provenga de un Adobe o de un tercero.

Para obtener más información sobre las extensiones, consulte [Extensión de Adobe](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/overview.html#adobe-extension) en la Guía del usuario del Experience Platform Launch.

**Este tema está diseñado para los siguientes usuarios:** Administradores de sitio, desarrolladores de la plataforma Experience Manager y personas en operaciones.

### Limitaciones de la integración {#limitations-of-the-integration}

* La integración de Experience Platform Launch para visores de Dynamic Media no funciona en el nodo de creación de Experience Manager. No puede ver ningún seguimiento de una página WCM hasta que se publique.
* La integración del Experience Platform Launch para los visores de Dynamic Media no es compatible con el modo de operación &quot;emergente&quot;, en el que la URL del visor se obtiene mediante el botón &quot;URL&quot; de la página Detalles del recurso.
* La integración del Experience Platform Launch no se puede usar simultáneamente con la integración de Analytics de los visores heredados (mediante el parámetro `config2=`).
* La compatibilidad con el seguimiento de vídeo se limita al seguimiento de &quot;reproducción principal&quot;, tal como se describe en [Información general del seguimiento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). En concreto, no se admite el seguimiento de QoS, anuncios, capítulos/segmentos o errores.
* La configuración de la duración del almacenamiento para elementos de datos no es compatible con los elementos de datos que utilizan la extensión *Visualizadores de Dynamic Media*. La duración del almacenamiento debe establecerse en **[!UICONTROL None]**.

### Ejemplos de uso de la integración {#use-cases-for-the-integration}

El caso de uso principal de la integración con Experience Platform Launch es el de los clientes que usan Adobe Experience Manager Assets y Adobe Experience Manager Sites. En estos casos, puede configurar una integración estándar entre el nodo de creación del Experience Manager y el Experience Platform Launch y, a continuación, asociar la instancia de Sites con la propiedad del Experience Platform Launch. Después, cualquier componente WCM de Dynamic Media añadido a una página Sitios rastreará datos y eventos de los visualizadores.

Consulte [Seguimiento de los visores de Dynamic Media en sitios de Experience Manager](#tracking-dynamic-media-viewers-in-aem-sites).

Un caso de uso secundario que admite la integración es el de los clientes que solo utilizan recursos de Experience Manager o Dynamic Media Classic. En estos casos, obtiene el código incrustado para el visor y lo añade a la página del sitio web. A continuación, obtenga la URL de producción de la biblioteca de Experience Platform Launch del Experience Platform Launch y agréguela manualmente al código de la página web.

Consulte [Seguimiento de visores de Dynamic Media mediante el código incrustado](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## Funcionamiento del seguimiento de datos y eventos en la integración {#how-data-and-event-tracking-works-in-the-integration}

La integración aprovecha dos tipos independientes de seguimiento de visores de Dynamic Media: *Adobe Analytics* y *Adobe Analytics para audio y vídeo*.

### Acerca del seguimiento con Adobe Analytics {#about-tracking-using-adobe-analytics}

Adobe Analytics permite rastrear las acciones que realiza el usuario final cuando interactúa con los visualizadores de Dynamic Media en el sitio web. Adobe Analytics también permite rastrear datos específicos del visor. Por ejemplo, puede rastrear y registrar eventos de carga de vista junto con el nombre del recurso, cualquier acción de zoom que se haya producido y acciones de reproducción de vídeo.

En Experience Platform Launch, los conceptos de *Elementos de datos* y *Reglas* colaboran para habilitar el seguimiento de Adobe Analytics.

#### Acerca de los elementos de datos en el Experience Platform Launch {#about-data-elements-in-adobe-launch}

Un elemento de datos en Experience Platform Launch es una propiedad con nombre cuyo valor se define de forma estática o se calcula dinámicamente en función del estado de una página web o de los datos de los visualizadores de Dynamic Media.

Las opciones disponibles para una definición de elemento de datos dependen de la lista de extensiones instaladas en la propiedad de Experience Platform Launch. La extensión &quot;Core&quot; está preinstalada y está disponible de forma predeterminada en cualquier configuración. Esta extensión &quot;Core&quot; permite definir un elemento de datos que tenga como resultado una cookie, un código JavaScript, una cadena de consulta y muchas otras fuentes.

Para el seguimiento de Adobe Analytics se deben instalar varias extensiones más, como se describe en [Instalación y configuración de extensiones](#installing-and-setup-of-extensions). La extensión Visualizadores de Dynamic Media permite definir un elemento de datos que sea un argumento del evento de visualizador dinámico. Por ejemplo, es posible hacer referencia al tipo de visualizador o al nombre del recurso que el visualizador haya informado al cargar, al nivel de zoom que se recoge cuando el usuario final amplía y mucho más.

La extensión del visor de Dynamic Media mantiene los valores de sus elementos de datos actualizados automáticamente.

Una vez definido, un elemento de datos se puede utilizar en otros lugares de la interfaz de usuario del Experience Platform Launch mediante el widget de selector de elementos de datos. En concreto, la acción Set Variables de la extensión de Adobe Analytics en la regla hace referencia a los elementos de datos definidos para los fines del seguimiento de visualizadores de Dynamic Media (consulte a continuación).

Consulte [Elementos de datos](https://experienceleague.adobe.com/docs/launch/using/ui/data-elements.html).

#### Acerca de las reglas en el Experience Platform Launch {#about-rules-in-adobe-launch}

Una regla en el Experience Platform Launch es una configuración agnóstica que define tres áreas que componen una regla: *Eventos*, *Condiciones* y *Acciones*:

* *Los eventos*  (si) indican al Experience Platform Launch cuándo realizar el déclencheur de una regla.
* *Las condiciones*  (si) indican al Experience Platform Launch qué otras restricciones se permiten o no al activar una regla.
* *Las acciones*  (entonces) indican al Experience Platform Launch qué hacer cuando se activa una regla.

Las opciones disponibles en la sección Eventos, condiciones y acciones dependen de las extensiones instaladas en la propiedad de Experience Platform Launch. La extensión *Core* está preinstalada y disponible de forma predeterminada en cualquier configuración. La extensión proporciona varias opciones para Eventos, como acciones básicas de explorador. Estas acciones incluyen cambio de enfoque, presiones clave y envíos de formularios. También incluye opciones para Condiciones, como el valor de la cookie, el tipo de explorador y mucho más. Para Acciones, solo está disponible la opción Código personalizado .

Para el seguimiento de Adobe Analytics, se deben instalar otras extensiones, tal como se describe en [Instalación y configuración de extensiones](#installing-and-setup-of-extensions). Específicamente:

* La extensión Visualizadores de Dynamic Media amplía la lista de eventos admitidos a eventos específicos de los visualizadores de Dynamic Media, como la carga del visualizador, el intercambio de recursos, el zoom y la reproducción de vídeo.
* La extensión de Adobe Analytics amplía la lista de acciones admitidas con dos acciones necesarias para enviar datos a los servidores de seguimiento: *Set Variables* y *Send Beacon*.

Para realizar el seguimiento de los visores de Dynamic Media, es posible utilizar cualquiera de los siguientes tipos:

* Eventos de la extensión de visores de Dynamic Media, la extensión principal o cualquier otra extensión.
* Condiciones de la definición de regla. O bien, puede dejar vacío el área de condiciones.

En la sección Actions , es necesario que tenga una acción *Set Variables*. Esta acción indica a Adobe Analytics cómo rellenar variables de seguimiento con datos. Al mismo tiempo, la acción *Set Variables* no envía nada al servidor de seguimiento.

La acción *Set Variables* debe ir seguida de una acción *Send Beacon*. La acción *Send Beacon* realmente envía datos al servidor de seguimiento de Analytics. Ambas acciones, *Set Variables* y *Send Beacon*, provienen de la extensión de Adobe Analytics.

Consulte [Reglas](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html).

#### Configuración de ejemplo {#sample-configuration}

La siguiente configuración de ejemplo en Experience Platform Launch muestra cómo rastrear un nombre de recurso al cargar el visor.

1. En la pestaña **[!UICONTROL Data Elements]**, defina un elemento de datos `AssetName` que haga referencia al parámetro `asset` del evento `LOAD` desde la extensión Visualizadores de Dynamic Media.

   ![image2019-11](assets/image2019-11.png)

1. En la pestaña **[!UICONTROL Rules]**, defina una regla *TrackAssetOnLoad*.

   En esta regla, el campo **[!UICONTROL Event]** utiliza el evento **[!UICONTROL LOAD]** de la extensión Visualizadores de Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. La configuración de acción tiene dos tipos de acción de la extensión de Adobe Analytics:

   *Establezca Variables*, que asignan una variable de análisis de su elección al valor del elemento de  `AssetName` datos.

   *Send Beacon*, que envía información de seguimiento a Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. La configuración de regla resultante tiene el siguiente aspecto:

   ![image2019-4](assets/image2019-4.png)

### Acerca de Adobe Analytics para audio y vídeo {#about-adobe-analytics-for-audio-and-video}

Cuando se suscribe una cuenta de Experience Cloud para utilizar Adobe Analytics para audio y vídeo, basta con habilitar el seguimiento de vídeo en la configuración de extensión *Dynamic Media Viewers*. Las métricas de vídeo están disponibles en Adobe Analytics. El seguimiento de vídeo depende de la presencia de la extensión de audio y vídeo de Adobe Medium Analytics.

Consulte [Instalación y configuración de extensiones](#installing-and-setup-of-extensions).

Actualmente, la compatibilidad con el seguimiento de vídeo está limitada únicamente al seguimiento de &quot;reproducción principal&quot;, tal como se describe en [Información general de seguimiento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). En concreto, no se admite el seguimiento de QoS, anuncios, capítulos/segmentos o errores.

## Uso de la extensión de visores de Dynamic Media {#using-the-dynamic-media-viewers-extension}

Como se menciona en [Ejemplos de uso de la integración](#use-cases-for-the-integration), es posible rastrear los visores de Dynamic Media con la nueva integración de Experience Platform Launch en sitios de Experience Manager y mediante el uso del código incrustado.

### Seguimiento de los visores de Dynamic Media en sitios de Experience Manager {#tracking-dynamic-media-viewers-in-aem-sites}

Para realizar un seguimiento de los visores de Dynamic Media en sitios de Experience Manager, se deben realizar todos los pasos que se enumeran en la sección [Configuración de todos los elementos de integración](#configuring-all-the-integration-pieces). Específicamente, debe crear la configuración de IMS y la configuración de Experience Platform Launch Cloud.

Siguiendo la configuración adecuada, cualquier visor de Dynamic Media que agregue a una página Sitios mediante un componente WCM compatible con Dynamic Media, rastreará automáticamente los datos en Adobe Analytics, Adobe Analytics para vídeo o ambos.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Seguimiento de visores de Dynamic Media mediante el código incrustado {#tracking-dynamic-media-viewers-using-embed-code}

Los clientes que no utilizan Experience Manager Sites, o que incrustan visores de Dynamic Media en páginas web fuera de Experience Manager Sites, o ambas, pueden seguir utilizando la integración de Experience Platform Launch.

Complete los pasos de configuración de las secciones [Configuración de Adobe Analytics](#configuring-adobe-analytics-for-the-integration) y [Configuración del Experience Platform Launch](#configuring-adobe-launch-for-the-integration). Sin embargo, no es necesario realizar pasos de configuración relacionados con el Experience Manager.

Siguiendo la configuración adecuada, puede añadir compatibilidad con Experience Platform Launch a una página web con un visor de Dynamic Media.

Consulte [Agregar el código incrustado de Platform launch](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html#configure-launch) para obtener más información sobre cómo utilizar el código incrustado de la biblioteca de Experience Platform Launch.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**Para realizar un seguimiento de los visores de Dynamic Media mediante el código incrustado:**

1. Tenga una página web lista para incrustar un visor de Dynamic Media.
1. Obtenga el código incrustado de la biblioteca de Experience Platform Launch iniciando sesión primero en el Experience Platform Launch (consulte [Configuración del Experience Platform Launch](#configuring-adobe-launch-for-the-integration)).
1. Haga clic en **[!UICONTROL Propiedad]** y, a continuación, haga clic en la pestaña **[!UICONTROL Entornos]**.
1. Elija el nivel Entorno que sea relevante para el entorno de la página web. A continuación, en la columna **[!UICONTROL Install]**, haga clic en el icono de cuadro.
1. **[!UICONTROL En el cuadro de diálogo]** Instrucciones de instalación web , copie el código incrustado completo de la biblioteca de Experience Platform Launch, junto con las  `<script/>` etiquetas que lo rodean.

## Guía de referencia para la extensión de visores de Dynamic Media {#reference-guide-for-the-dynamic-media-viewers-extension}

### Acerca de la configuración de visores de Dynamic Media {#about-the-dynamic-media-viewers-configuration}

La extensión del visor de Dynamic Media se integra automáticamente con la biblioteca de Experience Platform Launch si las siguientes condiciones son verdaderas:

* El objeto global de la biblioteca de Experience Platform Launch ( `_satellite`) está presente en la página.
* La función `_dmviewers_v001()` de extensión de visores de Dynamic Media se define en `_satellite`.

* `config2=` no se ha especificado el parámetro del visor, lo que significa que el visor no utiliza la integración heredada de Analytics.

Además, existe la opción de deshabilitar explícitamente la integración de Experience Platform Launch en el visor especificando el parámetro `launch=0` en la configuración del visor. El valor predeterminado de este parámetro es `1`.

### Configuración de la extensión de visores de Dynamic Media {#configuring-the-dynamic-media-viewers-extension}

La única opción de configuración para la extensión Visualizadores de Dynamic Media es **[!UICONTROL Habilitar Adobe Medium Analytics para audio y vídeo]**.

Cuando marca (activa) esta opción y la extensión de audio y vídeo de Adobe Medium Analytics está instalada y configurada, las métricas de reproducción de vídeo se envían a la solución Adobe Analytics para audio y vídeo . Al desactivar esta opción, se desactiva el seguimiento de vídeo.

Si activa esta opción *sin* tener instalada la extensión de Adobe Medium Analytics para audio y vídeo, la opción no causa ningún efecto.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Acerca de los elementos de datos en la extensión Visualizadores de Dynamic Media {#about-data-elements-in-the-dynamic-media-viewers-extension}

El único tipo de elemento de datos que proporciona la extensión Visualizadores de Dynamic Media es el **[!UICONTROL Evento de visualizador]** de la lista desplegable **[!UICONTROL Tipo de elemento de datos]**.

Cuando se selecciona, el editor de elementos de datos procesa un formulario con dos campos:

* **[!UICONTROL Tipo de datos de evento de visualizadores de DM]**: Una lista desplegable que identifica todos los eventos de visualizador admitidos por la extensión de visualizadores de Dynamic Media que tienen argumentos, además de un elemento especial **[!UICONTROL COMÚN]**. Un elemento **[!UICONTROL COMÚN]** representa una lista de parámetros de evento que son comunes a todos los tipos de eventos enviados por los visualizadores.
* **[!UICONTROL Parámetro de seguimiento]** : argumento del evento de visor de Dynamic Media seleccionado.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulte la [Guía de referencia de visores de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) para obtener una lista de los eventos admitidos por cada tipo de visor; vaya a la sección específico del visor y, a continuación, haga clic en la subsección Compatibilidad con el seguimiento de Adobe Analytics . Actualmente, la guía de referencia de visores de Dynamic Media no documenta argumentos de eventos.

Ahora considere el ciclo de vida de los visualizadores de Dynamic Media *Data Element*. El valor de dicho elemento de datos se rellena después de que el evento del visor de Dynamic Media correspondiente se produzca en la página. Por ejemplo, supongamos que el elemento de datos apunta al evento **[!UICONTROL LOAD]** y a su argumento &quot;asset&quot;. En este caso, el valor de dicho elemento de datos recibe datos válidos después de que el visor ejecute el evento **[!UICONTROL LOAD]** por primera vez. Si el elemento de datos señala al evento **[!UICONTROL ZOOM]** y a su argumento &quot;scale&quot;, el valor de dicho elemento de datos permanece vacío hasta que el usuario envía un evento **[!UICONTROL ZOOM]** por primera vez.

Del mismo modo, los valores de los elementos de datos se actualizan automáticamente cuando el visor envía un evento correspondiente a la página. La actualización de valor se produce incluso si el evento concreto no se especifica en la configuración de regla. Por ejemplo, supongamos que el elemento de datos **[!UICONTROL ZoomScale]** está definido para el parámetro &quot;scale&quot; del evento ZOOM. Sin embargo, la única regla presente en la configuración de regla se activa mediante el evento **[!UICONTROL LOAD]**. El valor de **[!UICONTROL ZoomScale]** se actualiza cada vez que un usuario ejecuta zoom dentro del visor.

Cualquier visualizador de Dynamic Media tiene un identificador único en la página web. El elemento de datos rastrea el propio valor y el visualizador que lo ha rellenado. Por ejemplo, supongamos que hay varios visualizadores en la misma página y un elemento de datos **[!UICONTROL AssetName]** que señala al evento **[!UICONTROL LOAD]** y a su argumento &quot;asset&quot;. El elemento de datos **[!UICONTROL AssetName]** mantiene una colección de nombres de recursos asociados a cada visualizador cargado en la página.

El valor exacto devuelto por el elemento de datos depende del contexto. Si se solicita el elemento de datos en una regla que se activó mediante un evento del visor de Dynamic Media, se devuelve el valor del elemento de datos para el visualizador que inició la regla. Además, el elemento de datos se solicita en una regla que se activó mediante un evento desde otra extensión de Platform launch. En este punto, el valor del elemento de datos proviene del último visor que actualizó este elemento de datos.

**Considere la siguiente configuración de ejemplo:**

* Una página web con dos visores de zoom Dynamic Media: *visor1* y *visor2*.

* **** El elemento ZoomScaleData apunta al  **** evento ZOOM y su argumento &quot;scale&quot;.
* **** TrackPanRule con lo siguiente:

   * Utiliza el evento **[!UICONTROL PAN]** del Visor de Dynamic Media como déclencheur.
   * Envía el valor del elemento de datos **[!UICONTROL ZoomScale]** a Adobe Analytics.

* **** TrackKeyRule con lo siguiente:

   * Utiliza el evento de prensa clave de la extensión del Experience Platform Launch principal como déclencheur.
   * Envía el valor del elemento de datos **[!UICONTROL ZoomScale]** a Adobe Analytics.

Ahora, supongamos que el usuario final carga la página web con los dos visores. En *viewer1*, aumentan la escala al 50%; a continuación, en *viewer2*, aumentan la escala al 25%. En *viewer1*, pan la imagen y, finalmente, seleccionan una tecla en el teclado.

La actividad del usuario final provoca que se realicen las dos llamadas de seguimiento siguientes a Adobe Analytics:

* La primera llamada se produce porque la regla **[!UICONTROL TrackPan]** se activa cuando el usuario aterriza en *viewer1*. Esa llamada envía el 50 % como valor de **[!UICONTROL ZoomScale]** Data Element porque el elemento de datos sabe que la regla se activa mediante *viewer1* y obtiene el valor de escala correspondiente;
* La segunda llamada se produce porque la regla **[!UICONTROL TrackKey]** se activa cuando el usuario pulsa una tecla en el teclado. Esa llamada envía el 25 % como valor del elemento de datos **[!UICONTROL ZoomScale]** porque el visor no activó la regla. Como tal, el elemento de datos devuelve el valor más actualizado.

El ejemplo configurado anteriormente también afecta a la duración del valor del elemento de datos. El valor del elemento de datos gestionado por el visualizador de Dynamic Media se almacena en el código de la biblioteca de Platform launch incluso después de que el propio visualizador se haya eliminado de la página web. Esta funcionalidad significa que si hay una regla activada por una extensión que no es de Dynamic Media Viewer y hace referencia a dicho elemento de datos, el elemento de datos devuelve el último valor conocido. Incluso si el visor ya no está presente en la página web.

En cualquier caso, los valores de los elementos de datos impulsados por los visualizadores de Dynamic Media no se almacenan en el almacenamiento local ni en el servidor; en su lugar, solo se mantienen en la biblioteca de Experience Platform Launch del lado del cliente. Los valores de dicho elemento de datos desaparecen cuando la página web se vuelve a cargar.

Por lo general, el editor de elementos de datos admite la [selección de duración del almacenamiento](https://experienceleague.adobe.com/docs/launch/using/ui/data-elements.html?lang=en#create-a-data-element). Sin embargo, los elementos de datos que utilizan la extensión Visualizadores de Dynamic Media solo admiten la opción de duración del almacenamiento **[!UICONTROL None]**. Es posible establecer cualquier otro valor en la interfaz de usuario, pero el comportamiento del elemento de datos no está definido en este caso. La extensión administra el valor del elemento de datos por su cuenta: el elemento de datos que mantiene el valor del argumento de evento del visor durante todo el ciclo de vida del visor.

### Acerca de las reglas en la extensión de visores de Dynamic Media {#about-rules-in-the-dynamic-media-viewers-extension}

En el editor de reglas, la extensión agrega nuevas opciones de configuración para el editor de eventos. Además, el editor proporciona una opción para hacer referencia manualmente a los parámetros de evento en el editor de acciones como una opción breve en lugar de utilizar elementos de datos preconfigurados.

#### Acerca del editor de eventos {#about-the-events-editor}

En el editor de eventos, la extensión Visualizadores de Dynamic Media agrega un **[!UICONTROL Tipo de evento]** denominado **[!UICONTROL Evento de visualizador]**.

Cuando se selecciona, el editor de eventos procesa la lista desplegable **[!UICONTROL Dynamic Media Viewer events]**, que enumera todos los eventos disponibles compatibles con los visores de Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Acerca del editor de acciones {#about-the-actions-editor}

La extensión Visualizadores de Dynamic Media permite utilizar parámetros de evento de visualizadores de Dynamic Media para asignarlos a variables de análisis en el editor Set Variables de la extensión de Adobe Analytics.

El método más sencillo para ello es completar el siguiente proceso de dos pasos:

* En primer lugar, defina uno o varios elementos de datos, donde cada elemento de datos representa un parámetro de un evento del visualizador de Dynamic Media.
* Finalmente, en el editor Set Variables de la extensión de Adobe Analytics, haga clic en el icono del selector de elementos de datos (tres discos apilados) para abrir el cuadro de diálogo Select Data Element y, a continuación, seleccione un Data Element de él.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Sin embargo, es posible utilizar un enfoque alternativo y evitar la creación de elementos de datos. Puede hacer referencia directamente a un argumento desde un evento de visualizador de Dynamic Media. Introduzca el nombre completo del argumento de evento en el campo de entrada **[!UICONTROL value]** de la asignación de variables de Analytics. Asegúrese de rodearlo con signos de porcentaje (%). Por ejemplo,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Existe una diferencia importante entre el uso de elementos de datos y la referencia de argumentos de eventos directos. Para el elemento de datos, no importa qué evento déclencheur la acción Set Variables. El evento que déclencheur la regla puede no estar relacionado con el visualizador dinámico. Por ejemplo, al hacer clic en la página web desde la extensión principal. Sin embargo, cuando se utiliza una referencia de argumento directo, es importante asegurarse de que el evento que déclencheur la regla corresponde al argumento de evento al que hace referencia.

Por ejemplo, la referencia `%event.detail.dm.LOAD.asset%` devuelve el nombre de recurso correcto si la regla se activa mediante el evento **[!UICONTROL LOAD]** de la extensión del visualizador de Dynamic Media. Sin embargo, devuelve un valor vacío para cualquier otro evento.

En la tabla siguiente se enumeran los eventos de visualizador de Dynamic Media y sus argumentos admitidos:

<table>
 <tbody>
  <tr>
   <td>Nombre del evento del visor</td>
   <td>Referencia de argumento</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configuración de todos los elementos de integración {#configuring-all-the-integration-pieces}

**ANTES DE COMENZAR**

Adobe recomienda revisar toda la documentación antes de esta sección para comprender la integración completa.

En esta sección se explican los pasos de configuración necesarios para integrar los visores de Dynamic Media con Adobe Analytics y Adobe Analytics para audio y vídeo. Aunque es posible utilizar la extensión de visores de Dynamic Media para otros fines en Experience Platform Launch, estos escenarios no se tratan en esta documentación.

Para configurar la integración, debe utilizar los siguientes productos de Adobe:

* Adobe Analytics: se utiliza para configurar variables de seguimiento e informes.
* Experience Platform Launch: se utiliza para definir una propiedad, una o varias reglas y uno o varios elementos de datos para habilitar el seguimiento del visor.

Además, si esta solución de integración se utiliza con Experience Manager Sites, también se debe realizar la siguiente configuración:

* [!DNL Adobe I/O] Consola : la integración se crea para el Experience Platform Launch.
* Nodo de creación del Experience Manager : configuración de IMS y configuración de nube del Experience Platform Launch.

Como parte de la configuración, asegúrese de tener acceso a una empresa de Adobe Experience Cloud que ya tenga Adobe Analytics y Experience Platform Launch habilitados.

## Configuración de Adobe Analytics para la integración {#configuring-adobe-analytics-for-the-integration}

Después de configurar Adobe Analytics, se configurará lo siguiente para la integración:

* Hay un grupo de informes listo y seleccionado.
* Las variables de Analytics están disponibles para recibir datos de seguimiento.
* Los informes están disponibles para ver los datos recopilados dentro de Adobe Analytics.

Consulte también [Guía de implementación de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Para configurar Adobe Analytics para la integración:**

1. Para empezar, acceda a Adobe Analytics desde la [página principal](https://experience.adobe.com/#/home) del Experience Cloud. En la barra de menús, haga clic en el icono Soluciones (una tabla de puntos de tres por tres) cerca de la esquina superior derecha de la página y, a continuación, haga clic en **[!UICONTROL Analytics]**.

   ![22-07-2019-18-08-47](assets/2019-07-22_18-08-47.png)

   Ahora, seleccione un grupo de informes.

### Selección de un grupo de informes {#selecting-a-report-suite}

1. Cerca de la esquina superior derecha de la página Adobe Analytics, a la derecha del campo **[!UICONTROL Buscar informes]**, seleccione el grupo de informes correcto en la lista desplegable. Si hay varios grupos de informes disponibles y no está seguro de cuál usar, póngase en contacto con el administrador de Adobe Analytics, que le ayudará a seleccionar qué grupo de informes utilizar.

   En la captura de pantalla siguiente, un usuario creó un grupo de informes denominado *DynamicMediaViewersExtensionDoc* y lo seleccionó en la lista desplegable. El nombre del grupo de informes es solo un nombre de ejemplo. El nombre del grupo de informes que seleccione en última instancia depende de usted.

   Si no hay ningún grupo de informes disponible, usted o el administrador de Adobe Analytics deben crear uno antes de continuar con la configuración.

   Consulte [Informes y grupos de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html#manage-report-suites) y [Crear un grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).

   En Adobe Analytics, los grupos de informes se administran en **[!UICONTROL Administración]** > **[!UICONTROL Grupos de informes]**.

   ![22-07-2019-18-09-49](assets/2019-07-22_18-09-49.png)

   Ahora, configure variables de Adobe Analytics.

### Configuración de variables de Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Designe una o más variables de Adobe Analytics que desee usar para rastrear el comportamiento de los visualizadores de Dynamic Media en la página web.

   Es posible utilizar cualquier tipo de variable admitida por Adobe Analytics. La decisión sobre el tipo de variable (como Tráfico personalizado [props], Conversión [eVar]) se debe a las necesidades específicas de la implementación de Analytics.

   Consulte [Información general sobre props y eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   A los efectos de esta documentación, solo se utilizará una variable de tráfico personalizado (props) porque estará disponible en un informe de Analytics en los pocos minutos siguientes a que se produzca una acción en una página web.

   Para habilitar una nueva variable de tráfico personalizado, en Adobe Analytics, en la barra de herramientas, haga clic en **[!UICONTROL Administración]** > **[!UICONTROL Grupos de informes]**.

1. En la página **[!UICONTROL Administrador del grupo de informes]** , seleccione el informe correcto y, en la barra de herramientas, haga clic en **[!UICONTROL Editar configuración]** > **[!UICONTROL Tráfico]** > **[!UICONTROL Variables de tráfico]**.
1. Seleccione una variable que no se utilice, asígnele un nombre descriptivo (**[!UICONTROL Recurso del visualizador (prop 30)]**) y cambie el cuadro combinado a &quot;Habilitado&quot; en la columna Activado.

   La siguiente captura de pantalla es un ejemplo de una variable de tráfico personalizado ( **[!UICONTROL prop30]**) para rastrear el nombre de un recurso que usa el visor:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. En la parte inferior de la lista de variables, haga clic en **[!UICONTROL Guardar]**.

### Configuración de un informe {#setting-up-a-report}

1. Por lo general, la configuración de un informe en Adobe Analytics depende de necesidades específicas del proyecto. De este modo, la configuración detallada del informe excede el ámbito de esta integración.

   Sin embargo, basta con saber que los informes Tráfico personalizado estarán disponibles automáticamente en Adobe Analytics después de configurar las variables Tráfico personalizado en [Configuración de variables de Adobe Analytics](#setting-up-adobe-analytics-variables).

   Por ejemplo, el informe de la variable **[!UICONTROL Recurso del visualizador (prop 30)]** está disponible en el menú Informes en **[!UICONTROL Tráfico personalizado]** > **[!UICONTROL Tráfico personalizado 21-30]** > **[!UICONTROL Recurso del visualizador (prop 30)]**.

   Al visitar este informe justo después de la creación de **[!UICONTROL Recursos del visualizador (prop 30)]**, no se muestra ningún dato; esto se espera en este punto de la integración.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configuración del Experience Platform Launch para la integración {#configuring-adobe-launch-for-the-integration}

Después de configurar el Experience Platform Launch, se configurará lo siguiente para la integración:

* La creación de una nueva propiedad para mantener todas las configuraciones juntas.
* Instalación y configuración de extensiones. El código del lado del cliente de todas las extensiones instaladas en la propiedad se compila en una biblioteca. Esta biblioteca la utiliza la página web más adelante.
* Configuración de elementos de datos y reglas. Esta configuración define qué datos capturar de los visualizadores de Dynamic Media, cuándo almacenar en déclencheur la lógica de seguimiento y dónde enviar los datos del visualizador en Adobe Analytics.
* Publicación de la biblioteca.

**Para configurar el Experience Platform Launch para la integración:**

1. Para empezar, acceda al Experience Platform Launch desde la [página principal](https://experience.adobe.com/#/home) del Experience Cloud. En la barra de menús, haga clic en el icono Soluciones (tres por tres tablas de puntos) cerca de la esquina superior derecha de la página y, a continuación, haga clic en **[!UICONTROL Iniciar]**.

   También puede [abrir el Experience Platform Launch directamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Creación de una propiedad en el Experience Platform Launch {#creating-a-property-in-adobe-launch}

Una propiedad en Experience Platform Launch es una configuración con nombre que mantiene juntos todos los ajustes. Se genera y publica una biblioteca de los ajustes de configuración en diferentes niveles de entorno (desarrollo, ensayo y producción).

Consulte también [Crear una propiedad de Launch](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html#configure-launch).

1. En el Experience Platform Launch, haga clic en **[!UICONTROL Nueva propiedad]**.
1. En el cuadro de diálogo **[!UICONTROL Crear propiedad]**, dentro del campo **[!UICONTROL Nombre]**, escriba un nombre descriptivo, como el título del sitio web. Por ejemplo, `DynamicMediaViewersProp.`
1. En el campo **[!UICONTROL Domains]**, introduzca el dominio del sitio web.
1. En la lista desplegable **[!UICONTROL Advanced Options]**, habilite **[!UICONTROL Configure for extension development (no se puede modificar posteriormente)]** en caso de que la extensión que desee utilizar (en este caso, *Dynamic Media Viewers*) aún no se haya publicado.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Haga clic en **[!UICONTROL Guardar]**.

   Haga clic en la propiedad recién creada y continúe con *Instalación y configuración de extensiones*.

### Instalación y configuración de extensiones {#installing-and-setup-of-extensions}

Todas las extensiones disponibles en el Experience Platform Launch se enumeran en **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**.

Para instalar una extensión, haga clic en **[!UICONTROL Install]**. Si es necesario, realice una configuración de extensión única y haga clic en **[!UICONTROL Guardar]**.

Cuando sea necesario, deben instalarse y configurarse las siguientes extensiones:

* (Obligatorio) Extensión *servicio de ID de Experience Cloud*.

No se necesita ninguna configuración adicional, acepte los valores propuestos. Cuando haya terminado, asegúrese de hacer clic en **[!UICONTROL Guardar]**.

Consulte [Extensión del servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html#extensions-ref).

* Extensión *Adobe Analytics* (obligatoria)

Para configurar esta extensión, necesita la ID del grupo de informes que se encuentra en Adobe Analytics, en **[!UICONTROL Administración]** > **[!UICONTROL Grupo de informes]**, en el encabezado de columna **[!UICONTROL ID del grupo de informes]**.

(Solo con fines de demostración, el ID del grupo de informes **[!UICONTROL DynamicMediaViewersExtensionDoc]** se utiliza en las siguientes capturas de pantalla. Este ID se creó y utilizó en [Selección de un grupo](#selecting-a-report-suite) de informes anteriormente).

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

En la página Instalar extensión, introduzca la ID del grupo de informes en el campo **[!UICONTROL Grupos de informes de desarrollo]**, en el campo **[!UICONTROL Grupos de informes de ensayo]** y en el campo **[!UICONTROL Grupos de informes de producción]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configure el siguiente elemento solo si planea utilizar el seguimiento de vídeo:*

En la página **[!UICONTROL Instalar extensión]**, expanda **[!UICONTROL General]** y, a continuación, especifique el Servidor de seguimiento. El Servidor de seguimiento sigue la plantilla `<trackingNamespace>.sc.omtrdc.net`, donde `<trackingNamespace>` es la información obtenida en el correo electrónico de aprovisionamiento.

Haga clic en **[!UICONTROL Guardar]**.

Consulte [Extensión de Adobe Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html#extensions-ref).

* (Opcional; solo es necesario si se necesita seguimiento de vídeo) *Extensión de Adobe Medium Analytics for Audio and Video*

Rellene el campo servidor de seguimiento . El servidor de seguimiento para la extensión *Adobe Medium Analytics para audio y vídeo* es diferente del servidor de seguimiento utilizado para Adobe Analytics. Sigue a la plantilla `<trackingNamespace>.hb.omtrdc.net`, donde `<trackingNamespace>` es la información del correo electrónico de aprovisionamiento.

Todos los demás campos son opcionales.

Consulte [Extensión de Adobe Medium Analytics para audio y vídeo](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#extensions-ref).

* Extensión *Dynamic Media Viewers* (obligatoria)

Seleccione **[!UICONTROL habilitar Adobe Analytics para vídeo]** para activar el seguimiento de Video Heartbeat.

Al momento de escribir este artículo, la extensión *Dynamic Media Viewers* solo está disponible si la propiedad de Experience Platform Launch se ha creado para el desarrollo.

Consulte [Creación de una propiedad en Experience Platform Launch](#creating-a-property-in-adobe-launch).

Una vez instaladas y configuradas las extensiones, como mínimo, las siguientes cinco extensiones (cuatro si no realiza el seguimiento de vídeo) se enumerarán en el área Extensiones > Instaladas .

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configuración de elementos de datos y reglas {#setting-up-data-elements-and-rules}

En Experience Platform Launch, cree los elementos de datos y las reglas que sean necesarios para rastrear los visores de Dynamic Media.

Consulte [Funcionamiento del seguimiento de datos y eventos en la integración](#how-data-and-event-tracking-works-in-the-integration) para obtener información general sobre el seguimiento con Experience Platform Launch.

Consulte [Configuración de muestra](#sample-configuration) para ver un ejemplo de configuración en el Experience Platform Launch que muestra cómo rastrear un nombre de recurso al cargar el visor.

Consulte [Configuración de la extensión de visores de Dynamic Media](#configuring-the-dynamic-media-viewers-extension) para obtener información detallada sobre las capacidades de la extensión.

### Publicación de una biblioteca {#publishing-a-library}

Para cambiar la configuración del Experience Platform Launch (incluidas la propiedad, las extensiones, las reglas y los elementos de datos configurados), debe *publicar* estos cambios. La publicación en el Experience Platform Launch se realiza desde la pestaña Publicación en la configuración de la propiedad.

platform launch puede tener varios entornos de desarrollo, un entorno de ensayo y un entorno de producción. De forma predeterminada, la Configuración de Platform launch Cloud en el Experience Manager apunta el nodo de autor del Experience Manager al entorno de ensayo del Platform launch. El nodo Publicación del Experience Manager apunta al entorno Producción de Platform launch. Esta disposición significa que con la configuración predeterminada del Experience Manager, es necesario publicar la biblioteca de Platforms launch en el entorno de ensayo. Al hacerlo, puede utilizarlo en el autor del Experience Manager. A continuación, puede publicarlo en el entorno Producción para que se pueda utilizar en la publicación en Experience Manager.

Consulte [Entornos](https://experienceleague.adobe.com/docs/launch/using/publish/environments/environments.html#environment-types) para obtener más información sobre los entornos de Experience Platform Launch.

La publicación de una biblioteca implica los dos pasos siguientes:

* Agregar y crear una nueva biblioteca incluyendo todos los cambios necesarios (nuevos y actualizaciones) en la biblioteca.
* Mover hacia arriba la biblioteca a través de los diferentes niveles de entorno (de Desarrollo a Ensayo y Producción).

#### Adición y creación de una nueva biblioteca {#adding-and-building-a-new-library}

1. La primera vez que abra la ficha Publicación en el Experience Platform Launch, la lista de la biblioteca estará vacía.

   En la columna izquierda, haga clic en **[!UICONTROL Agregar nueva biblioteca]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. En la página Crear nueva biblioteca , en el campo **[!UICONTROL Nombre]**, introduzca un nombre descriptivo para la nueva biblioteca. Por ejemplo,

   *DynamicMediaViewersLib*

   En la lista desplegable Entorno , elija el nivel Entorno . Inicialmente, solo el nivel de desarrollo está disponible para la selección. Cerca del lado inferior izquierdo de la página, haga clic en **[!UICONTROL Agregar todos los recursos modificados]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Guardar y crear para desarrollo]**.

   En unos minutos, la biblioteca se creará y estará lista para utilizarse.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >La próxima vez que cambie la configuración del Experience Platform Launch, vaya a la pestaña **[!UICONTROL Publicación]** en la configuración **[!UICONTROL Propiedad]** y, a continuación, haga clic en la biblioteca creada anteriormente.
   >
   >
   >En la pantalla de publicación de la biblioteca, haga clic en **[!UICONTROL Agregar todos los recursos modificados]** y, a continuación, haga clic en **[!UICONTROL Guardar y crear para desarrollo]**.

#### Mover hacia arriba una biblioteca a través de los niveles de entorno {#moving-a-library-up-through-environment-levels}

1. Una vez agregada una nueva biblioteca, se encuentra en el entorno de desarrollo. Para moverlo al nivel de entorno de ensayo (que corresponde a la columna Enviado ), en el menú desplegable de la biblioteca, haga clic en **[!UICONTROL Enviar para aprobación]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Enviar]**.

   Una vez que la biblioteca se mueva a la columna Enviado , en el menú desplegable de la biblioteca, haga clic en **[!UICONTROL Generar para ensayo]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Para mover la biblioteca del entorno de ensayo al entorno de producción (que es la columna Publicado ), siga un proceso similar.

   En primer lugar, en el menú desplegable, haga clic en **[!UICONTROL Aprobar para publicación]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. En el menú desplegable, haga clic en **[!UICONTROL Generar y publicar en producción]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulte [Publicación](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html) para obtener más información sobre el proceso de publicación en Experience Platform Launch.

## Configuración de Adobe Experience Manager para la integración {#configuring-adobe-experience-manager-for-the-integration}

Requisitos previos:

* Experience Manager ejecuta las instancias Autor y Publicar .
* El nodo de creación de Experience Manager está configurado en Dynamic Media - Modo de ejecución de Scene7 (dynamic_media_s7)
* Los componentes WCM de Dynamic Media están activados en Sitios de Experience Manager.

La configuración del Experience Manager consta de los dos pasos principales siguientes:

* Configuración de IMS Experience Manager.
* Configuración de Experience Platform Launch Cloud.

### Configuración de IMS de Experience Manager {#configuring-aem-ims}

1. En el autor del Experience Manager, haga clic en el icono Herramientas (martillo) y, a continuación, haga clic en **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. En la página Configuración de IMC de Adobe, cerca de la esquina superior izquierda, haga clic en **[!UICONTROL Crear]**.
1. En la página **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]**, en la lista desplegable **[!UICONTROL Solución de nube]**, haga clic en **[!UICONTROL Experience Platform Launch]**.
1. Active **[!UICONTROL Crear nuevo certificado]** y, a continuación, en el campo de texto, introduzca cualquier valor significativo para el certificado. Por ejemplo, *AdobeLaunchIMSCert*. Haga clic en **[!UICONTROL Crear certificado]**.

   Se muestra el siguiente mensaje de información:

   *Para recuperar un token de acceso válido, la nueva clave pública del certificado se agrega a la cuenta técnica en Adobe I/O.*

   Para cerrar el cuadro de diálogo Información, haga clic en **[!UICONTROL Aceptar]**.

   ![24-07-25_12-2019](assets/2019-07-25_12-09-24.png)

1. Para descargar un archivo de clave pública (*.crt) en el sistema local, haga clic en **[!UICONTROL Descargar clave pública]**.

   >[!NOTE]
   >
   >En este punto, ***deje abierta*** la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]**; ***no*** cierre la página y ***no*** haga clic en Siguiente. Volverá a esta página más adelante en los pasos.

   ![24-07-25_12-52-2019](assets/2019-07-25_12-52-24.png)

1. En una nueva pestaña del explorador, vaya a la [[!DNL Adobe I/O] Consola](https://console.adobe.io/integrations).

1. En la página **[!UICONTROL Integraciones de la consola de Adobe I/O]**, cerca de la esquina superior derecha, haga clic en **[!UICONTROL Nueva integración]**.
1. En el cuadro de diálogo **[!UICONTROL Crear una nueva integración]**, compruebe que está seleccionado la opción **[!UICONTROL Acceder a una API]** y, a continuación, haga clic en **[!UICONTROL Continuar]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. En la segunda página **[!UICONTROL Crear una nueva página de integración]**, active el botón de radio **[!UICONTROL API Experience Platform Launch]**. En la esquina inferior derecha de la página, haga clic en **[!UICONTROL Continuar]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. En la tercera **[!UICONTROL Crear una nueva página de integración]**, haga lo siguiente:

   * En el campo **[!UICONTROL Name]**, introduzca un nombre descriptivo. Por ejemplo, *DynamicMediaViewersIO*.

   * En el campo **[!UICONTROL Description]**, introduzca la descripción de la integración.

   * En el área **[!UICONTROL Public key certificates]** , cargue el archivo de clave pública (*.crt) que descargó anteriormente en estos pasos.

   * En el encabezado **[!UICONTROL Seleccione una función para la API del Experience Platform Launch]**, seleccione **[!UICONTROL Administración]**.

   * En el encabezado **[!UICONTROL Seleccione uno o varios perfiles de producto para la API del Experience Platform Launch]**, seleccione el perfil de producto denominado **[!UICONTROL Launch - &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Haga clic en **[!UICONTROL Crear integración]**.
1. En la página **[!UICONTROL Integration created]**, haga clic en **[!UICONTROL Continue to integration details]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Aparece una página de detalles de integraciones, **** similar a la siguiente:

   >[!NOTE]
   >
   >***Deje abierta esta página de detalles de integración***. En un momento necesitará información de las pestañas **[!UICONTROL Overview]** y **[!UICONTROL JWT]**.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Página de detalles de integración .

1. Vuelva a la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** que dejó abierta anteriormente. En la esquina superior derecha de la página, haga clic en **[!UICONTROL Siguiente]** para abrir la página **[!UICONTROL Cuenta]** en la ventana **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]**.

   (Si ha cerrado la página anteriormente, vuelva al autor del Experience Manager y haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS del Adobe]**. Haga clic en **[!UICONTROL Crear]**. En la lista desplegable **[!UICONTROL Cloud Solution]**, seleccione **[!UICONTROL Experience Platform Launch]**. En la lista desplegable **[!UICONTROL Certificado]**, seleccione el nombre del certificado creado anteriormente.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configuración de cuenta técnica de IMS de Adobe: página Certificado .

1. La página **[!UICONTROL Cuenta]** tiene cinco campos que debe rellenar utilizando la información de la página de detalles de integración del paso anterior.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configuración de cuenta técnica de IMS de Adobe: página de cuenta.

1. En la página **[!UICONTROL Cuenta]**, rellene los campos siguientes:

   * **[!UICONTROL Título]** : introduzca un título de cuenta descriptivo.
   * **[!UICONTROL Servidor de autorización]** : vuelva a la página de detalles de integración que abrió anteriormente. Haga clic en la pestaña **[!UICONTROL JWT]**. Copie el nombre del servidor (sin la ruta de acceso) como se indica a continuación.

(el nombre del servidor es solo un ejemplo)   Vuelva a la página **[!UICONTROL Cuenta]** y, a continuación, pegue el nombre en el campo correspondiente.
Por ejemplo, `https://ims-na1.adobelogin.com/`
(el nombre del servidor es solo un ejemplo)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Página de detalles de integración: pestaña JWT

1. **[!UICONTROL Clave de API]**: Vuelva a la página de detalles de la integración. Haga clic en la pestaña **[!UICONTROL Información general]** y, a continuación, a la derecha del campo **[!UICONTROL Clave de API (ID de cliente)]**, haga clic en **[!UICONTROL Copiar]**.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue la clave en el campo correspondiente ****.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Página de detalles de integración .

1. **[!UICONTROL Secreto del cliente]**: Regrese a la página de detalles de la integración. En la pestaña **[!UICONTROL Información general]**, haga clic en **[!UICONTROL Recuperar secreto de cliente]**. A la derecha del campo **[!UICONTROL Secreto de cliente]**, haga clic en **[!UICONTROL Copiar]**.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue la clave en el campo correspondiente.

1. **[!UICONTROL Carga útil]** : Vuelva a la página de detalles de la integración. Desde la pestaña **[!UICONTROL JWT]**, en el campo Carga útil JWT, copie todo el código de objeto JSON.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue el código en el campo correspondiente.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Página de detalles de integración: pestaña JWT

   La página Cuenta, con todos los campos rellenados, tiene un aspecto similar al siguiente:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Cerca de la esquina superior derecha de la página **[!UICONTROL Cuenta]**, haga clic en **[!UICONTROL Crear]**.

   Con el Experience Manager IMS configurado, ahora tiene un nuevo IMSAccount enumerado en **[!UICONTROL Configuraciones de IMS de Adobe]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configuración de Experience Platform Launch Cloud para la integración {#configuring-adobe-launch-cloud-for-the-integration}

1. En el autor del Experience Manager, cerca de la esquina superior izquierda, haga clic en el icono Herramientas (martillo) y, a continuación, haga clic en **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuraciones del Experience Platform Launch]**.

   ![26-12-10-38](assets/2019-07-26_12-10-38.png)

1. En la página **[!UICONTROL Configuraciones del Experience Platform Launch]**, en el panel izquierdo, seleccione un Sitio del Experience Manager para el cual desee aplicar la Configuración del Experience Platform Launch.

   Solo con fines de ejemplo, el **[!UICONTROL sitio de We.Retail]** está seleccionado en la captura de pantalla siguiente.

   ![26-12-2019-07-20-06](assets/2019-07-26_12-20-06.png)

1. Cerca de la esquina superior izquierda de la página, haga clic en **[!UICONTROL Crear]**.
1. En la página **[!UICONTROL General]** (1/3 páginas) de la ventana **[!UICONTROL Crear configuración de Experience Platform Launch]**, rellene los campos siguientes:

   * **[!UICONTROL Título]** : introduzca un título de configuración descriptivo. Por ejemplo, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL Configuración de IMS de Adobe asociado]** : seleccione la configuración de IMS que creó anteriormente en  [Configuración de IMS de Experience Manager](#configuring-aem-ims).

   * **[!UICONTROL Empresa]** : en la lista  **** desplegable Empresa, seleccione la empresa Experience Cloud. La lista se rellena automáticamente.

   * **[!UICONTROL Propiedad]** : en la lista desplegable Propiedad, seleccione la propiedad de Experience Platform Launch que creó anteriormente. La lista se rellena automáticamente.
   Después de completar todos los campos, la página **[!UICONTROL General]** tendrá un aspecto similar al siguiente:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Cerca de la esquina superior izquierda, haga clic en **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Ensayo]** (2/3 páginas) de la ventana **[!UICONTROL Crear configuración de Experience Platform Launch]**, rellene el siguiente campo:

   En el campo **[!UICONTROL URI de biblioteca]**, compruebe la ubicación de la versión de ensayo de la biblioteca de Experience Platform Launch. El Experience Manager rellena este campo automáticamente.

   Por ejemplo, solo para fines específicos, este paso utiliza bibliotecas de Experience Platform Launch que se implementan en CDN de Adobe.

   >[!NOTE]
   >
   >Compruebe que el URI de biblioteca rellenado automáticamente (identificador uniforme de recursos) no tenga un formato incorrecto. Si es necesario, corríjalo para que el URI represente un URI relativo al protocolo. Es decir, comienza con una barra doble hacia adelante.
   >
   >
   >Por ejemplo: `//assets.adobetm.com/launch-xxxx`.

   Es probable que la página **[!UICONTROL Ensayo]** aparezca similar a la siguiente. Las opciones **[!UICONTROL Archivar]** y **[!UICONTROL Cargar biblioteca asincrónicamente]** están ***no*** configuradas:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Cerca de la esquina superior derecha, haga clic en **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Producción]** (3/3 páginas) de la ventana **[!UICONTROL Crear configuración de Experience Platform Launch]**, si es necesario, corrija el URI de producción rellenado automáticamente de forma similar a como se hizo en la página anterior **[!UICONTROL Ensayo]**.
1. Cerca de la esquina superior derecha, haga clic en **[!UICONTROL Crear]**.

   La nueva configuración de nube de Experience Platform Launch ahora se crea y aparece junto al sitio web, de forma similar al siguiente ejemplo:

1. Seleccione la nueva configuración de nube de Experience Platform Launch (aparece una marca de verificación a la izquierda del título de configuración cuando está seleccionada). En la barra de herramientas, haga clic en **[!UICONTROL Publicar]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Actualmente, el autor del Experience Manager no admite la integración de visores de Dynamic Media con Experience Platform Launch.

Sin embargo, se admite en el nodo de publicación de Experience Manager. Utilizando la configuración predeterminada de Configuración de Platform launch Cloud, el nodo de publicación de Experience Manager utiliza el entorno de producción de Experience Platform Launch. Como tal, es necesario insertar las actualizaciones de la biblioteca de Experience Platform Launch desde Development hasta el entorno de producción cada vez que se realiza la prueba.

Es posible solucionar esta limitación. Especifique la URL de desarrollo o de ensayo de la biblioteca de Platform launch en la configuración de Platform launch Cloud para el nodo de publicación de Experience Manager anterior. Al hacerlo, el nodo de publicación del Experience Manager utiliza la versión de desarrollo o ensayo de la biblioteca de Platform launch.

Consulte [Integrar el Experience Manager con el Experience Platform Launch Via [!DNL Adobe I/O]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) para obtener más información sobre la configuración de la nube de Experience Platform Launch.
