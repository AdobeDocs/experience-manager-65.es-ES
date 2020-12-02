---
title: Personalización de las consolas
seo-title: Personalización de las consolas
description: AEM proporciona varios mecanismos que le permiten personalizar las consolas de la instancia de creación
seo-description: AEM proporciona varios mecanismos que le permiten personalizar las consolas de la instancia de creación
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---


# Personalización de las consolas {#customizing-the-consoles}

>[!CAUTION]
>
>En este documento se describe cómo personalizar consolas en la IU táctil moderna y no se aplica a la IU clásica.

AEM proporciona varios mecanismos para permitirle personalizar las consolas (y la [funcionalidad de creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)) de la instancia de creación.

* Clientlibs
Las bibliotecas de clientes permiten ampliar la implementación predeterminada para obtener una nueva funcionalidad, al mismo tiempo que se reutilizan las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.`. Por ejemplo, puede contener el código necesario para el componente personalizado.

* Superposiciones
Las superposiciones se basan en definiciones de nodos y permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no se requiere una copia 1:1 del original, ya que la fusión de recursos de sling permite la herencia.

Estos pueden utilizarse de muchas maneras para ampliar las consolas de AEM. A continuación se incluye una pequeña selección (de alto nivel).

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Usar y crear [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso y creación de [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
Este tema también se trata en la sesión [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html): [Personalización de la interfaz de usuario para AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y bien puede sobrescribirse al aplicar una revisión o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
   >
   >
1. Realice cualquier cambio dentro de `/apps`

>



Por ejemplo, se puede superponer la siguiente ubicación dentro de la estructura `/libs`:

* consolas (cualquier consola basada en páginas de la interfaz de usuario de Granite); por ejemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte el artículo de la Base de conocimiento, [Solución de problemas de AEM TouchUI](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obtener más sugerencias y herramientas.

## Personalización de la Vista predeterminada para una consola {#customizing-the-default-view-for-a-console}

Puede personalizar la vista predeterminada (columna, tarjeta, lista) para una consola:

1. Puede reordenar las vistas superponiendo la entrada requerida desde:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La primera entrada será la predeterminada.

   Los nodos disponibles se correlacionan con las opciones de vista disponibles:

   * `column`
   * `card`
   * `list`

1. Por ejemplo, en una superposición para lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina la siguiente propiedad:

   * **Nombre**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**:  `column`

### Añadir nueva acción en la barra de herramientas {#add-new-action-to-the-toolbar}

1. Puede crear sus propios componentes e incluir las bibliotecas de cliente correspondientes para acciones personalizadas. Por ejemplo, una acción **Promocionar a Twitter** en:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Esto se puede conectar a un elemento de la barra de herramientas de la consola:

   `/apps/<yourProject>/admin/ext/launches`

   Por ejemplo, en el modo de selección:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir una acción de barra de herramientas a un grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. Puede utilizar una condición de procesamiento personalizada para superponer la acción estándar e imponer condiciones específicas que deben cumplirse antes de procesarse.

   Por ejemplo, cree un componente para controlar las condiciones de procesamiento según el grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicarlas a la acción Crear sitio en la consola Sitios:

   `/libs/wcm/core/content/sites`

   Cree la superposición:

   `/apps/wcm/core/content/sites`

1. A continuación, agregue la condición de procesamiento para la acción:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Mediante las propiedades de este nodo puede definir el `groups` permitido para realizar la acción específica; por ejemplo, `administrators`

### Personalización de columnas en la Vista de Lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Esta función está optimizada para columnas de campos de texto; para otros tipos de datos, es posible superponer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` en `/apps`.

Para personalizar las columnas de la vista de lista:

1. Superponga la lista de las columnas disponibles.

   * En el nodo:

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Añada las nuevas columnas o elimine las existentes.
   Consulte [Uso de Overlays (y la fusión de recursos de Sling)](/help/sites-developing/overlays.md) para obtener más información.

1. De forma opcional:

   * Si desea conectar datos adicionales, debe escribir un [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con un
      `pageInfoProviderType` propiedad.

   Por ejemplo, consulte la clase o paquete adjunto (de GitHub) a continuación.

1. Ahora puede seleccionar la columna en el configurador de columnas de la vista de lista.

### Filtrado de recursos {#filtering-resources}

Cuando se utiliza una consola, un caso de uso común es cuando el usuario debe seleccionar entre los recursos (p. ej. páginas, componentes, recursos, etc.). Esto puede adoptar la forma de una lista, por ejemplo, desde la cual el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Consulte [este artículo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obtener más información.
