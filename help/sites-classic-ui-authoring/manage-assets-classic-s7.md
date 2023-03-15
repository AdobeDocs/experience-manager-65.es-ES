---
title: Añadir funciones de Dynamic Media Classic (Scene7) a la página
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

# Añadir funciones de Dynamic Media Classic (Scene7) a la página{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Puede ver los recursos del Experience Manager publicados en Dynamic Media Classic (Scene7) en varios visores:

* Zoom
* Flotante
* Vídeo
* Plantilla de imagen
* Imagen

Puede publicar recursos digitales directamente desde Experience Manager a Dynamic Media Classic (Scene7) y publicar recursos digitales desde Dynamic Media Classic (Scene7) a Experience Manager.

En este documento se describe cómo publicar recursos digitales de Experience Manager en Dynamic Media Classic (Scene7) y a la inversa. Los visores también se describen en detalle. Para obtener información sobre la configuración de Experience Manager para Dynamic Media Classic (Scene7), consulte [Integración de Dynamic Media Classic (Scene7) con Experience Manager](/help/sites-administering/scene7.md).

Consulte también [Añadir mapas de imagen](/help/assets/image-maps.md).

Para obtener más información sobre el uso de componentes de vídeo con Experience Manager, consulte lo siguiente:

* [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Si los recursos de Dynamic Media Classic (Scene7) no se muestran correctamente, asegúrese de que Dynamic Media está [inhabilitado](/help/assets/config-dynamic.md#disabling-dynamic-media) y luego actualice la página.

## Publicación manual en Dynamic Media Classic (Scene7) desde Assets {#manually-publishing-to-scene-from-assets}

Puede publicar recursos digitales en Dynamic Media Classic (Scene7) desde la consola Recursos en la IU clásica o directamente desde el recurso.

>[!NOTE]
>
>Experience Manager publica en Dynamic Media Classic (Scene7) de forma asíncrona. Después de seleccionar **[!UICONTROL Publish]** Sin embargo, su recurso puede tardar varios segundos en publicarse en Dynamic Media Classic (Scene7).

### Publicación desde la consola Recursos {#publishing-from-the-assets-console}

Puede publicar en Dynamic Media Classic (Scene7) desde la consola Recursos si los recursos están en una carpeta de destino de Dynamic Media Classic (Scene7).

1. En la IU de Experience Manager Classic, seleccione **[!UICONTROL Recursos digitales]** para acceder al administrador de recursos digitales.

1. Seleccione el recurso (o los recursos) o la carpeta en la carpeta de destino que desea publicar en Dynamic Media Classic (Scene7), haga clic con el botón derecho y seleccione **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]**. Como alternativa, puede seleccionar **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]** desde el **[!UICONTROL Herramientas]** menú.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Vaya a Dynamic Media Classic (Scene7) y confirme que los recursos están disponibles.

   >[!NOTE]
   >
   >Si los recursos no están en una carpeta sincronizada de Dynamic Media Classic (Scene7), **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]** en ambos menús está visible pero desactivado.

### Publicar desde un recurso {#publishing-from-an-asset}

Puede publicar manualmente un recurso siempre que esté ubicado dentro de la carpeta sincronizada de Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si el recurso no está en la carpeta sincronizada de Dynamic Media Classic (Scene7), el vínculo a **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]** no aparece.

Para publicar en Dynamic Media Classic (Scene7) directamente desde un recurso digital:

1. En Experience Manager, seleccione **[!UICONTROL Recursos digitales]** para acceder al administrador de recursos digitales.

1. Haga doble clic en dicha opción para abrir un recurso.

