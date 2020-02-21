---
title: Adición de funciones de Dynamic Media Classic a la página
description: Aprenda a añadir funciones y componentes de Dynamic Media Classic a su página de AEM.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: e9f5d8f63bc342723f2002f677c1673b4af6f891

---


# Adición de funciones de Dynamic Media Classic a la página {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Puede ver los recursos de AEM publicados en Dynamic Media Classic en varios visores:

* Zoom
* Flotante
* Vídeo
* Plantilla de imagen
* Imagen

Puede publicar recursos digitales directamente desde AEM en Dynamic Media Classic y puede publicar recursos digitales de Dynamic Media Classic en AEM.

Este documento describe cómo publicar recursos digitales de AEM en Dynamic Media Classic y viceversa. Los visores también se describen en detalle. Para obtener información sobre la configuración de AEM para Dynamic Media Classic, consulte [Integración de Dynamic Media Classic con AEM](/help/sites-administering/scene7.md).

Consulte también [Adición de mapas de imagen](image-maps.md).

For more information on using video components with AEM, see [Video](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## Publicación manual en Dynamic Media Classic desde recursos {#manually-publishing-to-scene-from-assets}

Puede publicar recursos digitales en Dynamic Media Classic de la siguiente manera:

* [En la interfaz de usuario clásica desde la consola Recursos](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [En la interfaz de usuario clásica desde un recurso](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [En la interfaz de usuario clásica desde fuera de la carpeta CQ Target](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM publica en Dynamic Media Classic de forma asíncrona. After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Componentes de Dynamic Media Classic {#scene-components}

Los siguientes componentes de Dynamic Media Classic están disponibles en AEM:

* Zoom
* Flotante (zoom)
* Plantilla de imagen
* Imagen
* Vídeo

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. Los recursos que aún no se han publicado en Dynamic Media Classic se publican en Dynamic Media Classic si se encuentran en una carpeta sincronizada o en una página o con una configuración de nube de Dynamic Media Classic.

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Aviso de final de asistencia para el visor Flash {#flash-viewers-end-of-life-notice}

A partir del 31 de enero de 2017, Adobe Dynamic Media Classic dejó de ser compatible con la plataforma de visor Flash.

Para obtener más información sobre este cambio importante, consulte las [Preguntas frecuentes sobre el final de asistencia para el visor Flash](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

Agregar un componente de Dynamic Media Classic (Scene7) a una página es lo mismo que agregar un componente a cualquier página. Los componentes de Dynamic Media Classic se describen en detalle en las siguientes secciones.

**Adición de un componente de Dynamic Media Classic (Scene7) a una página**

1. En AEM, abra la página en la que desea añadir el componente de Dynamic Media Classic (Scene7).

1. Si no hay componentes de Dynamic Media Classic disponibles, haga clic en el modo **[!UICONTROL Diseño]** , toque cualquier componente con un borde azul, toque el icono **[!UICONTROL Principal]** y, a continuación, el icono **[!UICONTROL Configuración]** . En **[!UICONTROL Parsys (Design)]**, seleccione todos los componentes de Dynamic Media Classic para que estén disponibles y haga clic en **[!UICONTROL Aceptar]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Haga clic en **[!UICONTROL Editar]** para volver al modo **[!UICONTROL Editar]** .

1. Arrastre un componente del grupo de Dynamic Media Classic en la barra de tareas a la página en la ubicación deseada.

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. Edite el componente según sea necesario y haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.
1. Arrastre la imagen o el vídeo desde el navegador de contenido al componente de Dynamic Media Classic que ha agregado a la página.

   >[!NOTE]
   >
   >Solo en la IU táctil, debe arrastrar y soltar la imagen o el vídeo en el componente de Dynamic Media Classic que haya colocado en la página. No se admite la selección y edición del componente de Dynamic Media Classic y, a continuación, la selección del recurso.

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

El diseño interactivo para sus recursos implica que estos se ajustan según el lugar en que se muestren. Con un diseño interactivo, los mismos recursos se pueden mostrar de forma eficaz en varios dispositivos.

Consulte también Diseño [adaptable para páginas](/help/sites-developing/responsive.md)Web.

**Para agregar una experiencia de visualización interactiva a un sitio interactivo**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Si los componentes de Dynamic Media Classic no están disponibles, asegúrese de [habilitarlos mediante el modo](/help/sites-authoring/default-components-designmode.md)Diseño.

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. Seleccione el componente y toque el icono de configuración.
1. En la ficha Configuración **** de Dynamic Media Classic, ajuste los puntos de interrupción.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Confirme que los visores cambian de tamaño de manera interactiva y que las interacciones están optimizadas para dispositivos de escritorio, tabletas y móviles.

### Configuración común a todos los componentes de Dynamic Media Classic {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL Referencia]** de archivo: busque un archivo al que desee hacer referencia. La referencia de archivo muestra la URL del recurso y no necesariamente la URL completa de Dynamic Media Classic, incluidos los comandos y parámetros de URL. En este campo no se pueden agregar comandos ni parámetros de URL de Dynamic Media Classic. Deben añadirse mediante la funcionalidad correspondiente del componente.
* **[!UICONTROL Anchura]** : permite definir la anchura.
* **[!UICONTROL Altura]** : permite definir la altura.

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

El recurso dispone de herramientas de zoom en la parte inferior. Toque **[!UICONTROL +]** para agrandar. Puntee **[!UICONTROL para reducir]** . Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. Puntee en las flechas diagonales para que se visualicen a pantalla completa. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flotante {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. Sin embargo, tenga en cuenta que existe una limitación en la configuración interactiva del componente. When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### Imagen {#image}

El componente **[!UICONTROL Imagen]** de Dynamic Media Classic le permite añadir la funcionalidad de Dynamic Media Classic a sus imágenes, como los modificadores de Dynamic Media Classic, los ajustes preestablecidos de imagen o visor y el enfoque. El componente **[!UICONTROL Imagen]** de Dynamic Media Classic es similar a otros componentes de imagen en AEM con una funcionalidad especial de Dynamic Media Classic. En este ejemplo, la imagen tiene el modificador de URL de Dynamic Media Classic, `&op_invert=1` aplicado.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Título, Texto]** alternativo: en la ficha **[!UICONTROL Avanzado]** , agregue un título a la imagen y texto alternativo para los usuarios que tienen gráficos desactivados.

**[!UICONTROL URL, Abrir en]** : puede definir un recurso desde para abrir un vínculo. Defina la **[!UICONTROL dirección URL]** y, en **[!UICONTROL Abrir en]**, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor existente en el menú desplegable. Si el ajuste preestablecido de visor que busca no está visible, es posible que tenga que hacerlo visible. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). No es posible seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen, y viceversa.

**[!UICONTROL Configuración]** de Dynamic Media Classic: seleccione la configuración de Dynamic Media Classic que desee utilizar para recuperar los ajustes preestablecidos de imagen activos de SPS.

**[!UICONTROL Ajuste preestablecido]** de imagen: seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que busca no está visible, es posible que tenga que hacerlo visible. Consulte [Administración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md). No es posible seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen, y viceversa.

**[!UICONTROL Formato]** de salida: seleccione el formato de salida de la imagen, por ejemplo jpeg. En función del formato de salida que seleccione, puede tener opciones de configuración adicionales. Consulte [Prácticas recomendadas para ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Enfoque]** : seleccione cómo desea enfocar la imagen. El enfoque se explica en detalle en [Prácticas recomendadas para ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md#image-preset-options) y en [Prácticas recomendadas para el enfoque](/help/assets/assets/s7_sharpening_images.pdf).

**[!UICONTROL Modificadores]** de URL: puede cambiar los efectos de imagen proporcionando comandos de imagen adicionales de Dynamic Media Classic. Estos se describen en [Ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md) y [Referencia del comando](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

**[!UICONTROL Puntos de interrupción]** : si el sitio web responde, desea ajustar los puntos de interrupción. Los puntos de interrupción deben separarse con comas ( , ).

### Plantilla de imagen {#image-template}

[Las plantillas](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) de imagen de Dynamic Media Classic son contenido de Photoshop en capas que se importó a Dynamic Media Classic, donde el contenido y las propiedades se parametrizaron para la variabilidad. El componente **[!UICONTROL Plantilla de imagen]** le permite importar imágenes y cambiar el texto de forma dinámica en AEM. Además, puede configurar el componente **[!UICONTROL Plantilla de imágenes]** para utilizar valores de ClientContext, de modo que cada usuario experimenta la imagen de una forma personalizada.

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Referencia de archivo, Anchura, Altura]** : consulte los ajustes comunes a todos los componentes de ScDynamic Media Classicene7.

>[!NOTE]
>
>Los comandos y parámetros de URL de Dynamic Media Classic no se pueden agregar directamente a la URL de referencia de archivo. Solo se pueden definir en la interfaz de usuario del componente en el panel **[!UICONTROL Parámetro]**.

**[!UICONTROL Título, Texto]** alternativo: en la ficha Plantilla de imagen de Dynamic Media Classic, agregue un título a la imagen y texto alternativo para los usuarios que tienen gráficos desactivados.

**[!UICONTROL URL, Abrir en]** : puede definir un recurso desde para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Panel]** de parámetros: al importar una imagen, los parámetros se rellenan previamente con información de la imagen. Si no existe contenido que se pueda cambiar de forma dinámica, esta ventana está vacía.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Cambio del texto de forma dinámica {#changing-text-dynamically}

Para cambiar el texto de forma dinámica, escriba el nuevo texto en los campos y haga clic en **[!UICONTROL Aceptar]**. En este ejemplo, el **[!UICONTROL Precio]** es ahora $50 y el envío cuesta 99 centavos.

![chlimage_1-234](assets/chlimage_1-234.png)

El texto de la imagen cambia. You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Cambio del texto para reflejar un valor de ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK]**. En este ejemplo, el nombre cambia en función de la vinculación de valor de Nombre con el nombre con formato que consta en el perfil.

![chlimage_1-236](assets/chlimage_1-236.png)

El texto refleja el nombre del usuario de la sesión actual. Para restablecer el texto al valor original, haga clic en **[!UICONTROL Restablecer]** junto al campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Convertir la plantilla de imagen de Dynamic Media Classic en un vínculo {#making-the-scene-image-template-a-link}

1. En la página con el componente Plantilla **[!UICONTROL de]** imagen de Dynamic Media Classic, toque **[!UICONTROL Editar]**.
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. In the **[!UICONTROL Open in]** field, select whether you want the target to open (a new window or same window).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Toque **[!UICONTROL Aceptar]**.

### Componente de vídeo {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. Este componente es un reproductor de vídeo HTML5; se trata de un visor único que se puede utilizar en múltiples canales.

Se puede usar para conjuntos de vídeos adaptables, un solo vídeo MP4 o un solo vídeo F4V.

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. Además, consulte [el componente Vídeo de Dynamic Media Classic en comparación con el componente](s7-video.md)Vídeo de base.

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitaciones conocidas del componente de vídeo {#known-limitations-for-the-video-component}

Adobe DAM y WCM muestran si se ha cargado un vídeo maestro. No muestran estos recursos de proxy:

* Representaciones codificadas de Dynamic Media Classic
* Conjuntos de vídeos adaptables de Dynamic Media Classic

Al utilizar un conjunto de vídeos adaptables con el componente de vídeo de Dynamic Media Classic, debe cambiar el tamaño del componente para adaptarlo a las dimensiones del vídeo.

## Navegador de contenido de Dynamic Media Classic {#scene-content-browser}

El navegador de contenido de Dynamic Media Classic le permite ver contenido de Dynamic Media Classic directamente en AEM. To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. La funcionalidad es idéntica en ambas interfaces de usuario.

Si tiene varias configuraciones, AEM muestra de forma predeterminada la [configuración predeterminada](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puede seleccionar diferentes configuraciones directamente en el navegador de contenido de Dynamic Media Classic en el menú desplegable.

>[!NOTE]
>
>* Los recursos ubicados en la carpeta ad-hoc no aparecerán en el navegador de contenido de Dynamic Media Classic.
>* Cuando se habilita [Vista previa](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)segura, los recursos publicados y no publicados en Dynamic Media Classic aparecen en el navegador de contenido de Dynamic Media Classic.
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* Para vídeo, el navegador de contenido de Dynamic Media Classic admite:
   >   * Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
   >   * Vídeo MP4 sencillo
   >   * Vídeo F4V sencillo


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

Puede acceder al navegador de contenido desde la IU táctil o clásica. Actualmente, la función táctil optimizada tiene las siguientes limitaciones:

* Los recursos FXG y Flash de Dynamic Media Classic no son compatibles.

Para examinar los recursos de Dynamic Media Classic, seleccione **[!UICONTROL Dynamic Media Classic]** en el tercer menú desplegable. Dynamic Media Classic no aparece en la lista si no ha configurado la integración de Dynamic Media Classic/AEM.

>[!NOTE]
>
>* El navegador de contenido de Dynamic Media Classic carga unos 100 recursos y los ordena por nombre.
>* Si dispone de un servidor de vista previa seguro, el navegador utilizará ese servidor de vista previa para procesar miniaturas y recursos.
>



![chlimage_1-240](assets/chlimage_1-240.png)

Además, puede examinar la información de resolución, el tamaño, los días transcurridos desde la modificación y el nombre del archivo pasando el ratón por el recurso en el navegador.

![chlimage_1-241](assets/chlimage_1-241.png)

* En el caso de los conjuntos de vídeos adaptables y las plantillas, no se genera información de tamaño para las miniaturas.
* Para los conjuntos de vídeos adaptables, no se genera ninguna resolución para las miniaturas.

### Búsqueda de recursos de Dynamic Media Classic con el navegador de contenido {#searching-for-scene-assets-with-the-content-browser}

La búsqueda de recursos de Dynamic Media Classic es similar a la búsqueda de recursos de AEM, pero al realizar una búsqueda, se ve una vista remota de los recursos en el sistema de Dynamic Media Classic, en lugar de importarlos directamente en AEM.

Puede utilizar la interfaz de usuario clásica o la optimizada para el uso táctil para ver y buscar recursos. Según la interfaz, la búsqueda es ligeramente diferente.

Al buscar en cualquier interfaz de usuario, puede filtrar según los criterios siguientes (aquí se muestra la IU optimizada para el uso táctil):

**[!UICONTROL Escriba palabras clave]** : puede buscar recursos por nombre. Al buscar, las palabras clave que introduce es por lo que comienza el nombre de archivo. Por ejemplo, al escribir la palabra “natación”, el sistema buscaría cualquier nombre de archivo de recurso que comience por esas letras en ese orden. Asegúrese de tocar Intro después de escribir el término para buscar el recurso.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Carpeta/ruta]** : el nombre de la carpeta que aparece se basa en la configuración seleccionada. Puede desplazarse a niveles inferiores tocando el icono de la carpeta, seleccionando una subcarpeta y, a continuación, tocando la marca de verificación para seleccionarla.

Si introduce una palabra clave y selecciona una carpeta, AEM realiza la búsqueda en esa carpeta y todas las subcarpetas. Sin embargo, si no introduce ninguna palabra clave cuando realice la búsqueda, al seleccionar la carpeta solo se mostrarán los recursos de esa carpeta y no se incluirá ninguna de las subcarpetas.

De forma predeterminada, AEM realiza la búsqueda en la carpeta seleccionada y todas las subcarpetas.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo de recurso]** : seleccione **[!UICONTROL Dynamic Media Classic]** para examinar el contenido de Dynamic Media Classic. Esta opción solo está disponible si se ha configurado Dynamic Media Classic.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuración]** : si tiene más de una configuración de Dynamic Media Classic definida en Servicios [!UICONTROL de]nube, puede seleccionarla aquí. Como resultado, la carpeta cambiará según la configuración que haya elegido.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo]** de recurso: en el navegador de Dynamic Media Classic, puede filtrar los resultados para incluir cualquiera de los siguientes elementos: imágenes, plantillas, vídeos y conjuntos de vídeos adaptables. Si no selecciona ningún tipo de recurso, AEM busca de manera predeterminada todos los tipos de recursos.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* En la interfaz de usuario clásica; también puede buscar **Flash** y **FXG**. Actualmente, no se pueden filtrar estos valores en la interfaz de usuario optimizada para dispositivos táctiles.
   >
   >
* Al buscar vídeos, se busca una sola representación. Los resultados devuelven la representación original (solo &amp;ast;.mp4) y la representación codificada.
>* Al buscar un conjunto de vídeos adaptables, busca en la carpeta y en todas las subcarpetas, pero solo si ha añadido una palabra clave a la búsqueda. Si no ha añadido ninguna palabra clave, AEM no busca en las subcarpetas.
>



**[!UICONTROL Estado]** de publicación: puede filtrar los recursos en función del estado de publicación: **[!UICONTROL No publicado]** o **[!UICONTROL publicado]**. If you do not select any **[!UICONTROL Publish Status]**, AEM by default searches all publish statuses.

![chlimage_1-247](assets/chlimage_1-247.png)

