---
title: Uso de la nube de etiquetas de Social
seo-title: Uso de la nube de etiquetas de Social
description: Añadir un componente de Social Tag Cloud en una página
seo-description: Añadir un componente de Social Tag Cloud en una página
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 5%

---


# Uso de Social Tag Cloud {#using-social-tag-cloud}

## Introducción {#introduction}

El componente `Social Tag Cloud` resalta las etiquetas aplicadas por los miembros de la comunidad al publicar contenido. Es una forma de identificar los temas de tendencia y permitir que los visitantes del sitio localicen rápidamente el contenido etiquetado.

Para obtener otro medio de identificar las tendencias actuales, visite [Tendencias de Actividad](trends.md).

Esta página documentos la configuración del cuadro de diálogo del componente `Social Tag Cloud` y describe la experiencia del usuario.

Para obtener información detallada sobre los desarrolladores, consulte [Tag Essentials](tag.md).

Consulte [Administración de etiquetas](../../help/sites-administering/tags.md) para obtener información sobre la creación y administración de etiquetas, así como también sobre las etiquetas de contenido que se han aplicado.

## Añadir una nube de etiquetas de Social {#adding-a-social-tag-cloud}

Para agregar un componente `Social Tag Cloud` a una página en modo de autor, utilice el navegador de componentes para ubicar `Communities / Social Tag Cloud` y arrástrelo a su lugar en una página donde debería aparecer la nube de etiquetas.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](tag.md#essentials-for-client-side), así es como aparecerá el componente `Social Tag Cloud`:

![etiqueta social](assets/social-tag.png)

## Configuración de Social Tag Cloud {#configuring-social-tag-cloud}

Seleccione el componente `Social Tag Cloud` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **[!UICONTROL Social Tag Cloud]**, especifique qué etiquetas mostrar y, si las etiquetas son vínculos activos, la ubicación de la página para los resultados de búsqueda:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Etiquetas sociales para]**
mostrarIdentifique qué etiquetas UGC mostrar. Las opciones desplegables son:

   * `From page and child pages`
   * `All tags`

   El valor predeterminado es `From page and child pages`, donde &quot;page&quot; hace referencia a la configuración **Página** a continuación.

* **[!UICONTROL Página]**

   (Necesario si no es `All tags)` La ruta de acceso a UGC para una página. El valor predeterminado es la página actual si se deja en blanco.

* **[!UICONTROL Sin vínculos ni etiquetas]**

   Si se selecciona, las etiquetas se muestran en la nube de etiquetas como texto sin formato. Si no se selecciona, las etiquetas se muestran como vínculos activos que buscan todo el contenido al que se aplica esa etiqueta. El valor predeterminado no está marcado y requiere que se establezca la **[!UICONTROL ruta de resultados de búsqueda]**.

* **[!UICONTROL Ruta de resultados de búsqueda]**

   La ruta a una página en la que se ha colocado un componente `Search Result`, configurado para hacer referencia a UGC, que incluye la ruta UGC especificada por la configuración **Página**.

## Cambiar la visualización de la nube de etiquetas de Social {#change-display-of-social-tag-cloud}

Para editar la visualización de la **Nube de etiquetas sociales**, introduzca [Modo de diseño](../../help/sites-authoring/default-components-designmode.md) y haga clic en el doble del componente `Social Tag Cloud` ubicado para abrir un cuadro de diálogo con una ficha adicional.

Mediante la ficha **[!UICONTROL Social Tag Cloud (Design)]**, especifique cómo se muestran las etiquetas. Una etiqueta puede ser una etiqueta simple, una sola palabra de la Área de nombres predeterminada o una taxonomía jerárquica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostrar rutas de título completas]**

   Si se selecciona, muestra los títulos de las etiquetas principales y la Área de nombres de cada etiqueta aplicada.

   Por ejemplo:

   * Activados: `Geometrixx Media: Gadgets / Cars`
   * Desactivado: `Cars`

   No hay diferencia para una etiqueta simple.

   El valor predeterminado no está marcado.

* **[!UICONTROL Mostrar solo etiquetas de hoja]**

   Si se selecciona, muestra únicamente las etiquetas aplicadas que no contienen ninguna otra etiqueta.

   Por ejemplo, dado el TagID de:

   `Geometrixx Media: Gadgets / Cars`

   Se pueden aplicar tres etiquetas:

   `Geometrixx Media (the namespace)`,  `Gadgets`y  `Cars`

   * Activado: Solo se mostrará `Cars` si se aplica.
   * Desmarcado: `Geometrixx Media` y `Gadgets`así como `Cars` se mostrarán, si se aplican.

   Una etiqueta simple es una etiqueta de hoja.

   El valor predeterminado no está marcado.

* **[!UICONTROL Plantilla de vínculo]**

   Una plantilla, distinta de la predeterminada, que se utiliza para mostrar los vínculos en una nube de etiquetas, cuando los vínculos se activan mediante el cuadro de diálogo de edición de componentes.

* **[!UICONTROL Mismo tamaño para todas las etiquetas]**

   Si se selecciona, todas las palabras de la nube de etiquetas tienen el mismo estilo. Si no se selecciona, el estilo de las palabras varía en función de su uso. El valor predeterminado no está marcado.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Tag Essentials](tag.md) para desarrolladores.

Consulte [Etiquetado de contenido generado por el usuario](tag-ugc.md) (UGC) para obtener información sobre cómo crear y administrar etiquetas.
