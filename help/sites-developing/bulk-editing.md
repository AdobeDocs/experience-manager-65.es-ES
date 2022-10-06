---
title: Configuración de la página para la edición masiva de las propiedades de página
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: La edición masiva de propiedades de página permite editar las propiedades de varias páginas a la vez
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 7%

---

# Configuración de la página para la edición masiva de las propiedades de página {#configuring-your-page-for-bulk-editing-of-page-properties}

[Edición masiva de propiedades de página](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) permite editar las propiedades de varias páginas a la vez.

Debido a la posibilidad de que haya diferentes valores, las propiedades de página no están habilitadas para la edición por lotes como predeterminadas. Se deben permitir explícitamente (activados). Al definir las propiedades de página que estarán disponibles para la edición por lotes, debe tener en cuenta determinadas implicaciones, como:

* Determinados campos suelen ser únicos; por ejemplo, un título de página. Debe decidir si es significativo habilitar estos campos para la edición por lotes, cuando se aplicará un valor.
* Algunos campos pueden tener varios valores, lo que requiere una representación significativa al procesarlos.

   Por ejemplo, una casilla de verificación que indica &quot;Listo para publicación&quot;. Esto puede tener varios valores antes de la edición masiva (por ejemplo, listo, en revisión, en curso).

>[!CAUTION]
>
>La edición masiva de propiedades de página es:
>
>* No disponible en la IU clásica.
>* No está disponible para páginas dentro de una Live Copy.
>* Solo está disponible para páginas con el mismo tipo de recurso.
>


>[!NOTE]
>
>La edición por lotes también está disponible para Assets. Se parece mucho, pero presenta algunos aspectos diferentes. Consulte [Edición de propiedades de varios recursos](/help/assets/metadata.md) para obtener más información. Puede personalizar los campos del editor de metadatos masivos para los recursos mediante la función [Editor de esquemas](/help/assets/metadata-schemas.md).

## Activación de un campo {#enabling-a-field}

>[!NOTE]
>
>Algunos campos pueden tener varios valores, lo que requiere una representación significativa al procesarlos. Por este motivo, solo debe habilitar los siguientes tipos de campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


Los campos se activan en el componente de página (*not* en la plantilla):

1. Con el CRXDE Lite (o un método equivalente), abra el componente de página.

   Por ejemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >En este ejemplo se supone que los componentes principales se han instalado en la instancia, como sucede si la instancia se está ejecutando con contenido de muestra de We.Retail. Consulte la [Documentación de componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) para obtener más información.

1. Vaya al campo requerido dentro del `cq:dialog` definición.
1. Defina la siguiente propiedad en el nodo de campo:

   * **Nombre**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por ejemplo, para la página estándar [componente base](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   La propiedad se definiría en:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >You ***must*** no cambie nada en la variable `/libs` ruta.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >    1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
   >    1. Realice cambios dentro de `/apps`


1. Select **Guardar todo** para mantener las actualizaciones.