1. En el panel de detalles del recurso, seleccione **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. El vínculo cambia a **[!UICONTROL Publicando...]** y, a continuación, a **[!UICONTROL Publicado]**. Vaya a Dynamic Media Classic (Scene7) y confirme que el recurso está disponible.

   >[!NOTE]
   >
   >Si el recurso no se publica correctamente en Dynamic Media Classic (Scene7), el vínculo cambia a **[!UICONTROL Error de publicación]**. Si el recurso ya se ha publicado en Dynamic Media Classic (Scene7), el vínculo indica lo siguiente **[!UICONTROL Volver a publicar en Dynamic Media Classic (Scene7)]**. La republicación permite cambiar recursos en Experience Manager y volver a publicarlos.

### Publicar recursos desde fuera de la carpeta de destino de CQ {#publishing-assets-from-outside-the-cq-target-folder}

El Adobe recomienda publicar los recursos en Dynamic Media Classic (Scene7) únicamente desde los recursos de la carpeta de destino de Dynamic Media Classic (Scene7). Sin embargo, si debe cargar recursos desde una carpeta fuera de la carpeta de destino, aún puede hacerlo cargándolos en una carpeta bajo demanda en Dynamic Media Classic (Scene7). En primer lugar, configure Cloud para la página en la que desea que aparezca el recurso. A continuación, agregue un componente de Dynamic Media Classic (Scene7) a la página y arrastre y suelte un recurso en el componente. Una vez establecidas las propiedades de página para esa página, se crea un **[!UICONTROL Publicación en Dynamic Media Classic (Scene7)]** Este vínculo aparece cuando los déclencheur seleccionados se cargan en Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Los recursos que se encuentran en la carpeta bajo demanda no aparecen en el Explorador de contenido de Dynamic Media Classic (Scene7).

**Para publicar recursos desde fuera de la carpeta de destino de CQ:**

1. En Experience Manager, en la IU clásica, seleccione **[!UICONTROL Sitios web]** y vaya a la página web a la que desee agregar un recurso digital que aún no se haya publicado en Dynamic Media Classic (Scene7). (Se aplican las reglas de herencia de página habituales).

1. En la barra de tareas, seleccione **[!UICONTROL Página]** y seleccione **[!UICONTROL Propiedades de página]**.

