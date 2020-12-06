---
title: Facetas de búsqueda para filtrar los resultados de búsqueda
description: Cómo crear, modificar y utilizar facetas de búsqueda en [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: adeb20c1e7222e7c5702061cba73350002f5154c
workflow-type: tm+mt
source-wordcount: '2424'
ht-degree: 17%

---


# Facetas de búsqueda {#search-facets}

Una implementación en toda la empresa de [!DNL Adobe Experience Manager Assets] tiene la capacidad de almacenar muchos recursos. A veces, encontrar el recurso correcto puede ser difícil y llevar mucho tiempo si sólo se utilizan las capacidades de búsqueda genéricas de [!DNL Experience Manager].

Utilice las facetas de búsqueda del panel Filtros para agregar más granularidad a la experiencia de búsqueda y hacer que la funcionalidad de búsqueda sea más eficiente y versátil. Las facetas de búsqueda agregan varias dimensiones (predicados) que le permiten realizar búsquedas más complejas. El panel Filtros incluye algunas facetas estándar. También puede agregar facetas de búsqueda personalizadas.

En resumen, las facetas de búsqueda permiten buscar recursos de varias formas en lugar de hacerlo en un único orden taxonómico predeterminado. Puede desplazarse fácilmente hasta el nivel de detalle deseado para una búsqueda más enfocada.

Por ejemplo, si busca una imagen, puede elegir si desea un mapa de bits o una imagen vectorial. Puede reducir aún más el alcance de la búsqueda especificando el tipo MIME para la imagen. Del mismo modo, al buscar documentos, puede especificar el formato, por ejemplo PDF o MS Word.

## Añadir un predicado {#adding-a-predicate}

Las facetas de búsqueda que aparecen en el panel Filtros se definen en el formulario de búsqueda subyacente mediante predicados. Para mostrar más o diferentes facetas, agregue predicados al formulario predeterminado o utilice un formulario personalizado que incluya facetas de su elección.

Para las búsquedas de texto completo, agregue el predicado [!UICONTROL Texto completo] al formulario. Utilice el predicado Propiedad para buscar recursos que coincidan con una sola propiedad especificada. Utilice el predicado Opciones para buscar recursos que coincidan con uno o varios valores de una propiedad concreta. Añada el predicado Intervalo de fechas para buscar recursos creados dentro de un intervalo de fechas especificado.

1. Haga clic en el logotipo [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página Buscar en Forms, seleccione **[!UICONTROL Raíl de búsqueda de administración de recursos]** y haga clic en **[!UICONTROL Editar]** ![icono de edición](assets/do-not-localize/aemassets_edit.png).

   ![Busque y seleccione los recursos o el carril de búsqueda de administrador](assets/assets_admin_searchrail.png)

   >[!NOTE]
   >
   >Para utilizar la funcionalidad de búsqueda de carpetas desde el **carril de búsqueda de administración de recursos** preconfigurado de una versión anterior, lleve a cabo los siguientes pasos:
   >
   >1. Vaya a `/conf/global/settings/dam/search/facets/assets/jcr:content/items` en CRXDE.
   >1. Elimine el nodo **type**.
   >1. Desde la ruta `/libs/settings/dam/search/facets/assets/jcr:content/items`, copie los nodos `asset`, `directory`, `typeor`, `excludepaths` y `searchtype` a la ruta mencionada en el paso 1.
   >1. Guarde los cambios.


1. En la página [!UICONTROL Editar búsqueda en Forms], arrastre un predicado de la ficha **[!UICONTROL Seleccionar predicado]** al panel principal. Por ejemplo, arrastre **[!UICONTROL Predicado de propiedades]**.

   ![Seleccionar y mover un predicado para personalizar los filtros de búsqueda](assets/drag_predicate.png)

   *Figura: Seleccione y mueva un predicado para personalizar los filtros de búsqueda.*

1. En la ficha [!UICONTROL Configuración], introduzca una etiqueta de campo, texto de marcador de posición y descripción para el predicado. Especifique un nombre válido para la propiedad de metadatos que desea asociar con el predicado. La etiqueta de encabezado de la ficha [!UICONTROL Configuración] identifica el tipo del predicado seleccionado.

1. En el campo **[!UICONTROL Nombre de propiedad]**, indique un nombre válido para la propiedad de metadatos que desea asociar al predicado. Es el nombre sobre el cual se realiza la búsqueda. Por ejemplo, escriba `jcr:content/metadata/dc:description` o `./jcr:content/metadata/dc:description`.

   También puede seleccionar un nodo existente en el cuadro de diálogo de selección.

   ![Asociación de una propiedad de metadatos con un predicado en el campo Nombre de propiedad](assets/property_settings.png)

   Asociación de una propiedad de metadatos con un predicado en el campo Nombre de propiedad

1. Haga clic en la **[!UICONTROL Previsualización]** ![previsualización](assets/do-not-localize/preview_icon.png) para generar una previsualización del panel Filtros tal como aparece después de agregar el predicado.
1. Revise la presentación del predicado en el modo de Previsualización.

   ![Previsualización del formulario de búsqueda antes de enviar los cambios](assets/preview-1.png)

   Previsualización del formulario de búsqueda antes de enviar los cambios

1. Para cerrar la previsualización, haga clic en **[!UICONTROL Cerrar]** ![cerrar](assets/do-not-localize/close.png) en la esquina superior derecha de la previsualización.
1. Haga clic en **[!UICONTROL Listo]** para guardar la configuración.
1. Vaya al panel Buscar en la interfaz de usuario [!DNL Assets]. El predicado Propiedad se agrega al panel.
1. Escriba una descripción del recurso que se buscará en el cuadro de texto. Por ejemplo, escriba `Adobe`. Cuando realiza una búsqueda, los recursos con una descripción que coincide con `Adobe` se enumeran en los resultados de la búsqueda.

## Añadir un predicado de opciones {#adding-an-options-predicate}

El predicado Opciones permite agregar varias opciones de búsqueda en el panel Filtros. Puede seleccionar una o varias de estas opciones en el panel Filtros para buscar recursos. Por ejemplo, para buscar recursos en función del tipo de archivo, configure opciones como Imágenes, Multimedia, Documentos y Archivos en el formulario de búsqueda. Después de configurar estas opciones, la búsqueda se realiza en recursos de tipo GIF, JPEG, PNG, etc., al seleccionar la opción Imágenes en el panel Filtros.

Para asignar las opciones a la propiedad correspondiente, cree una estructura de nodos para las opciones y proporcione la ruta del nodo principal en la propiedad Nombre de propiedad del predicado Opciones. El nodo principal debe ser de tipo `sling`: `OrderedFolder`. Las opciones deben ser de tipo `nt:unstructured`. Los nodos de opciones deben tener configuradas las propiedades `jcr:title` y `value`.

La propiedad `jcr:title` es un nombre práctico para la opción que se muestra en el panel Filtros. El campo `value` se utiliza en la consulta para coincidir con la propiedad especificada.

Al seleccionar una opción, la búsqueda se realiza en función de la propiedad `value` del nodo de opciones y sus nodos secundarios, si los hay. Se atraviesa todo el árbol bajo el nodo de opciones y se combina la propiedad `value` de cada nodo secundario mediante una operación OR para formar la consulta de búsqueda.

Por ejemplo, si selecciona “Imágenes” para los tipos de archivo, la consulta de búsqueda de los recursos se genera combinando la propiedad `value` mediante una operación O. Por ejemplo, la búsqueda de imágenes se genera combinando los resultados coincidentes para *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, e *image/tiff* `jcr:content/metadata/dc:format` para la propiedad mediante una operación OR.

![La propiedad Value de un tipo de archivo, como se ve en CRXDE, se utiliza para que funcionen las consultas de búsqueda](assets/filetype-value-property.png)

La propiedad Value de un tipo de archivo, como se ve en CRXDE, se utiliza para que funcionen las consultas de búsqueda

En lugar de crear manualmente una estructura de nodos para las opciones del repositorio CRXDE, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Nombre de propiedad]**. Por ejemplo, puede definir los pares clave-valor `image/bmp`, `image/gif`, `image/jpeg` y `image/png`, y especificar sus valores como se muestra en el siguiente archivo JSON de muestra. En el campo **[!UICONTROL Nombre de propiedad]**, puede especificar la ruta de CRXDE para este archivo.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Si desea utilizar un nodo existente, especifíquelo mediante el cuadro de diálogo de selección.

>[!NOTE]
>
>El predicado Opciones es un contenedor personalizado que incluye predicados de propiedades para mostrar el comportamiento descrito. Actualmente, no hay ningún extremo REST disponible para admitir la funcionalidad de forma nativa.

1. Haga clic en el logotipo [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página **[!UICONTROL Buscar en Forms]**, seleccione **[!UICONTROL Raíl de búsqueda de administración de recursos]** y haga clic en **[!UICONTROL Editar]**.
1. En la página **[!UICONTROL Editar formulario de búsqueda]**, arrastre **[!UICONTROL Predicado de opciones]** desde la pestaña **[!UICONTROL Seleccionar predicado]** al panel principal.
1. En la pestaña **[!UICONTROL Configuración]**, indique una etiqueta y un nombre para la propiedad. Por ejemplo, para buscar recursos en función de su formato, especifique un nombre práctico para la etiqueta, por ejemplo, **[!UICONTROL Tipo de archivo]**. Indique la propiedad en función de la cual se realizará la búsqueda en el campo de propiedad, por ejemplo `jcr:content/metadata/dc:format.`
1. Realice una de las acciones siguientes:

   * En el campo **[!UICONTROL Nombre de propiedad]**, mencione la ruta del archivo JSON donde define los nodos para las opciones y especifique los pares de clave-valor correspondientes.
   * Haga clic en el símbolo `+` situado junto al campo Opciones para especificar el texto y el valor de visualización de las opciones que desea proporcionar en el panel Filtros. Para agregar otra opción, haga clic en el símbolo `+` y repita el paso.

1. Compruebe que la opción **[!UICONTROL Selección única]** se borra para que el usuario pueda seleccionar varias opciones a la vez para diferentes tipos de archivos (por ejemplo, imágenes, documentos, multimedia y archivos). Si elige **[!UICONTROL Selección única]**, el usuario solo puede seleccionar una opción para diferentes tipos de archivo a la vez.

   ![Campos disponibles en el predicado Opciones](assets/options_predicate.png)

   Campos disponibles en el predicado Opciones

1. En el campo **[!UICONTROL Descripción]**, introduzca una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Buscar. El predicado Opciones se agrega al panel **Buscar**. Las opciones para **[!UICONTROL Tipo de archivo]** se muestran como casillas de verificación.

## Añadir un predicado de propiedades de varios valores {#adding-a-multi-value-property-predicate}

El predicado de propiedades de varios valores permite buscar varios valores en los recursos. Imagine un escenario en el que tiene imágenes de varios productos en [!DNL Assets] y los metadatos de cada imagen incluyen un número de SKU asociado al producto. Puede utilizar este predicado para buscar imágenes de producto basadas en varios números de SKU.

1. Haga clic en el logotipo [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página Buscar en Forms, seleccione **[!UICONTROL Raíl de búsqueda de administración de recursos]** y haga clic en **[!UICONTROL Editar]** ![icono de edición](assets/do-not-localize/aemassets_edit.png).
1. En la página Editar formulario de búsqueda, arrastre un **[!UICONTROL predicado de propiedades de varios valores]** desde la pestaña **[!UICONTROL Seleccionar predicado]** hasta el panel principal.
1. En la ficha **[!UICONTROL Configuración]**, introduzca una etiqueta y un texto de marcador de posición para el predicado. Especifique el nombre de propiedad en función del cual se realizará la búsqueda en el campo de propiedad, por ejemplo `jcr:content/metadata/dc:value`. También puede utilizar el cuadro de diálogo de selección para seleccionar un nodo.
1. Asegúrese de que la opción **[!UICONTROL Compatibilidad con delimitadores]** está seleccionada. En el campo **[!UICONTROL Delimitadores de entrada]**, especifique delimitadores para separar valores individuales. De forma predeterminada, se especifica una coma como delimitador. Puede especificar un delimitador diferente.
1. En el campo **Descripción**, introduzca una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Filtros de la interfaz de usuario [!DNL Assets]. El predicado **[!UICONTROL Propiedad de varios valores]** se agrega al panel.
1. Especifique varios valores en el campo Valor múltiple separado por los delimitadores y realice la búsqueda. El predicado obtiene una coincidencia de texto exacta para los valores especificados.

## Añadir un predicado de etiquetas {#adding-a-tags-predicate}

El predicado de etiquetas permite realizar búsquedas de recursos basadas en etiquetas. De forma predeterminada, [!DNL Assets] busca en los recursos una o varias etiquetas coincidentes en función de las etiquetas que especifique. En otras palabras, la consulta de búsqueda realiza una operación O utilizando las etiquetas especificadas. Sin embargo, puede utilizar la opción de coincidencia con todas las etiquetas para buscar recursos que incluyan todas las etiquetas que especifique.

1. Haga clic en el logotipo [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página Buscar en Forms, seleccione **[!UICONTROL Raíl de búsqueda de administración de recursos]** y haga clic en **[!UICONTROL Editar]** ![icono de edición](assets/do-not-localize/aemassets_edit.png).
1. En la página Editar formulario de búsqueda, arrastre **[!UICONTROL Predicado de etiquetas]** de la ficha Seleccionar predicado al panel principal.
1. En la ficha Configuración, introduzca un texto de marcador de posición para el predicado. Especifique el nombre de propiedad en función del cual se realizará la búsqueda en el campo de propiedad, por ejemplo *jcr:content/metadata/cq:tags*. También puede seleccionar un nodo en CRXDE desde el cuadro de diálogo de selección.
1. Configure la propiedad de ruta de las etiquetas raíz de este predicado para rellenar varias etiquetas en la lista Etiquetas.
1. Seleccione la opción **[!UICONTROL Mostrar todas las etiquetas]** para buscar recursos que incluyan todas las etiquetas que especifique.

1. En el campo **[!UICONTROL Descripción]**, introduzca una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Buscar. El predicado **[!UICONTROL Etiquetas]** se agrega al panel Buscar.
1. Especifique las etiquetas en función de las cuales desee buscar recursos o seleccione entre la lista de sugerencias.

1. Seleccione **[!UICONTROL Coincidir con todo]** para buscar coincidencias que incluyan todas las etiquetas que especifique.

## Añadir otros predicados {#adding-other-predicates}

De forma similar a como se agrega un predicado de propiedad o un predicado de opciones, se pueden agregar los siguientes predicados adicionales al panel Buscar:

| Nombre del predicado | Descripción | Propiedades |
|---|---|---|
| [!UICONTROL Texto completo] | El predicado de búsqueda realiza una búsqueda de texto completo en todo un nodo de recursos. Se asigna con el operador jcr:contains. Puede especificar una ruta relativa si desea realizar una búsqueda de texto completo en una parte específica del nodo de recursos. | <ul><li>Etiqueta</li><li>Marcador de posición</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Navegador de rutas] | Buscar predicado para buscar recursos en carpetas y subcarpetas en una ruta raíz preconfigurada | <ul><li>Marcador de posición</li><li>Ruta raíz</li><li>Descripción</li></ul> |
| [!UICONTROL Ruta] | Utilícelo para filtrar los resultados según la ubicación. Puede especificar diferentes rutas como opciones. | <ul><li>Etiqueta</li><li>Ruta</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de publicación] | Buscar predicado para buscar recursos en función de su estado de publicación | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Fecha relativa] | El predicado de búsqueda busca recursos en función de la fecha relativa de su creación. Por ejemplo, puede configurar opciones, como hace 2 meses, hace 3 semanas, etc. | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Fecha relativa</li></ul> |
| [!UICONTROL Intervalo] | El predicado de búsqueda busca recursos que se encuentran dentro de un rango especificado. En el panel Buscar, puede especificar los valores mínimo y máximo para el rango. | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Intervalo de fechas] | El predicado de búsqueda busca recursos creados dentro de un intervalo especificado para una propiedad de fecha. En el panel Buscar, puede especificar las fechas de Inicio y de finalización mediante selectores de fecha. | <ul><li>Etiqueta</li><li>Marcador de posición</li><li>Nombre de la propiedad </li><li>Texto de rango (Desde)</li><li>Texto de intervalo (hasta)</li><li>Descripción</li></ul> |
| [!UICONTROL Fecha] | Busque en el predicado una búsqueda de recursos basada en deslizadores basada en una propiedad de fecha. | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Tamaño del archivo] | El predicado de búsqueda busca recursos en función de su tamaño. Se trata de un predicado basado en el silenciador en el que se seleccionan las opciones del deslizador de un nodo configurable. Las opciones predeterminadas se definen en /libs/dam/options/predicates/filesize en el repositorio de CRXDE. El tamaño del archivo se proporciona en bytes. | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Ruta</li><li>Descripción</li></ul> |
| [!UICONTROL Última modificación del recurso] | Buscar predicado para buscar recursos modificados recientemente | <ul><li>Nombre de la propiedad </li><li>Valor de propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de publicación] | Buscar predicado para buscar recursos en función de su estado de publicación | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Clasificación] | Buscar predicado para buscar recursos en función de su clasificación promedio | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Ruta de opción</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de caducidad] | Buscar predicado para buscar recursos en función de su estado de caducidad | <ul><li>Etiqueta</li><li>Nombre de la propiedad </li><li>Descripción</li></ul> |
| [!UICONTROL Oculto] | Predicado de búsqueda que define una propiedad de campo oculto para buscar recursos | <ul><li>Nombre de la propiedad </li><li>Valor de propiedad</li><li>Descripción</li></ul> |

