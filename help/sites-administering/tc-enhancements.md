---
title: Mejoras en la traducción
seo-title: Mejoras en la traducción
description: Mejoras de traducción en AEM.
seo-description: Mejoras de traducción en AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Mejoras en la traducción{#translation-enhancements}

Esta página presenta mejoras y mejoras incrementales en las capacidades de administración de traducción de AEM.

## Automatización del proyecto de traducción {#translation-project-automation}

Se han agregado opciones para mejorar la productividad trabajando con proyectos de traducción, como promover y eliminar automáticamente lanzamientos de traducción y programar la ejecución recurrente de un proyecto de traducción.

1. En el proyecto de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico Resumen **de** traducción.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la ficha **Avanzado** . En la parte inferior, puede seleccionar Promocionar **automáticamente inicios** de traducción.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. De forma opcional, puede seleccionar si, después de recibir contenido traducido, los inicios de traducción deben promocionarse y eliminarse automáticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para seleccionar la ejecución recurrente de un proyecto de traducción, seleccione la frecuencia con el menú desplegable en **Repetir traducción**. La ejecución de proyectos recurrentes creará y ejecutará automáticamente trabajos de traducción en los intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Proyectos de traducción multilingües {#multilingual-translation-projects}

Es posible configurar varios idiomas de destino en un proyecto de traducción, para reducir el número total de proyectos de traducción creados.

1. En el proyecto de traducción, toque o haga clic en los puntos de la parte inferior del mosaico Resumen **de** traducción.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la ficha **Avanzado** . Puede agregar varios idiomas en Idioma **de** destino.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Como alternativa, si está iniciando la traducción mediante el carril de referencias en Sitios, agregue sus idiomas y seleccione **Crear proyecto** de traducción en varios idiomas.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Los trabajos de traducción se crearán en el proyecto para cada idioma de destino. Pueden iniciarse una por una dentro del proyecto o de una vez ejecutando el proyecto de forma global en Administración de proyectos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Actualizaciones de memoria de traducción {#translation-memory-updates}

Las ediciones manuales del contenido traducido se pueden sincronizar con el sistema de administración de traducciones (TMS) para capacitar su memoria de traducción.

1. Desde la consola Sitios, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria** de traducción.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista de lista muestra una comparación paralela del origen y la traducción para cada componente de texto que se editó. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y seleccione **Actualizar memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM devolverá las cadenas seleccionadas al sistema de administración de traducciones.

## Copias de idioma en varios niveles {#language-copies-on-multiple-levels}

Las raíces de idioma ahora pueden agruparse bajo nodos, por ejemplo por región, mientras se siguen reconociendo como raíces de las copias de idioma.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Solo se permite un nivel. Por ejemplo, lo siguiente no permitirá que la página &quot;es&quot; se resuelva en una copia de idioma:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>
Esta copia de idioma no se detectará porque está a 2 niveles (América/Centroamérica) lejos del `es` `en` nodo.

>[!NOTE]
>
>Las raíces de idioma pueden tener cualquier nombre de página, en lugar de sólo el código ISO del idioma. AEM siempre comprobará primero la ruta y el nombre, pero si el nombre de la página no identifica un idioma, AEM comprobará la identificación del idioma en la propiedad cq:language de la página.

## Informes de estado de traducción {#translation-status-reporting}

Ahora se puede seleccionar una propiedad en la vista de lista Sitios que muestra si una página se ha traducido, se está traduciendo o no se ha traducido. Para mostrarlo:

1. En Sitios, cambie a Vista **de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Toque o haga clic en **Ver configuración**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Marque la casilla **Traducida** en **Traducción** y toque o haga clic en **Actualizar**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ahora puede ver una columna **Traducida** que muestra el estado de traducción de las páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

