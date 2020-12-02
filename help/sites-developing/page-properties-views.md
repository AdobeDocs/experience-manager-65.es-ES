---
title: Personalización de Vistas de propiedades de página
seo-title: Personalización de Vistas de propiedades de página
description: Cada página tiene un conjunto de propiedades que puede editar según sea necesario
seo-description: Cada página tiene un conjunto de propiedades que puede editar según sea necesario
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Personalización de Vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-authoring/editing-page-properties.md) que los usuarios pueden ver y editar; algunas son necesarias al crear la página (crear vista), otras se pueden ver y editar (editar vista) en una etapa posterior. Estas propiedades de página se definen y quedan disponibles mediante el cuadro de diálogo ( `cq:dialog`) del componente de página correspondiente.

>[!CAUTION]
>
>La personalización de la vista de las propiedades de página no está disponible en la IU clásica.

El estado predeterminado de cada propiedad de página es:

* oculto en la vista de creación (p. ej. **Asistente para crear página**)

* disponible en la vista de edición (p. ej. **Propiedades de Vista**)

Los campos deben configurarse específicamente si se requiere algún cambio. Esto se realiza con las propiedades de nodo correspondientes:

* Propiedad de página disponible en la vista de creación (p. ej. **Asistente para crear página**):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propiedad de página disponible en la vista de edición (p. ej. **Vista**/**Editar**) **Propiedades** (opción):

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por ejemplo, consulte la configuración de los campos agrupados en **Más títulos y descripción** en la ficha **Básico** para el componente Página base. Estos están visibles en el asistente para **Crear página**, ya que `cq:showOnCreate` se ha configurado como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte el [tutorial Propiedades de la página de ampliación](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía sobre la personalización de las propiedades de la página.

## Configuración de las propiedades de la página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo correspondientes.

Por ejemplo: de forma predeterminada, el asistente [**Crear página** muestra los campos agrupados en **Más títulos y descripción**. ](/help/sites-authoring/managing-pages.md#creating-a-new-page) Para ocultarlos, configure:

1. Cree el componente de página en `/apps`.
1. Cree una anulación (mediante *cuadro de diálogo diff* proporcionado por la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md)) para la sección `basic` del componente de página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referencia, véase:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Sin embargo, ***no debe*** cambiar nada en la ruta `/libs`.
   Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y bien puede sobrescribirse al aplicar una revisión o un paquete de funciones).
   El método recomendado para la configuración y otros cambios es:
   1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
   1. Realice cualquier cambio dentro de `/apps`


1. Establezca la propiedad `path` en `basic` para que señale a la anulación de la ficha básica (consulte también el paso siguiente). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación de la sección `basic` - `moretitles` en la ruta correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo correspondiente:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**:  `false`

   La sección **Más títulos y descripción** ya no se mostrará en el asistente para **Crear página**.

>[!NOTE]
Al configurar las propiedades de página para su uso con copias en vivo, consulte [Configuración de los bloqueos de MSM en las propiedades de página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de cuadro de diálogo de la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md); incluido el uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). También ilustra el uso de `cq:showOnCreate` y `cq:hideOnEdit`.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de Aem-authoring-extension-page-dialog en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
