---
title: Edición de lanzamientos
seo-title: Edición de lanzamientos
description: 'Después de crear el lanzamiento para la página (o el conjunto de páginas), se puede editar el contenido de la copia de inicio de las páginas. '
seo-description: 'Después de crear el lanzamiento para la página (o el conjunto de páginas), se puede editar el contenido de la copia de inicio de las páginas. '
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 6f1f4fbaf9ee4b5ab073a27a58cb040c76230ebd
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 93%

---


# Edición de lanzamientos{#editing-launches}

## Editar páginas de lanzamiento {#editing-launch-pages}

Cuando se crea un lanzamiento de una página (o conjunto de páginas), se puede editar el contenido de la copia de lanzamiento de la página.

1. Acceda a [Lanzamiento desde las referencias (consola de sitios)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Ir a página** para abrir la página para editarla.

>[!NOTE]
>
>No se le permite mover una página dentro de un lanzamiento. Si se intenta esta acción, se activará un mensaje de advertencia:
>
>* Advertencia: Esta página es el origen de un lanzamiento. No se permite mover la página.


### Editar páginas de lanzamiento sujetas a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Si el lanzamiento se basa en una [Live Copy](/help/sites-administering/msm.md), deberá hacer lo siguiente:

* consulte los símbolos de bloqueo (en forma de pequeños candados) cuando edite un componente (contenido y/o propiedades).
* consulte la ficha **Live Copy** en **Propiedades de página**

Se utiliza una Live Copy para sincronizar contenido *desde* la rama de origen *a* la rama de lanzamiento (para mantener el lanzamiento actualizado con los cambios realizados en la fuente).

Puede realizar cambios, del mismo modo que puede editar una Live Copy estándar; por ejemplo:

* Al hacer clic en un candado cerrado interrumpirá la sincronización y podrá utilizar nuevas actualizaciones de contenido en el lanzamiento. Una vez que se desbloquea (icono del candado abierto), los cambios no se sobrescriben con ningún cambio que se realice en la misma ubicación de la rama de origen.
* **Suspender** (y **reanudar**) la herencia de una página específica.

Consulte [Cambiar el contenido de una Live Copy](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para obtener más información.

## Comparar una página de lanzamiento con su página de origen {#comparing-a-launch-page-to-its-source-page}

Para rastrear los cambios realizados, puede ver el lanzamiento en **Referencias** y comparar la página de lanzamiento con la página de origen:

1. En la consola **Sitios**, [vaya a la página de origen del lanzamiento y selecciónela](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. Abra el panel **[Referencias](/help/sites-authoring/basic-handling.md#references)** y seleccione **Lanzamientos**.
1. Seleccione un lanzamiento específico y la opción **Comparar con el origen**:

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. Las dos páginas (lanzamiento y origen) se abrirán en paralelo.

   Para obtener información completa sobre el uso de esta característica, consulte la [diferencia de la página](/help/sites-authoring/page-diff.md).

## Cambiar las páginas de origen utilizadas  {#changing-the-source-pages-used}

Puede añadir en cualquier momento las páginas en el rango de páginas de origen para el lanzamiento, o eliminarlas: 

1. Acceda y seleccione el lanzamiento de:

   * La [consola Lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

      * Seleccione **Editar**.
   * [Referencias (consola Sitios)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles:

      * Seleccione **Editar lanzamiento**. 

   Las páginas de origen se mostrarán.

1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

   >[!NOTE]
   >
   >Para añadir páginas a un lanzamiento, deben estar bajo una raíz de idioma común; es decir, dentro de un solo sitio.

## Editar una configuración de lanzamiento  {#editing-a-launch-configuration}

Las propiedades del lanzamiento se pueden editar en cualquier momento:

1. Acceda y seleccione el lanzamiento de:

   * La [consola Lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

      * Seleccione **Propiedades**.
   * [Referencias (consola Sitios)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles:

      * Seleccione **Editar propiedades**. 

   Se mostrarán los detalles.

1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

   Consulte [Lanzamientos: orden de eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener información sobre la finalidad y la interacción de los campos **Fecha de inicio** y **Producción lista**.

## Detección del estado de lanzamiento de una página  {#discovering-the-launch-status-of-a-page}

Se muestra el estado cuando se selecciona un lanzamiento específico en la ficha de referencias (consulte [Lanzamientos en las referencias (consola Sitios)](/help/sites-authoring/launches.md#launches-in-references-sites-console)).

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
