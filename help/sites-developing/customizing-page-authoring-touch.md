---
title: Personalización de la creación de páginas
seo-title: Personalización de la creación de páginas
description: AEM proporciona varios mecanismos que le permiten personalizar la funcionalidad de creación de páginas
seo-description: AEM proporciona varios mecanismos que le permiten personalizar la funcionalidad de creación de páginas
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Personalización de la creación de páginas{#customizing-page-authoring}

>[!CAUTION]
>
>En este documento se describe cómo personalizar la creación de páginas en la moderna IU táctil y no se aplica a la IU clásica.

AEM proporciona varios mecanismos que le permiten personalizar la funcionalidad de creación de páginas (y las [consolas](/help/sites-developing/customizing-consoles-touch.md)) de la instancia de creación.

* Clientlibs

   Las bibliotecas de clientes permiten ampliar la implementación predeterminada para obtener una nueva funcionalidad, al mismo tiempo que se reutilizan las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.` La nueva clientlib debe:

   * depender de la clientlib de creación `cq.authoring.editor.sites.page`
   * formar parte de la categoría adecuada `cq.authoring.editor.sites.page.hook`

* Superposiciones

   Las superposiciones se basan en definiciones de nodos y permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no se requiere una copia 1:1 del original, ya que la combinación [de recursos](/help/sites-developing/sling-resource-merger.md) de sling permite la herencia.

>[!NOTE]
>
>Para obtener más información, consulte el conjunto [de documentación de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)JS.

Se pueden utilizar de muchas formas para ampliar la funcionalidad de creación de páginas en la instancia de AEM. A continuación se incluye una selección (de alto nivel).

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Usar y crear [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso y creación de [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estructura de la IU](/help/sites-developing/touch-ui-structure.md) táctil de AEM para obtener detalles sobre las áreas estructurales utilizadas para la creación de páginas.
>
>
Este tema también se trata en la sesión [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) : personalización de la interfaz [de usuario para AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>No ***debe*** cambiar nada en la `/libs` ruta.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
>1. Realice los cambios en `/apps`


## Agregar nueva capa (modo) {#add-new-layer-mode}

Al editar una página, hay varios [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponibles. Estos modos se implementan mediante [capas](/help/sites-developing/touch-ui-structure.md#layer). Permiten el acceso a diferentes tipos de funcionalidad para el mismo contenido de página. Las capas estándar son: editar, previsualizar, anotar, desarrollar y segmentar.

### Ejemplo de capa:Estado de Live Copy {#layer-example-live-copy-status}

Una instancia de AEM estándar proporciona la capa MSM. Esto accede a los datos relacionados con la administración [de](/help/sites-administering/msm.md) varios sitios y los resalta en la capa.

Para verlo en acción, puede editar cualquier página de copia [del idioma](/help/sites-developing/we-retail-globalized-site-structure.md) We.Retail (o cualquier otra página de Live Copy) y seleccionar el modo de estado **de** Live Copy.

Puede encontrar la definición de capa MSM (como referencia) en:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Ejemplo de código {#code-sample}

Este es un paquete de muestra que muestra cómo crear una nueva capa (modo), que es una nueva capa para la vista MSM.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de modo de nueva capa de creación de AEM en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Agregar nueva categoría de selección al navegador de recursos {#add-new-selection-category-to-asset-browser}

El navegador de recursos muestra recursos de diversos tipos o categorías (por ejemplo, imágenes, documentos, etc.). Los recursos también se pueden filtrar por estas categorías de recursos.

### Ejemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` es un paquete de muestra que muestra cómo agregar un nuevo grupo al buscador de recursos. Este ejemplo se conecta al flujo público de [Flickr](https://www.flickr.com)y se muestra en el panel lateral.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-authoring-extension-assetfinder-flickr en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrado de recursos {#filtering-resources}

Al crear páginas, el usuario debe seleccionar a menudo entre los recursos (p. ej. páginas, componentes, recursos, etc.). Esto puede adoptar la forma de una lista, por ejemplo, desde la que el autor debe elegir un elemento.

Para mantener la lista en un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Por ejemplo, si se utiliza el componente [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite [](/help/sites-developing/touch-ui-concepts.md#granite-ui) para permitir al usuario seleccionar la ruta a un recurso determinado, las rutas presentadas se pueden filtrar de la siguiente manera:

* Implementar el predicado personalizado mediante la implementación de la [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) interfaz.
* Especifique un nombre para el predicado y consulte ese nombre al usar el `pathbrowser`.

Para obtener más información sobre la creación de un predicado personalizado, consulte [este artículo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>La implementación de un predicado personalizado mediante la implementación de `com.day.cq.commons.predicate.AbstractNodePredicate` una interfaz también funciona en la IU clásica.
>
>Consulte [este artículo](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) de la base de conocimientos para ver un ejemplo de implementación de un predicado personalizado en la IU clásica.

## Agregar nueva acción a una barra de herramientas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente (normalmente) tiene una barra de herramientas que proporciona acceso a una serie de acciones que se pueden realizar en dicho componente.

### Ejemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` es un paquete de muestra que muestra cómo crear una acción de barra de herramientas personalizada para procesar componentes.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de captura de pantalla de la barra de herramientas de aem-authoring-extension-toolbar en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Agregar nuevo editor in-situ {#add-new-in-place-editor}

### Editor in situ estándar {#standard-in-place-editor}

En una instalación estándar de AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene definiciones de los diversos editores disponibles.

1. Hay una conexión entre el editor y cada tipo de recurso (como en el componente) que puede utilizarlo:

   * `cq:inplaceEditing`

      por ejemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propiedad: `editorType`

            Define el tipo de editor en línea que se utilizará cuando se active la edición in-situ para ese componente;p. ej. `text`, `textimage`, `image`, `title`.

1. Los detalles de configuración adicionales del editor se pueden configurar usando un `config` nodo que contenga configuraciones, así como otro `plugin` nodo que contenga los detalles de configuración del complemento necesarios.

   A continuación se muestra un ejemplo de definición de proporciones de aspecto para el complemento de recorte de imagen del componente de imagen. Tenga en cuenta que debido al potencial de tamaño de pantalla muy limitado, las proporciones de aspecto de recorte se movieron al editor de pantalla completa y solo se pueden ver allí.

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
   >Tenga en cuenta que en las relaciones de recorte de AEM, definidas por la `ratio` propiedad, se definen como **altura/ancho**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas heredados. The authoring users will not be aware of any difference provided you define the `name` property clearly since this is what is displayed in the UI.

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

#### Ejemplo de código para crear un nuevo editor in situ {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` es un paquete de muestra que muestra cómo crear un nuevo editor in situ en AEM.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de editor de aem-authoring-extension-in-place en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuración de varios editores in situ {#configuring-multiple-in-place-editors}

Es posible configurar un componente para que tenga varios editores in-situ. Cuando se configuran varios editores in situ, puede seleccionar el contenido adecuado y abrir el editor correspondiente. Consulte la documentación [Configuración de varios editores](/help/sites-developing/multiple-inplace-editors.md) in-situ para obtener más información.

## Add a New Page Action {#add-a-new-page-action}

Para agregar una nueva acción de página a la barra de herramientas de la página, por ejemplo una acción **Volver a sitios** (consola).

### Ejemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` es un paquete de muestra que muestra cómo crear una acción de barra de encabezado personalizada para volver a la consola Sitios.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de aem-authoring-extension-header-backtosites en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalización del flujo de trabajo de solicitud de activación {#customizing-the-request-for-activation-workflow}

El flujo de trabajo predeterminado, **Solicitud de activación**, se activa automáticamente cuando un autor de contenido no tiene los derechos de replicación adecuados.

Para tener un comportamiento personalizado tras dicha activación, puede superponer el flujo de trabajo de **Solicitud de activación** :

1. En `/apps` superposición, el asistente **Sitios** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Esto mismo anula la instancia común de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Actualice el modelo [de](/help/sites-developing/workflows-models.md) flujo de trabajo y las configuraciones/secuencias de comandos relacionadas según sea necesario.
1. Eliminar el derecho a la [ acción `replicate`](/help/sites-administering/security.md#actions) de todos los usuarios correspondientes para todas las páginas relevantes; para que este flujo de trabajo se active como acción predeterminada cuando cualquiera de los usuarios intente publicar (o replicar) una página.

