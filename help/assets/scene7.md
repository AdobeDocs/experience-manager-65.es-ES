---
title: Agregar características de Dynamic Media Classic a páginas
description: Cómo añadir funciones y componentes de Dynamic Media Classic a una página de Adobe Experience Manager.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 15%

---

# Agregar características de Dynamic Media Classic a páginas {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos a pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Puede ver los recursos de Experience Manager publicados en Dynamic Media Classic en varios visores:

* Zoom
* Flotante
* Vídeo
* Plantilla de imagen
* Imagen

Puede publicar recursos digitales directamente de Experience Manager a Dynamic Media Classic y los recursos digitales de Dynamic Media Classic a Experience Manager.

En este documento se describe cómo publicar recursos digitales de Experience Manager a Dynamic Media Classic y, a la inversa, cómo hacerlo. Los visores también se describen en detalle. Para obtener información sobre la configuración de Experience Manager para Dynamic Media Classic, consulte [Integración de Dynamic Media Classic con el Experience Manager](/help/sites-administering/scene7.md).

Consulte también [Añadir mapas de imagen](image-maps.md).

Para obtener más información sobre el uso de componentes de vídeo con Experience Manager, consulte [Vídeo](video.md).

>[!NOTE]
>
>Si los recursos de Dynamic Media Classic no se muestran correctamente, asegúrese de que Dynamic Media esté [disabled](config-dynamic.md#disabling-dynamic-media) y, a continuación, actualice la página.

## Publicación manual en Dynamic Media Classic desde recursos {#manually-publishing-to-scene-from-assets}

Puede publicar recursos digitales en Dynamic Media Classic de la siguiente manera:

* [En la interfaz de usuario clásica desde la consola Recursos](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [En la interfaz de usuario clásica desde un recurso](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [En la interfaz de usuario clásica desde fuera de la carpeta de destino de CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager publica en Dynamic Media Classic de forma asíncrona. Después de seleccionar **[!UICONTROL Publicación]**, el recurso tarda varios segundos en publicarse en Dynamic Media Classic.

## Componentes de Dynamic Media Classic {#scene-components}

Los siguientes componentes de Dynamic Media Classic están disponibles en Experience Manager:

* Zoom
* Flotante (zoom)
* Plantilla de imagen
* Imagen
* Vídeo

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben seleccionarse en **[!UICONTROL Diseño]** antes de utilizar.

Una vez que estén disponibles en **[!UICONTROL Diseño]** , puede añadir los componentes a la página como cualquier otro componente de Experience Manager. Los recursos que aún no se han publicado en Dynamic Media Classic se publican en Dynamic Media Classic si se encuentran en una carpeta sincronizada o en una página o con una configuración de nube de Dynamic Media Classic.

>[!NOTE]
>
>Si está creando y desarrollando visores personalizados y utilizando el Buscador de contenido, debe agregar explícitamente la variable `allowfullscreen` parámetro.

### Aviso de fin de vida útil para el visualizador Flash {#flash-viewers-end-of-life-notice}

A partir del 31 de enero de 2017, Adobe Dynamic Media Classic dejó de ser compatible con la plataforma del visor de Flash.

### Añadir un componente de Dynamic Media Classic (Scene7) a una página {#adding-a-scene-component-to-a-page}

Añadir un componente Dynamic Media Classic (Scene7) a una página es lo mismo que añadir un componente a cualquier página. Los componentes de Dynamic Media Classic se describen en detalle en las secciones siguientes.

**Para añadir un componente de Dynamic Media Classic (Scene7) a una página:**

1. En el Experience Manager, abra la página a la que desea agregar la variable **[!UICONTROL Dynamic Media Classic (Scene7)]** componente.

1. Si no hay componentes de Dynamic Media Classic disponibles, seleccione **[!UICONTROL Diseño]** , seleccione cualquier componente con un borde azul y, a continuación, seleccione el **[!UICONTROL Principal]** y luego la función **[!UICONTROL Configuración]** icono. En **[!UICONTROL Parsys (diseño)]**, seleccione todos los componentes de Dynamic Media Classic para que estén disponibles y seleccione **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Select **[!UICONTROL Editar]** para que pueda volver a **[!UICONTROL Editar]** en el menú contextual.

1. Arrastre un componente del grupo Dynamic Media Classic de la barra de tareas hasta la página en la ubicación deseada.

1. Seleccione el **[!UICONTROL Configuración]** para poder abrir el componente.

1. Edite el componente como sea necesario y seleccione **[!UICONTROL OK]** para guardar los cambios.
1. Arrastre la imagen o el vídeo desde el navegador de contenido al componente Dynamic Media Classic que ha agregado a la página.

   >[!NOTE]
   >
   >Solo en la IU táctil, debe arrastrar y soltar la imagen o el vídeo en el componente de Dynamic Media Classic que haya colocado en la página. No se admite la selección y edición del componente Dynamic Media Classic y, a continuación, la selección del recurso.

### Agregar una experiencia de visualización interactiva a un sitio interactivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

El diseño interactivo de los recursos significa que el recurso se adapta según el lugar en que se muestre. Con un diseño interactivo, los mismos recursos se pueden mostrar de forma eficaz en varios dispositivos.

Consulte también [Diseño interactivo para páginas web](/help/sites-developing/responsive.md).

**Para añadir una experiencia de visualización interactiva a un sitio interactivo:**

1. Inicie sesión en el Experience Manager y asegúrese de que ha [Cloud Services configurados de Adobe Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-scene-integration) y que los componentes de Dynamic Media Classic están disponibles.

   >[!NOTE]
   >
   >Si los componentes de Dynamic Media Classic no están disponibles, asegúrese de que [para activarlos mediante el modo Diseño](/help/sites-authoring/default-components-designmode.md).

1. En un sitio web con la variable **[!UICONTROL Dynamic Media Classic]** componentes habilitados, arrastre y **[!UICONTROL Imagen]** a la página.
1. Seleccione el componente y el icono de configuración.
1. En el **[!UICONTROL Configuración de Dynamic Media Classic]** , ajuste los puntos de interrupción.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Confirme que los visores cambian de tamaño de manera interactiva y que las interacciones están optimizadas para dispositivos de escritorio, tabletas y móviles.

### Configuración común a todos los componentes de Dynamic Media Classic {#settings-common-to-all-scene-components}

Aunque las opciones de configuración varían, las siguientes son comunes a todas las [!UICONTROL Dynamic Media Classic] componentes:

* **[!UICONTROL Referencia del archivo]**: navegue a un archivo al que quiera hacer referencia. La referencia de archivo muestra la URL del recurso y no necesariamente la URL completa de Dynamic Media Classic, incluidos los comandos y parámetros de URL. No se pueden agregar comandos y parámetros de URL de Dynamic Media Classic en este campo. En su lugar, puede agregarlas a través de la funcionalidad correspondiente del componente.
* **[!UICONTROL Anchura]**: le permite definir la anchura.
* **[!UICONTROL Altura]**: le permite definir la altura.

Para establecer estas opciones de configuración, abra (haga doble clic en) un componente Dynamic Media Classic, por ejemplo, al abrir un **[!UICONTROL Zoom]** componente:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

El componente Zoom del HTML5 muestra una imagen más grande al pulsar el botón **[!UICONTROL +]** botón.

El recurso dispone de herramientas de zoom en la parte inferior. Select **[!UICONTROL +]** si desea ampliar; select **[!UICONTROL -]** si desea reducir. Al tocar **[!UICONTROL x]** o la flecha para restablecer el zoom devuelve la imagen al tamaño original que se importó como. Seleccione las flechas diagonales para que se hagan a pantalla completa. Select **[!UICONTROL Editar]** para que pueda configurar el componente. Con este componente, puede configurar [configuración común a todos [!UICONTROL Dynamic Media Classic] componentes](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flotante {#flyout}

En el HTML5 **[!UICONTROL Flotante]** componente, el recurso se muestra como pantalla dividida; dejó el recurso en el tamaño especificado; a la derecha se muestra la porción de zoom. Select **[!UICONTROL Editar]** para que pueda configurar el componente. Con este componente, puede configurar [configuración común a todos los componentes de Dynamic Media Classic](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Si su **[!UICONTROL Flotante]** utiliza un tamaño personalizado, se utiliza ese tamaño personalizado y se desactiva la configuración interactiva del componente.
>
>Si su **[!UICONTROL Flotante]** el componente utiliza el tamaño predeterminado, tal como se establece en **[!UICONTROL Vista diseño]**, se utilizará el tamaño predeterminado y el componente se ampliará para dar cabida al tamaño del diseño de página con la configuración interactiva del componente habilitada. Existe una limitación en la configuración interactiva del componente. Al usar la variable **[!UICONTROL Flotante]** con configuración interactiva, no la utilice con la extensión de página completa. De lo contrario, la función **[!UICONTROL Flotante]** se extiende más allá del borde derecho de la página.

![chlimage_1-228](assets/chlimage_1-228.png)

### Imagen {#image}

Dynamic Media Classic **[!UICONTROL Imagen]** permite añadir funciones de Dynamic Media Classic a las imágenes, como modificadores de Dynamic Media Classic, ajustes preestablecidos de visor o imagen y nitidez. Dynamic Media Classic **[!UICONTROL Imagen]** es similar a otros componentes de imagen en Experience Manager con funciones especiales de Dynamic Media Classic. En este ejemplo, la imagen tiene el modificador Dynamic Media Classic URL, `&op_invert=1` aplicado.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Título, Texto alternativo]** - En el **[!UICONTROL Avanzadas]** , añada un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**[!UICONTROL URL, Abrir en]** - Puede configurar un recurso de para abrir un vínculo. Defina la **[!UICONTROL dirección URL]** y, en **[!UICONTROL Abrir en]**, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Ajuste preestablecido del visor]** - Seleccione un ajuste preestablecido de visualizador existente en el menú desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

**[!UICONTROL Configuración de Dynamic Media Classic]** - Seleccione la configuración de Dynamic Media Classic que desea utilizar para recuperar los ajustes preestablecidos de imagen activos de SPS.

**[!UICONTROL Ajuste preestablecido de imagen]** - Seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte [Administrar ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md). No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

**[!UICONTROL Formato de salida]** - Seleccione el formato de salida de la imagen, por ejemplo jpeg. Según el formato de salida que seleccione, hay opciones de configuración adicionales. Consulte [Prácticas recomendadas para ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Enfoque]** - Seleccione cómo desea enfocar la imagen. El enfoque se explica en detalle en [Prácticas recomendadas para ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md#image-preset-options) y en [Prácticas recomendadas para el enfoque](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL Modificadores de URL]** - Puede cambiar los efectos de imagen suministrando comandos de imagen Dynamic Media Classic adicionales. Estos comandos se describen en [Ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md) y [Referencia de comandos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Puntos de interrupción]** - Si su sitio web es interactivo, desea ajustar los puntos de interrupción. Los puntos de interrupción deben separarse con comas ( , ).

### Plantilla de imagen {#image-template}

[Plantillas de imagen de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) son contenido de Photoshop en capas que se importó a Dynamic Media Classic, donde el contenido y las propiedades se parametrizaron para la variabilidad. La variable **[!UICONTROL Plantilla de imagen]** permite importar imágenes y cambiar el texto de forma dinámica en Experience Manager. Además, puede configurar el componente **[!UICONTROL Plantilla de imágenes]** para utilizar valores de ClientContext, de modo que cada usuario experimenta la imagen de una forma personalizada.

Select **[!UICONTROL Editar]** si desea configurar el componente. Puede configurar [configuración común a todos los componentes de Dynamic Media Classic](#settings-common-to-all-scene-components) y otras configuraciones descritas en esta sección.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Referencia del archivo, Anchura y Altura]** - Consulte la configuración común a todos los componentes de ScDynamic Media Classic7 .

>[!NOTE]
>
>Los comandos y parámetros de URL de Dynamic Media Classic no se pueden agregar directamente a la URL de referencia de archivo. Solo se pueden definir en la interfaz de usuario del componente en el panel **[!UICONTROL Parámetro]**.

**[!UICONTROL Título, Texto alternativo]** - En la pestaña Plantilla de imagen de Dynamic Media Classic , añada un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**[!UICONTROL URL, Abrir en]** - Puede configurar un recurso de para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Panel de parámetros]** - Al importar una imagen, los parámetros se rellenan previamente con información de la imagen. Si no existe contenido que se pueda cambiar de forma dinámica, esta ventana está vacía.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Cambiar texto dinámicamente {#changing-text-dynamically}

Para cambiar el texto de forma dinámica, introduzca texto nuevo en los campos y seleccione **[!UICONTROL OK]**. En este ejemplo, el **[!UICONTROL Precio]** es ahora $50 y el envío cuesta 99 centavos.

![chlimage_1-234](assets/chlimage_1-234.png)

El texto de la imagen cambia. Para restablecer el texto al valor original, pulse **[!UICONTROL Restablecer]** junto al campo .

![chlimage_1-235](assets/chlimage_1-235.png)

#### Cambiar texto para reflejar el valor de un valor de ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular un campo a un valor de ClientContext, seleccione **[!UICONTROL Select]** para abrir el menú client-context, seleccione client context y seleccione **[!UICONTROL OK]**. En este ejemplo, el nombre cambia en función de la vinculación de valor de Nombre con el nombre con formato que consta en el perfil.

![chlimage_1-236](assets/chlimage_1-236.png)

El texto refleja el nombre del usuario de la sesión actual. Para restablecer el texto al valor original, haga clic en **[!UICONTROL Restablecer]** junto al campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Conversión de la plantilla de imagen de Dynamic Media Classic en un vínculo {#making-the-scene-image-template-a-link}

1. En la página con Dynamic Media Classic **[!UICONTROL Plantilla de imagen]** componente, seleccione **[!UICONTROL Editar]**.
1. En el **[!UICONTROL URL]** , introduzca la dirección URL a la que se dirigen los usuarios cuando toca la imagen. En el **[!UICONTROL Abrir en]** , seleccione si desea que se abra el destino (una nueva ventana o la misma ventana).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Select **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

Dynamic Media Classic **[!UICONTROL Vídeo]** (disponible en la sección Dynamic Media Classic de la barra de tareas) utiliza la detección de dispositivos y ancho de banda para ofrecer el vídeo correcto a cada pantalla. Este componente es un reproductor de vídeo HTML5; se trata de un visor único que se puede utilizar en múltiples canales.

Se puede usar para conjuntos de vídeos adaptables, un solo vídeo MP4 o un solo vídeo F4V.

Consulte [Vídeo](s7-video.md) para obtener más información sobre cómo funcionan los vídeos con la integración de Dynamic Media Classic. Además, consulte [el componente Vídeo de Dynamic Media Classic frente al componente Vídeo de base](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitaciones conocidas del componente de vídeo {#known-limitations-for-the-video-component}

Adobe DAM y WCM muestran si se ha cargado un vídeo de origen principal. No muestran estos recursos de proxy:

* Representaciones codificadas de Dynamic Media Classic
* Conjuntos de vídeos adaptables de Dynamic Media Classic

Al utilizar un conjunto de vídeos adaptables con el componente de vídeo de Dynamic Media Classic, debe cambiar el tamaño del componente para que se ajuste a las dimensiones del vídeo.

## Navegador de contenido de Dynamic Media Classic {#scene-content-browser}

El navegador de contenido de Dynamic Media Classic le permite ver el contenido de Dynamic Media Classic directamente en el Experience Manager. Para acceder al navegador de contenido, en la **[!UICONTROL Buscador de contenido]**, seleccione **[!UICONTROL Dynamic Media Classic]** en la interfaz de usuario táctil o en la **[!UICONTROL S7]** en la interfaz de usuario clásica. La funcionalidad es idéntica en ambas interfaces de usuario.

Si tiene varias configuraciones, el Experience Manager muestra de forma predeterminada la variable [configuración predeterminada](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puede seleccionar diferentes configuraciones directamente en el navegador de contenido de Dynamic Media Classic en el menú desplegable.

>[!NOTE]
>
>* Los recursos de la carpeta bajo demanda no aparecen en el explorador de contenido de Dynamic Media Classic.
>* When [La vista previa segura está activada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), tanto los recursos publicados como los no publicados en Dynamic Media Classic aparecen en el navegador de contenido de Dynamic Media Classic.
>* Si no ve **[!UICONTROL Dynamic Media Classic]** o **[!UICONTROL S7]** como opción en el navegador de contenido, debe [configuración de Dynamic Media Classic para que funcione con Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, el navegador de contenido de Dynamic Media Classic admite:
   >
   >   * Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
   >   * Un solo vídeo MP4
   >   * Vídeo F4V único


### Examinar contenido en la IU táctil {#browsing-content-in-the-touch-optimized-ui}

Puede acceder al navegador de contenido desde la IU táctil o clásica. Actualmente, la optimizada para el tacto tiene la siguiente limitación:

* Los recursos FXG y de Flash de Dynamic Media Classic no son compatibles.

Examinar los recursos de Dynamic Media Classic seleccionando **[!UICONTROL Dynamic Media Classic]** en el tercer menú desplegable. Dynamic Media Classic no aparece en la lista si no ha configurado la integración de Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* El navegador de contenido de Dynamic Media Classic carga unos 100 activos y los ordena por nombre.
>* Si tiene configurado un servidor de vista previa seguro, el navegador utiliza ese servidor de vista previa para procesar miniaturas y recursos.
>


![chlimage_1-240](assets/chlimage_1-240.png)

Además, puede examinar la información de resolución, el tamaño, los días transcurridos desde la modificación y el nombre de archivo pasando el ratón por encima del recurso en el explorador.

![chlimage_1-241](assets/chlimage_1-241.png)

* Para los conjuntos de vídeos adaptables y las plantillas, no se genera información de tamaño para las miniaturas.
* Para los conjuntos de vídeos adaptables, no se genera ninguna resolución para las miniaturas.

### Busque recursos de Dynamic Media Classic con el navegador de contenido {#searching-for-scene-assets-with-the-content-browser}

La búsqueda de recursos en Dynamic Media Classic es similar a la búsqueda de recursos en Experience Manager Assets. Sin embargo, cuando realice la búsqueda, verá una vista remota de los recursos en el sistema Dynamic Media Classic, en lugar de importarlos directamente en el Experience Manager.

Puede utilizar la interfaz de usuario clásica o la optimizada para el uso táctil para ver y buscar recursos. Según la interfaz, la búsqueda es ligeramente diferente.

Al buscar en cualquier interfaz de usuario, puede filtrar según los criterios siguientes (aquí se muestra la IU optimizada para el uso táctil):

**[!UICONTROL Escribir palabras clave]** - Puede buscar recursos por nombre. Al buscar, las palabras clave introducidas son por lo que comienza el nombre del archivo. Por ejemplo, al escribir la palabra “natación”, el sistema buscaría cualquier nombre de archivo de recurso que comience por esas letras en ese orden. Asegúrese de pulsar Intro después de escribir el término para buscar el recurso.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Carpeta/ruta]** - El nombre de la carpeta que se ve se basa en la configuración seleccionada. Para desplazarse a los niveles inferiores, toque el icono de la carpeta, seleccione una subcarpeta y, a continuación, pulse la marca de verificación para seleccionarla.

Si introduce una palabra clave y selecciona una carpeta, el Experience Manager busca esa carpeta y las subcarpetas. Sin embargo, si no introduce ninguna palabra clave al buscar, la selección de la carpeta solo muestra los recursos de esa carpeta y no incluye ninguna subcarpeta.

De forma predeterminada, el Experience Manager busca la carpeta seleccionada y todas las subcarpetas.

![imagen_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo de recurso]** - Seleccionar **[!UICONTROL Dynamic Media Classic]** para examinar el contenido de Dynamic Media Classic. Esta opción solo está disponible si se ha configurado Dynamic Media Classic.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuración]** - Si tiene más de una configuración de Dynamic Media Classic definida en [!UICONTROL Cloud Services], puede seleccionarlo aquí. Como resultado, la carpeta cambia según la configuración elegida.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo de recurso]** - Dentro del explorador de Dynamic Media Classic, puede filtrar los resultados para incluir cualquiera de los siguientes elementos: imágenes, plantillas, vídeos y conjuntos de vídeos adaptables. Si no selecciona ningún tipo de recurso, el Experience Manager, de forma predeterminada, busca todos los tipos de recurso.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* En la interfaz de usuario clásica; también puede buscar **Flash** y **FXG**. No se admite el filtrado para estos tipos en la IU táctil.
>
>* Al buscar vídeos, se busca una sola representación. Los resultados devuelven la representación original (solo &amp;ast;.mp4) y la representación codificada.
>* Al buscar un conjunto de vídeos adaptables, está buscando en la carpeta y en todas las subcarpetas, pero solo si ha añadido una palabra clave a la búsqueda. Si no ha añadido ninguna palabra clave, el Experience Manager no busca en las subcarpetas.
>


**[!UICONTROL Estado de publicación]** - Puede filtrar los recursos en función del estado de publicación: **[!UICONTROL Sin publicar]** o **[!UICONTROL Publicado]**. Si no selecciona ninguna **[!UICONTROL Estado de publicación]**, Experience Manager busca de forma predeterminada todos los estados de publicación.

![chlimage_1-247](assets/chlimage_1-247.png)
