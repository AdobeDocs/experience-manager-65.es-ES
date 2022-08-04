---
title: Mejoras en la traducción
seo-title: Translation Enhancements
description: Mejoras de traducción en AEM.
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 4%

---

# Mejoras en la traducción{#translation-enhancements}

Esta página presenta mejoras y mejoras incrementales en las capacidades de administración de AEM traducción.

## Traducción Automatización del proyecto {#translation-project-automation}

Se han añadido opciones para mejorar la productividad trabajando con proyectos de traducción, como promocionar y eliminar automáticamente lanzamientos de traducción y programar la ejecución recurrente de un proyecto de traducción.

1. En el proyecto de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del **Resumen de traducción** mosaico.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la **Avanzadas** pestaña . En la parte inferior, puede seleccionar **Promocionar automáticamente los lanzamientos de traducción**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. De forma opcional, puede seleccionar si, después de recibir el contenido traducido, los lanzamientos de traducción deben promocionarse y eliminarse automáticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para seleccionar la ejecución recurrente de un proyecto de traducción, seleccione la frecuencia con la lista desplegable en **Repetir traducción**. La ejecución de proyectos recurrentes creará y ejecutará automáticamente trabajos de traducción en los intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Proyectos de traducción multilingües {#multilingual-translation-projects}

Es posible configurar varios idiomas de destino en un proyecto de traducción para reducir el número total de proyectos de traducción creados.

1. En el proyecto de traducción, toque o haga clic en los puntos de la parte inferior del **Resumen de traducción** mosaico.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Cambie a la **Avanzadas** pestaña . Puede añadir varios idiomas en **Idioma de Target**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Alternativamente, si está iniciando la traducción a través del carril de referencias en Sitios, añada sus idiomas y seleccione **Crear proyecto de traducción en varios idiomas**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Los trabajos de traducción se crean en el proyecto para cada idioma de destino. Pueden iniciarse de una en una dentro del proyecto o de una en una ejecutando el proyecto globalmente en Administración de proyectos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Actualizaciones en la memoria de traducción {#translation-memory-updates}

Las ediciones manuales del contenido traducido se pueden sincronizar de nuevo con el Sistema de Gestión de Traducciones (TMS) para entrenar su memoria de traducción.

1. Desde la consola Sitios, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria de traducción**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista de lista muestra una comparación en paralelo de la fuente y la traducción de cada componente de texto editado. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y seleccione **Actualización de memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM actualiza la traducción de las cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.

* La acción actualiza la traducción de cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.
* No crea nuevos trabajos de traducción.
* Envía las traducciones de vuelta al sistema de administración de etiquetas, a través de AEM API de traducción (ver abajo).

Para usar esta función:

* Se debe configurar un sistema de administración de etiquetas para su uso con AEM.
* El conector debe implementar el método [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * El código dentro de este método determina qué sucede con la solicitud de actualización de memoria de traducción.
   * El marco de traducción de AEM envía los pares de valor de cadena (traducción original y actualizada) al sistema de administración de etiquetas mediante esta implementación de método.

Las actualizaciones de la memoria de traducción se pueden interceptar y enviar a un destino personalizado, en los casos en que se utilice una memoria de traducción propia.

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
>Esta `es` la copia de idioma no se detectará porque está a 2 niveles (américa/centroamérica) lejos del `en` nodo .

>[!NOTE]
>
>Las raíces de idioma pueden tener cualquier nombre de página, en lugar de solo el código ISO del idioma. AEM siempre comprobará primero la ruta y el nombre, pero si el nombre de la página no identifica ningún idioma, AEM comprobará la propiedad cq:language de la página para la identificación del idioma.

## Informes de estado de traducción {#translation-status-reporting}

Ahora se puede seleccionar una propiedad en la vista de lista Sitios que muestre si una página se ha traducido, si está traducida o si aún no se ha traducido. Para mostrarlo:

1. En Sitios, cambie a **Vista de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Toque o haga clic en **Configuración de vista**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Marque **Traducido** casilla de verificación en **Traducción** y toque o haga clic **Actualizar**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ahora puede ver un **Traducido** que muestra el estado de traducción de las páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
