---
title: Personalización de la creación de páginas
seo-title: Customizing Page Authoring
description: AEM La ofrece varios mecanismos para permitirle personalizar la funcionalidad de creación de páginas
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---

# Personalización de la creación de páginas{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento describe cómo personalizar la creación de páginas en la IU moderna y táctil, y no se aplica a la IU clásica.

AEM proporciona varios mecanismos para permitirle personalizar la funcionalidad de creación de páginas (y la variable [consolas](/help/sites-developing/customizing-consoles-touch.md)) de la instancia de creación.

* Clientlibs

   Clientlibs le permite ampliar la implementación predeterminada para obtener nuevas funcionalidades, mientras reutiliza las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.` La nueva clientlib debe:

   * dependen de la clientlib de creación `cq.authoring.editor.sites.page`
   * formar parte de la `cq.authoring.editor.sites.page.hook` categoría

* Superposiciones

   Las superposiciones se basan en definiciones de nodos y permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no es necesaria una copia 1:1 del original, ya que la variable [fusión de recursos de sling](/help/sites-developing/sling-resource-merger.md) permite la herencia.

>[!NOTE]
>
>Para obtener más información, consulte la [Conjunto de documentación JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

AEM Se pueden utilizar de muchas maneras para ampliar la funcionalidad de creación de páginas en la instancia de. A continuación se describen algunas opciones (en un nivel superior).

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* Uso y creación de [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso y creación de [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM Estructura de la interfaz de usuario táctil de la](/help/sites-developing/touch-ui-structure.md) para obtener más información sobre las áreas estructurales utilizadas para la creación de páginas.
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
>1. Realice cualquier cambio en `/apps`


## Añadir nueva capa (modo) {#add-new-layer-mode}

Al editar una página, hay varias opciones [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponible. Estos modos se implementan mediante [capas](/help/sites-developing/touch-ui-structure.md#layer). Permiten acceder a diferentes tipos de funcionalidades para el mismo contenido de página. Las capas estándar son: editar, previsualizar, anotar, desarrollador y segmentación.

### Ejemplo de capa: estado de Live Copy {#layer-example-live-copy-status}

AEM Una instancia de estándar proporciona la capa de MSM. Esto accede a los datos relacionados con [administración de varios sitios](/help/sites-administering/msm.md) y lo resalta en la capa.

Para verlo en acción, puede editar cualquiera [Copia de idioma de We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (o cualquier otra página de live copy) y seleccione la **Estado de Live Copy** modo.

Puede encontrar la definición de capa de MSM (para referencia) en:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Ejemplo de código {#code-sample}

Este es un paquete de muestra que muestra cómo crear una nueva capa (modo), que es una nueva capa para la vista MSM.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-new-layer-mode en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Añadir nueva categoría de selección al navegador de recursos {#add-new-selection-category-to-asset-browser}

El explorador de recursos muestra recursos de varios tipos o categorías (por ejemplo, imágenes, documentos, etc.). Los recursos también se pueden filtrar por estas categorías de recursos.

### Ejemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` es un paquete de muestra que muestra cómo agregar un nuevo grupo al buscador de recursos. Este ejemplo conecta con [Flickr](https://www.flickr.com)El flujo público de y los muestra en el panel lateral.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-assetfinder-flickr en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrado de recursos {#filtering-resources}

Al crear páginas, el usuario debe seleccionar a menudo entre recursos (p. ej. páginas, componentes, recursos, etc.). Esto puede adoptar la forma de una lista, por ejemplo, desde la que el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Por ejemplo, si la variable [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) se utiliza para permitir al usuario seleccionar la ruta a un recurso concreto, las rutas presentadas se pueden filtrar de la siguiente manera:

* Implementar el predicado personalizado implementando [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) interfaz.
* Especifique un nombre para el predicado y haga referencia a ese nombre cuando utilice la variable `pathbrowser`.

Para obtener más información sobre la creación de un predicado personalizado, consulte [este artículo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementación de un predicado personalizado mediante la implementación `com.day.cq.commons.predicate.AbstractNodePredicate` La interfaz de también funciona en la IU clásica.
>
>Consulte [este artículo de la base de conocimiento](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) para ver un ejemplo de implementación de un predicado personalizado en la IU clásica.

## Agregar una nueva acción a una barra de herramientas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente (normalmente) tiene una barra de herramientas que proporciona acceso a una serie de acciones que se pueden realizar en ese componente.

### Ejemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de herramientas para procesar componentes.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-toolbar-screenshot en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Añadir nuevo editor en contexto {#add-new-in-place-editor}

### Editor in situ estándar {#standard-in-place-editor}

En una instalación estándar de AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene definiciones de los distintos editores disponibles.

1. Existe una conexión entre el editor y cada tipo de recurso (como en el componente ) que puede utilizarlo:

   * `cq:inplaceEditing`

      por ejemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propiedad: `editorType`

            Define el tipo de editor en línea que se utilizará cuando se active la edición in situ para ese componente; p. ej., `text`, `textimage`, `image`, `title`.

1. Se pueden configurar detalles de configuración adicionales del editor mediante una `config` nodo que contiene configuraciones, así como un `plugin` para contener los detalles de configuración del complemento necesarios.

   A continuación se muestra un ejemplo de definición de relaciones de aspecto para el complemento de recorte de imágenes del componente de imagen. Tenga en cuenta que debido al potencial del tamaño de pantalla muy limitado, las relaciones de aspecto de recorte se trasladaron al editor de pantalla completa y solo se pueden ver allí.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >AEM Tenga en cuenta que en las proporciones de recorte de la, según lo establecido por la variable `ratio` , se definen como **alto/ancho**. Esto difiere de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios autores no notarán ninguna diferencia siempre que defina la variable `name` claramente, ya que esto es lo que se muestra en la interfaz de usuario.

#### Creación de un nuevo editor in situ {#creating-a-new-in-place-editor}

Para implementar un nuevo editor in situ (dentro de la clientlib):

>[!NOTE]
>
>Por ejemplo, consulte:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre el editor (incluye el constructor):

   * `editor.register`

1. Proporcione la conexión entre el editor y cada tipo de recurso (como en el componente) que pueda utilizarlo.

#### Ejemplo de código para crear un nuevo editor en contexto {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` AEM es un paquete de muestra que muestra cómo crear un nuevo editor in situ en el entorno de trabajo de.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-in-place-editor en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuración de varios editores locales {#configuring-multiple-in-place-editors}

Es posible configurar un componente para que tenga varios editores in situ. Cuando se configuran varios editores locales, puede seleccionar el contenido adecuado y abrir el editor correspondiente. Consulte la [Configuración de varios editores locales](/help/sites-developing/multiple-inplace-editors.md) para obtener más información.

## Añadir una acción de nueva página {#add-a-new-page-action}

Para agregar una acción de nueva página a la barra de herramientas de la página, por ejemplo, una **Volver a Sitios** Acción (consola).

### Ejemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de encabezado para volver a la consola Sitios.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-authoring-extension-header-backtosites en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizar el flujo de trabajo de solicitud de activación {#customizing-the-request-for-activation-workflow}

El flujo de trabajo listo para usar, **Solicitud de activación**:

* Aparecerá automáticamente en el menú apropiado cuando un autor de contenido **no tiene** los derechos de replicación adecuados, pero **tiene** Pertenencia a DAM-Users y Authors.

* De lo contrario, no se mostrará nada, ya que se han eliminado los derechos de replicación.

Para tener un comportamiento personalizado tras dicha activación, puede superponer la variable **Solicitud de activación** flujo de trabajo:

1. Entrada `/apps` superponga el **Sites** asistente:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Esto en sí, anula la instancia común de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Actualice el [modelo de flujo de trabajo](/help/sites-developing/workflows-models.md) y configuraciones/scripts relacionados según sea necesario.
1. Retire el derecho a la [ `replicate` acción](/help/sites-administering/security.md#actions) de todos los usuarios adecuados para todas las páginas relevantes; para que este flujo de trabajo se active como una acción predeterminada cuando cualquiera de los usuarios intente publicar (o replicar) una página.
