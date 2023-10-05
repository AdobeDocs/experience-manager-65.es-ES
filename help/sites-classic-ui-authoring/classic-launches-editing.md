---
title: Edición de lanzamientos
description: Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 27%

---

# Edición de lanzamientos{#editing-launches}

## Edición de páginas de lanzamiento {#editing-launch-pages}

Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.

1. Abra la página para editarla.
1. En Sidekick, seleccione la opción **Versiones** , luego expanda la pestaña **Lanzamientos** grupo. El título del lanzamiento que se está editando actualmente utiliza una fuente en negrita.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Seleccione el lanzamiento en el que desea trabajar y, a continuación, haga clic en **Cambiar**.
1. Empiece a editar.

   >[!NOTE]
   >
   >Puede usar el complemento **Página** pestaña de la barra de tareas para realizar acciones como **Crear página secundaria**, entre otros.

## Edición de una configuración de lanzamiento {#editing-a-launch-configuration}

Después de crear un lanzamiento, puede cambiar su nombre y la fecha. También puede especificar una imagen para asociarla al lanzamiento.

1. Abra la página de administración de lanzamientos ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Seleccione el lanzamiento necesario y haga clic en **Editar** para abrir el cuadro de diálogo:

   * En el **General** , puede editar:

      * **Título**
      * **Fecha de lanzamiento**: esto equivale a la fecha de lanzamiento
      * **Producción lista**

     Consulte [Lanzamientos: el orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener información sobre el propósito y la interacción de estos campos.

   * En el **Imagen** pestaña, puede cargar un archivo de imagen.

1. Haga clic en **Guardar**.

## Descubrimiento del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

Cuando está editando el lanzamiento de una página, la información sobre el lanzamiento aparece en la parte inferior de la página **Versiones** pestaña del Sidekick:

* Nombre del lanzamiento.
* La hora desde el último cambio.
* El usuario que realizó el último cambio.
* El estado del **Producción lista** indicador (naranja=no establecido; verde=establecido).

![chlimage_1-186](assets/chlimage_1-186.png)