## Restaurar las facetas de búsqueda predeterminadas {#restoring-default-search-facets}

De forma predeterminada, aparece un icono de bloqueo ![icono de bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg) antes de **[!UICONTROL Raíl de búsqueda de administración de recursos]** en la página **[!UICONTROL Buscar en Forms]**. El icono Bloquear en una opción de la página Buscar en Forms indica que la configuración predeterminada está intacta y no está personalizada. El icono ![bloquear icono cerrado](assets/do-not-localize/lock_closed_icon.svg) desaparece si agrega facetas de búsqueda al formulario que indican que se ha modificado el formulario predeterminado.

![El icono Bloquear en una opción de la página Buscar en Forms indica que la configuración predeterminada está intacta y no está personalizada.](assets/locked_admin_rail.png)

Para restaurar la faceta de búsqueda predeterminada, realice los siguientes pasos:

1. Seleccione **[!UICONTROL Raíl de búsqueda de administración de recursos]** en la página **[!UICONTROL Buscar en Forms]**.
1. Haga clic en **[!UICONTROL Eliminar]** ![eliminar contorno](assets/do-not-localize/deleteoutline.png) en la barra de herramientas.
1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Eliminar]** para eliminar los cambios personalizados.

   Después de eliminar los cambios personalizados en las facetas de búsqueda, el icono de bloqueo ![icono de bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg) vuelve a aparecer antes que **[!UICONTROL Raíl de búsqueda de administración de recursos]** en la página **[!UICONTROL Buscar en Forms]**.

## Permisos de usuario {#user-permissions}

Si no se le asigna una función de administrador, aquí tiene una lista de permisos que necesita para realizar acciones de edición, eliminación y previsualización que involucran facetas de búsqueda.

| Acción | Permisos    |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Editar] | Permisos de lectura y escritura en el nodo `/apps` de CRXDE |
| [!UICONTROL Eliminar] | Permisos de lectura, escritura y eliminación en el nodo `/apps` de CRXDE |
| [!UICONTROL Vista previa] | Permisos de lectura, escritura y eliminación en el nodo `/var/dam/content` de CRXDE. Además, los permisos de lectura y escritura en el nodo `/apps`. |

>[!MORELIKETHIS]
>
>* [Ampliar la capacidad de búsqueda de recursos](searchx.md)
>* [Buscar recursos](search-assets.md)