1. Seleccionar **[!UICONTROL Cloud Services]**.
1. Seleccionar **[!UICONTROL Agregar servicios]**.
1. Seleccionar **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. En el **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]** , seleccione la configuración que desee y seleccione **[!UICONTROL OK]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. En la página web, agregue un componente Dynamic Media Classic (Scene7) a la ubicación deseada en la página.
1. En el buscador de contenido, arrastre un recurso digital hasta el componente. Verá un vínculo a **[!UICONTROL Comprobar el estado de publicación de Dynamic Media Classic (Scene7)]**.

   >[!NOTE]
   >
   >Si el recurso digital está en la carpeta de destino de CQ, no habrá ningún vínculo a **[!UICONTROL Comprobar el estado de publicación de Dynamic Media Classic (Scene7)]** aparece. Los recursos se colocan en el componente.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Seleccionar **[!UICONTROL Comprobar el estado de publicación de Dynamic Media Classic (Scene7)]**. Si los recursos no se publican, Experience Manager publica el recurso en Dynamic Media Classic (Scene7). Una vez cargado, el recurso se encuentra en la carpeta bajo demanda. De forma predeterminada, la carpeta bajo demanda se encuentra en **[!UICONTROL name_of_the_company/CQ5_adhoc]**. Puede [configurar la carpeta bajo demanda, si es necesario](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Si el recurso no está en una carpeta sincronizada de Dynamic Media Classic (Scene7) y no hay ninguna configuración de nube de Dynamic Media Classic (Scene7) asociada a la página actual, se produce un error en la carga.

## Componentes de Dynamic Media Classic (Scene7) {#scene-components}

Los siguientes componentes de Dynamic Media Classic (Scene7) están disponibles en Experience Manager:

* Zoom
* Flotante (zoom)
* Plantilla de imagen
* Imagen
* Vídeo

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben seleccionarse en el modo Diseño antes de utilizar.

Una vez que estén disponibles en el modo Diseño, puede agregar los componentes a la página como cualquier otro componente del Experience Manager. Los recursos que aún no se han publicado en Dynamic Media Classic (Scene7) se publican en Dynamic Media Classic (Scene7) si se encuentran en una carpeta sincronizada o en una página, o con una configuración de nube de Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si está creando y desarrollando visores S7 personalizados y utiliza el buscador de contenido, debe agregar explícitamente el `allowfullscreen` parámetro.

### Aviso de fin de vida útil para el visualizador Flash {#flash-viewers-end-of-life-notice}

A partir del 31 de enero de 2017, Adobe Dynamic Media Classic (Scene7) dejará de ofrecer oficialmente asistencia para la plataforma de visor de Flash.

### Añadir un componente Dynamic Media Classic (Scene7) a una página {#adding-a-scene-component-to-a-page}

Añadir un componente de Dynamic Media Classic (Scene7) a una página es lo mismo que añadir un componente a cualquier página. Los componentes de Dynamic Media Classic (Scene7) se describen en detalle en las secciones siguientes.

Para añadir un componente o visor de Dynamic Media Classic (Scene7) a una página en la IU clásica:

1. En Experience Manager, abra la página donde desea agregar el componente Dynamic Media Classic (Scene7).

1. Si no hay componentes de Dynamic Media Classic (Scene7) disponibles, seleccione la regla de la barra de tareas para introducirla. **Diseño** modo, seleccione **[!UICONTROL Editar]** parsys y seleccione todas las **[!UICONTROL Dynamic Media Classic (Scene7)]** componentes para que estén disponibles.

1. Volver a **Editar** modo seleccionando el lápiz en la barra de tareas.

1. Arrastre un componente desde el **[!UICONTROL Dynamic Media Classic (Scene7)]** grupo en la barra de tareas a la página en la ubicación deseada.

1. Seleccionar ***[!UICONTROL Editar]** para poder abrir el componente.

1. Edite el componente según sea necesario y seleccione **[!UICONTROL OK]** para guardar los cambios.

### Añadir experiencias de visualización interactivas a un sitio web interactivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

El diseño interactivo para sus recursos significa que los recursos se adaptarán según dónde se muestren. Con un diseño interactivo, los mismos recursos se pueden mostrar de forma eficaz en varios dispositivos.

Para añadir una experiencia de visualización interactiva a un sitio interactivo en la interfaz de usuario clásica:

1. Inicie sesión en el Experience Manager de y asegúrese de que dispone de lo siguiente [Cloud Services configurados de Adobe Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#configuring-scene-integration) y que los componentes de Dynamic Media Classic (Scene7) están disponibles.

   >[!NOTE]
   >
   >Si los componentes WCM de Dynamic Media Classic (Scene7) no están disponibles, asegúrese de activarlos en el modo Diseño.

1. En un sitio web con los componentes de Dynamic Media Classic (Scene7) habilitados, arrastre un **[!UICONTROL Imagen]** visualizador a la página.
1. Edite el componente y ajuste los puntos de interrupción en **[!UICONTROL Configuración de Dynamic Media Classic (Scene7)]** pestaña.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Confirme que los visores cambian de tamaño de manera interactiva y que las interacciones están optimizadas para dispositivos de escritorio, tabletas y móviles.

### Configuración común a todos los componentes de Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Aunque las opciones de configuración varían, los siguientes elementos son comunes a todos los componentes de Dynamic Media Classic (Scene7):

* **Referencia del archivo**: navegue a un archivo al que quiera hacer referencia. La referencia de archivo muestra la URL del recurso y no necesariamente la URL completa de Dynamic Media Classic (Scene7), incluidos los comandos y parámetros de URL. No puede añadir comandos y parámetros de URL de Dynamic Media Classic (Scene7) en este campo. En su lugar, se deben agregar a través de la funcionalidad correspondiente en el componente.
* **Anchura**: le permite definir la anchura.
* **Altura**: le permite definir la altura.

Estas opciones de configuración se establecen abriendo (haciendo doble clic) en un componente de Dynamic Media Classic (Scene7), por ejemplo, al abrir un **Zoom** componente:

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

El componente Zoom HTML5 muestra una imagen más grande al pulsar el botón +.

El recurso dispone de herramientas de zoom en la parte inferior. Seleccionar **[!UICONTROL +]** para ampliar. Seleccionar **[!UICONTROL -]** para reducir. Selección de la **[!UICONTROL x]** o la flecha para restablecer el zoom devuelve la imagen al tamaño original con el que se importó. Seleccione las flechas diagonales para que pueda hacerlo a pantalla completa. Seleccionar **[!UICONTROL Editar]** para poder configurar el componente. Con este componente, puede configurar lo siguiente [configuración común a todos los componentes de Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### Flotante {#flyout}

En el componente Flotante HTML5, el recurso se muestra como una pantalla dividida: a la izquierda aparece con el tamaño especificado y a la derecha aparece la porción modificada con el zoom. Seleccionar **[!UICONTROL Editar]** para poder configurar el componente. Con este componente, puede configurar lo siguiente [configuración común a todos los componentes de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Si el componente Flotante utiliza un tamaño personalizado, se utiliza dicho tamaño y se desactiva la configuración interactiva del componente.
>
>Si el componente flotante utiliza el tamaño predeterminado, tal como se establece en la vista Diseño, se utilizará el tamaño predeterminado. El componente se expande para dar cabida al tamaño del diseño de página con la configuración adaptable del componente habilitada. Sin embargo, tenga en cuenta que existe una limitación en la configuración interactiva del componente. Cuando utilice el componente flotante con configuración adaptable, no debe utilizarlo con ampliación de página completa. De lo contrario, el menú flotante puede extenderse más allá del borde derecho de la página.

![chlimage_1-53](assets/chlimage_1-53.png)

### Imagen {#image}

El componente Imagen de Dynamic Media Classic (Scene7) permite añadir la funcionalidad de Dynamic Media Classic (Scene7) a las imágenes, como los modificadores de Dynamic Media Classic (Scene7), los ajustes preestablecidos de imagen o visualizador y la función de enfoque. El componente de imagen de Dynamic Media Classic (Scene7) es similar a otros componentes de imagen en Experience Manager con funcionalidad especial de Dynamic Media Classic (Scene7). En este ejemplo, la imagen tiene el modificador de URL Dynamic Media Classic (Scene7), `&op_invert=1` aplicado.

![](do-not-localize/chlimage_1-4.png)

**Título, texto alternativo** : en la pestaña Avanzado, agregue un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**URL, Abrir en** : puede configurar un recurso desde para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-54](assets/chlimage_1-54.png)

**Ajuste preestablecido de visor** - Seleccione un ajuste preestablecido de visualizador existente en el menú desplegable. Si el ajuste preestablecido de visualizador que busca no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. No puede seleccionar un ajuste preestablecido de visualizador si utiliza un ajuste preestablecido de imagen y a la inversa.

**Configuración de Dynamic Media Classic (Scene7)** : seleccione la configuración de Dynamic Media Classic (Scene7) que desee utilizar para recuperar ajustes preestablecidos de imagen activos de SPS.

**Ajuste preestablecido de imagen** - Seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de imagen. No puede seleccionar un ajuste preestablecido de visualizador si utiliza un ajuste preestablecido de imagen y a la inversa.

**Formato de salida** - Seleccione el formato de salida de la imagen, por ejemplo jpeg. En función del formato de salida que seleccione, puede tener opciones de configuración adicionales. Consulte Prácticas recomendadas para ajustes preestablecidos de imagen.

**Enfoque** - Seleccione cómo desea enfocar la imagen. El enfoque se explica en detalle en Prácticas recomendadas para ajustes preestablecidos de imagen y en Prácticas recomendadas para el enfoque.

**Modificadores de URL** : Puede cambiar los efectos de imagen suministrando comandos de imagen S7 adicionales. Estos comandos se describen en Ajustes preestablecidos de imagen y en la Referencia del comando.

**Puntos de interrupción** : Si el sitio web es adaptable, desea ajustar los puntos de interrupción. Los puntos de interrupción deben separarse con comas (,).

### Plantilla de imagen {#image-template}

Las plantillas de imagen de Dynamic Media Classic (Scene7) son contenidos de Photoshop por capas que se importaron a Dynamic Media Classic (Scene7), donde el contenido y las propiedades se parametrizaron para tener en cuenta la variabilidad. El **[!UICONTROL Plantilla de imagen]** Este componente permite importar imágenes y cambiar el texto de forma dinámica en Experience Manager. Además, puede configurar el componente **[!UICONTROL Plantilla de imágenes]** para utilizar valores de ClientContext, de modo que cada usuario experimenta la imagen de una forma personalizada.

Seleccionar **[!UICONTROL Editar]** : para configurar el componente. Puede configurar [configuración común a todos los componentes de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) y otras configuraciones descritas en esta sección.

![chlimage_1-55](assets/chlimage_1-55.png)

**Referencia de archivo, Anchura, Altura** - Consulte [configuración común a todos los componentes de Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Los comandos y parámetros de URL de Dynamic Media Classic (Scene7) no se pueden añadir directamente a la URL de referencia de archivos. Solo se pueden definir en la interfaz de usuario del componente en el panel **[!UICONTROL Parámetro]**.

**Título, texto alternativo** : En la pestaña Plantilla de imagen de Dynamic Media Classic (Scene7) , agregue un título a la imagen y texto alternativo para los usuarios que tengan los gráficos desactivados.

**URL, Abrir en** : puede configurar un recurso desde para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

![chlimage_1-56](assets/chlimage_1-56.png)

**Panel de parámetros** : Al importar una imagen, los parámetros se rellenan previamente con información de la imagen. Si no existe contenido que se pueda cambiar de forma dinámica, esta ventana está vacía.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Cambio del texto de forma dinámica {#changing-text-dynamically}

Para cambiar el texto dinámicamente, introduzca el nuevo texto en los campos y seleccione **[!UICONTROL OK]**. En este ejemplo, el **Precio** es ahora $50 y el envío cuesta 99 centavos.

![chlimage_1-58](assets/chlimage_1-58.png)

El texto de la imagen cambia. Puede restablecer el texto al valor original seleccionando **[!UICONTROL Restablecer]** junto al campo.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Cambiar texto para reflejar el valor de un valor de contexto de cliente {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular un campo a un valor de contexto de cliente, seleccione **[!UICONTROL Seleccionar]** para abrir el menú client-context, seleccione client context y seleccione **[!UICONTROL OK]**. En este ejemplo, el nombre cambia en función de la vinculación de valor de Nombre con el nombre con formato que consta en el perfil.

![chlimage_1-60](assets/chlimage_1-60.png)

El texto refleja el nombre del usuario de la sesión actual. Puede restablecer el texto al valor original seleccionando **[!UICONTROL Restablecer]** junto al campo.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Hacer de la plantilla de imagen de Dynamic Media Classic (Scene7) un vínculo {#making-the-scene-image-template-a-link}

Puede hacer que el componente de plantilla de imagen de Dynamic Media Classic (Scene7) sea un vínculo en el que se puede hacer clic.

1. En la página con el componente de plantilla de imagen de Dynamic Media Classic (Scene7), seleccione **[!UICONTROL Editar]**.
1. En el campo **[!UICONTROL URL]**, introduzca la dirección URL a la que los usuarios se dirigen al hacer clic en la imagen. En el **[!UICONTROL Abrir en]** , seleccione si desea que se abra el destino (una nueva ventana o la misma ventana).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Seleccionar **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL Vídeo]** (disponible en la sección Dynamic Media Classic (Scene7) de la barra de tareas) utiliza la detección de dispositivo y ancho de banda para proporcionar el vídeo adecuado a cada pantalla. Este componente es un reproductor de vídeo HTML5; se trata de un visor único que se puede utilizar en múltiples canales.

Se puede usar para conjuntos de vídeos adaptables, un solo vídeo MP4 o un solo vídeo F4V.

Consulte [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) para obtener más información sobre cómo funcionan los vídeos con la integración de Dynamic Media Classic (Scene7). Además, vea cómo [el **Vídeo de Dynamic Media Classic (Scene7)** El componente se compara con la base **video** componente](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitaciones conocidas del componente de vídeo {#known-limitations-for-the-video-component}

Adobe DAM y WCM muestra si se ha cargado un vídeo de origen principal. No muestran estos recursos de proxy:

* Representaciones codificadas en Dynamic Media Classic (Scene7)
* Conjuntos de vídeos adaptables de Dynamic Media Classic (Scene7)

Cuando se utiliza un conjunto de vídeos adaptable con el componente de vídeo de Dynamic Media Classic (Scene7), se debe cambiar el tamaño del componente para adaptarlo a las dimensiones del vídeo.

## Explorador de contenido de Dynamic Media Classic (Scene7) {#scene-content-browser}

El explorador de contenido Dynamic Media Classic (Scene7) le permite ver contenido de Dynamic Media Classic (Scene7) directamente en Experience Manager. Para acceder al navegador de contenido, en el Buscador de contenido, seleccione **Dynamic Media Classic (Scene7)** en la interfaz de usuario táctil o en el **S7** en la interfaz de usuario clásica de. La funcionalidad es idéntica en ambas interfaces de usuario.

Si tiene varias configuraciones, Experience Manager muestra de forma predeterminada la variable [configuración predeterminada](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puede seleccionar diferentes configuraciones directamente en el explorador de contenido de Dynamic Media Classic (Scene7) en el menú desplegable.

>[!NOTE]
>
>* Los recursos de la carpeta bajo demanda no aparecen en el explorador de contenido de Dynamic Media Classic (Scene7).
>* Cuándo [La previsualización segura está activada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)Sin embargo, los recursos publicados y no publicados en Dynamic Media Classic (Scene7) no aparecen en el explorador de contenido de Dynamic Media Classic (Scene7).
>* Si no ve **[!UICONTROL Dynamic Media Classic (Scene7)]** o el **[!UICONTROL S7]** como opción en el navegador de contenido, debe hacer lo siguiente [configuración de Dynamic Media Classic (Scene7) para que funcione con Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, el explorador de contenido de Dynamic Media Classic (Scene7) admite:
   >   * Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
   >   * Vídeo MP4 único
   >   * Vídeo F4V único


### Examinar contenido {#browsing-content-in-the-classic-ui}

Examine el contenido en Dynamic Media Classic (Scene7) seleccionando la variable **[!UICONTROL S7]** pestaña.

Puede cambiar la configuración a la que accede seleccionando la configuración. Las carpetas cambian según la configuración que seleccione.

![chlimage_1-64](assets/chlimage_1-64.png)

Al igual que ocurre con el buscador de contenido para los recursos, puede buscar recursos y filtrar los resultados. Sin embargo, a diferencia del buscador de recursos, al introducir una palabra clave en la pestaña **S7**, el nombre del archivo **comienza por** la cadena introducida, en lugar de **contener** la palabra clave en el nombre de archivo.

De forma predeterminada, los recursos se muestran por el nombre de archivo. Sin embargo, también puede filtrar los resultados por tipo de recurso.

>[!NOTE]
>
>Para el vídeo, el explorador de contenido Dynamic Media Classic (Scene7) de WCM admite:
>
>* Conjuntos de vídeos adaptables: contenedor de todas las representaciones de vídeo necesarias para la reproducción sin errores en varias pantallas.
>* Vídeo MP4 único
>* Vídeo F4V único
>


### Busque recursos de Dynamic Media Classic (Scene7) con el explorador de contenido {#searching-for-scene-assets-with-the-content-browser}

La búsqueda de recursos de Dynamic Media Classic (Scene7) es similar a la búsqueda de recursos de Experience Manager. La excepción es que, al realizar una búsqueda, realmente ve una vista remota de los recursos en el sistema de Dynamic Media Classic (Scene7), en lugar de importarlos directamente a Experience Manager.

Puede utilizar la interfaz de usuario clásica o la optimizada para el uso táctil para ver y buscar recursos. Según la interfaz, la búsqueda es ligeramente diferente.

Al buscar en cualquier interfaz de usuario, puede filtrar según los criterios siguientes (aquí se muestra la IU optimizada para el uso táctil):

**Escribir palabras clave** : puede buscar recursos por su nombre. Al buscar las palabras clave, escriba el nombre del archivo por el que comienza. Por ejemplo, al escribir la palabra “natación”, el sistema buscaría cualquier nombre de archivo de recurso que comience por esas letras en ese orden. Asegúrese de seleccionar Intro después de escribir el término para buscar el recurso.

![chlimage_1-65](assets/chlimage_1-65.png)

**Carpeta/ruta** : el nombre de la carpeta se basa en la configuración seleccionada. Puede explorar en profundidad los niveles inferiores seleccionando el icono de carpeta y una subcarpeta, y después la marca de verificación para seleccionarla.

Si introduce una palabra clave y selecciona una carpeta, Experience Manager busca en ella y en las subcarpetas. Sin embargo, si no introduce ninguna palabra clave al buscar, al seleccionar la carpeta solo se muestran los recursos de esa carpeta y no se incluye ninguna subcarpeta.

De forma predeterminada, Experience Manager busca en la carpeta seleccionada y en todas las subcarpetas.

![chlimage_1-66](assets/chlimage_1-66.png)

**Tipo de recurso** : seleccione Dynamic Media Classic (Scene7) para examinar el contenido de Dynamic Media Classic (Scene7). Esta opción solo está disponible si se ha configurado Dynamic Media Classic (Scene7).

![chlimage_1-67](assets/chlimage_1-67.png)

**Configuración** : si tiene más de una configuración de Dynamic Media Classic (Scene7) definida en Cloud Services, puede seleccionarla aquí. Como resultado, la carpeta cambia según la configuración elegida.

![chlimage_1-68](assets/chlimage_1-68.png)

**Tipo de recurso** : En el explorador Dynamic Media Classic (Scene7), puede filtrar los resultados para incluir cualquiera de los siguientes elementos: imágenes, plantillas, vídeos y conjuntos de vídeos adaptables. Si no selecciona ningún tipo de recurso, Experience Manager busca de forma predeterminada en todos los tipos de recursos.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* En la interfaz de usuario clásica; también puede buscar **Flash** y **FXG**. No se admite el filtrado para estos dos términos en la IU táctil optimizada.
>
>* Al buscar vídeos, se busca una sola representación. Los resultados devuelven la representación original (solo &#42;.mp4) y la representación codificada.
>* Al buscar en un conjunto de vídeos adaptable, está buscando en la carpeta y en todas las subcarpetas, pero solo si ha añadido una palabra clave a la búsqueda. Si no ha añadido una palabra clave, Experience Manager no busca en las subcarpetas.
>


**Estado de publicación** : puede filtrar por recursos en función del estado de publicación: No publicado o Publicado. Si no selecciona ningún Estado de publicación, el Experience Manager busca de forma predeterminada en todos los estados de publicación.

![chlimage_1-70](assets/chlimage_1-70.png)
