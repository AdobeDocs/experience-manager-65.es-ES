---
title: Creación de lanzamientos
seo-title: Creación de lanzamientos
description: Cree un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará en el futuro. Al crear un lanzamiento, especificará un título y la página de origen.
seo-description: Cree un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará en el futuro. Al crear un lanzamiento, especificará un título y la página de origen.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 93%

---


# Creación de lanzamientos{#creating-launches}

Cree un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará en el futuro. Al crear un lanzamiento, especificará un título y la página de origen:

* El título aparece en la **barra de tareas**, desde donde los autores pueden acceder a ellos para trabajar en ellos.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede utilizar solo una página de origen.
* De forma predeterminada, [Live Copy](/help/sites-administering/msm.md) actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos.

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

## Creación de un lanzamiento {#creating-a-launch}

En el siguiente procedimiento se crea un lanzamiento.

1. Abra la página Administración del sitio web ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Haga clic en **Nuevo…** y luego en **Nuevo Lanzamiento…**.
1. En el cuadro de diálogo **Crear lanzamiento**, especifique valores para las propiedades siguientes:

   * **Título de lanzamiento**: el nombre del lanzamiento. El nombre debería tener sentido para los autores.
   * **Página de origen**: la ruta a la página para la que se creará el lanzamiento. De forma predeterminada, se incluyen todas las páginas secundarias.
   * **Excluir páginas secundarias**: seleccione esta opción para crear el lanzamiento solo para la página de origen sin incluir las páginas secundarias. De forma predeterminada, está opción no está seleccionada.
   * **Mantener sincronizado**: seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Para ello, el lanzamiento se convierte en una [Live Copy](/help/sites-administering/msm.md).
   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Haga clic en **Crear**.

## Eliminación de un lanzamiento {#deleting-a-launch}

También puede eliminar un lanzamiento. 

1. En la [consola de lanzamientos](/help/sites-classic-ui-authoring/classic-launches.md), seleccione el lanzamiento necesario.
1. Haga clic en **Eliminar** (se necesita confirmación :)

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Al eliminar lanzamientos anidados, debe eliminar primero los niveles inferiores.

