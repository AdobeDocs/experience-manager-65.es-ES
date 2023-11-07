---
title: Mejoras de traducción
description: AEM Mejoras y refinamientos incrementales de las capacidades de administración de traducciones de la.
topic-tags: site-features
content-type: reference
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 27%

---

# Mejoras de traducción{#translation-enhancements}

AEM Esta página presenta mejoras y refinamientos incrementales en las capacidades de administración de traducciones de la.

## Automatización del proyecto de traducción {#translation-project-automation}

Se han añadido opciones para mejorar la productividad al trabajar con proyectos de traducción, como promocionar y eliminar automáticamente los lanzamientos de traducción y programar la ejecución recurrente de un proyecto de traducción.

1. En el proyecto de traducción, toque o haga clic en los puntos suspensivos en la parte inferior de la **Resumen de traducción** mosaico.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la **Avanzadas** pestaña. En la parte inferior, puede seleccionar **Promocionar automáticamente lanzamientos de traducción**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. De forma opcional, puede seleccionar si, después de recibir contenido traducido, los lanzamientos de traducción deben promocionarse y eliminarse automáticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para seleccionar la ejecución recurrente de un proyecto de traducción, seleccione la frecuencia con el menú desplegable debajo de **Repetir traducción**. La ejecución recurrente de proyectos creará y ejecutará automáticamente trabajos de traducción en los intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Proyectos de traducción multilingües {#multilingual-translation-projects}

Es posible configurar varios idiomas de destino en un proyecto de traducción para reducir el número total de proyectos de traducción creados.

1. En el proyecto de traducción, toque o haga clic en los puntos en la parte inferior de la **Resumen de traducción** mosaico.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la **Avanzadas** pestaña. Puede añadir varios idiomas en **Idioma de destino**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Alternativamente, si está iniciando la traducción a través del carril de referencias en Sites, añada los idiomas y seleccione **Creación de un proyecto de traducción en varios idiomas**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Se crearán trabajos de traducción en el proyecto para cada idioma de destino. Se pueden iniciar uno a uno dentro del proyecto o todos a la vez ejecutando el proyecto globalmente en Administración de proyectos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Actualizaciones de memoria de traducción {#translation-memory-updates}

Las ediciones manuales del contenido traducido se pueden sincronizar de nuevo con el sistema de gestión de traducciones (TMS) para mejorar su memoria de traducción.

1. Desde la consola Sites, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria de traducción**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista de lista muestra una comparación en paralelo de la fuente y la traducción de cada componente de texto editado. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y seleccione **Actualizar memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM actualiza la traducción de las cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.

* La acción actualiza la traducción de cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.
* No crea nuevos trabajos de traducción.
* Envía las traducciones de vuelta al sistema de administración de etiquetas, a través de la API de traducción de AEM (se muestra a continuación).

Para usar esta función, haga lo siguiente:

* Configure un sistema de administración de etiquetas para su uso con AEM.
* El conector debe implementar el método [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * El código dentro de este método determina qué sucede con la solicitud de actualización de memoria de traducción.
   * El marco de traducción de AEM envía los pares de valor de cadena (traducción original y actualizada) al sistema de gestión de etiquetas mediante esta implementación de método.

Las actualizaciones de la memoria de traducción se pueden interceptar y enviar a un destino personalizado, en los casos en que se utilice una memoria de traducción propia.

## Copias de idioma en varios niveles {#language-copies-on-multiple-levels}

Las raíces de los idiomas ahora se pueden agrupar en nodos, por ejemplo, por región, aunque se siguen reconociendo como raíces de las copias de idiomas.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Solo se permite un nivel. Por ejemplo, lo siguiente no permitirá que la página &quot;es&quot; resuelva una copia de idioma:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>Esta `es` no se detectará la copia de idioma porque es de 2 niveles (américa/centroamérica) fuera del `en` nodo.

>[!NOTE]
>
>Las raíces de idioma pueden tener cualquier nombre de página, en lugar de solo el código ISO del idioma. AEM AEM siempre comprobará primero la ruta y el nombre, pero si el nombre de la página no identifica un idioma, comprobará la propiedad cq:language de la página para la identificación del idioma.

## Informes de estado de traducción {#translation-status-reporting}

Ahora se puede seleccionar una propiedad en la vista de lista de sitios que muestre si una página se ha traducido, está en proceso de traducción o aún no se ha traducido. Para mostrarlo:

1. En Sitios, cambie a **Vista de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Haga clic o toque **Configuración de vista**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Marque **Traducido** casilla de verificación bajo **Traducción** y pulse o haga clic en **Actualizar**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ahora puede ver una **Traducido** que muestra el estado de traducción de las páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
