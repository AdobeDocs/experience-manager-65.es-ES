---
title: Uso de Ocultar condiciones
description: Ocultar condiciones se puede utilizar para determinar si un recurso de componente se procesa o no.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# Uso de Ocultar condiciones {#using-hide-conditions}

Ocultar condiciones se puede utilizar para determinar si un recurso de componente se procesa o no. Un ejemplo de esto sería cuando un autor de plantillas configura el componente principal [componente de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) en el [editor de plantillas](/help/sites-authoring/templates.md) y decide deshabilitar las opciones para generar la lista en función de las páginas secundarias. Al desactivar esta opción en el cuadro de diálogo de diseño, se establece una propiedad de modo que, cuando se represente el componente de lista, se evalúe la condición de ocultar y no se muestre la opción para mostrar páginas secundarias.

## Información general {#overview}

Los cuadros de diálogo pueden llegar a ser complejos, con numerosas opciones para el usuario, que sólo puede utilizar una fracción de las opciones de las que dispone. Esto puede generar experiencias de interfaz de usuario abrumadoras para los usuarios.

Al utilizar las condiciones de ocultación, los administradores, los desarrolladores y los superusuarios tienen una forma de ocultar los recursos en función de un conjunto de reglas. Esta función les permite decidir qué recursos se deben mostrar cuando un autor edita el contenido.

>[!NOTE]
>
>Al ocultar un recurso basado en una expresión, no se reemplazan los permisos ACL. El contenido sigue siendo editable, pero no se muestra.

## Detalles de implementación y uso {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` es responsable de filtrar los recursos en función de la existencia y el valor de `granite:hide` propiedad, ubicada en el campo que se va a filtrar. La implementación de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` incluye una instancia de `FilteringResourceWrapper.`

La implementación hace uso de Granite [API de ELResolver](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) y añade un `cqDesign` variable personalizada mediante ExpressionCustomizer.

A continuación, se muestran algunos ejemplos de condiciones de ocultación en un nodo de diseño ubicado en `etc/design` o como una política de contenido.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Al definir la expresión Hide, tenga en cuenta lo siguiente:

* Para ser válido, se debe expresar el ámbito en el que se encuentra la propiedad (por ejemplo, `cqDesign.myProperty`).
* Los valores son de solo lectura.
* Las funciones (si es necesario) deben limitarse a un conjunto determinado proporcionado por el servicio.

## Ejemplos {#example}

AEM Se pueden encontrar ejemplos de condiciones de ocultación a lo largo de la y la [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) en particular. Por ejemplo, considere la [componente principal de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en).

[Uso del editor de plantillas](/help/sites-authoring/templates.md), el autor de la plantilla puede definir en el cuadro de diálogo de diseño qué opciones del componente de lista están disponibles para el autor de la página. Pueden habilitarse o deshabilitarse opciones como permitir que la lista sea una lista estática, una lista de páginas secundarias, una lista de páginas etiquetadas, etc.

Si un autor de una plantilla decide deshabilitar la opción de páginas secundarias, se establece una propiedad de diseño y se evalúa una condición de ocultación con respecto a ella, lo que hace que la opción no se procese para el autor de la página.

1. De forma predeterminada, el autor de la página puede utilizar el componente principal de la lista para crear una lista con páginas secundarias eligiendo la opción **Páginas secundarias**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. En el cuadro de diálogo de diseño del componente principal de lista, el autor de la plantilla puede elegir la opción **Desactivar elementos secundarios** para evitar que la opción de generar una lista basada en páginas secundarias se muestre al autor de la página.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Se crea un nodo de directivas en `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` con una propiedad `disableChildren` establezca en `true`.
1. La condición de ocultar se define como el valor de un `granite:hide` en el nodo de propiedades del cuadro de diálogo `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. El valor de `disableChildren` se extrae de la configuración de diseño y de la expresión `${cqDesign.disableChildren}` se evalúa como `false`, lo que significa que la opción no se procesará como parte del componente.

   Puede ver la expresión &quot;hide&quot; como el valor del `granite:hide` propiedad [en GitHub aquí](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. La opción **Páginas secundarias** ya no se representa para el autor de la página al utilizar el componente de lista.

   ![chlimage_1-221](assets/chlimage_1-221.png)
