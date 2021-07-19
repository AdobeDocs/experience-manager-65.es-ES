---
title: Agregar características de Dynamic Media Classic (Scene7) a su página
description: Adobe Dynamic Media Classic (Scene7) es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 18%

---

# Agregar características de Dynamic Media Classic (Scene7) a su página{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html)  es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Puede ver los recursos de Experience Manager publicados en Dynamic Media Classic (Scene7) en varios visores:

* Zoom
* Flotante
* Vídeo
* Plantilla de imagen
* Imagen

Puede publicar recursos digitales directamente de Experience Manager a Dynamic Media Classic (Scene7) y recursos digitales de Dynamic Media Classic (Scene7) a Experience Manager.

En este documento se describe cómo publicar recursos digitales de Experience Manager a Dynamic Media Classic (Scene7) y, a la inversa, cómo hacerlo. Los visores también se describen en detalle. Para obtener información sobre la configuración de Experience Manager para Dynamic Media Classic (Scene7), consulte [Integración de Dynamic Media Classic (Scene7) con Experience Manager](/help/sites-administering/scene7.md).

Consulte también [Agregar mapas de imagen](/help/assets/image-maps.md).

Para obtener más información sobre el uso de componentes de vídeo con Experience Manager, consulte lo siguiente:

* [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Si los recursos de Dynamic Media Classic (Scene7) no se muestran correctamente, asegúrese de que Dynamic Media esté [deshabilitado](/help/assets/config-dynamic.md#disabling-dynamic-media) y, a continuación, actualice la página.

## Publicación manual en Dynamic Media Classic (Scene7) desde Assets {#manually-publishing-to-scene-from-assets}

Puede publicar recursos digitales en Dynamic Media Classic (Scene7) desde la consola Recursos en la IU clásica o directamente desde el recurso.

>[!NOTE]
>
>Experience Manager publica en Dynamic Media Classic (Scene7) de forma asíncrona. Después de seleccionar **[!UICONTROL Publicar]**, puede que el recurso tarde varios segundos en publicarse en Dynamic Media Classic (Scene7).


### Publicación desde la consola Recursos {#publishing-from-the-assets-console}

Puede publicar en Dynamic Media Classic (Scene7) desde la consola Recursos si los recursos están en una carpeta de destino de Dynamic Media Classic (Scene7).

1. En la IU clásica de Experience Manager, seleccione **[!UICONTROL Recursos digitales]** para acceder al administrador de recursos digitales.

1. Seleccione el recurso (o recursos) o la carpeta de la carpeta de destino que desea publicar en Dynamic Media Classic (Scene7), haga clic con el botón derecho y seleccione **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]**. También puede seleccionar **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]** en el menú **[!UICONTROL Herramientas]**.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Vaya a Dynamic Media Classic (Scene7) y confirme que los recursos están disponibles.

   >[!NOTE]
   >
   >Si los recursos no están en una carpeta sincronizada de Dynamic Media Classic (Scene7), **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]** en ambos menús estará visible pero deshabilitada.

### Publicar desde un recurso {#publishing-from-an-asset}

Puede publicar manualmente un recurso siempre que este se encuentre dentro de la carpeta sincronizada de Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si el recurso no está en la carpeta sincronizada de Dynamic Media Classic (Scene7), no aparece el vínculo **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]**.

Para publicar en Dynamic Media Classic (Scene7) directamente desde un recurso digital:

1. En el Experience Manager, seleccione **[!UICONTROL Recursos digitales]** para acceder al administrador de recursos digitales.

1. Haga doble clic en dicha opción para abrir un recurso.

1. En el panel de detalles del recurso, seleccione **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. El vínculo cambia a **[!UICONTROL Publicando...]** y, a continuación, a **[!UICONTROL Publicado]**. Vaya a Dynamic Media Classic (Scene7) y confirme que el recurso está disponible.

   >[!NOTE]
   >
   >Si el recurso no se publica correctamente en Dynamic Media Classic (Scene7), el vínculo cambia a **[!UICONTROL Error al publicar]**. Si el recurso ya se ha publicado en Dynamic Media Classic (Scene7), el vínculo reza **[!UICONTROL Volver a publicar en Dynamic Media Classic (Scene7)]**. La republicación permite cambiar recursos en el Experience Manager y volver a publicarlos.

### Publicar recursos desde fuera de la carpeta de destino de CQ {#publishing-assets-from-outside-the-cq-target-folder}

