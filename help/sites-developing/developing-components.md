---
title: Desarrollo de componentes AEM
seo-title: Desarrollo de componentes AEM
description: AEM componentes se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.
seo-description: AEM componentes se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: d0842a5994068b1e9a92cd14c1a59f1ea1a6c8b8
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 1%

---


# Desarrollo de componentes de AEM{#developing-aem-components}

AEM componentes se utilizan para mantener, dar formato y procesar el contenido disponible en las páginas web.

* Al [crear páginas](/help/sites-authoring/default-components.md), los componentes permiten a los autores editar y configurar el contenido.

   * Al construir un sitio [Comercio](/help/sites-administering/ecommerce.md), los componentes pueden, por ejemplo, recopilar y procesar información del catálogo.
Consulte [Desarrollo de comercio electrónico](/help/sites-developing/ecommerce.md) para obtener más información.

   * Al construir un sitio [Communities](/help/communities/author-communities.md), los componentes pueden proporcionar información a sus visitantes y recopilarla.
Consulte [Desarrollo de comunidades](/help/communities/communities.md) para obtener más información.

* En la instancia de publicación, los componentes representan el contenido, presentándolo como se requiere a los visitantes del sitio web.

>[!NOTE]
>
>Esta página es una continuación del documento [Componentes de AEM: Conceptos básicos](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Los componentes siguientes `/libs/cq/gui/components/authoring/dialog` están pensados para utilizarse solo en el Editor (cuadros de diálogo de componentes en la creación). Si se utilizan en otro lugar (por ejemplo, en un cuadro de diálogo de asistente), es posible que no se comporten del modo esperado.

## Ejemplos de código {#code-samples}

Esta página proporciona la documentación de referencia (o vínculos a la documentación de referencia) necesaria para desarrollar nuevos componentes para AEM. Consulte [Desarrollo de componentes de AEM - Ejemplos de código](/help/sites-developing/developing-components-samples.md) para ver algunos ejemplos prácticos.

## Estructura {#structure}

La estructura básica de un componente se describe en la página [Componentes de AEM: Conceptos básicos](/help/sites-developing/components-basics.md#structure). Ese documento abarca tanto las IU táctiles como las clásicas. Aunque no necesite usar la configuración clásica en el nuevo componente, puede ser de ayuda que los conozca al heredar de componentes existentes.

## Ampliación de los cuadros de diálogo y componentes existentes {#extending-existing-components-and-dialogs}

Según el componente que desee implementar, podría ser posible ampliar o personalizar una instancia existente, en lugar de definir y desarrollar toda la [estructura](#structure) desde cero.

Al ampliar o personalizar un componente o cuadro de diálogo existente, puede copiar o replicar toda la estructura o la estructura necesaria para el cuadro de diálogo antes de realizar los cambios.

### Ampliación de un componente existente {#extending-an-existing-component}

Se puede ampliar un componente existente con [Jerarquía de tipo de recurso](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) y los mecanismos de herencia relacionados.

>[!NOTE]
>
>Los componentes también se pueden redefinir con una superposición basada en la lógica de ruta de búsqueda. Sin embargo, en este caso, la [fusión de recursos Sling](/help/sites-developing/sling-resource-merger.md) no se activará y `/apps` debe definir la superposición completa.

>[!NOTE]
>
>El [componente de fragmento de contenido](/help/sites-developing/customizing-content-fragments.md) también se puede personalizar y ampliar, aunque se deben tener en cuenta la estructura completa y las relaciones con los recursos.

### Personalización de un cuadro de diálogo de componente existente {#customizing-a-existing-component-dialog}

También es posible anular un *cuadro de diálogo de componentes* mediante la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y la definición de la propiedad `sling:resourceSuperType`.

Esto significa que sólo necesita redefinir las diferencias requeridas, en lugar de redefinir todo el cuadro de diálogo (usando `sling:resourceSuperType`). Ahora se recomienda utilizar este método para ampliar un cuadro de diálogo de componentes

Consulte la [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) para obtener más detalles.

## Definición del marcado {#defining-the-markup}

El componente se procesará con [HTML](https://www.w3schools.com/htmL/html_intro.asp). El componente debe definir el HTML necesario para tomar el contenido necesario y, a continuación, procesarlo según sea necesario, tanto en el entorno de creación como en el de publicación.

### Uso del lenguaje de plantilla HTML {#using-the-html-template-language}

El [lenguaje de plantillas HTML (HTL)](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html), introducido con AEM 6.0, sustituye a JSP (páginas de JavaServer) como sistema de plantillas preferido y recomendado en el servidor para HTML. Para los desarrolladores web que necesitan crear sitios web empresariales sólidos, HTL ayuda a lograr una mayor seguridad y eficiencia de desarrollo.

>[!NOTE]
>
>Aunque tanto HTL como JSP pueden utilizarse para desarrollar componentes, ilustraremos el desarrollo con HTL en esta página, ya que es el lenguaje de secuencias de comandos recomendado para AEM.

## Desarrollo de la lógica de contenido {#developing-the-content-logic}

Esta lógica opcional selecciona o calcula el contenido que se va a representar. Se invoca desde expresiones HTL con el patrón de uso-API adecuado.

El mecanismo para separar la lógica de la apariencia ayuda a aclarar lo que se necesita para una vista determinada. También permite una lógica diferente para diferentes vistas del mismo recurso.

### Uso de Java {#using-java}

[La Use-API de HTL Java permite que un archivo HTL acceda a los métodos de ayuda en una clase](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) Java personalizada. Esto le permite utilizar código Java para implementar la lógica de selección y configuración del contenido del componente.

### Uso de JavaScript {#using-javascript}

[La Use-API de JavaScript de HTL permite que un archivo HTL acceda al código de ayuda escrito en JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Esto le permite utilizar código JavaScript para implementar la lógica de selección y configuración del contenido del componente.

### Uso de bibliotecas HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a solucionar este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente. El sistema de biblioteca del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Lea [Uso de bibliotecas HTML del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente, incluyendo atributos como acciones disponibles para el componente, características del editor in-situ y los oyentes relacionados con eventos en el componente. La configuración es común a la IU táctil y a la clásica, aunque con ciertas diferencias específicas.

El comportamiento de [edición de un componente se configura](/help/sites-developing/components-basics.md#edit-behavior) agregando un nodo `cq:editConfig` de tipo `cq:EditConfig` debajo del nodo del componente (de tipo `cq:Component`) y agregando propiedades y nodos secundarios específicos.

## Configuración del comportamiento de Previsualización {#configuring-the-preview-behavior}

La cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) se establece al cambiar al modo **Previsualización** incluso cuando la página no se actualiza.

Para los componentes con una representación sensible al modo WCM, deben definirse para actualizarse específicamente y, a continuación, basarse en el valor de la cookie.

>[!NOTE]
>
>En la IU táctil, solo se utilizan los valores `EDIT` y `PREVIEW` para la cookie [Modo WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Creación y configuración de un cuadro de diálogo {#creating-and-configuring-a-dialog}

Los cuadros de diálogo se utilizan para permitir que el autor interactúe con el componente. El uso de un cuadro de diálogo permite a los autores y/o administradores editar contenido, configurar el componente o definir parámetros de diseño (mediante un [Diálogo de diseño](#creating-and-configuring-a-design-dialog))

### Interfaz de usuario de Coral y Granite {#coral-ui-and-granite-ui}

[La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) interfaz de usuario de Coral y la  [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) interfaz de usuario de Granite definen el aspecto moderno de AEM.

[La interfaz de usuario de Granite proporciona una amplia gama de componentes básicos (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necesarios para crear el cuadro de diálogo en el entorno de creación. Cuando sea necesario, puede ampliar esta selección y [crear su propia utilidad](#creatinganewwidget).

Para obtener más información sobre el desarrollo de componentes mediante tipos de recursos de Coral y Granite, consulte: [Generación de componentes de Experience Manager mediante tipos de recursos corales/graníticos](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html).

Para obtener más información, consulte:

* Interfaz de usuario de Coral

   * Proporciona una interfaz de usuario coherente en todas las soluciones de nube
   * [Conceptos de la IU táctil AEM: IU de Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guía de Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interfaz de usuario de granito

   * Proporciona marcas de Coral UI incluidas en los componentes de Sling para crear consolas de interfaz de usuario y cuadros de diálogo
   * [Conceptos de la IU táctil AEM: IU granita](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>Debido a la naturaleza de los componentes de la interfaz de usuario Granite (y a las diferencias con los widgets ExtJS), hay algunas diferencias entre la forma en que los componentes interactúan con la IU táctil y la [IU clásica](/help/sites-developing/developing-components-classic.md).

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Cuadros de diálogo para la IU táctil:

* se denominan `cq:dialog`.
* se definen como un nodo `nt:unstructured` con el conjunto de propiedades `sling:resourceType`.

* se encuentran bajo su nodo `cq:Component` y junto a su definición de componente.
* se procesan en el servidor (como componentes Sling), según su estructura de contenido y la propiedad `sling:resourceType`.
* utilice la interfaz de usuario Granite.
* contiene una estructura de nodos que describe los campos del cuadro de diálogo.

   * estos nodos son `nt:unstructured` con la propiedad `sling:resourceType` requerida.

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
>Si un componente no tiene ningún cuadro de diálogo definido para la IU táctil, el cuadro de diálogo de la IU clásica se utiliza como alternativa dentro de una capa de compatibilidad. Para personalizar este cuadro de diálogo, debe personalizar el cuadro de diálogo de IU clásica. Consulte [Componentes de AEM para la IU clásica](/help/sites-developing/developing-components-classic.md).

### Personalización de los campos del cuadro de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* la sesión de AEM Gems en [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* el código de muestra relacionado cubierto en [Ejemplo de código - Cómo personalizar campos de diálogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).

>



#### Creación de un nuevo campo {#creating-a-new-field}

Las utilidades de la interfaz de usuario táctil se implementan como componentes de la interfaz de usuario de Granite.

Para crear una nueva utilidad para utilizarla en un cuadro de diálogo de componentes para la IU táctil, debe [crear un nuevo componente de campo de la interfaz de usuario de Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Para obtener información detallada sobre la interfaz de usuario de Granite, consulte la [documentación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Si considera el cuadro de diálogo como un contenedor sencillo para un elemento de formulario, también puede ver el contenido principal del cuadro de diálogo como campos de formulario. La creación de un nuevo campo de formulario requiere la creación de un tipo de recurso; esto equivale a crear un componente nuevo. Para ayudarle en esa tarea, la interfaz de usuario de Granite oferta un componente de campo genérico del que heredar (mediante `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Más específicamente, la interfaz de usuario de Granite proporciona una serie de componentes de campo que se pueden utilizar en diálogos (o, en términos más generales, en [formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Esto difiere de la IU clásica, donde los widgets se representan con nodos `cq:Widgets`, cada uno con un `xtype` particular para establecer la relación con su widget ExtJS correspondiente. Desde el punto de vista de la implementación, estos widgets se procesaron en el lado del cliente mediante el marco de trabajo de ExtJS.

Una vez creado el tipo de recurso, puede crear una instancia del campo agregando un nuevo nodo en el cuadro de diálogo, con la propiedad `sling:resourceType` que hace referencia al tipo de recurso que acaba de introducir.

#### Creación de una biblioteca de clientes para estilo y comportamiento {#creating-a-client-library-for-style-and-behavior}

Si desea definir el estilo y el comportamiento de su componente, puede crear una [biblioteca de cliente](/help/sites-developing/clientlibs.md) dedicada que defina su CSS/LESS y JS personalizados.

Para que la biblioteca de cliente se cargue únicamente para el cuadro de diálogo de componentes (es decir, no se cargará para otro componente), debe establecer la propiedad `extraClientlibs`**** del cuadro de diálogo en el nombre de categoría de la biblioteca de cliente que acaba de crear. Esto es aconsejable si la biblioteca del cliente es bastante grande y/o si el campo es específico de ese cuadro de diálogo y no será necesario en otros cuadros de diálogo.

Para que la biblioteca de cliente se cargue para todos los cuadros de diálogo, establezca la propiedad de categoría de la biblioteca de cliente en `cq.authoring.dialog`. Es el nombre de la categoría de la biblioteca del cliente que se incluye de forma predeterminada al procesar todos los cuadros de diálogo. Desea hacerlo si la biblioteca de cliente es pequeña o si el campo es genérico y puede reutilizarse en otros cuadros de diálogo.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * proporcionado por la [Muestra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ampliación (Heredación de) un campo {#extending-inheriting-from-a-field}

Según sus necesidades, puede:

* Extender un determinado campo de la interfaz de usuario de Granite por herencia de componentes ( `sling:resourceSuperType`)
* Extender un widget determinado desde la biblioteca de utilidades subyacente (en el caso de la interfaz de usuario de Granite, es Coral UI), siguiendo la API de la biblioteca de utilidades (herencia de JS/CSS)

#### Acceso a los campos del cuadro de diálogo {#access-to-dialog-fields}

También puede utilizar condiciones de procesamiento ( `rendercondition`) para controlar quién tiene acceso a fichas o campos específicos en el cuadro de diálogo; por ejemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestión de Eventos de campo {#handling-field-events}

El método de administración de eventos en campos de diálogo ahora se realiza con [oyentes en una biblioteca de cliente personalizada](#listeners-in-a-custom-client-library). Este es un cambio con respecto al método anterior de tener [oyentes en la estructura de contenido](#listenersinthecontentstructureclassicui).

#### Oyentes en una biblioteca de clientes personalizada {#listeners-in-a-custom-client-library}

Para insertar lógica en el campo, debe:

1. Marque el campo con una clase CSS determinada (el *gancho*).
1. Defina, en la biblioteca de cliente, un detector JS conectado al nombre de la clase CSS (esto garantiza que la lógica personalizada solo se alcance en el campo y no afecta a otros campos del mismo tipo).

Para lograrlo, debe conocer la biblioteca de utilidades subyacente con la que desea interactuar. Consulte la [documentación de Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) para identificar a qué evento desea reaccionar. Esto es muy similar al proceso que tenía que realizar con ExtJS en el pasado: busque la página de documentación de una utilidad determinada y, a continuación, compruebe los detalles de su API de evento.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * proporcionado por la [Muestra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Oyentes en la estructura de contenido {#listeners-in-the-content-structure}

En la IU clásica con ExtJS, era habitual tener oyentes para una utilidad determinada en la estructura de contenido. Lograr lo mismo en la IU táctil es diferente ya que el código de escucha de JS (o cualquier código) ya no se define en el contenido.

La estructura de contenido describe la estructura semántica; no debe implicar la naturaleza del widget subyacente. Al no tener el código JS en la estructura de contenido, puede cambiar los detalles de implementación sin tener que cambiar la estructura de contenido. En otras palabras, puede cambiar la biblioteca de utilidades sin necesidad de tocar la estructura de contenido.

#### Detección de la disponibilidad del cuadro de diálogo {#dialog-ready}

Si tiene un JavaScript personalizado que sólo debe ejecutarse cuando el cuadro de diálogo esté disponible y listo, debe escuchar el evento `dialog-ready`.

Este evento se activa cada vez que se carga (o recarga) el cuadro de diálogo y está listo para usarse, lo que significa que siempre que haya un cambio (crear/actualizar) en el DOM del cuadro de diálogo.

`dialog-ready` puede utilizarse para enlazar el código personalizado de JavaScript que realiza personalizaciones en los campos dentro de un cuadro de diálogo o tareas similares.

### Validación de campo {#field-validation}

#### Campo obligatorio {#mandatory-field}

Para marcar un campo determinado como obligatorio, establezca la siguiente propiedad en el nodo de contenido del campo:

* Nombre: `required`
* Tipo: `Boolean`

Para ver un ejemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validación de campos (IU granítica) {#field-validation-granite-ui}

La validación de campos en la interfaz de usuario de Granite y los componentes de la interfaz de usuario de Granite (equivalentes a widgets) se realiza mediante la API `foundation-validation`. [Consulte la documentación de  `foundation-valdiation` Granite para obtener más información.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * proporcionado por la [Muestra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creación y configuración de un cuadro de diálogo de diseño {#creating-and-configuring-a-design-dialog}

El cuadro de diálogo Diseño se proporciona cuando un componente tiene detalles de diseño que se pueden editar en [Modo de diseño](/help/sites-authoring/default-components-designmode.md).

La definición es muy similar a la de un cuadro de diálogo [utilizado para editar contenido](#creating-a-new-dialog), con la diferencia de que se define como nodo:

* Nombre del nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creación y configuración de un editor en contexto {#creating-and-configuring-an-inplace-editor}

Un editor in-situ permite al usuario editar contenido directamente en el flujo de párrafos, sin necesidad de abrir un cuadro de diálogo. Por ejemplo, los componentes estándar Texto y Título tienen un editor in situ.

Un editor in situ no es necesario ni significativo para cada tipo de componente.

Consulte [Ampliación de la creación de páginas: Añadir nuevo editor de entrada](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) para obtener más información.

## Personalización de la barra de herramientas del componente {#customizing-the-component-toolbar}

La [barra de herramientas de componentes](/help/sites-developing/touch-ui-structure.md#component-toolbar) proporciona al usuario acceso a una serie de acciones para el componente, como editar, configurar, copiar y eliminar.

Consulte [Ampliación de la creación de páginas: Añadir nueva acción a una barra de herramientas de componentes](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) para obtener más información.

## Configuración de un componente para el carril de referencias (prestado/alquilado) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Si el nuevo componente hace referencia a contenido de otras páginas, puede considerar si desea que afecte a las secciones **Contenido prestado** y **Contenido prestado** del raíl [**Referencias**](/help/sites-authoring/basic-handling.md#references).

La AEM lista para usar solo comprueba el componente Referencia. Para agregar su componente, debe configurar el paquete OSGi **Configuración de referencia de contenido de creación de WCM**.

Cree una nueva entrada en la definición, especificando el componente, junto con la propiedad que se va a comprobar. Por ejemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Al trabajar con AEM existen varios métodos para administrar la configuración de dichos servicios. Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y las prácticas recomendadas.

## Habilitar y Añadir el componente en el sistema de párrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Una vez desarrollado el componente, debe habilitarse para su uso en un sistema de párrafos adecuado, de modo que pueda utilizarse en las páginas requeridas.

Esto se puede realizar mediante:

* uso del [modo de diseño](/help/sites-authoring/default-components-designmode.md) al editar una página específica.
* [definición de la  `components` propiedad en el sistema de párrafos de una plantilla](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configuración de un sistema de párrafos para que al arrastrar un recurso se cree una instancia de componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM oferta la posibilidad de configurar un sistema de párrafos en la página para que [una instancia del nuevo componente se cree automáticamente cuando un usuario arrastra un recurso (apropiado) a una instancia de esa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (en lugar de tener que arrastrar siempre un componente vacío a la página).

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
   * `assetMimetype`::

      * Tipo: `String`
      * Valor: el tipo MIME del activo correspondiente; por ejemplo `image/*`
   * `droptarget`::

      * Tipo: `String`
      * Valor: el destinatario de caída; por ejemplo, `image`
   * `resourceType`::

      * Tipo: `String`
      * Valor: el recurso de componente relacionado; por ejemplo, `foundation/components/image`
   * `type`::

      * Tipo: `String`
      * Valor: el tipo, por ejemplo, `Images`






Para ver ejemplos, consulte:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto aem-project-archetype en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creación automática de instancias de componente ahora se puede configurar fácilmente dentro de la interfaz de usuario al utilizar [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) y Plantillas editables. Consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) para obtener más información sobre cómo definir qué componentes se asocian automáticamente a determinados tipos de medios.

## Uso de la Extensión de AEM-corchetes {#using-the-aem-brackets-extension}

La [Extensión de corchetes de AEM](/help/sites-developing/aem-brackets.md) proporciona un flujo de trabajo suave para editar AEM componentes y bibliotecas de clientes. Se basa en el editor de código [Bracks](https://brackets.io/).

La extensión:

* Facilita la sincronización (no se requiere Maven ni File Vault) para ayudar a aumentar la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos AEM limitados a participar en los proyectos.
* Proporciona compatibilidad con [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), el lenguaje de plantilla diseñado para simplificar el desarrollo de componentes y aumentar la seguridad.

>[!NOTE]
>
>Los corchetes son el mecanismo recomendado para crear componentes. Reemplaza la funcionalidad CRXDE Lite - Crear componente, diseñada para la IU clásica.

## Migración desde un componente clásico {#migrating-from-a-classic-component}

Al migrar un componente diseñado para su uso con la IU clásica a un componente que se pueda utilizar con la IU táctil (exclusiva o conjuntamente), se deben tener en cuenta los siguientes problemas:

* HTL

   * El uso de [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) no es obligatorio, pero si el componente necesita actualizarse, es el momento ideal para considerar la [migración de JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar el código [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) que utiliza funciones específicas de la IU clásica
   * RTE, para obtener más información, consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md).
   * [Migrar  `cq:listener` ](#migrating-cq-listener-code) código que utiliza funciones específicas de la IU clásica

* Cuadros de diálogo

   * Deberá crear un nuevo cuadro de diálogo para utilizarlo en la IU táctil. Sin embargo, por motivos de compatibilidad, la IU táctil puede utilizar la definición de un cuadro de diálogo de IU clásica cuando no se ha definido ningún cuadro de diálogo para la IU táctil.
   * La [Herramienta de conversión de cuadro de diálogo](/help/sites-developing/dialog-conversion.md) se proporciona para ayudarle a ampliar los componentes existentes.
   * [La asignación de ExtJS a ](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) componentes de interfaz de usuario de Granite proporciona información general sobre los tipos de nodo y xtype de ExtJS con sus tipos de recursos de interfaz de usuario de Granite equivalentes.
   * Personalización de campos, para obtener más información, consulte la sesión de AEM Gems sobre [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Migrar de tipos a [validación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Con los oyentes JS, para obtener más información, consulte [Gestión de Eventos de campo](#handling-field-events) y la sesión de AEM Gems en [Personalización de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migración del código cq:listener {#migrating-cq-listener-code}

Si está migrando un proyecto diseñado para la IU clásica, el código `cq:listener` (y los clientes relacionados con componentes) pueden utilizar funciones específicas de la IU clásica (como `CQ.wcm.*`). Para la migración, debe actualizar dicho código con los objetos o funciones equivalentes de la IU táctil.

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

## Documentando el componente {#documenting-your-component}

Como desarrollador, desea acceder fácilmente a la documentación de componentes para que pueda comprender rápidamente:

* Descripción
* Uso previsto
* Estructura y propiedades del contenido
* API y puntos de extensión expuestos
* Etc.

Por este motivo, es bastante fácil hacer que cualquier marca de documentación existente que tenga disponible dentro del propio componente.

Todo lo que debe hacer es colocar un archivo `README.md` en la estructura de componentes. Esta marca se mostrará en la [consola de componentes](/help/sites-authoring/default-components-console.md).

![climage_1-7](assets/chlimage_1-7.png)

La marca admitida es la misma que para [fragmentos de contenido](/help/assets/content-fragments/content-fragments-markdown.md).
