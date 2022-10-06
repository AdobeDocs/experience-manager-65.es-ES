---
title: Personalización de vistas de propiedades de página
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# Personalización de vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-authoring/editing-page-properties.md) que los usuarios pueden ver y editar; algunas son necesarias para crear la página (crear vista), otras se pueden ver y editar (editar vista) en una etapa posterior. Estas propiedades de página se definen y el cuadro de diálogo las pone a disposición ( `cq:dialog`) del componente de página correspondiente.

>[!CAUTION]
>
>La personalización de la vista de las propiedades de página no está disponible en la IU clásica.

El estado predeterminado de cada propiedad de página es:

* oculto en la vista de creación (p. ej. **Crear página** asistente)

* disponible en la vista de edición (p. ej. **Ver propiedades**)

Los campos deben configurarse específicamente si es necesario realizar algún cambio. Esto se realiza utilizando las propiedades de nodo apropiadas:

* Propiedad de página que estará disponible en la vista de creación (p. ej. **Crear página** asistente):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propiedad de página que estará disponible en la vista de edición (p. ej. **Ver**/**Editar**) **Propiedades** ):

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por ejemplo, consulte la configuración de los campos agrupados en el **Más títulos y descripción** en el **Básico** para el componente base Página. Se pueden ver en la sección **Crear página** asistente como `cq:showOnCreate` se ha configurado como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte la [Tutorial sobre la ampliación de las propiedades de la página](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía sobre cómo personalizar las propiedades de página.

## Configuración de las propiedades de página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo apropiadas.

Por ejemplo, de forma predeterminada, la variable [**Crear página** asistente](/help/sites-authoring/managing-pages.md#creating-a-new-page) muestra los campos agrupados en **Más títulos y descripción**. Para ocultarlos, configure:

1. Cree el componente de página en `/apps`.
1. Crear una anulación (mediante *diferencias de cuadro de diálogo* proporcionado por el [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md)) para la variable `basic` del componente de página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referencia, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Sin embargo, usted ***must*** no cambie nada en la variable `/libs` ruta.
   Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
   El método recomendado para la configuración y otros cambios es:
   1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
   1. Realice cambios dentro de `/apps`


1. Configure las variables `path` propiedad en `basic` para señalar la anulación de la pestaña basic (consulte también el paso siguiente). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación del `basic` - `moretitles` en la ruta correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo adecuada:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   La variable **Más títulos y descripción** ya no se mostrará en la sección **Crear página** asistente.

>[!NOTE]
Al configurar las propiedades de página para su uso con Live Copies, consulte [Configuración de los bloqueos de MSM en las propiedades de página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de cuadro de diálogo del [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md); incluido el uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). También ilustra el uso de ambos `cq:showOnCreate` y `cq:hideOnEdit`.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-page-dialog en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
