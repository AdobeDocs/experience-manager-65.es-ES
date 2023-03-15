---
title: Personalizar vistas de propiedades de página
seo-title: Customizing Views of Page Properties
description: Cada página tiene un conjunto de propiedades que puede editar según sea necesario
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Personalizar vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-authoring/editing-page-properties.md) que los usuarios pueden ver y editar; algunos son necesarios al crear la página (vista crear), otros se pueden ver y editar (vista editar) en una etapa posterior. Estas propiedades de página se definen y se ponen a disposición mediante el cuadro de diálogo ( `cq:dialog`) del componente de página correspondiente.

>[!CAUTION]
>
>La personalización de la vista de las propiedades de página no está disponible en la IU clásica.

El estado predeterminado de cada propiedad de página es:

* oculto en la vista crear (p. ej., **Crear página** wizard)

* disponible en la vista de edición (p. ej., **Ver propiedades**)

Los campos deben configurarse específicamente si se requiere algún cambio. Esto se realiza mediante las propiedades de nodo adecuadas:

* Propiedad de página que estará disponible en la vista de creación (por ejemplo, **Crear página** asistente):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propiedad de página que estará disponible en la vista de edición (por ejemplo, **Ver**/**Editar**) **Propiedades** opción):

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por ejemplo, consulte la configuración de los campos agrupados en **Más títulos y descripciones** en el **Básico** para el componente Página de base. Estos se pueden ver en **Crear página** asistente como `cq:showOnCreate` se ha establecido en `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte la [Tutorial sobre Ampliación de propiedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía para personalizar las propiedades de la página.

## Configuración de las propiedades de página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo adecuadas.

Por ejemplo, de forma predeterminada la variable [**Crear página** asistente](/help/sites-authoring/managing-pages.md#creating-a-new-page) muestra los campos agrupados bajo **Más títulos y descripciones**. Para ocultarlos, configure lo siguiente:

1. Cree su componente de página en `/apps`.
1. Creación de una anulación (mediante *diff de diálogo* proporcionadas por el [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md)) para el `basic` de su componente de página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referencia, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Sin embargo, usted ***debe*** no cambie nada en el `/libs` ruta.
   Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
   El método recomendado para la configuración y otros cambios es:
   1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
   1. Realice cualquier cambio en `/apps`


1. Configure las variables `path` propiedad en `basic` para señalar a la anulación de la pestaña básica (consulte el paso siguiente también). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación de `basic` - `moretitles` en la ruta correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo adecuada:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   El **Más títulos y descripciones** ya no se mostrará en la sección **Crear página** asistente.

>[!NOTE]
Al configurar las propiedades de página para usarlas con Live Copies, consulte [Configurar los bloqueos MSM en las propiedades de página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de diálogo del [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md); incluido el uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). También ilustra el uso de ambos `cq:showOnCreate` y `cq:hideOnEdit`.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-page-dialog en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
