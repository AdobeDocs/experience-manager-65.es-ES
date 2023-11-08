---
title: Personalización de las consolas
seo-title: Customizing the Consoles
description: AEM varios mecanismos para permitirle personalizar las consolas de su instancia de creación
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# Personalización de las consolas {#customizing-the-consoles}

>[!CAUTION]
>
>Este documento describe cómo personalizar las consolas en la IU moderna y táctil, y no se aplica a la IU clásica.

AEM proporciona varios mecanismos para permitirle personalizar las consolas (y la variable [funcionalidad de creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)) de la instancia de creación.

* Clientlibs Clientlibs le permite ampliar la implementación predeterminada para obtener nuevas funcionalidades, mientras reutiliza las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.` Por ejemplo, puede contener el código necesario para el componente personalizado.

* Las superposiciones se basan en definiciones de nodos y permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no se requiere una copia 1:1 del original, ya que la fusión de recursos de sling permite la herencia.

AEM Se pueden utilizar de muchas maneras para ampliar las consolas de la. Una pequeña selección se cubren a continuación (en un nivel alto).

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* Uso y creación de [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso y creación de [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>Usted ***debe*** no cambie nada en el `/libs` ruta.
>
>Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
>
>1. Realice cualquier cambio en `/apps`
>

Por ejemplo, la siguiente ubicación dentro de `/libs` La estructura se puede superponer:

* consolas (cualquier consola basada en páginas de interfaz de usuario de Granite); por ejemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte el artículo de la Base de conocimiento, [AEM Solución de problemas de IU táctil](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obtener más sugerencias y herramientas.

## Personalización de la Vista Predeterminada para una Consola {#customizing-the-default-view-for-a-console}

Puede personalizar la vista predeterminada (columna, tarjeta, lista) de una consola:

1. Puede reordenar las vistas superponiendo la entrada requerida desde:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La primera entrada es la predeterminada.

   Los nodos disponibles se correlacionan con las opciones de vista disponibles:

   * `column`
   * `card`
   * `list`

1. Por ejemplo, en una superposición para la lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina la siguiente propiedad:

   * **Nombre**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**: `column`

### Agregar nueva acción a la barra de herramientas {#add-new-action-to-the-toolbar}

1. Puede crear sus propios componentes e incluir las bibliotecas de cliente correspondientes para las acciones personalizadas. Por ejemplo, una **Promocionar a Twitter** acción en:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   A continuación, se puede conectar a un elemento de la barra de herramientas de la consola:

   `/apps/<yourProject>/admin/ext/launches`

   Por ejemplo, en el modo de selección:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir una acción de barra de herramientas a un grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. Puede utilizar una condición de procesamiento personalizada para superponer la acción estándar e imponer condiciones específicas que deben cumplirse antes de que se procese.

   Por ejemplo, cree un componente para controlar las condiciones de procesamiento según el grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicarlos a la acción Crear sitio en la consola Sitios:

   `/libs/wcm/core/content/sites`

   Cree la superposición:

   `/apps/wcm/core/content/sites`

1. A continuación, añada la condición de procesamiento para la acción:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Con las propiedades de este nodo puede definir la variable `groups` puede realizar la acción específica; por ejemplo, `administrators`

### Personalización de columnas en la vista de lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Esta función está optimizada para columnas de campos de texto; para otros tipos de datos es posible superponer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Para personalizar las columnas en la vista de lista:

1. Superponga la lista de columnas disponibles.

   * En el nodo:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Añada las columnas nuevas o elimine las existentes.

   Consulte [Uso de superposiciones (y la fusión de recursos de Sling)](/help/sites-developing/overlays.md) para obtener más información.

1. Opcionalmente:

   * Si desea conectar datos adicionales, debe escribir un [PageInfoProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con un
     `pageInfoProviderType` propiedad.

   Por ejemplo, consulte la clase/paquete adjunto (de GitHub) a continuación.

1. Ahora puede seleccionar la columna en el configurador de columnas de la vista de lista.

### Filtrado de recursos {#filtering-resources}

Al utilizar una consola, un caso de uso común es cuando el usuario debe seleccionar entre recursos (por ejemplo, páginas, componentes, recursos, etc.). Esto puede adoptar la forma de una lista, por ejemplo, desde la que el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Consulte [este artículo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obtener más información.
