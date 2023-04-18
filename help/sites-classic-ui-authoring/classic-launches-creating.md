---
title: Creación de lanzamientos
description: Cree un lanzamiento para permitir la actualización de una nueva versión de páginas web existentes para su activación futura. Al crear un lanzamiento, especificará un título y la página de origen.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 29%

---

# Creación de lanzamientos{#creating-launches}

Cree un lanzamiento para permitir la actualización de una nueva versión de páginas web existentes para su activación futura. Al crear un lanzamiento, especificará un título y la página de origen:

* El título aparece en la sección **Barra de tareas**, desde donde los autores pueden acceder para trabajar en ellos.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede usar solamente la página de origen.
* De forma predeterminada, [Live Copy](/help/sites-administering/msm.md) actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos.

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

## Creación de un lanzamiento {#creating-a-launch}

El siguiente procedimiento crea un lanzamiento.

1. Abra la página de administración del sitio web ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Haga clic en **Nuevo...** then **Nuevo lanzamiento...**.
1. En el **Crear Launch** , especifique valores para las siguientes propiedades:

   * **Título de lanzamiento**: Nombre del lanzamiento. El nombre debe tener sentido para los autores.
   * **Página de origen**: Ruta a la página para la que se crea el lanzamiento. De forma predeterminada, se incluyen todas las páginas secundarias.
   * **Excluir páginas secundarias**: Seleccione esta opción para crear el lanzamiento solo para la página de origen y no para las páginas secundarias. De forma predeterminada, esta opción no está seleccionada.
   * **Mantener sincronizado**: Seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Esto se logra convirtiendo el lanzamiento en un [live copy](/help/sites-administering/msm.md).
   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![imagen_1-99](assets/chlimage_1-99a.png)

1. Haga clic en **Crear**.

## Eliminación de un lanzamiento {#deleting-a-launch}

También puede eliminar un lanzamiento.

1. En el [inicia la consola](/help/sites-classic-ui-authoring/classic-launches.md), seleccione el lanzamiento requerido.
1. Haga clic en **Eliminar** - se requiere confirmación:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Al eliminar lanzamientos anidados, primero debe eliminar los niveles inferiores.