Adobe recomienda publicar recursos en Dynamic Media Classic (Scene7) solo desde recursos de la carpeta de destino de Dynamic Media Classic (Scene7). Sin embargo, si debe cargar recursos de una carpeta que esté fuera de la carpeta de destino, puede hacerlo cargándolos en una carpeta bajo demanda en Dynamic Media Classic (Scene7). En primer lugar, configure la configuración de Cloud para la página en la que desea que aparezca el recurso. A continuación, agregue un componente de Dynamic Media Classic (Scene7) a la página y arrastre y suelte un recurso en el componente. Una vez que las propiedades de página están establecidas para esa página, aparece un vínculo **[!UICONTROL Publicar en Dynamic Media Classic (Scene7)]** que, cuando se seleccionan los déclencheur que se cargan en Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Los recursos que se encuentran en la carpeta bajo demanda no aparecen en el navegador de contenido de Dynamic Media Classic (Scene7).

**Para publicar recursos desde fuera de la carpeta de destino de CQ:**

1. En el Experience Manager de la IU clásica, seleccione **[!UICONTROL Sitios web]** y vaya a la página web a la que desee agregar un recurso digital que aún no se haya publicado en Dynamic Media Classic (Scene7). (Se aplican las reglas de herencia de página habituales).

1. En la barra de tareas, seleccione el icono **[!UICONTROL Página]** y seleccione **[!UICONTROL Propiedades de página]**.

1. Seleccione **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Add services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]**, seleccione la configuración que desee y seleccione **[!UICONTROL Aceptar]**.

   ![imagen_1-49](assets/chlimage_1-49.png)

1. En la página web, agregue un componente de Dynamic Media Classic (Scene7) a la ubicación deseada en la página.
1. En el buscador de contenido, arrastre un recurso digital hasta el componente. Aparece un vínculo a **[!UICONTROL Comprobar estado de publicación de Dynamic Media Classic (Scene7)]**.

   >[!NOTE]
   >
   >Si el recurso digital está en la carpeta de destino de CQ, no aparecerá ningún vínculo a **[!UICONTROL Comprobar estado de publicación de Dynamic Media Classic (Scene7)]**. Los recursos se colocan en el componente.

   ![imagen_1-50](assets/chlimage_1-50.png)

