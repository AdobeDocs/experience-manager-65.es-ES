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
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# Mejoras de traducción{#translation-enhancements}

Esta página presenta mejoras y mejoras incrementales en las capacidades de administración de AEM traducción.

## Automatización del proyecto de traducción {#translation-project-automation}

Se han añadido opciones para mejorar la productividad trabajando con proyectos de traducción, como promocionar y eliminar automáticamente lanzamientos de traducción y programar la ejecución recurrente de un proyecto de traducción.

1. En el proyecto de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico **Resumen de traducción**.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la pestaña **Advanced**. En la parte inferior, puede seleccionar **Promocionar automáticamente lanzamientos de traducción**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. De forma opcional, puede seleccionar si, después de recibir el contenido traducido, los lanzamientos de traducción deben promocionarse y eliminarse automáticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para seleccionar la ejecución recurrente de un proyecto de traducción, seleccione la frecuencia con el menú desplegable en **Repetir traducción**. La ejecución de proyectos recurrentes creará y ejecutará automáticamente trabajos de traducción en los intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Proyectos de traducción multilingüe {#multilingual-translation-projects}

Es posible configurar varios idiomas de destino en un proyecto de traducción para reducir el número total de proyectos de traducción creados.

1. En el proyecto de traducción, toque o haga clic en los puntos en la parte inferior del mosaico **Resumen de traducción**.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la pestaña **Advanced**. Puede agregar varios idiomas en **Idioma de destino**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Alternativamente, si está iniciando la traducción a través del carril de referencias en Sitios, añada sus idiomas y seleccione **Crear proyecto de traducción en varios idiomas**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Los trabajos de traducción se crean en el proyecto para cada idioma de destino. Pueden iniciarse de una en una dentro del proyecto o de una en una ejecutando el proyecto globalmente en Administración de proyectos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Actualizaciones de memoria de traducción {#translation-memory-updates}

Las ediciones manuales del contenido traducido se pueden sincronizar de nuevo con el Sistema de Gestión de Traducciones (TMS) para entrenar su Memoria de Traducción.

1. Desde la consola Sitios, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria de traducción**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista de lista muestra una comparación en paralelo de la fuente y la traducción de cada componente de texto que se editó. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y seleccione **Actualizar memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM enviará las cadenas seleccionadas de nuevo al sistema de administración de traducción.

## Copias de idioma en varios niveles {#language-copies-on-multiple-levels}

Las raíces de los idiomas ahora se pueden agrupar en nodos, por ejemplo por región, aunque se siguen reconociendo como raíces de las copias de idiomas.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Solo se permite un nivel. Por ejemplo, lo siguiente no permite que la página &quot;es&quot; se resuelva en una copia de idioma:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`

>
>
Esta `es` copia de idioma no se detectará porque está a 2 niveles (americas/centroamérica) fuera del nodo `en`.

>[!NOTE]
>
>Las raíces de idioma pueden tener cualquier nombre de página, en lugar de solo el código ISO del idioma. AEM siempre comprobará primero la ruta y el nombre, pero si el nombre de la página no identifica ningún idioma, AEM comprobará la propiedad cq:language de la página para la identificación del idioma.

## Informes de estado de traducción {#translation-status-reporting}

Ahora se puede seleccionar una propiedad en la vista de lista Sitios que muestre si una página se ha traducido, si está traducida o si aún no se ha traducido. Para mostrarlo:

1. En Sitios, cambie a **Vista de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Toque o haga clic en **Ver configuración**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Marque la casilla **Translated** en **Translation** y pulse o haga clic en **Update**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ahora puede ver una columna **Translated** que muestra el estado de traducción de las páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

