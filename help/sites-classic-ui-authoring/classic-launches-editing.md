---
title: Edición de lanzamientos
seo-title: Edición de lanzamientos
description: Cuando se crea un lanzamiento de una página (o conjunto de páginas), se puede editar el contenido de la copia de lanzamiento de la página.
seo-description: Cuando se crea un lanzamiento de una página (o conjunto de páginas), se puede editar el contenido de la copia de lanzamiento de la página.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 99%

---


# Edición de lanzamientos{#editing-launches}

## Editar páginas de lanzamiento {#editing-launch-pages}

Cuando se crea un lanzamiento de una página (o conjunto de páginas), se puede editar el contenido de la copia de lanzamiento de la página.

1. Abra la página para su edición.
1. En la barra de tareas, seleccione la ficha **Versiones** y amplíe el grupo **Lanzamientos**. El título del lanzamiento que se esté editando estará en negrita.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Seleccione el lanzamiento en el que quiere trabajar y haga clic en **Cambiar**.
1. Comience a editar.

   >[!NOTE]
   >
   >Puede utilizar la ficha **Página** de la barra de tareas para realizar acciones como **Crear página secundaria**, entre otras. 

## Editar una configuración de lanzamiento {#editing-a-launch-configuration}

Tras crear un lanzamiento, puede cambiar el nombre y la fecha del lanzamiento. También puede especificar una imagen que desee asociar con el lanzamiento.

1. Abra la página de administración de lanzamientos ([http://localhost:4502/libs/launches/content/admin.html)](http://localhost:4502/libs/launches/content/admin.html).

1. Seleccione el lanzamiento requerido y haga clic en **Editar** para abrir el cuadro de diálogo:

   * En la ficha **General**, puede editar:

      * **Título**
      * **Fecha de lanzamiento**: equivale a la fecha de 
      * **La producción está lista**

      Consulte [Lanzamientos: orden de eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener información sobre la finalidad y la interacción de los campos.

   * En la ficha **Imagen**, puede cargar un archivo de imagen.


1. Haga clic en **Guardar**.

## Detección del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

Cuando se edita un lanzamiento de una página, la información del lanzamiento aparecerá en la parte inferior de la ficha **Versión** de la barra de tareas:

* Nombre del lanzamiento.
* Tiempo desde el último cambio.
* Usuario que realizó el último cambio.
* Estado del indicador **Listo para producción** (naranja = sin establecer; verde = establecido).

![chlimage_1-186](assets/chlimage_1-186.png)