1. Seleccione **[!UICONTROL Comprobar estado de publicación de Dynamic Media Classic (Scene7)]**. Si los recursos no se publican, Experience Manager los publica en Dynamic Media Classic (Scene7). Una vez cargado, el recurso se encuentra en la carpeta bajo demanda. De forma predeterminada, la carpeta bajo demanda se encuentra en **[!UICONTROL name_of_the_company/CQ5_adhoc]**. Puede [configurar la carpeta bajo demanda, si es necesario](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Si el recurso no está en una carpeta sincronizada de Dynamic Media Classic (Scene7) y no hay ninguna configuración de nube de Dynamic Media Classic (Scene7) asociada a la página actual, la carga falla.

## Componentes de Dynamic Media Classic (Scene7) {#scene-components}

Los siguientes componentes de Dynamic Media Classic (Scene7) están disponibles en Experience Manager:

* Zoom
* Flotante (zoom)
* Plantilla de imagen
* Imagen
* Vídeo

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben seleccionarse en el modo Diseño antes de utilizarlos.

Una vez que estén disponibles en el modo Diseño, puede añadir los componentes a la página como cualquier otro componente de Experience Manager. Los recursos que aún no se han publicado en Dynamic Media Classic (Scene7) se publican en Dynamic Media Classic (Scene7) si se encuentran en una carpeta sincronizada o en una página o con una configuración de nube de Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si está creando y desarrollando visores personalizados de S7 y utilizando el Buscador de contenido, debe añadir explícitamente el parámetro `allowfullscreen`.

### Aviso de fin de vida útil para el visualizador Flash {#flash-viewers-end-of-life-notice}

A partir del 31 de enero de 2017, Adobe Dynamic Media Classic (Scene7) dejó de ofrecer asistencia para la plataforma del visor de Flash.

### Añadir un componente de Dynamic Media Classic (Scene7) a una página {#adding-a-scene-component-to-a-page}

Añadir un componente de Dynamic Media Classic (Scene7) a una página es lo mismo que añadir un componente a cualquier página. Los componentes de Dynamic Media Classic (Scene7) se describen detalladamente en las secciones siguientes.

Para añadir un componente/visor de Dynamic Media Classic (Scene7) a una página de la IU clásica:

1. En el Experience Manager, abra la página a la que desea añadir el componente Dynamic Media Classic (Scene7).

1. Si no hay componentes de Dynamic Media Classic (Scene7) disponibles, seleccione la regla en la barra de tareas para entrar al modo **Diseño**, seleccione **[!UICONTROL Editar]** parsys y seleccione todos los componentes de **[!UICONTROL Dynamic Media Classic (Scene7)]** para que estén disponibles.

1. Vuelva al modo **Editar** seleccionando el lápiz en la barra de tareas.

1. Arrastre un componente desde el grupo **[!UICONTROL Dynamic Media Classic (Scene7)]** de la barra de tareas hasta la página en la ubicación deseada.

1. Seleccione ***[!UICONTROL Editar]** para poder abrir el componente.

1. Edite el componente según sea necesario y seleccione **[!UICONTROL OK]** para guardar los cambios.

### Añadir experiencias de visualización interactivas a un sitio web interactivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

El diseño interactivo de los recursos significa que estos se adaptan según el lugar en que se muestren. Con un diseño interactivo, los mismos recursos se pueden mostrar de forma eficaz en varios dispositivos.

Para añadir una experiencia de visualización interactiva a un sitio interactivo en la interfaz de usuario clásica:

1. Inicie sesión en Experience Manager y asegúrese de que tiene [Cloud Services configurados de Adobe de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#configuring-scene-integration) y de que los componentes de Dynamic Media Classic (Scene7) están disponibles.

   >[!NOTE]
   >
   >Si los componentes WCM de Dynamic Media Classic (Scene7) no están disponibles, asegúrese de activarlos mediante el modo Diseño .

1. En un sitio web con los componentes de Dynamic Media Classic (Scene7) activados, arrastre un visor de **[!UICONTROL Image]** a la página.
1. Edite el componente y ajuste los puntos de interrupción en la pestaña **[!UICONTROL Configuración de Dynamic Media Classic (Scene7)]**.

   ![imagen_1-51](assets/chlimage_1-51.png)

1. Confirme que los visores cambian de tamaño de manera interactiva y que las interacciones están optimizadas para dispositivos de escritorio, tabletas y móviles.

### Configuración común a todos los componentes de Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Aunque las opciones de configuración varían, las siguientes son comunes a todos los componentes de Dynamic Media Classic (Scene7):

* **Referencia del archivo**: navegue a un archivo al que quiera hacer referencia. La referencia de archivo muestra la URL del recurso y no necesariamente la URL completa de Dynamic Media Classic (Scene7), incluidos los comandos y parámetros de URL. No puede añadir comandos ni parámetros de URL de Dynamic Media Classic (Scene7) en este campo. En su lugar, se deben añadir a través de la funcionalidad correspondiente del componente.
* **Anchura**: le permite definir la anchura.
* **Altura**: le permite definir la altura.

Para establecer estas opciones de configuración, abra (haga doble clic en) un componente de Dynamic Media Classic (Scene7), por ejemplo, al abrir un componente **Zoom**:

![imagen_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

El componente Zoom HTML5 muestra una imagen más grande al pulsar el botón +.

El recurso dispone de herramientas de zoom en la parte inferior. Seleccione **[!UICONTROL +]** para ampliar. Seleccione **[!UICONTROL -]** para reducir. Al seleccionar **[!UICONTROL x]** o la flecha de zoom de restablecimiento, la imagen vuelve al tamaño original que se importó como. Seleccione las flechas diagonales para poder hacerlo a pantalla completa. Seleccione **[!UICONTROL Editar]** para que pueda configurar el componente. Con este componente, puede configurar [opciones comunes a todos los componentes de Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### Flotante {#flyout}

En el componente Flotante HTML5, el recurso se muestra como una pantalla dividida: a la izquierda aparece con el tamaño especificado y a la derecha aparece la porción modificada con el zoom. Seleccione **[!UICONTROL Editar]** para que pueda configurar el componente. Con este componente, puede configurar [opciones comunes a todos los componentes de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Si el componente Flotante utiliza un tamaño personalizado, se utiliza dicho tamaño y se desactiva la configuración interactiva del componente.
>
>Si el componente Flotante utiliza el tamaño predeterminado, tal como se establece en la vista Diseño, se utilizará el tamaño predeterminado. El componente se expande para dar cabida al tamaño del diseño de página con la configuración interactiva del componente habilitada. Sin embargo, tenga en cuenta que hay una limitación en la configuración interactiva del componente. Cuando se utiliza el componente Flotante con configuración interactiva, no se debe usar con la ampliación de página completa. De lo contrario, el menú flotante podría extenderse más allá del borde derecho de la página.

![imagen_1-53](assets/chlimage_1-53.png)

### Imagen {#image}

El componente Imagen de Dynamic Media Classic (Scene7) le permite añadir la funcionalidad de Dynamic Media Classic (Scene7) a sus imágenes, como modificadores de Dynamic Media Classic (Scene7), ajustes preestablecidos de imágenes o visores y nitidez. El componente de imagen Dynamic Media Classic (Scene7) es similar a otros componentes de imagen en Experience Manager con la funcionalidad especial de Dynamic Media Classic (Scene7). En este ejemplo, la imagen tiene el modificador de URL de Dynamic Media Classic (Scene7), `&op_invert=1` aplicado.

![](do-not-localize/chlimage_1-4.png)

**Título, Texto alternativo** : en la ficha Avanzado, añada un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**URL, Abrir en** : puede configurar un recurso de para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![imagen_1-54](assets/chlimage_1-54.png)

**Ajuste preestablecido de visualizador** : seleccione un ajuste preestablecido de visualizador existente en el menú desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

**Configuración de Dynamic Media Classic (Scene7)** : seleccione la configuración de Dynamic Media Classic (Scene7) que desee utilizar para recuperar ajustes preestablecidos de imagen activos de SPS.

**Ajuste preestablecido de imagen** : seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de imagen. No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

**Formato de salida** : seleccione el formato de salida de la imagen, por ejemplo jpeg. En función del formato de salida que seleccione, puede tener opciones de configuración adicionales. Consulte Prácticas recomendadas para ajustes preestablecidos de imagen.

**Enfoque** : seleccione cómo desea enfocar la imagen. El enfoque se explica en detalle en Prácticas recomendadas para ajustes preestablecidos de imagen y en Prácticas recomendadas para el enfoque.

**Modificadores de URL** : puede cambiar los efectos de imagen suministrando comandos de imagen S7 adicionales. Estos comandos se describen en Ajustes preestablecidos de imagen y en la referencia de comandos.

**Puntos de interrupción** : si su sitio web es interactivo, desea ajustar los puntos de interrupción. Los puntos de interrupción deben separarse con comas (,).

### Plantilla de imagen {#image-template}

Las plantillas de imagen de Dynamic Media Classic (Scene7) son contenido Photoshop en capas importado a Dynamic Media Classic (Scene7), donde el contenido y las propiedades se han parametrizado para la variabilidad. El componente **[!UICONTROL Image template]** permite importar imágenes y cambiar el texto de forma dinámica en el Experience Manager. Además, puede configurar el componente **[!UICONTROL Plantilla de imágenes]** para utilizar valores de ClientContext, de modo que cada usuario experimenta la imagen de una forma personalizada.

Seleccione **[!UICONTROL Edit]** - para configurar el componente. Puede configurar las [opciones comunes a todos los componentes de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) y otras opciones que se describen en esta sección.

![imagen_1-55](assets/chlimage_1-55.png)

**Referencia del archivo, Anchura y Altura** : consulte la  [configuración común a todos los componentes](/help/sites-administering/scene7.md#settingscommontoallscene7components) de Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Los comandos y parámetros de URL de Dynamic Media Classic (Scene7) no se pueden agregar directamente a la URL de referencia de archivos. Solo se pueden definir en la interfaz de usuario del componente en el panel **[!UICONTROL Parámetro]**.

**Título, Texto alternativo** : en la pestaña Plantilla de imagen de Dynamic Media Classic (Scene7), añada un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**URL, Abrir en** : puede configurar un recurso de para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![imagen_1-56](assets/chlimage_1-56.png)

**Panel de parámetros** : al importar una imagen, los parámetros se rellenan previamente con información de la imagen. Si no existe contenido que se pueda cambiar de forma dinámica, esta ventana está vacía.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Cambio del texto de forma dinámica {#changing-text-dynamically}

Para cambiar el texto de forma dinámica, introduzca texto nuevo en los campos y seleccione **[!UICONTROL OK]**. En este ejemplo, el **Precio** es ahora $50 y el envío cuesta 99 centavos.

![chlimage_1-58](assets/chlimage_1-58.png)

El texto de la imagen cambia. Para restablecer el texto al valor original, seleccione **[!UICONTROL Reset]** junto al campo.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Cambiar texto para reflejar el valor de un valor de ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular un campo a un valor de ClientContext, seleccione **[!UICONTROL Select]** para abrir el menú client-context, seleccione ClientContext y **[!UICONTROL OK]**. En este ejemplo, el nombre cambia en función de la vinculación de valor de Nombre con el nombre con formato que consta en el perfil.

![imagen_1-60](assets/chlimage_1-60.png)

El texto refleja el nombre del usuario de la sesión actual. Para restablecer el texto al valor original, seleccione **[!UICONTROL Reset]** junto al campo.

![climage_1-61](assets/chlimage_1-61.png)

#### Conversión de la plantilla de imagen de Dynamic Media Classic (Scene7) en un vínculo {#making-the-scene-image-template-a-link}

Puede convertir el componente de plantilla de imagen de Dynamic Media Classic (Scene7) en un vínculo en el que se puede hacer clic.

1. En la página con el componente de plantilla de imagen de Dynamic Media Classic (Scene7), seleccione **[!UICONTROL Editar]**.
1. En el campo **[!UICONTROL URL]**, introduzca la dirección URL a la que los usuarios se dirigen al hacer clic en la imagen. En el campo **[!UICONTROL Open in]**, seleccione si desea que se abra el destino (una nueva ventana o la misma ventana).

   ![imagen_1-62](assets/chlimage_1-62.png)

1. Seleccione **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

El componente **[!UICONTROL Vídeo]** de Dynamic Media Classic (Scene7) (disponible en la sección Dynamic Media Classic (Scene7) de la barra de tareas) utiliza la detección de dispositivos y ancho de banda para ofrecer el vídeo correcto a cada pantalla. Este componente es un reproductor de vídeo HTML5; se trata de un visor único que se puede utilizar en múltiples canales.

Se puede usar para conjuntos de vídeos adaptables, un solo vídeo MP4 o un solo vídeo F4V.

Consulte [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) para obtener más información sobre cómo funcionan los vídeos con la integración de Dynamic Media Classic (Scene7). Además, vea cómo el [componente **Dynamic Media Classic (Scene7) video** se compara con el componente básico **video**](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![imagen_1-63](assets/chlimage_1-63.png)

### Limitaciones conocidas del componente de vídeo {#known-limitations-for-the-video-component}

Adobe DAM y WCM muestran si se ha cargado un vídeo de origen principal. No muestran estos recursos de proxy:

* Representaciones codificadas de Dynamic Media Classic (Scene7)
* Conjuntos de vídeos adaptables de Dynamic Media Classic (Scene7)

Al utilizar un conjunto de vídeos adaptables con el componente de vídeo de Dynamic Media Classic (Scene7), se debe cambiar el tamaño del componente para que se ajuste a las dimensiones del vídeo.

## Navegador de contenido de Dynamic Media Classic (Scene7) {#scene-content-browser}

El navegador de contenido de Dynamic Media Classic (Scene7) le permite ver el contenido de Dynamic Media Classic (Scene7) directamente en el Experience Manager. Para acceder al navegador de contenido, en el Buscador de contenido, seleccione **Dynamic Media Classic (Scene7)** en la interfaz de usuario táctil o el icono **S7** en la interfaz de usuario clásica. La funcionalidad es idéntica en ambas interfaces de usuario.

Si tiene varias configuraciones, el Experience Manager muestra de forma predeterminada la [configuración predeterminada](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puede seleccionar diferentes configuraciones directamente en el navegador de contenido de Dynamic Media Classic (Scene7) en el menú desplegable.

>[!NOTE]
>
>* Los recursos de la carpeta On-demand no aparecen en el navegador de contenido de Dynamic Media Classic (Scene7).
>* Cuando [Previsualización segura está habilitada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), los recursos publicados y no publicados en Dynamic Media Classic (Scene7) sí aparecen en el navegador de contenido de Dynamic Media Classic (Scene7).
>* Si no ve **[!UICONTROL Dynamic Media Classic (Scene7)]** o el icono **[!UICONTROL S7]** como una opción en el navegador de contenido, debe [configurar Dynamic Media Classic (Scene7) para que funcione con el Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, el navegador de contenido de Dynamic Media Classic (Scene7) es compatible con:
   >   * Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
   >   * Un solo vídeo MP4
   >   * Vídeo F4V único


### Examinar contenido {#browsing-content-in-the-classic-ui}

Para examinar el contenido en Dynamic Media Classic (Scene7), seleccione la pestaña **[!UICONTROL S7]** .

Puede cambiar la configuración a la que accede seleccionando la configuración . Las carpetas cambian según la configuración que seleccione.

![imagen_1-64](assets/chlimage_1-64.png)

Al igual que ocurre con el buscador de contenido para los recursos, puede buscar recursos y filtrar los resultados. Sin embargo, a diferencia del buscador de recursos, al introducir una palabra clave en la pestaña **S7**, el nombre del archivo **comienza por** la cadena introducida, en lugar de **contener** la palabra clave en el nombre de archivo.

De forma predeterminada, los recursos se muestran por el nombre de archivo. Sin embargo, también puede filtrar los resultados por tipo de recurso.

>[!NOTE]
>
>Para vídeo, el navegador de contenido Dynamic Media Classic (Scene7) de WCM admite:
>
>* Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
>* Un solo vídeo MP4
>* Vídeo F4V único

>



### Busque recursos de Dynamic Media Classic (Scene7) con el navegador de contenido {#searching-for-scene-assets-with-the-content-browser}

La búsqueda de recursos de Dynamic Media Classic (Scene7) es similar a la búsqueda de recursos de Experience Manager. La excepción es que, cuando realice una búsqueda, verá una vista remota de los recursos en el sistema de Dynamic Media Classic (Scene7), en lugar de importarlos directamente en el Experience Manager.

Puede utilizar la interfaz de usuario clásica o la optimizada para el uso táctil para ver y buscar recursos. Según la interfaz, la búsqueda es ligeramente diferente.

Al buscar en cualquier interfaz de usuario, puede filtrar según los criterios siguientes (aquí se muestra la IU optimizada para el uso táctil):

**Escriba palabras clave** : puede buscar recursos por nombre. Al buscar las palabras clave, debe especificar con qué comienza el nombre del archivo. Por ejemplo, al escribir la palabra “natación”, el sistema buscaría cualquier nombre de archivo de recurso que comience por esas letras en ese orden. Asegúrese de seleccionar Intro después de escribir el término para buscar el recurso.

![chlimage_1-65](assets/chlimage_1-65.png)

**Carpeta/ruta** : el nombre de la carpeta se basa en la configuración seleccionada. Puede explorar en profundidad los niveles inferiores seleccionando el icono de carpeta y una subcarpeta, y luego seleccionando la marca de verificación para seleccionarla.

Si introduce una palabra clave y selecciona una carpeta, el Experience Manager busca esa carpeta y las subcarpetas. Sin embargo, si no introduce ninguna palabra clave al buscar, la selección de la carpeta solo muestra los recursos de esa carpeta y no incluye ninguna subcarpeta.

De forma predeterminada, el Experience Manager busca la carpeta seleccionada y todas las subcarpetas.

![imagen_1-66](assets/chlimage_1-66.png)

**Tipo de recurso** : seleccione Dynamic Media Classic (Scene7) para examinar el contenido de Dynamic Media Classic (Scene7). Esta opción solo está disponible si se ha configurado Dynamic Media Classic (Scene7).

![chlimage_1-67](assets/chlimage_1-67.png)

**Configuración** : si tiene más de una configuración de Dynamic Media Classic (Scene7) definida en Cloud Services, puede seleccionarla aquí. Como resultado, la carpeta cambia según la configuración elegida.

![chlimage_1-68](assets/chlimage_1-68.png)

**Tipo de recurso** : en el navegador Dynamic Media Classic (Scene7), puede filtrar los resultados para incluir cualquiera de los siguientes elementos: imágenes, plantillas, vídeos y conjuntos de vídeos adaptables. Si no selecciona ningún tipo de recurso, el Experience Manager busca de forma predeterminada todos los tipos de recurso.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* En la interfaz de usuario clásica; también puede buscar **Flash** y **FXG**. No se admite el filtrado de estos dos términos en la IU táctil.
   >
   >
* Al buscar vídeos, se busca una sola representación. Los resultados devuelven la representación original (solo *.mp4) y la representación codificada.
* Al buscar un conjunto de vídeos adaptables, está buscando en la carpeta y en todas las subcarpetas, pero solo si ha añadido una palabra clave a la búsqueda. Si no ha añadido ninguna palabra clave, el Experience Manager no busca en las subcarpetas.



**Estado de publicación** : puede filtrar los recursos en función del estado de publicación: No publicado o publicado. Si no selecciona ningún estado de publicación, el Experience Manager busca de forma predeterminada todos los estados de publicación.

![chlimage_1-70](assets/chlimage_1-70.png)
