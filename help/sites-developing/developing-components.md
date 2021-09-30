---
title: Desarrollo de componentes AEM
seo-title: Developing AEM Components
description: AEM componentes se utilizan para guardar, dar formato y procesar el contenido disponible en las páginas web.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: f2a208acfa28f23cbf63d055c5d28698df476892
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 2%

---

# Desarrollo de componentes AEM{#developing-aem-components}

AEM componentes se utilizan para guardar, dar formato y procesar el contenido disponible en las páginas web.

* Al [crear páginas](/help/sites-authoring/default-components.md), los componentes permiten a los autores editar y configurar el contenido.

   * Al construir un sitio de [Commerce](/help/commerce/cif-classic/administering/ecommerce.md), los componentes pueden, por ejemplo, recopilar y procesar información del catálogo.
Consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md) para obtener más información.

   * Al construir un sitio de [Communities](/help/communities/author-communities.md), los componentes pueden proporcionar información a los visitantes y recabarla.
Consulte [Desarrollo de comunidades](/help/communities/communities.md) para obtener más información.

* En la instancia de publicación, los componentes representan el contenido, presentándolo como lo necesita a los visitantes del sitio web.

>[!NOTE]
>
>Esta página es una continuación del documento [Componentes de AEM: Conceptos básicos](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Los componentes siguientes `/libs/cq/gui/components/authoring/dialog` están pensados para utilizarse únicamente en el Editor (cuadros de diálogo de componentes en la creación). Si se utilizan en otra parte (como en un cuadro de diálogo de asistente, por ejemplo), es posible que no se comporten del modo esperado.

## Ejemplos de código {#code-samples}

Esta página proporciona la documentación de referencia (o vínculos a la documentación de referencia) necesaria para desarrollar nuevos componentes para AEM. Consulte [Desarrollo de componentes de AEM: ejemplos de código](/help/sites-developing/developing-components-samples.md) para ver algunos ejemplos prácticos.

## Estructura {#structure}

La estructura básica de un componente se explica en la página [Componentes de AEM: Conceptos básicos](/help/sites-developing/components-basics.md#structure). Ese documento cubre tanto las IU táctiles como las clásicas. Aunque no necesite utilizar la configuración clásica en el nuevo componente, puede ser útil que los tenga en cuenta al heredar de componentes existentes.

## Ampliación de los componentes y cuadros de diálogo existentes {#extending-existing-components-and-dialogs}

Según el componente que desee implementar, puede que sea posible ampliar o personalizar una instancia existente en lugar de definir y desarrollar toda la [estructura](#structure) desde cero.

Al ampliar o personalizar un componente o cuadro de diálogo existente, puede copiar o replicar toda la estructura o la estructura necesaria para el cuadro de diálogo antes de realizar los cambios.

### Ampliación de un componente existente {#extending-an-existing-component}

La ampliación de un componente existente se puede lograr con [Jerarquía de tipo de recurso](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) y los mecanismos de herencia relacionados.

>[!NOTE]
>
>Los componentes también se pueden redefinir con una superposición basada en la lógica de ruta de búsqueda. Sin embargo, en este caso, la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) no se activará y `/apps` debe definir la superposición completa.

>[!NOTE]
>
>El [componente de fragmento de contenido](/help/sites-developing/customizing-content-fragments.md) también se puede personalizar y ampliar, aunque se deben tener en cuenta la estructura y las relaciones completas con Assets.

### Personalización de un cuadro de diálogo de componente existente {#customizing-a-existing-component-dialog}

También es posible anular un *cuadro de diálogo de componentes* utilizando la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y definiendo la propiedad `sling:resourceSuperType`.

Esto significa que solo necesita redefinir las diferencias necesarias, en lugar de redefinir todo el cuadro de diálogo (mediante `sling:resourceSuperType`). Este es ahora el método recomendado para ampliar un cuadro de diálogo de componentes

Consulte la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) para obtener más información.

## Definición del marcado {#defining-the-markup}

El componente se procesará con [HTML](https://www.w3schools.com/htmL/html_intro.asp). El componente debe definir el HTML necesario para tomar el contenido requerido y luego procesarlo según sea necesario, tanto en el entorno de autor como de publicación.

### Uso del lenguaje de plantilla HTML {#using-the-html-template-language}

El [lenguaje de plantilla HTML (HTL)](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html), introducido con AEM 6.0, sustituye a JSP (páginas de JavaServer) como sistema de plantillas preferido y recomendado en el lado del servidor para HTML. Para los desarrolladores web que necesitan crear sitios web empresariales sólidos, HTL ayuda a lograr una mayor seguridad y eficacia en el desarrollo.

>[!NOTE]
>
>Aunque tanto HTL como JSP pueden utilizarse para desarrollar componentes, ilustraremos el desarrollo con HTL en esta página, ya que es el lenguaje de secuencias de comandos recomendado para AEM.

## Desarrollo de la lógica de contenido {#developing-the-content-logic}

Esta lógica opcional selecciona o calcula el contenido que se va a procesar. Se invoca desde expresiones HTL con el patrón de uso-API apropiado.

El mecanismo para separar la lógica de la apariencia ayuda a aclarar lo que se necesita para una vista determinada. También permite lógicas diferentes para vistas diferentes del mismo recurso.

### Uso de Java {#using-java}

[La HTL Java Use-API permite que un archivo HTL acceda a los métodos de ayuda en una clase](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) Java personalizada. Esto le permite utilizar código Java para implementar la lógica de selección y configuración del contenido del componente.

### Uso de JavaScript {#using-javascript}

[La HTL JavaScript Use-API permite que un archivo HTL acceda al código de ayuda escrito en JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Esto le permite utilizar código JavaScript para implementar la lógica de selección y configuración del contenido del componente.

### Uso de bibliotecas HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Lea [Uso de bibliotecas HTML del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente, incluidos atributos como acciones disponibles para el componente, características del editor in situ y los oyentes relacionados con eventos en el componente. La configuración es común a la IU táctil y a la clásica, aunque con ciertas diferencias específicas.

El comportamiento de edición [de un componente se configura](/help/sites-developing/components-basics.md#edit-behavior) añadiendo un nodo `cq:editConfig` de tipo `cq:EditConfig` debajo del nodo del componente (de tipo `cq:Component`) y añadiendo propiedades específicas y nodos secundarios.

## Configuración del comportamiento de vista previa {#configuring-the-preview-behavior}

La cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) se establece al cambiar al modo **Preview** incluso cuando la página no se actualiza.

Para los componentes con una renderización que son sensibles al modo WCM, deben definirse para actualizarse específicamente y luego depender del valor de la cookie.

>[!NOTE]
>
>En la IU táctil solo se utilizan los valores `EDIT` y `PREVIEW` para la cookie [Modo WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Creación y configuración de un cuadro de diálogo {#creating-and-configuring-a-dialog}

Los cuadros de diálogo se utilizan para permitir que el autor interactúe con el componente. El uso de un cuadro de diálogo permite a los autores o administradores editar contenido, configurar el componente o definir parámetros de diseño (mediante un [Diálogo de diseño](#creating-and-configuring-a-design-dialog))

### Interfaz de usuario de Coral y Granite {#coral-ui-and-granite-ui}

[La ](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) interfaz de usuario de Coral y la  [interfaz de usuario de ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite definen el aspecto moderno de AEM.

[La interfaz de usuario de Granite proporciona una amplia gama de componentes básicos (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)  necesarios para crear el cuadro de diálogo en el entorno de creación. Si es necesario, puede ampliar esta selección y [crear su propio widget](#creatinganewwidget).

Para obtener más información, consulte:

* Interfaz de usuario de Coral

   * Proporciona una interfaz de usuario uniforme en todas las soluciones de la nube
   * [Conceptos de la IU AEM táctil: IU de Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guía de Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interfaz de usuario de Granite

   * Proporciona un marcado de Coral UI dentro de componentes de Sling para crear consolas de interfaz de usuario y cuadros de diálogo
   * [Conceptos de la IU AEM táctil: Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>Debido a la naturaleza de los componentes de la interfaz de usuario de Granite (y a las diferencias con los widgets de ExtJS), hay algunas diferencias entre la forma en que los componentes interactúan con la IU táctil y la [IU clásica](/help/sites-developing/developing-components-classic.md).

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Cuadros de diálogo para la IU táctil:

* se denominan `cq:dialog`.
* se definen como un nodo `nt:unstructured` con la propiedad `sling:resourceType` establecida.

* se encuentran en su nodo `cq:Component` y junto a su definición de componente.
* se procesan en el lado del servidor (como componentes Sling), según su estructura de contenido y la propiedad `sling:resourceType` .
* utilice el marco de la interfaz de usuario de Granite.
* contiene una estructura de nodos que describe los campos dentro del cuadro de diálogo.

   * estos nodos son `nt:unstructured` con la propiedad `sling:resourceType` requerida.

Un ejemplo de estructura de nodos podría ser:

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

La personalización de un cuadro de diálogo es similar al desarrollo de un componente, ya que el cuadro de diálogo es en sí mismo un componente (es decir, el marcado procesado por un script de componente junto con el comportamiento/estilo proporcionado por una biblioteca de cliente).

Para ver ejemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Si un componente no tiene ningún cuadro de diálogo definido para la IU táctil, el cuadro de diálogo de la IU clásica se utiliza como alternativa dentro de una capa de compatibilidad. Para personalizar este cuadro de diálogo, debe personalizar el cuadro de diálogo IU clásica. Consulte [Componentes AEM para la IU clásica](/help/sites-developing/developing-components-classic.md).

### Personalización de campos de cuadro de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* la sesión AEM Gems en [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* el código de muestra relacionado que se trata en [Ejemplo de código - Cómo personalizar campos de diálogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).

>


#### Creación de un nuevo campo {#creating-a-new-field}

Las utilidades de la IU táctil se implementan como componentes de Granite UI.

Para crear un nuevo widget para utilizarlo en un cuadro de diálogo de componentes para la IU táctil, es necesario [crear un nuevo componente de campo de Granite UI](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Para obtener más información sobre la interfaz de usuario de Granite, consulte la [documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Si considera el cuadro de diálogo como un contenedor simple para un elemento de formulario, también puede ver el contenido principal del contenido del cuadro de diálogo como campos de formulario. La creación de un nuevo campo de formulario requiere la creación de un tipo de recurso; esto equivale a crear un componente nuevo. Para ayudarle en esa tarea, la interfaz de usuario de Granite ofrece un componente de campo genérico del que heredar (mediante `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Más específicamente, la interfaz de usuario de Granite proporciona una serie de componentes de campo que son adecuados para su uso en diálogos (o, en términos más generales, en [formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Esto difiere de la IU clásica, donde los widgets se representan mediante nodos `cq:Widgets`, cada uno con un `xtype` particular para establecer la relación con su widget ExtJS correspondiente. Desde el punto de vista de la implementación, estas utilidades se representaron en el lado del cliente mediante el marco de trabajo de ExtJS.

Una vez creado el tipo de recurso, puede crear una instancia del campo añadiendo un nuevo nodo en el cuadro de diálogo. La propiedad `sling:resourceType` hace referencia al tipo de recurso que acaba de introducir.

#### Creación de una biblioteca de cliente para estilos y comportamientos {#creating-a-client-library-for-style-and-behavior}

Si desea definir el estilo y el comportamiento de su componente, puede crear una [biblioteca de cliente](/help/sites-developing/clientlibs.md) dedicada que defina su CSS/LESS y JS personalizados.

Para que la biblioteca de cliente se cargue únicamente para el cuadro de diálogo de componentes (es decir, no se cargará para otro componente), debe establecer la propiedad `extraClientlibs`** **del cuadro de diálogo en el nombre de categoría de la biblioteca de cliente que acaba de crear. Esto es aconsejable si la biblioteca de cliente es bastante grande o si el campo es específico de ese cuadro de diálogo y no lo necesitará en otros cuadros de diálogo.

Para que la biblioteca de cliente se cargue en todos los cuadros de diálogo, establezca la propiedad category de la biblioteca de cliente en `cq.authoring.dialog`. Este es el nombre de categoría de la biblioteca de cliente que se incluye de forma predeterminada al procesar todos los cuadros de diálogo. Desea hacerlo si la biblioteca de cliente es pequeña o si el campo es genérico y podría reutilizarse en otros cuadros de diálogo.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * proporcionado por el [Código de muestra](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ampliación (herencia) de un campo {#extending-inheriting-from-a-field}

Según sus necesidades, puede:

* Ampliar un campo de interfaz de usuario de Granite determinado por herencia de componentes ( `sling:resourceSuperType`)
* Ampliar un widget determinado desde la biblioteca de widgets subyacente (en el caso de la interfaz de usuario de Granite, esta es Coral UI), siguiendo la API de biblioteca de utilidades (herencia de JS/CSS)

#### Acceso a campos de cuadro de diálogo {#access-to-dialog-fields}

También puede utilizar condiciones de renderización ( `rendercondition`) para controlar quién tiene acceso a pestañas/campos específicos en el cuadro de diálogo; por ejemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestión de eventos de campo {#handling-field-events}

El método para gestionar eventos en campos de diálogo ahora se realiza con [oyentes en una biblioteca de cliente personalizada](#listeners-in-a-custom-client-library). Esto supone un cambio con respecto al método anterior de tener [oyentes en la estructura de contenido](#listenersinthecontentstructureclassicui).

#### Oyentes en una biblioteca de cliente personalizada {#listeners-in-a-custom-client-library}

Para insertar lógica en el campo, debe:

1. Tenga marcado el campo con una clase CSS determinada (el *gancho*).
1. Defina, en la biblioteca de cliente, un oyente JS conectado a ese nombre de clase CSS (esto garantiza que la lógica personalizada tenga ámbitos únicamente en el campo y no afecte a otros campos del mismo tipo).

Para conseguirlo, debe conocer la biblioteca de widgets subyacente con la que desea interactuar. Consulte la [documentación de Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) para identificar a qué evento desea reaccionar. Esto es muy similar al proceso que tenía que realizar con ExtJS en el pasado: busque la página de documentación de un widget determinado y, a continuación, compruebe los detalles de su API de evento.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * proporcionado por el [Código de muestra](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Oyentes en la estructura de contenido {#listeners-in-the-content-structure}

En la IU clásica con ExtJS, era habitual tener oyentes para un widget determinado en la estructura de contenido. Lograr lo mismo en la IU táctil es diferente cuando el código de oyente de JS (o cualquier código en absoluto) ya no está definido en el contenido.

La estructura de contenido describe la estructura semántica; no debe implicar la naturaleza del widget subyacente. Al no tener código JS en la estructura de contenido, puede cambiar los detalles de implementación sin tener que cambiar la estructura de contenido. En otras palabras, puede cambiar la biblioteca de utilidades sin necesidad de tocar la estructura de contenido.

#### Detección de la disponibilidad del cuadro de diálogo {#dialog-ready}

Si tiene un JavaScript personalizado que debe ejecutarse únicamente cuando el cuadro de diálogo esté disponible y listo, debe escuchar el evento `dialog-ready` .

Este evento se activa cada vez que se carga (o recarga) el cuadro de diálogo y está listo para utilizarse, lo que significa que siempre que haya un cambio (crear/actualizar) en el DOM del cuadro de diálogo.

`dialog-ready` se puede utilizar para conectar en código personalizado JavaScript que realiza personalizaciones en los campos dentro de un cuadro de diálogo o tareas similares.

### Validación de campos {#field-validation}

#### Campo obligatorio {#mandatory-field}

Para marcar un campo determinado como obligatorio, establezca la siguiente propiedad en el nodo de contenido del campo:

* Nombre: `required`
* Tipo: `Boolean`

Para ver un ejemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validación de campos (interfaz de usuario de Granite) {#field-validation-granite-ui}

La validación de campos en la interfaz de usuario de Granite y los componentes de Granite UI (equivalentes a las utilidades) se realiza mediante la API `foundation-validation`. [Consulte la documentación de  `foundation-valdiation` Granite para obtener más información.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * proporcionado por el [Código de muestra](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creación y configuración de un cuadro de diálogo de diseño {#creating-and-configuring-a-design-dialog}

El cuadro de diálogo Diseño se proporciona cuando un componente tiene detalles de diseño que se pueden editar en [modo de diseño](/help/sites-authoring/default-components-designmode.md).

La definición es muy similar a la de un cuadro de diálogo [utilizado para editar contenido](#creating-a-new-dialog), con la diferencia de que se define como un nodo:

* Nombre del nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creación y configuración de un editor in situ {#creating-and-configuring-an-inplace-editor}

Un editor in situ permite al usuario editar contenido directamente en el flujo de párrafos, sin necesidad de abrir un cuadro de diálogo. Por ejemplo, los componentes estándar Texto y Título tienen un editor in situ.

Un editor in situ no es necesario ni significativo para cada tipo de componente.

Consulte [Ampliación de la creación de páginas: agregar nuevo editor in situ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) para obtener más información.

## Personalización de la barra de herramientas del componente {#customizing-the-component-toolbar}

La [barra de herramientas de componentes](/help/sites-developing/touch-ui-structure.md#component-toolbar) proporciona al usuario acceso a una serie de acciones para el componente, como editar, configurar, copiar y eliminar.

Consulte [Ampliación de la creación de páginas: agregar nueva acción a una barra de herramientas de componentes](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) para obtener más información.

## Configuración de un componente para el carril de referencias (prestado/alquilado) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Si el nuevo componente hace referencia al contenido de otras páginas, puede considerar si desea que afecte a las secciones **Contenido prestado** y **Contenido de Cuarentena** del carril [**Referencias**](/help/sites-authoring/basic-handling.md#references).

La AEM predeterminada solo comprueba el componente de referencia. Para añadir su componente, debe configurar el paquete OSGi **WCM Authoring Content Reference Configuration**.

Cree una nueva entrada en la definición, especificando el componente, junto con la propiedad que se va a comprobar. Por ejemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios. Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Activación y adición del componente al sistema de párrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Una vez desarrollado el componente, debe habilitarse para su uso en un sistema de párrafos apropiado, de modo que se pueda utilizar en las páginas requeridas.

Esto se puede hacer mediante:

* uso del [modo Diseño](/help/sites-authoring/default-components-designmode.md) al editar una página específica.
* [definición de la  `components` propiedad en el sistema de párrafos de una plantilla](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurar un sistema de párrafos para que al arrastrar un recurso se cree una instancia de componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM ofrece la posibilidad de configurar un sistema de párrafos en la página para que [una instancia del nuevo componente se cree automáticamente cuando un usuario arrastra un recurso (adecuado) a una instancia de esa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (en lugar de tener que arrastrar siempre un componente vacío a la página).

Se puede configurar este comportamiento y la relación entre activos y componentes necesaria:

1. En la definición de párrafo del diseño de la página. Por ejemplo:

   * `/etc/designs/<myApp>/page/par`

   Cree un nuevo nodo:

   * Nombre: `cq:authoring`
   * Tipo: `nt:unstructured`


1. En este nodo, cree un nuevo nodo para albergar todas las asignaciones de recursos a componentes:

   * Nombre: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Para cada asignación de recursos a componentes, cree un nodo:

   * Nombre: texto; se recomienda que el nombre indique el recurso y el tipo de componente relacionado; por ejemplo, image
   * Tipo: `nt:unstructured`

   Cada una con las siguientes propiedades:

   * `assetGroup`:

      * Tipo: `String`
      * Valor: el grupo al que pertenece el recurso relacionado; por ejemplo, `media`
   * `assetMimetype`:

      * Tipo: `String`
      * Valor: el tipo mime del recurso relacionado; por ejemplo `image/*`
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

* [Abra el proyecto aem-project-archetype en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creación automática de instancias de componentes ahora se puede configurar fácilmente dentro de la interfaz de usuario al utilizar [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) y Plantillas editables. Consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) para obtener más información sobre cómo definir qué componentes se asocian automáticamente a determinados tipos de medios.

## Uso de la extensión AEM Brackets {#using-the-aem-brackets-extension}

La [Extensión AEM Brackets](/help/sites-developing/aem-brackets.md) proporciona un flujo de trabajo suave para editar AEM componentes y bibliotecas de cliente. Se basa en el editor de código [Brackets](https://brackets.io/).

La extensión:

* Facilita la sincronización (no se requiere Maven ni File Vault) para ayudar a aumentar la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos AEM limitados a participar en proyectos.
* Proporciona compatibilidad con [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), el lenguaje de plantilla diseñado para simplificar el desarrollo de componentes y aumentar la seguridad.

>[!NOTE]
>
>Brackets es el mecanismo recomendado para crear componentes. Reemplaza la funcionalidad CRXDE Lite - Crear componente , que se diseñó para la IU clásica.

## Migración desde un componente clásico {#migrating-from-a-classic-component}

Al migrar un componente diseñado para su uso con la IU clásica a un componente que se pueda utilizar con la IU táctil (solo o conjuntamente), se deben tener en cuenta los siguientes problemas:

* HTL

   * El uso de [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) no es obligatorio, pero si su componente necesita actualizarse, es el momento ideal para considerar la [migración de JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar código [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) que utilice funciones específicas de la IU clásica
   * Complemento RTE, para obtener más información, consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md).
   * [Migrar  `cq:listener` ](#migrating-cq-listener-code) código que utiliza funciones específicas de la IU clásica

* Cuadros de diálogo

   * Deberá crear un cuadro de diálogo nuevo para utilizarlo en la IU táctil. Sin embargo, por motivos de compatibilidad, la IU táctil puede utilizar la definición de un cuadro de diálogo de IU clásica cuando no se ha definido ningún cuadro de diálogo para la IU táctil.
   * Las [AEM Herramientas de modernización](/help/sites-developing/modernization-tools.md) se proporcionan para ayudarle a ampliar los componentes existentes.
   * [La asignación de ExtJS a los ](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) componentes de la interfaz de usuario de Granite proporciona una visión general práctica de los xtype y tipos de nodo de ExtJS con sus tipos de recursos de la interfaz de usuario de Granite equivalentes.
   * Personalización de campos, para obtener más información, consulte la sesión AEM Gems sobre [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Migración de tipos a [Granite UI validation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Con los oyentes JS, para obtener más información, consulte [Gestión de eventos de campo](#handling-field-events) y la sesión de Gems de AEM en [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migración de código cq:listener {#migrating-cq-listener-code}

Si está migrando un proyecto diseñado para la IU clásica, el código `cq:listener` (y clientlibs relacionados con componentes) pueden utilizar funciones específicas de la IU clásica (como `CQ.wcm.*`). Para la migración, debe actualizar dicho código utilizando los objetos o funciones equivalentes en la IU táctil.

Si el proyecto se está migrando por completo a la IU táctil, debe reemplazarlo para que utilice los objetos y funciones relevantes para la IU táctil.

Sin embargo, si el proyecto debe ocuparse tanto de la IU clásica como de la IU táctil durante el período de migración (el escenario habitual), debe implementar un conmutador para diferenciar el código independiente que hace referencia a los objetos adecuados.

Este mecanismo de conmutación se puede implementar de la siguiente manera:

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

Por este motivo, es bastante fácil hacer cualquier desglose de documentación existente que tenga disponible dentro del propio componente.

Todo lo que debe hacer es colocar un archivo `README.md` en la estructura de componentes. Este marcado se muestra en la [consola de componentes](/help/sites-authoring/default-components-console.md).

![Chlimage_1-7](assets/chlimage_1-7.png)

El marcado admitido es el mismo que para [fragmentos de contenido](/help/assets/content-fragments/content-fragments-markdown.md).
