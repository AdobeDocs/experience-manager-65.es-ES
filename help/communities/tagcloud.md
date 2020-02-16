---
title: Uso de la nube de etiquetas de Social
seo-title: Uso de la nube de etiquetas de Social
description: Adición de un componente de Social Tag Cloud a una página
seo-description: Adición de un componente de Social Tag Cloud a una página
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de la nube de etiquetas de Social {#using-social-tag-cloud}

## Introducción {#introduction}

El `Social Tag Cloud` componente resalta las etiquetas aplicadas por los miembros de la comunidad al publicar contenido. Es un medio para identificar los temas de tendencia y permitir que los visitantes del sitio localicen rápidamente el contenido etiquetado.

Para obtener otro modo de identificar las tendencias actuales, visite Tendencias [de](trends.md)actividad.

Esta página documenta la configuración del cuadro de diálogo del `Social Tag Cloud` componente y describe la experiencia del usuario.

Para obtener información detallada sobre los desarrolladores, consulte [Tag Essentials](tag.md).

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Adición de una nube de etiquetas de Social {#adding-a-social-tag-cloud}

Para agregar un `Social Tag Cloud` componente a una página en modo de autor, utilice el navegador de componentes para buscarlo `Communities / Social Tag Cloud` y arrastrarlo a su lugar en una página en la que debería aparecer la nube de etiquetas.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](tag.md#essentials-for-client-side) necesarias, así es como aparecerá el `Social Tag Cloud` componente:

![chlimage_1-303](assets/chlimage_1-303.png)

## Configuración de Social Tag Cloud {#configuring-social-tag-cloud}

Seleccione el componente colocado al que desea acceder y seleccione el `Social Tag Cloud` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-304](assets/chlimage_1-304.png)

En la ficha **[!UICONTROL Social Tag Cloud]** , especifique qué etiquetas mostrar y, si las etiquetas son vínculos activos, la ubicación de la página para los resultados de búsqueda.:

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL Etiquetas sociales para mostrar]** Identifique qué etiquetas UGC mostrar. Las opciones desplegables son

   * `From page and child pages`
   * `All tags`
   El valor predeterminado es `From page and child pages`, donde &quot;página&quot; se refiere a la configuración de **página** siguiente.

* **[!UICONTROL Página]**(obligatorio si no es `All tags)` la ruta de acceso a UGC de una página. El valor predeterminado es la página actual si se deja en blanco.

* **[!UICONTROL No hay vínculos en las etiquetas]** Si se selecciona, las etiquetas se muestran en la nube de etiquetas como texto sin formato. Si no se selecciona, las etiquetas se muestran como vínculos activos que buscan todo el contenido al que se aplica esa etiqueta. El valor predeterminado no está marcado y requiere que se establezca la ruta **[!UICONTROL de resultados de]** búsqueda.

* **[!UICONTROL Ruta]** del resultado de la búsquedaRuta a una página en la que se ha colocado un `Search Result` componente, configurada para hacer referencia a UGC, que incluye la ruta UGC especificada por la configuración de la **página** .

## Cambiar la visualización de la nube de etiquetas sociales {#change-display-of-social-tag-cloud}

Para editar la visualización de **Social Tag Cloud**, introduzca el modo [de](../../help/sites-authoring/default-components-designmode.md) diseño y haga doble clic en el componente colocado `Social Tag Cloud` para abrir un cuadro de diálogo con una ficha adicional.

En la ficha **[!UICONTROL Social Tag Cloud (Diseño)]** , especifique cómo se muestran las etiquetas. Una etiqueta puede ser una etiqueta simple, una sola palabra en el espacio de nombres predeterminado o una taxonomía jerárquica:

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL Mostrar rutas]** de título completas Si se selecciona, muestra los títulos de las etiquetas principales y el espacio de nombres de cada etiqueta aplicada.

   Por ejemplo:

   * Activados: `Geometrixx Media: Gadgets / Cars`
   * Desactivado: `Cars`
   No hay diferencia para una etiqueta simple.

   El valor predeterminado no está marcado.

* **[!UICONTROL Mostrar solo etiquetas]** de hoja Si está activada, solo muestra las etiquetas aplicadas que no contienen ninguna otra etiqueta.

   Por ejemplo, dado el TagID de

   `Geometrixx Media: Gadgets / Cars`

   Se pueden aplicar tres etiquetas: `Geometrixx Media (the namespace)`, `Gadgets`y `Cars`

   * Activado: solo `Cars` se mostrará si se aplica
   * Desmarcado: `Geometrixx Media` y `Gadgets`así como `Cars` se mostrará, si se aplica
   Una etiqueta simple es una etiqueta de hoja.

   El valor predeterminado no está marcado.

* **[!UICONTROL Plantilla]** de vínculo Una plantilla, distinta de la predeterminada, que se utiliza para mostrar los vínculos en una nube de etiquetas, cuando los vínculos se activan mediante el cuadro de diálogo de edición de componentes.

* **[!UICONTROL El mismo tamaño para todas las etiquetas]** Si se selecciona, todas las palabras de la nube de etiquetas tienen el mismo estilo. Si no se selecciona, el estilo de las palabras varía en función de su uso. El valor predeterminado no está marcado.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Tag Essentials](tag.md) para desarrolladores.

Consulte [Etiquetado de contenido](tag-ugc.md) generado por el usuario (UGC) para obtener información sobre la creación y administración de etiquetas.
