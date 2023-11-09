---
title: Búsqueda completa
description: Encuentre su contenido más rápidamente con una búsqueda completa.
uuid: 21605b96-b467-4d01-9a64-9d0648d539f1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 4ec15013-f7ab-44d6-8053-ed28b14f95e2
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 68%

---

# Búsqueda{#searching}

El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.

>[!NOTE]
>
>Fuera del entorno de creación, también hay otros mecanismos disponibles para la búsqueda, como el [Generador de consultas](/help/sites-developing/querybuilder-api.md) y [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Conceptos básicos de búsqueda {#search-basics}

La función de búsqueda está disponible en la barra de herramientas superior:

![Buscar](do-not-localize/chlimage_1-17.png)

Con el carril de búsqueda puede:

* Busque una palabra clave, una ruta o una etiqueta específicas..
* Filtre según criterios específicos de recurso, como fechas de modificación, estados de página, tamaño de archivo, etc.
* Defina y utilice una [búsqueda guardada](#saved-searches) según los criterios anteriores.

>[!NOTE]
>
>También se puede iniciar una búsqueda con la tecla de función `/` (barra diagonal) cuando el carril de búsqueda esté visible.

## Buscar y filtrar {#search-and-filter}

Para buscar y filtrar sus recursos: 

1. Abra **Buscar** (con la lupa de la barra de herramientas) y escriba el término de búsqueda. Se muestran sugerencias que puede seleccionar:

   ![s-01](assets/s-01.png)

   De forma predeterminada, los resultados de la búsqueda estarán limitados a su ubicación actual (es decir, la consola y el tipo de recurso relacionado):

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. Si es necesario, puede quitar el filtro de ubicación (seleccione **X** en el filtro que desea eliminar) para buscar en todas las consolas/tipos de recursos.
1. Los resultados se muestran agrupados según la consola y el tipo de recurso relacionado.

   Puede seleccionar un recurso específico (para realizar más acciones), o profundizar seleccionando el tipo de recurso necesario; por ejemplo, **Ver todos los sitios**:

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. Si desea explorar más en profundidad, seleccione el símbolo de carril (parte superior izquierda) para abrir el panel lateral **Filtros y opciones**.

   ![Filtros y opciones](do-not-localize/screen_shot_2018-03-23at101542.png)

   Según el tipo de recurso, la búsqueda mostrará una selección predefinida de criterios de búsqueda o de filtro.

   El panel lateral permite seleccionar:

   * Búsquedas guardadas
   * Directorio de búsqueda
   * Etiquetas
   * Criterios de búsqueda; por ejemplo, fechas de modificación, estado de publicación o estado de LiveCopy

   >[!NOTE]
   >
   >Los criterios de búsqueda pueden variar:
   >
   >
   >
   >    * Según el tipo de recurso que haya seleccionado; por ejemplo, los criterios de Assets y Comunidades son comprensiblemente especializados.
   >    * Su instancia como [Buscar Forms](/help/sites-administering/search-forms.md) AEM se puede personalizar (según la ubicación dentro de la ubicación de la).
   >
   >

   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. También se pueden agregar términos de búsqueda adicionales:

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. Cierre **Buscar** con la **X** (parte superior derecha).

>[!NOTE]
>
>Los criterios de búsqueda se mantienen al seleccionar un elemento en los resultados de la búsqueda.
>
>Cuando se selecciona un elemento en la página de resultados de la búsqueda, al volver a la página de búsqueda después de usar el botón Atrás del explorador, los criterios de búsqueda se mantienen. 

## Búsquedas guardadas {#saved-searches}

Además de buscar aplicando una amplia gama de criterios, también puede guardar una configuración de búsqueda determinada para recuperarla y utilizarla en otro momento:

1. Defina los criterios de búsqueda y seleccione **Guardar**.

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. Asigne un nombre y luego utilice **Guardar** para confirmar la acción:

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. La próxima vez que acceda al panel de búsqueda, la búsqueda guardada estará disponible en el selector:

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. Una vez guardada, puede hacer lo siguiente:

   * Use **x** (con el nombre de la búsqueda guardada) para iniciar una nueva consulta (la búsqueda guardada en sí no se eliminará).
   * Use la opción **Editar búsqueda guardada**, cambie las condiciones de búsqueda y luego utilice **Guardar** nuevamente.

Las búsquedas guardadas se pueden modificar seleccionando la búsqueda guardada y haciendo clic en **Editar búsqueda guardada** en la parte inferior del panel de búsqueda.

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
