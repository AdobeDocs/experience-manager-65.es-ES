---
title: Uso de Social Tag Cloud
description: Aprenda a añadir un componente de Nube de etiquetas social a una página que permita a los miembros de la comunidad conectados identificar rápidamente los temas de tendencia y localizar el contenido etiquetado.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---

# Uso de Social Tag Cloud {#using-social-tag-cloud}

## Introducción {#introduction}

El `Social Tag Cloud` el componente resalta las etiquetas aplicadas por los miembros de la comunidad al publicar contenido. Es un medio para identificar los temas de tendencia y permitir que los visitantes del sitio localicen rápidamente el contenido etiquetado.

Si desea conocer otras formas de identificar las tendencias actuales, visite [Tendencias de actividades](trends.md).

Esta página documenta los `Social Tag Cloud` configuración del cuadro de diálogo de componentes y describe la experiencia del usuario.

Para obtener información detallada para los desarrolladores, consulte [Tag Essentials](tag.md).

Consulte [Administración de etiquetas](../../help/sites-administering/tags.md) para obtener información sobre cómo crear y administrar etiquetas, y a qué etiquetas de contenido se han aplicado.

## Adición de una nube de etiquetas social {#adding-a-social-tag-cloud}

Para agregar un `Social Tag Cloud` a una página en modo de autor, utilice el navegador de componentes para localizar `Communities / Social Tag Cloud` y arrástrela a su lugar en una página en la que debería aparecer la nube de etiquetas.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](tag.md#essentials-for-client-side) están incluidos, así es como se `Social Tag Cloud` el componente aparece:

![social-tag](assets/social-tag.png)

## Configuración de Social Tag Cloud {#configuring-social-tag-cloud}

Seleccione el colocado `Social Tag Cloud` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En el **[!UICONTROL Nube de etiquetas social]** , especifique qué etiquetas mostrar y, si las etiquetas son vínculos activos, la ubicación de la página para los resultados de búsqueda:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Etiquetas sociales para mostrar]**
Identifique las etiquetas UGC que desea mostrar. Las opciones desplegables son:

   * `From page and child pages`
   * `All tags`

  El valor predeterminado es `From page and child pages`, donde &quot;página&quot; hace referencia a **Página** configuración a continuación.

* **[!UICONTROL Página]**

  (Obligatorio si no `All tags)` La ruta al UGC para una página. Si se deja en blanco, la página actual es la predeterminada.

* **[!UICONTROL Sin vínculos ni etiquetas]**

  Si se selecciona, las etiquetas se muestran en la nube de etiquetas como texto sin formato. Si no se selecciona, las etiquetas se muestran como vínculos activos que buscan todo el contenido al que se aplica esa etiqueta. El valor predeterminado está desmarcado y requiere **[!UICONTROL Ruta de resultados de búsqueda]** que se va a establecer.

* **[!UICONTROL Ruta de resultados de búsqueda]**

  La ruta a una página en la que `Search Result` El componente se ha colocado, configurado para hacer referencia a UGC que incluye la ruta UGC especificada por el **Página** configuración.

## Cambiar la visualización de Nube de etiquetas social {#change-display-of-social-tag-cloud}

Para editar la visualización de **Nube de etiquetas social**, introduzca [Modo de diseño](../../help/sites-authoring/default-components-designmode.md) y haga doble clic en el elemento colocado `Social Tag Cloud` para abrir un cuadro de diálogo con una pestaña adicional.

Uso del **[!UICONTROL Nube de etiquetas social (Diseño)]** , especifique cómo se muestran las etiquetas. Una etiqueta puede ser una etiqueta simple, una sola palabra en el área de nombres predeterminada o una taxonomía jerárquica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostrar rutas de título completas]**

  Si se selecciona, muestra los títulos de las etiquetas principales y el área de nombres de cada etiqueta aplicada.

  Por ejemplo:

   * Comprobado: `Geometrixx Media: Gadgets / Cars`
   * Desactivado: `Cars`

  No hay diferencia para una etiqueta simple.

  El valor predeterminado está desmarcado.

* **[!UICONTROL Mostrar solo etiquetas de hoja]**

  Si se selecciona esta opción, solo se muestran las etiquetas aplicadas que no contienen otras etiquetas.

  Por ejemplo, dado el TagID de:

  `Geometrixx Media: Gadgets / Cars`

  Se pueden aplicar tres etiquetas:

  `Geometrixx Media (the namespace)`, `Gadgets`, y `Cars`

   * Activado: solo `Cars` se muestran, si se aplican.
   * Desactivado: `Geometrixx Media`, `Gadgets`, y `Cars` se muestran, si se aplican.

  Una etiqueta simple es una etiqueta de hoja.

  El valor predeterminado está desmarcado.

* **[!UICONTROL Plantilla de vínculo]**

  Una plantilla, que no es una predeterminada, utilizada para mostrar los vínculos en una nube de etiquetas cuando los vínculos están habilitados a través del cuadro de diálogo de edición de componentes.

* **[!UICONTROL Mismo tamaño para todas las etiquetas]**

  Si se selecciona, todas las palabras de la nube de etiquetas tienen el mismo estilo. Si no se selecciona, las palabras tienen un estilo diferente según su uso. El valor predeterminado está desmarcado.

## Información adicional {#additional-information}

Puede encontrar más información en la [Tag Essentials](tag.md) para desarrolladores.

Consulte [Etiquetado del contenido generado por el usuario](tag-ugc.md) (UGC) para obtener información sobre cómo crear y administrar etiquetas.
