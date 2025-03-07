---
title: Edición de lanzamientos
description: Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 7%

---

# Edición de lanzamientos{#editing-launches}

## Edición de páginas de lanzamiento {#editing-launch-pages}

Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.

1. Abra la página para editarla.
1. En Sidekick, seleccione la ficha **Creación de versiones** y, a continuación, expanda el grupo **Lanzamientos**. El título del lanzamiento que se está editando actualmente utiliza una fuente en negrita.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Seleccione el lanzamiento en el que desea trabajar y, a continuación, haga clic en **Cambiar**.
1. Empiece a editar.

   >[!NOTE]
   >
   >Puede usar la ficha **Página** de la barra de tareas para realizar acciones como **Crear página secundaria**, entre otras.

## Edición de una configuración de lanzamiento {#editing-a-launch-configuration}

Después de crear un lanzamiento, puede cambiar su nombre y la fecha. También puede especificar una imagen para asociarla al lanzamiento.

1. Abra la página de administración de inicios ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Seleccione el lanzamiento necesario y haga clic en **Editar** para abrir el cuadro de diálogo:

   * En la ficha **General**, puede editar:

      * **Título**
      * **Fecha de lanzamiento**: es equivalente a la fecha de lanzamiento
      * **Producción lista**

     Consulte [Lanzamientos: el orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener información sobre el propósito y la interacción de estos campos.

   * En la ficha **Imagen**, puede cargar un archivo de imagen.

1. Haga clic en **Guardar**.

## Descubrimiento del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

Cuando está editando el lanzamiento de una página, la información sobre el lanzamiento aparece en la parte inferior de la pestaña **Versiones** del Sidekick:

* Nombre del lanzamiento.
* La hora desde el último cambio.
* El usuario que realizó el último cambio.
* El estado del indicador **Listo para la producción** (naranja=no establecido; verde=establecido).

![chlimage_1-186](assets/chlimage_1-186.png)
