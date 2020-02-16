---
title: Administración de búsquedas y etiquetas inteligentes
description: Actualice o elimine las etiquetas inteligentes imprecisas para mejorar la relevancia de las etiquetas
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Administración de búsquedas y etiquetas inteligentes {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta incorrecta que se haya asignado a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a restringir las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas aparezcan en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a una imagen. La promoción de una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se realiza una búsqueda en función de la etiqueta en particular.

1. En el cuadro OmniSearch, busque recursos basados en una etiqueta.
1. Inspeccione los resultados de la búsqueda para identificar una imagen que no considere relevante para la búsqueda.
1. Seleccione la imagen y, a continuación, toque **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]** , inspeccione las etiquetas. Si no desea buscar la imagen en función de una etiqueta específica, seleccione la etiqueta y, a continuación, toque **[!UICONTROL Eliminar]** en la barra de herramientas. También puede tocar o hacer clic en el símbolo que aparece junto a la etiqueta. `X`
1. Para asignar una clasificación superior a una etiqueta, seleccione la etiqueta y toque **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta promocionada se mueve a la sección **[!UICONTROL Etiquetas]** .
1. Toque o haga clic en **[!UICONTROL Guardar]** y, a continuación, toque o haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo de éxito.
1. Vaya a la página de propiedades de la imagen. Observe que la etiqueta promocionada tiene una alta relevancia y, por lo tanto, aparece más arriba en los resultados de búsqueda.

## Comprender los resultados de búsqueda de AEM con etiquetas inteligentes {#understandsearch}

De forma predeterminada, la búsqueda de AEM combina los términos de búsqueda con una `AND` cláusula. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una `OR` cláusula adicional para encontrar cualquiera de los términos de búsqueda en las etiquetas inteligentes de aplicación. For example, consider searching for `woman running`. Los recursos con solo `woman` o solamente `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, en una consulta de búsqueda de este tipo aparece un recurso etiquetado con etiquetas inteligentes `woman` o `running` con etiquetas inteligentes. Los resultados de la búsqueda son una combinación de:

* recursos con `woman` y `running` palabras clave en los metadatos.

* los recursos se etiquetaron de forma inteligente con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. coincidencias de en `woman running` los distintos campos de metadatos.
1. coincidencias de `woman running` en etiquetas inteligentes.
1. coincidencias de `woman` o de `running` en etiquetas inteligentes.
