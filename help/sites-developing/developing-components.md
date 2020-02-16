---
title: Desarrollo de componentes de AEM
seo-title: Desarrollo de componentes de AEM
description: Los componentes de AEM se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.
seo-description: Los componentes de AEM se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Desarrollo de componentes de AEM{#developing-aem-components}

Los componentes de AEM se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.

* Al [crear páginas](/help/sites-authoring/default-components.md), los componentes permiten a los autores editar y configurar el contenido.

   * Al construir un sitio de [comercio](/help/sites-administering/ecommerce.md) , los componentes pueden, por ejemplo, recopilar y procesar información del catálogo.
See [Developing eCommerce](/help/sites-developing/ecommerce.md) for more information.

   * Al construir un sitio de [comunidades](/help/communities/author-communities.md) , los componentes pueden proporcionar información a los visitantes y recopilarla.
See [Developing Communities](/help/communities/communities.md) for more information.

* En la instancia de publicación, los componentes representan el contenido y lo presentan como es necesario para los visitantes del sitio web.

>[!NOTE]
>
>Esta página es una continuación del documento Componentes de [AEM: conceptos básicos](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Los siguientes componentes `/libs/cq/gui/components/authoring/dialog` están pensados para utilizarse solo en el Editor (cuadros de diálogo de componentes en Creación). Si se utilizan en otro lugar (por ejemplo, en un cuadro de diálogo de asistente), es posible que no se comporten del modo esperado.

## Ejemplos de código {#code-samples}

Esta página proporciona la documentación de referencia (o vínculos a la documentación de referencia) necesaria para desarrollar nuevos componentes para AEM. Consulte [Desarrollo de componentes de AEM: ejemplos](/help/sites-developing/developing-components-samples.md) de código para ver algunos ejemplos prácticos.

## Estructura {#structure}

La estructura básica de un componente se describe en la página Componentes de [AEM: Conceptos básicos](/help/sites-developing/components-basics.md#structure). Ese documento abarca tanto las IU táctiles como las clásicas. Aunque no necesite usar la configuración clásica en el nuevo componente, puede ser de ayuda que los conozca al heredar de componentes existentes.

## Ampliación de los componentes y cuadros de diálogo existentes {#extending-existing-components-and-dialogs}

Según el componente que desee implementar, puede que sea posible ampliar o personalizar una instancia existente, en lugar de definir y desarrollar toda la [estructura](#structure) desde cero.

Al ampliar o personalizar un componente o cuadro de diálogo existente, puede copiar o replicar toda la estructura o la estructura necesaria para el cuadro de diálogo antes de realizar los cambios.

### Ampliación de un componente existente {#extending-an-existing-component}

La ampliación de un componente existente se puede lograr con la jerarquía [de tipo de](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) recurso y los mecanismos de herencia relacionados.

>[!NOTE]
>
>Los componentes también se pueden redefinir con una superposición basada en la lógica de ruta de búsqueda. Sin embargo, en este caso, la fusión [de recursos](/help/sites-developing/sling-resource-merger.md) Sling no se activará y `/apps` debe definir la superposición completa.

>[!NOTE]
>
>El componente [de fragmento de](/help/sites-developing/customizing-content-fragments.md) contenido también se puede personalizar y ampliar, aunque se debe tener en cuenta la estructura completa y las relaciones con Recursos.

### Personalización de un cuadro de diálogo de componente existente {#customizing-a-existing-component-dialog}

También es posible anular un cuadro de diálogo *de* componente mediante la fusión [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling y la definición de la propiedad `sling:resourceSuperType`.

Esto significa que solo necesita redefinir las diferencias necesarias, en lugar de redefinir todo el cuadro de diálogo (mediante `sling:resourceSuperType`). Ahora se recomienda utilizar este método para ampliar un cuadro de diálogo de componentes

Consulte la Fusión [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling para obtener más detalles.

## Definición de la marca {#defining-the-markup}

El componente se procesará con [HTML](https://www.w3schools.com/htmL/html_intro.asp). El componente debe definir el HTML necesario para tomar el contenido necesario y, a continuación, procesarlo según sea necesario, tanto en el entorno de creación como en el de publicación.

### Uso del lenguaje de plantilla HTML {#using-the-html-template-language}

The [HTML Templating Language (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), introduced with AEM 6.0, takes the place of JSP (JavaServer Pages) as the preferred and recommended server-side template system for HTML. Para los desarrolladores web que necesitan crear sitios web empresariales sólidos, HTL ayuda a lograr una mayor seguridad y eficiencia de desarrollo.

>[!NOTE]
>
>Aunque tanto HTL como JSP pueden utilizarse para desarrollar componentes, ilustraremos el desarrollo con HTL en esta página, ya que es el lenguaje de secuencias de comandos recomendado para AEM.

## Desarrollo de la lógica de contenido {#developing-the-content-logic}

Esta lógica opcional selecciona o calcula el contenido que se va a representar. Se invoca desde expresiones HTL con el patrón de uso-API adecuado.

El mecanismo para separar la lógica de la apariencia ayuda a aclarar lo que se necesita para una vista determinada. También permite una lógica diferente para distintas vistas del mismo recurso.

### Uso de Java {#using-java}

[La Use-API de HTL Java permite que un archivo HTL acceda a los métodos de ayuda en una clase](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)Java personalizada. Esto le permite utilizar código Java para implementar la lógica de selección y configuración del contenido del componente.

### Uso de JavaScript {#using-javascript}

[La Use-API de JavaScript de HTL permite que un archivo HTL acceda al código de ayuda escrito en JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Esto le permite utilizar código JavaScript para implementar la lógica de selección y configuración del contenido del componente.

### Uso de bibliotecas HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a solucionar este problema, AEM proporciona carpetas **de biblioteca del lado del** cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente. El sistema de biblioteca del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Lea [Uso de bibliotecas](/help/sites-developing/clientlibs.md) HTML del lado del cliente para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente, incluyendo atributos como acciones disponibles para el componente, características del editor in-situ y los oyentes relacionados con los eventos del componente. La configuración es común a la IU táctil y a la clásica, aunque con ciertas diferencias específicas.

El comportamiento de [edición de un componente se configura](/help/sites-developing/components-basics.md#edit-behavior) agregando un `cq:editConfig` nodo de tipo `cq:EditConfig` debajo del nodo del componente (de tipo `cq:Component`) y agregando propiedades y nodos secundarios específicos.

## Configuración del comportamiento de vista previa {#configuring-the-preview-behavior}

La cookie de modo [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM se establece al cambiar al modo de **vista previa** aunque la página no se actualice.

Para los componentes con una representación sensible al modo WCM, deben definirse para actualizarse específicamente y, a continuación, basarse en el valor de la cookie.

>[!NOTE]
>
>En la IU táctil solo se utilizan los valores `EDIT` y `PREVIEW` para la cookie de modo [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM.

## Creación y configuración de un cuadro de diálogo {#creating-and-configuring-a-dialog}

Los cuadros de diálogo se utilizan para permitir que el autor interactúe con el componente. El uso de un cuadro de diálogo permite a los autores y/o administradores editar contenido, configurar el componente o definir parámetros de diseño (mediante un cuadro de diálogo [de](#creating-and-configuring-a-design-dialog)diseño)

### IU de Coral y Granite {#coral-ui-and-granite-ui}

[La interfaz de usuario](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) de Coral y la interfaz de usuario de [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) definen el aspecto moderno de AEM.

[La interfaz de usuario de Granite proporciona una amplia gama de componentes básicos (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necesarios para crear el cuadro de diálogo en el entorno de creación. Cuando sea necesario, puede ampliar esta selección y [crear su propia utilidad](#creatinganewwidget).

Para obtener más información sobre el desarrollo de componentes mediante tipos de recursos de Coral y Granite, consulte: [Creación de componentes de Experience Manager mediante tipos](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)de recursos de Coral/Granite.

Para obtener más información, consulte:

* Interfaz de usuario de Coral

   * Proporciona una interfaz de usuario coherente en todas las soluciones de nube
   * [Conceptos de la IU táctil de AEM: IU de Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guía de Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interfaz de usuario de granito

   * Proporciona marcas de Coral UI incluidas en los componentes de Sling para crear consolas de interfaz de usuario y cuadros de diálogo
   * [Conceptos de la interfaz de usuario táctil de AEM: Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>Debido a la naturaleza de los componentes de la interfaz de usuario Granite (y a las diferencias con los widgets ExtJS), hay algunas diferencias entre la forma en que los componentes interactúan con la interfaz de usuario táctil y la IU [](/help/sites-developing/developing-components-classic.md)clásica.

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Cuadros de diálogo para la IU táctil:

* se denominan `cq:dialog`.
* se definen como un `nt:unstructured` nodo con el conjunto de `sling:resourceType` propiedades.

* se encuentran bajo su `cq:Component` nodo y junto a su definición de componente.
* se procesan en el servidor (como componentes Sling), según la estructura de contenido y la `sling:resourceType` propiedad.
* utilice la interfaz de usuario Granite.
* contiene una estructura de nodos que describe los campos del cuadro de diálogo.

   * estos nodos están `nt:unstructured` con la `sling:resourceType` propiedad requerida.

Una estructura de nodos de ejemplo puede ser:

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

La personalización de un cuadro de diálogo es similar al desarrollo de un componente, ya que el cuadro de diálogo es un componente (es decir, el marcado procesado por un script de componente junto con el comportamiento o estilo proporcionado por una biblioteca de cliente).

Para ver ejemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Si un componente no tiene ningún cuadro de diálogo definido para la IU táctil, el cuadro de diálogo de la IU clásica se utiliza como alternativa dentro de una capa de compatibilidad. Para personalizar este cuadro de diálogo, debe personalizar el cuadro de diálogo de IU clásica. Consulte Componentes de [AEM para la IU](/help/sites-developing/developing-components-classic.md)clásica.

### Personalización de los campos del cuadro de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* la sesión de AEM Gems sobre la [personalización de los campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)del cuadro de diálogo.
>* el código de muestra relacionado cubierto en Ejemplo de [código: Cómo personalizar campos](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)de cuadro de diálogo.
>



#### Creación de un nuevo campo {#creating-a-new-field}

Las utilidades de la interfaz de usuario táctil se implementan como componentes de la interfaz de usuario de Granite.

Para crear una nueva utilidad para utilizarla en un cuadro de diálogo de componentes para la IU táctil, es necesario [crear un nuevo componente](/help/sites-developing/granite-ui-component.md)de campo de la interfaz de usuario de Granite.

>[!NOTE]
>
>Para obtener más información sobre la interfaz de usuario de Granite, consulte la documentación [de la interfaz de usuario de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Granite.

Si considera el cuadro de diálogo como un contenedor sencillo para un elemento de formulario, también puede ver el contenido principal del cuadro de diálogo como campos de formulario. La creación de un nuevo campo de formulario requiere la creación de un tipo de recurso; esto equivale a crear un componente nuevo. Para ayudarle en esa tarea, la interfaz de usuario de Granite ofrece un componente de campo genérico del que heredar (mediante `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Más específicamente, la interfaz de usuario de Granite proporciona una serie de componentes de campo que se pueden utilizar en los diálogos (o, más generalmente, en [formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Esto difiere de la IU clásica, en la que los widgets se representan mediante `cq:Widgets` nodos, cada uno con un `xtype` objeto concreto de establecer la relación con el widget ExtJS correspondiente. Desde el punto de vista de la implementación, estos widgets se procesaron en el lado del cliente mediante el marco de trabajo de ExtJS.

Una vez creado el tipo de recurso, puede crear una instancia del campo agregando un nuevo nodo en el cuadro de diálogo, con la propiedad `sling:resourceType` que hace referencia al tipo de recurso que acaba de introducir.

#### Creación de una biblioteca de clientes para estilo y comportamiento {#creating-a-client-library-for-style-and-behavior}

Si desea definir el estilo y el comportamiento de su componente, puede crear una biblioteca [de](/help/sites-developing/clientlibs.md) cliente dedicada que defina su CSS/LESS y JS personalizados.

Para que la biblioteca de cliente se cargue únicamente para el cuadro de diálogo de componentes (es decir, no se cargará para otro componente), debe establecer la propiedad `extraClientlibs`*** **del cuadro de diálogo en el nombre de categoría de la biblioteca de cliente que acaba de crear. Esto es aconsejable si la biblioteca del cliente es bastante grande y/o si el campo es específico de ese cuadro de diálogo y no será necesario en otros cuadros de diálogo.

Para que la biblioteca de cliente se cargue en todos los cuadros de diálogo, establezca la propiedad category de la biblioteca de cliente en `cq.authoring.dialog`. Es el nombre de categoría de la biblioteca del cliente que se incluye de forma predeterminada al procesar todos los cuadros de diálogo. Desea hacerlo si la biblioteca de cliente es pequeña o si el campo es genérico y puede reutilizarse en otros cuadros de diálogo.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * proporcionado por la muestra de [código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ampliación (heredado) de un campo {#extending-inheriting-from-a-field}

Según sus necesidades, puede:

* Extender un campo de la interfaz de usuario de Granite determinado por herencia de componentes ( `sling:resourceSuperType`)
* Extender un widget determinado desde la biblioteca de utilidades subyacente (en el caso de la interfaz de usuario de Granite, es Coral UI), siguiendo la API de la biblioteca de utilidades (herencia de JS/CSS)

#### Acceso a los campos del cuadro de diálogo {#access-to-dialog-fields}

También puede utilizar las condiciones de procesamiento ( `rendercondition`) para controlar quién tiene acceso a fichas o campos específicos en el cuadro de diálogo; por ejemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestión de eventos de campo {#handling-field-events}

El método de gestión de eventos en campos de diálogo ahora se realiza con [oyentes en una biblioteca](#listeners-in-a-custom-client-library)de cliente personalizada. Esto supone un cambio con respecto al método anterior de tener [oyentes en la estructura](#listenersinthecontentstructureclassicui)de contenido.

#### Oyentes en una biblioteca de clientes personalizada {#listeners-in-a-custom-client-library}

Para insertar lógica en el campo, debe:

1. Marque el campo con una clase CSS determinada (el *gancho*).
1. Defina, en la biblioteca de cliente, un detector JS conectado al nombre de la clase CSS (esto garantiza que la lógica personalizada solo se alcance en el campo y no afecta a otros campos del mismo tipo).

Para lograrlo, debe conocer la biblioteca de utilidades subyacente con la que desea interactuar. Consulte la documentación [de la interfaz de usuario de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) Coral para identificar el evento al que desea reaccionar. Esto es muy similar al proceso que tenía que realizar con ExtJS en el pasado: busque la página de documentación de una utilidad determinada y, a continuación, compruebe los detalles de su API de evento.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * proporcionado por la muestra de [código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Oyentes en la estructura de contenido {#listeners-in-the-content-structure}

En la IU clásica con ExtJS, era habitual tener oyentes para una utilidad determinada en la estructura de contenido. Lograr lo mismo en la IU táctil es diferente ya que el código de escucha de JS (o cualquier código) ya no se define en el contenido.

La estructura de contenido describe la estructura semántica; no debe implicar la naturaleza del widget subyacente. Al no tener el código JS en la estructura de contenido, puede cambiar los detalles de implementación sin tener que cambiar la estructura de contenido. En otras palabras, puede cambiar la biblioteca de utilidades sin necesidad de tocar la estructura de contenido.

### Validación de campos {#field-validation}

#### Campo obligatorio {#mandatory-field}

Para marcar un campo determinado como obligatorio, establezca la siguiente propiedad en el nodo de contenido del campo:

* Nombre: `required`
* Tipo: `Boolean`

Para ver un ejemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validación de campos (IU granítica) {#field-validation-granite-ui}

La validación de campos en la interfaz de usuario de Granite y los componentes de la interfaz de usuario de Granite (equivalentes a widgets) se realiza mediante la `foundation-validation` API. [Consulte la documentación de `foundation-valdiation` Granite para obtener más información.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * proporcionado por la muestra de [código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creación y configuración de un cuadro de diálogo de diseño {#creating-and-configuring-a-design-dialog}

El cuadro de diálogo Diseño se muestra cuando un componente tiene detalles de diseño que se pueden editar en el modo [](/help/sites-authoring/default-components-designmode.md)Diseño.

La definición es muy similar a la de un [cuadro de diálogo utilizado para editar contenido](#creating-a-new-dialog), con la diferencia de que se define como nodo:

* Node name: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creación y configuración de un editor en contexto {#creating-and-configuring-an-inplace-editor}

Un editor in-situ permite al usuario editar contenido directamente en el flujo de párrafos, sin necesidad de abrir un cuadro de diálogo. Por ejemplo, los componentes estándar Texto y Título tienen un editor in situ.

Un editor in situ no es necesario ni significativo para cada tipo de componente.

Consulte [Ampliación de la creación de páginas - Agregar nuevo editor](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) de entrada para obtener más información.

## Personalización de la barra de herramientas del componente {#customizing-the-component-toolbar}

La barra de herramientas [de](/help/sites-developing/touch-ui-structure.md#component-toolbar) componentes proporciona al usuario acceso a una serie de acciones para el componente, como editar, configurar, copiar y eliminar.

Consulte [Ampliación de la creación de páginas - Agregar nueva acción a una barra de herramientas](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) de componentes para obtener más información.

## Configuración de un componente para el carril de referencias (prestado/alquilado) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Si el nuevo componente hace referencia a contenido de otras páginas, puede considerar si desea que afecte a las secciones Contenido **** prestado y Contenido de **Cuartos** de [**referencias **](/help/sites-authoring/basic-handling.md#references)del raíl.

AEM incorporado solo comprueba el componente Referencia. Para agregar el componente, debe configurar la configuración **de referencia de contenido de creación** WCM del paquete OSGi.

Cree una nueva entrada en la definición, especificando el componente, junto con la propiedad que se va a comprobar. Por ejemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services. See [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## Activación y adición del componente al sistema de párrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Una vez desarrollado el componente, debe habilitarse para su uso en un sistema de párrafos adecuado, de modo que pueda utilizarse en las páginas requeridas.

Esto se puede realizar mediante:

* uso del modo [](/help/sites-authoring/default-components-designmode.md) Diseño al editar una página específica.
* [definición de la `components` propiedad en el sistema de párrafos de una plantilla](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM ofrece la posibilidad de configurar un sistema de párrafos en la página para que [una instancia del nuevo componente se cree automáticamente cuando un usuario arrastra un recurso (adecuado) a una instancia de esa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (en lugar de arrastrar siempre un componente vacío a la página).

Se puede configurar este comportamiento y la relación entre los recursos y los componentes necesaria:

1. Bajo la definición de párrafo del diseño de página. Por ejemplo:

   * `/etc/designs/<myApp>/page/par`
   Crear un nuevo nodo:

   * Nombre: `cq:authoring`
   * Tipo: `nt:unstructured`


1. En este campo, cree un nuevo nodo para albergar todas las asignaciones de recursos a componentes:

   * Nombre: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Para cada asignación de recursos a componentes, cree un nodo:

   * Nombre: texto; se recomienda que el nombre indique el recurso y el tipo de componente relacionado; por ejemplo, image
   * Tipo: `nt:unstructured`
   Cada una con las siguientes propiedades:

   * `assetGroup`:

      * Tipo: `String`
      * Valor: el grupo al que pertenece el activo relacionado; por ejemplo, `media`
   * `assetMimetype`:

      * Tipo: `String`
      * Valor: el tipo MIME del activo correspondiente; por ejemplo `image/*`
   * `droptarget`:

      * Tipo: `String`
      * Valor: el objetivo de colocación; por ejemplo, `image`
   * `resourceType`:

      * Tipo: `String`
      * Valor: el recurso de componente relacionado; por ejemplo, `foundation/components/image`
   * `type`:

      * Tipo: `String`
      * Valor: el tipo, por ejemplo, `Images`






Para ver ejemplos, consulte:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto aem-project-archetype en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creación automática de instancias de componentes ahora se puede configurar fácilmente en la interfaz de usuario al utilizar componentes [principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) y plantillas editables. Consulte [Creación de plantillas](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) de página para obtener más información sobre cómo definir qué componentes se asocian automáticamente a determinados tipos de medios.

## Uso de la extensión de corchetes AEM {#using-the-aem-brackets-extension}

La extensión [AEM Bracks](/help/sites-developing/aem-brackets.md) proporciona un flujo de trabajo sencillo para editar componentes de AEM y bibliotecas de clientes. Se basa en el editor de código [Corchetes](https://brackets.io/) .

La extensión:

* Facilita la sincronización (no se requiere Maven ni File Vault) para ayudar a aumentar la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos limitados de AEM a participar en los proyectos.
* Proporciona cierta compatibilidad con [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) , el lenguaje de plantilla diseñado para simplificar el desarrollo de componentes y aumentar la seguridad.

>[!NOTE]
>
>Los corchetes son el mecanismo recomendado para crear componentes. Sustituye a la funcionalidad CRXDE Lite - Crear componente, diseñada para la IU clásica.

## Migración desde un componente clásico {#migrating-from-a-classic-component}

Al migrar un componente diseñado para su uso con la IU clásica a un componente que se pueda utilizar con la IU táctil (exclusiva o conjuntamente), se deben tener en cuenta los siguientes problemas:

* HTL

   * El uso de [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) no es obligatorio, pero si su componente necesita actualizarse, entonces es el momento ideal para considerar la [migración de JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar [ código `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) que utiliza funciones específicas de la IU clásica
   * RTE, para obtener más información, consulte [Configuración del editor](/help/sites-administering/rich-text-editor.md)de texto enriquecido.
   * [Migrar `cq:listener` código](#migrating-cq-listener-code) que utiliza funciones específicas de la IU clásica

* Cuadros de diálogo

   * Deberá crear un nuevo cuadro de diálogo para utilizarlo en la IU táctil. Sin embargo, por motivos de compatibilidad, la IU táctil puede utilizar la definición de un cuadro de diálogo de IU clásica cuando no se ha definido ningún cuadro de diálogo para la IU táctil.
   * La herramienta [de conversión de](/help/sites-developing/dialog-conversion.md) cuadro de diálogo se proporciona para ayudarle a ampliar los componentes existentes.
   * [La asignación de ExtJS a los componentes](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) de la interfaz de usuario de Granite proporciona una visión general práctica de los xtypes y tipos de nodo de ExtJS con sus tipos de recursos de la interfaz de usuario de Granite equivalentes.
   * Personalización de campos, para obtener más información, consulte la sesión de AEM Gems sobre la [personalización de campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)de cuadro de diálogo.
   * Migración de tipos a la validación [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Con los oyentes JS, para obtener más información, consulte [Gestión de eventos](#handling-field-events) de campo y la sesión de AEM Gems sobre la [personalización de campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)de cuadro de diálogo.

### Migración de código cq:listener {#migrating-cq-listener-code}

Si está migrando un proyecto diseñado para la IU clásica, el `cq:listener` código (y los clientes relacionados con componentes) pueden utilizar funciones específicas de la IU clásica (como `CQ.wcm.*`). Para la migración, debe actualizar dicho código con los objetos o funciones equivalentes de la IU táctil.

Si el proyecto se está migrando completamente a la IU táctil, debe reemplazar dicho código para utilizar los objetos y funciones relevantes para la IU táctil.

Sin embargo, si el proyecto debe ocuparse tanto de la IU clásica como de la táctil durante el período de migración (el escenario habitual), deberá implementar un conmutador para diferenciar el código independiente que hace referencia a los objetos correspondientes.

Este mecanismo de cambio se puede implementar de la siguiente manera:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentar el componente {#documenting-your-component}

Como desarrollador, desea acceder fácilmente a la documentación de componentes para que pueda comprender rápidamente:

* Descripción
* Uso previsto
* Estructura y propiedades del contenido
* API y puntos de extensión expuestos
* Etc.

Por este motivo, es bastante fácil hacer que cualquier marca de documentación existente que tenga disponible dentro del propio componente.

Todo lo que necesita es colocar un `README.md` archivo en la estructura de componentes. Esta marca se mostrará en la consola [de](/help/sites-authoring/default-components-console.md)componentes.

![climage_1-7](assets/chlimage_1-7.png)

La marca admitida es la misma que la de los fragmentos [de](/help/assets/content-fragments-markdown.md)contenido.
