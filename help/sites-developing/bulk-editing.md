---
title: Configuración de la página para la edición masiva de las propiedades de la página
seo-title: Configuración de la página para la edición masiva de las propiedades de la página
description: La edición masiva de propiedades de página permite editar las propiedades de varias páginas a la vez
seo-description: La edición masiva de propiedades de página permite editar las propiedades de varias páginas a la vez
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuring your Page for Bulk Editing of Page Properties {#configuring-your-page-for-bulk-editing-of-page-properties}

[La edición masiva de propiedades](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) de página le permite editar las propiedades de varias páginas a la vez.

Debido a la posibilidad de valores diferentes, las propiedades de página no están habilitadas para la edición masiva como predeterminadas. Deben estar explícitamente en la lista blanca (habilitada). Al definir las propiedades de la página para que estén disponibles para la edición masiva, debe tener en cuenta ciertas implicaciones, como:

* Determinados campos suelen ser únicos; por ejemplo, un título de página. Debe decidir si es significativo habilitar estos campos para la edición masiva, cuando se aplicará un valor.
* Ciertos campos pueden tener varios valores; esto requiere una representación significativa al procesar.

   Por ejemplo, una casilla de verificación que indica &quot;Listo para publicación&quot;. Esto puede tener varios valores antes de la edición masiva (por ejemplo, listo, en revisión, en curso).

>[!CAUTION]
>
>La edición masiva de propiedades de página es:
>
>* No disponible en la IU clásica.
>* No está disponible para páginas dentro de una Live Copy.
>* Solo disponible para páginas con el mismo tipo de recurso.
>



>[!NOTE]
>
>La edición masiva también está disponible para Recursos. Se parece mucho, pero presenta algunos aspectos diferentes. Consulte [Edición de propiedades de varios recursos](/help/assets/managing-multiple-assets.md) para obtener más información. Puede personalizar los campos en el editor de metadatos masivos para recursos con el editor [de esquemas](/help/assets/metadata-schemas.md).

## Activación de un campo {#enabling-a-field}

>[!NOTE]
>
>Ciertos campos pueden tener varios valores; esto requiere una representación significativa al procesar. Por este motivo, solo debe habilitar los siguientes tipos de campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>



Los campos están activados en el componente de página (*no* en la plantilla):

1. Con CRXDE Lite (o un método equivalente) abra el componente de página.

   Por ejemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >En este ejemplo se asume que los componentes principales se han instalado en la instancia, lo que sucede si la instancia se está ejecutando con contenido de ejemplo de We.Retail. See the [Core Components documentation](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) for more information.

1. Vaya al campo requerido dentro de la `cq:dialog` definición.
1. Defina la siguiente propiedad en el nodo de campo:

   * **Nombre**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`
   Por ejemplo, para el componente [de](/help/sites-authoring/default-components-foundation.md)base de página estándar:

   `/libs/foundation/components/page`

   La propiedad se definiría en:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >No ***debe*** cambiar nada en la `/libs` ruta.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >    1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
   >    1. Realice los cambios en `/apps`


1. Seleccione **Guardar todo** para mantener las actualizaciones.

