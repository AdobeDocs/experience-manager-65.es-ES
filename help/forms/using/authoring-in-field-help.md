---
title: Creación de ayuda en contexto para campos de formulario
seo-title: Creación de ayuda en contexto para campos de formulario
description: AEM Forms le permite añadir ayuda en contexto a los paneles y campos de formulario adaptables, como texto o medios enriquecidos, incluidos vídeos.
seo-description: AEM Forms le permite añadir ayuda en contexto a los paneles y campos de formulario adaptables, como texto o medios enriquecidos, incluidos vídeos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# Creación de ayuda en contexto para campos de formulario{#authoring-in-context-help-for-form-fields}

## Introducción {#introduction}

Hay situaciones en las que los usuarios finales que rellenen un formulario no están seguros de cómo rellenar los detalles de un campo de formulario concreto. Para solucionar estos problemas, los formularios adaptables permiten agregar texto o ayuda en contexto enriquecida a un campo de formulario. Ayuda a mejorar la experiencia de cumplimentación de formularios y evita cualquier ambigüedad para los usuarios finales.

En este artículo se explica cómo los autores de formularios pueden agregar ayuda en contexto durante la creación de Forms adaptable.

## Agregar ayuda en contexto {#add-in-context-help}

Puede especificar ayuda en contexto mediante las siguientes opciones de la sección Contenido de ayuda de la ficha Propiedades de la barra lateral.

* [Descripción breve](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Descripción larga](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Ayuda en contexto para campos de formulario](assets/descriptions.png)

>[!NOTE]
>
>La descripción larga anula la descripción corta. Si ha especificado ambos, solo aparecerá una descripción larga.

### Descripción breve {#short-description}

El campo Short description proporciona sugerencias rápidas y cortas sobre cómo rellenar un campo de formulario. El texto especificado en el campo Short description se muestra como información de objeto al pasar el ratón por encima del campo.

![Descripción breve para agregar ayuda en contexto para campos de formulario](assets/tooltip.png)

>[!NOTE]
>
>Seleccione **Mostrar siempre la descripción breve** para mostrar de forma permanente el texto de ayuda debajo del campo.

![Ayuda breve permanente en contexto debajo del campo](assets/short1.png)

### Descripción larga {#long-description}

Puede utilizar el campo Descripción larga para especificar texto largo o incrustar contenido multimedia enriquecido, incluidos vídeos, como ayuda en contexto. Por ejemplo, la siguiente imagen muestra cómo incrustar un vídeo como ayuda en contexto.

![Adición de medios enriquecidos como ayuda en contexto para campos de formulario](assets/long-descriptions.png)

Al agregar una descripción larga, se muestra **?** junto al campo . Al hacer clic en el icono , se muestra el contenido añadido en la sección de descripción larga.

![Ejemplo de ayuda de medios enriquecidos en contexto](assets/photoshop.png)

### Ayuda a nivel de panel {#panel-level-help}

Además de la ayuda en contexto para los campos de formulario, puede especificar ayuda a nivel de panel en la ficha Contenido de la ayuda del cuadro de diálogo de edición del panel.

![Adición de ayuda en contexto para un panel de formulario](assets/panel-level-help.png)

Al agregar ayuda para el panel, se muestra un **?** junto a la descripción del panel. Al hacer clic en el icono, se muestra el contenido añadido en la sección Contenido de ayuda del cuadro de diálogo de edición del panel.

![Ejemplo de ayuda en contexto en el nivel de panel de formulario](assets/photoshop-1.png)

