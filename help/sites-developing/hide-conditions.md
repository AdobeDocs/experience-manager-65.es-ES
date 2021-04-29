---
title: Uso de Ocultar condiciones
seo-title: Uso de Ocultar condiciones
description: Las condiciones de ocultado se pueden utilizar para determinar si un recurso de componente se representa o no.
seo-description: Las condiciones de ocultado se pueden utilizar para determinar si un recurso de componente se representa o no.
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
translation-type: tm+mt
source-git-commit: baf2c6339a554743b6cc69486fb77b121048ba4b
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# Uso de Ocultar condiciones {#using-hide-conditions}

Las condiciones de ocultado se pueden utilizar para determinar si un recurso de componente se representa o no. Un ejemplo de esto sería cuando un autor de plantillas configura el componente principal [list component](https://helpx.adobe.com/experience-manager/core-components/using/list.html) en el [editor de plantillas](/help/sites-authoring/templates.md) y decide desactivar las opciones para crear la lista en función de las páginas secundarias. Al desactivar esta opción en el cuadro de diálogo de diseño, se establece una propiedad de modo que, cuando se procesa el componente de lista, se evalúe la condición de ocultado y no se muestre la opción para mostrar páginas secundarias.

## Información general {#overview}

Los diálogos pueden llegar a ser muy complejos con numerosas opciones para el usuario, que sólo puede utilizar una fracción de las opciones a su disposición. Esto puede generar experiencias de interfaz de usuario abrumadoras para los usuarios.

Al utilizar condiciones ocultas, los administradores, desarrolladores y superusuarios pueden ocultar recursos en función de un conjunto de reglas. Esta función les permite decidir qué recursos deben mostrarse cuando un autor edita el contenido.

>[!NOTE]
>
>Ocultar un recurso basado en una expresión no reemplaza los permisos ACL. El contenido permanece editable, pero simplemente no se muestra.

## Detalles de implementación y uso {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` es responsable de filtrar los recursos en función de la existencia y el valor de la  `granite:hide` propiedad, ubicada en el campo que se va a filtrar. La implementación de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` incluye una instancia de `FilteringResourceWrapper.`

La implementación utiliza la [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) de Granite y agrega una `cqDesign` variable personalizada a través de ExpressionCustomizer.

A continuación, se muestran algunos ejemplos de condiciones de ocultamiento en un nodo de diseño ubicado en `etc/design` o como una Política de contenido.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Al definir la expresión de ocultación, tenga en cuenta:

* Para que sea válido, debe expresarse el ámbito en el que se encuentra la propiedad (p. ej. `cqDesign.myProperty`).
* Los valores son de solo lectura.
* Las funciones (si es necesario) deben limitarse a un conjunto determinado proporcionado por el servicio.

## Ejemplo {#example}

Se pueden encontrar ejemplos de condiciones de ocultamiento en AEM y en los [componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) en particular. Por ejemplo, considere el [componente principal de lista](https://helpx.adobe.com/experience-manager/core-components/using/list.html).

[Con el editor](/help/sites-authoring/templates.md) de plantillas, el autor de plantillas puede definir en el cuadro de diálogo de diseño qué opciones del componente de lista están disponibles para el autor de la página. Tales opciones como si se permite que la lista sea una lista estática, una lista de páginas secundarias, una lista de páginas etiquetadas, etc. se puede activar o desactivar.

Si un autor de plantillas decide desactivar la opción de páginas secundarias, se establece una propiedad de diseño y se evalúa una condición de ocultamiento en relación con ella, lo que hace que la opción no se muestre para el autor de la página.

1. De forma predeterminada, el autor de la página puede utilizar el componente principal de la lista para crear una lista utilizando páginas secundarias seleccionando la opción **Páginas secundarias**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. En el cuadro de diálogo de diseño del componente principal de la lista, el autor de la plantilla puede elegir la opción **Deshabilitar elementos secundarios** para evitar que la opción para generar una lista basada en páginas secundarias se muestre al autor de la página.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Se crea un nodo de política en `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` con una propiedad `disableChildren` establecida en `true`.
1. La condición de ocultación se define como el valor de una propiedad `granite:hide` en el nodo de propiedad de cuadro de diálogo `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. El valor de `disableChildren` se extrae de la configuración de diseño y la expresión `${cqDesign.disableChildren}` se evalúa como `false`, lo que significa que la opción no se procesará como parte del componente.

   Puede ver la expresión oculta como el valor de la propiedad `granite:hide` [en GitHub aquí](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. La opción **Páginas secundarias** ya no se representa para el autor de la página al utilizar el componente de lista.

   ![chlimage_1-221](assets/chlimage_1-221.png)
