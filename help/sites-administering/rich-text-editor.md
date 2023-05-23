---
title: Configure el Editor de texto enriquecido para crear contenido en Adobe Experience Manager.
description: Aprenda a configurar el Editor de texto enriquecido de Adobe Experience Manager para que cree contenido en Adobe Experience Manager.
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: 53a18ec48331f1c25c15e8f7a59bd57e95639895
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 1%

---

# Configuración del editor de texto enriquecido {#configure-the-rich-text-editor}

El Editor de texto enriquecido (RTE) proporciona a los autores una amplia gama de funcionalidades para editar el contenido de texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto WYSIWYG.

Para saber cómo utilizar las funciones RTE para la creación, consulte [Uso del Editor de texto enriquecido para la creación](/help/sites-authoring/rich-text-editor.md). RTE se puede configurar para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. El siguiente flujo de trabajo ilustra el orden recomendado para completar las tareas de configuración de RTE en Experience Manager.

![Secuencia de pasos para aprender a configurar RTE](assets/rte_workflow_v1.png)

*Figura: Secuencia de pasos para aprender a configurar RTE*

## Explicación de la IU táctil y la IU clásica {#understand-touch-enabled-ui-and-classic-ui}

La IU táctil es la interfaz de usuario estándar para Experience Manager. El Adobe introdujo la IU táctil con [diseño interactivo](/help/sites-authoring/responsive-layout.md) para el entorno de creación. La interfaz de usuario táctil está diseñada para dispositivos táctiles y de escritorio. La interfaz difiere considerablemente de la IU clásica original.

![Barra de herramientas del Editor de texto enriquecido en la interfaz de usuario táctil](assets/chlimage_1-35.png)

*Imagen: barra de herramientas del Editor de texto enriquecido en la IU táctil*

![Barra de herramientas del Editor de texto enriquecido en la IU clásica](assets/rtedefault.png)

*Imagen: barra de herramientas del Editor de texto enriquecido en la IU clásica*

>[!MORELIKETHIS]
>
>* [Recomendaciones de IU](/help/sites-deploying/ui-recommendations.md)
>* Acerca de la desaprobación de la IU clásica, consulte [Notas de la versión de Experience Manager 6.5](/help/release-notes/deprecated-removed-features.md)
>* Para ver las diferencias entre las IU, consulte [IU táctil e IU clásica](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* Para comprender en detalle la IU táctil, consulte [Conceptos de la IU táctil del Experience Manager](/help/sites-developing/touch-ui-concepts.md)


## Varios modos de edición {#editingmodes}

Los autores pueden crear y editar contenido textual en Experience Manager utilizando los diferentes modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido, así como la experiencia del usuario con componentes con RTE en diferentes modos de edición, varían en función de las configuraciones de RTE.

| Modo de edición | Área de edición | Funciones recomendadas que se deben habilitar | IU táctil | IU clásica |
|--- |--- |--- |--- |--- |
| En línea | Edición in situ para realizar ediciones rápidas y secundarias; Formato sin abrir un cuadro de diálogo | Funciones RTE mínimas | Y | Y |
| Pantalla completa RTE | Abarca toda la página | Todas las funciones RTE necesarias | Y | N |
| Cuadro de diálogo | Cuadro de diálogo en la parte superior del contenido de la página, pero no cubre toda la página | Todas las funciones RTE necesarias en la IU clásica; habilite las funciones con prudencia en la IU táctil | Y | Y |
| Pantalla completa de diálogo | Igual que el modo de pantalla completa; contiene campos del cuadro de diálogo junto con RTE | Todas las funciones RTE necesarias | Y | N |

>[!NOTE]
>
>La función de edición de origen no está disponible en el modo de edición en línea en la IU táctil. No puede arrastrar imágenes en el modo de pantalla completa. Todas las demás funciones funcionan en todos los modos.

### Edición en línea {#inline-editing}

Cuando se abre (con un doble toque o clic lento), el contenido se puede editar dentro de la página. Se presenta una barra de herramientas compacta con opciones muy básicas.

![Edición en línea con la barra de herramientas básica en la IU táctil](assets/chlimage_1-36.png)

*Imagen: edición en línea con la barra de herramientas básica en la IU táctil*

En la IU clásica, un doble clic lento en el componente permite la edición en línea y una descripción naranja resalta el contenido. Si el buscador de contenido está abierto, se muestra una barra de herramientas con las opciones de formato RTE disponibles en la parte superior de la ventana. Si el buscador de contenido no está abierto, las opciones de formato no se muestran y solo puede realizar ediciones de texto básicas.

### Edición de pantalla completa {#full-screen-editing}

Los componentes del Experience Manager se pueden abrir en la vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar a pantalla completa una versión detallada de la edición en línea, ya que ofrece la mayoría de las opciones de edición. Se puede abrir haciendo clic en ![rte_fullscreen](assets/rte_fullscreen.png), en la barra de herramientas compacta cuando se utiliza el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo es aplicable a un cuadro de diálogo que contenga RTE junto con otros componentes.

![La barra de herramientas RTE detallada al editar en modo de pantalla completa en la IU táctil](assets/chlimage_1-37.png)

*Imagen: barra de herramientas RTE detallada al editar en modo de pantalla completa en la IU táctil*

### Edición de diálogos {#dialog-editing}

Al hacer doble clic en un componente, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición del cuadro de diálogo en la IU táctil](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edición del cuadro de diálogo en la IU táctil*

![Cuadro de diálogo de la IU clásica que contiene la barra de herramientas detallada para la edición](assets/chlimage_1-38.png)

*Imagen: cuadro de diálogo de la IU clásica que contiene la barra de herramientas detallada para su edición*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible a través de una serie de complementos, cada uno con:

* A `features` propiedad:

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento
   * Esto se puede configurar mediante un procedimiento estandarizado

* Si procede, propiedades y opciones adicionales que requieran una configuración especializada.

Las funciones básicas del RTE se activan o desactivan mediante el valor del `features` en un nodo específico del complemento correspondiente.

En la tabla siguiente se enumeran los complementos actuales, mostrando:

* ID de complemento con un vínculo a la documentación de la API. El ID se utiliza como nombre de nodo cuando [activación de un complemento](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para `features` propiedad.
* Una descripción de la funcionalidad proporcionada por el complemento.

| ID de complemento | características | Descripción |
|--- |--- |--- |
| editar | cortar copiar pegar-predeterminado pegar-texto sin formato pegar-wordhtml | [Cortar, copiar y pegar los tres modos](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | buscar reemplazar | Buscar y reemplazar. |
| formato | negrita cursiva subrayado | [Formato de texto básico](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| image | image | Compatibilidad con imágenes básica (arrastre desde contenido o Buscador de contenido). Según el explorador, la compatibilidad tiene comportamientos diferentes para los autores |
| teclas |  | Para definir este valor, consulte [tamaño de ficha](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| justificar | justifyleft justifycenter justifcopyright | Alineación de párrafo. |
| vínculos | modificar delimitador de desvinculación de vínculo | [Hipervínculos y anclajes](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| listas | anulación de sangría ordenada sin ordenar | Este complemento controla ambos [sangría y listas](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin); incluyendo listas anidadas. |
| herramientas diversas | specialchars sourceedit | Varias herramientas permiten a los autores introducir [caracteres especiales](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) o editar el origen del HTML. Además, puede agregar un todo [intervalo de caracteres especiales](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) si desea definir su propia lista. |
| Paraformato | paraformato | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>`, y `<h3>`). Puede [agregar más formatos de párrafo](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) o ampliar la lista. |
| revisión ortográfica | texto de comprobación | [Corrector ortográfico según el idioma](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | estilos | Compatibilidad con el estilo mediante una clase CSS. [Añadir nuevos estilos de texto](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) si desea agregar (o ampliar) su propia gama de estilos para utilizarlos con texto. |
| subíndice | superíndice de subíndice | Extensiones a los formatos básicos, añadiendo sub y super-script. |
| tabla | tabla quitadareinsertarrow removerow insertarcolumna removercolumna propiedades celulares combinarceldas dividircelda selectrow selectcolumns | Consulte [configurar estilos de tabla](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles), si desea agregar sus propios estilos para tablas completas o celdas individuales. |
| deshacer | deshacer rehacer | Tamaño del historial de [deshacer y rehacer](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) operaciones. |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de diálogo. Uso del `dialogFullScreen` configuración para configurar la barra de herramientas para el modo de pantalla completa.

## Comprender las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

El [modo de edición RTE (y la interfaz de usuario)](#editingmodes) que proporcione para que los autores decidan la ubicación de los detalles de configuración cuando [activación de los complementos RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin):

| Modo de edición | Ubicación de la IU táctil | Ubicación de la IU clásica |
|---|---|---|
| En línea | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| Pantalla completa | `cq:editConfig/cq:inplaceEditing` | No aplicable |
| Cuadro de diálogo | `cq:dialog` | `dialog` |
| Cuadro de diálogo Pantalla completa | `cq:dialog` | No aplicable |

>[!NOTE]
>
>No asigne un nombre al nodo en `cq:inplaceEditing` as `config`. Activado `cq:inplaceEditing` , defina las siguientes propiedades:
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real
>
>No asigne un nombre al nodo de configuración RTE como `config`. De lo contrario, las configuraciones de RTE se aplican solo para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición del cuadro de diálogo solo en la IU táctil:

* `useFixedInlineToolbar`: establezca esta propiedad booleana definida en el nodo RTE (una con sling:resourceType= `cq/gui/components/authoring/dialog/richtext`) a `True`, para que la barra de herramientas RTE sea fija en lugar de flotante.

   Cuando esta propiedad es true, la edición de Richtext se inicia de forma predeterminada en el evento &quot;foundation-contentloaded&quot;.

   Para evitarlo, establezca la propiedad `customStart` hasta `True`y déclencheur el evento &quot;rte-start&quot; para iniciar la edición de RTE. Cuando esta propiedad tiene el valor &quot;true&quot;, el comportamiento predeterminado, iniciar al hacer clic, no funciona.

* `customStart`: establezca esta propiedad booleana definida en el nodo RTE en `True`, para controlar cuándo iniciar RTE activando el evento `rte-start`.

* `rte-start`: Almacene en Déclencheur este evento en la `contenteditable-div` de RTE, cuándo iniciar la edición de RTE. Esto solo funciona si `customStart` se ha establecido en true.

Cuando se utiliza RTE en el cuadro de diálogo táctil, establecer la propiedad `useFixedInlineToolbar` El valor de es verdadero es obligatorio para evitar problemas.

## Personalizar la edición in situ {#customizing-in-place-editing}

Puede definir en qué selector de HTML comienza el editor de texto configurando las siguientes propiedades:

* **`editElementQuery`** - Definido en `cq:InplaceEditingConfig`, esta propiedad se utiliza para especificar un selector del elemento HTML en el que se iniciará la edición en línea del componente Texto. Si no se especifica, la edición en línea se inicia directamente en el HTML del componente Texto.
* **`textPropertyName`** - Definido en `cq:InplaceEditingConfig`, esta propiedad se utiliza para especificar el nombre de la propiedad que se guardará en el nodo de contenido, donde el valor de HTML del componente de texto se mantendrá después de la edición en línea.

La propiedad correspondiente para el modo de diálogo es `name`.

## Habilitar las funcionalidades de RTE activando complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con la propiedad features. Puede configurar la propiedad features para habilitar o deshabilitar las distintas funciones de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [Cómo activar y configurar los complementos RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**Muestra**: Descargar [esta configuración de muestra](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) que ilustra cómo configurar RTE. En este paquete todas las características están habilitadas.

>[!NOTE]
>
>El [Componente de texto de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=en#the-text-component-and-the-rich-text-editor) permite a los editores de plantillas configurar muchos complementos RTE en una GUI como políticas de contenido, lo que elimina la necesidad de configuración técnica. Las políticas de contenido pueden funcionar con configuraciones de IU RTE como se describe en este documento.
>
>Para obtener más información, consulte la [Configuración de la IU de RTE y políticas de contenido](/help/sites-administering/rich-text-editor.md) de este documento, así como [Creación de plantillas de página](/help/sites-authoring/templates.md) y el [Documentación para desarrolladores de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se encuentran en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

## Configuración de la barra de herramientas RTE {#dialogfullscreen}

AEM le permite configurar la interfaz del Editor de texto enriquecido de forma diferente para los distintos modos de edición. A continuación se proporcionan los ajustes predeterminados. Puede sustituir estos valores predeterminados según sus necesidades. Puede personalizar únicamente las características de la barra de herramientas que desea proporcionar a los autores. No es necesario especificar todas las configuraciones de la barra de herramientas.

Para configurar la barra de herramientas para `dialogFullScreen`, utilice la siguiente configuración de ejemplo.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Se utilizan diferentes configuraciones de interfaz de usuario para el modo en línea y el modo de pantalla completa. La propiedad toolbar se utiliza para especificar los botones de la barra de herramientas.

Por ejemplo, si el botón es en sí mismo una función (por ejemplo, `Bold`), se especifica como `PluginName#FeatureName` (por ejemplo, `links#modifylink`).

Si el botón es una ventana emergente (que contiene algunas funciones de un complemento), se especifica como `#PluginName` (por ejemplo, `#format`).

Separadores (`|`) entre un grupo de botones se puede especificar con `-`.

El nodo emergente bajo el modo en línea o de pantalla completa contiene una lista de los botones que se están utilizando. Cada nodo secundario bajo el nodo &quot;fuentes&quot; recibe el nombre del complemento (por ejemplo, formato). Tiene una propiedad &quot;items&quot; que contiene una lista de funciones del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario de RTE y políticas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las políticas de contenido definen las propiedades de diseño de un componente cuando se utilizan como parte de una [plantilla editable](/help/sites-authoring/templates.md). Por ejemplo, si un componente de texto que utiliza RTE se utiliza con una plantilla editable, la política de contenido puede definir que la opción de negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido se pueden reutilizar y aplicar en varias plantillas.

Las opciones disponibles en RTE fluyen hacia abajo desde las configuraciones de interfaz de usuario hasta las políticas de contenido.

* Las opciones de configuración de la interfaz de usuario definen qué opciones están disponibles para las directivas de contenido.
* Si la configuración de interfaz de usuario de RTE se ha eliminado o no habilita un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a las funciones que están disponibles en las configuraciones de interfaz de usuario y en las directivas de contenido.

A modo de ejemplo, puede ver el [Documentación del componente principal Texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=en#the-text-component-and-the-rich-text-editor).

## Personalizar la asignación entre los iconos y comandos de la barra de herramientas {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas RTE y los comandos disponibles. No se puede usar ningún otro icono aparte de los iconos de Coral.

1. Cree un nodo llamado `icons` bajo `uiSettings/cui`.

1. Cree nodos para los iconos individuales debajo de ella.
1. En cada uno de los nodos de icono individuales, especifique un icono de Coral y un comando para asignarlo al icono.

A continuación se muestra un fragmento de ejemplo para asignar el comando Negrita al icono de Coral denominado `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Cambiar al editor de texto enriquecido de CoralUI 2 {#switch-to-coralui-rich-text-editor}

En una página, puede incluir CoralUI 2 RTE clientlib o CoralUI 3 RTE clientlib. De forma predeterminada, el Editor de texto enriquecido incluye la clientlib CoralUI 3 RTE. Para cambiar a CoralUI 2 RTE, realice los siguientes pasos.

>[!NOTE]
>
>El Adobe no lo recomienda como práctica recomendada. Cambie a CoralUI 2 RTE como último recurso. Los complementos personalizados para CoralUI 2 RTE funcionan con CoralUI 3 RTE si los complementos no dependen de internos RTE, como clases.
>
>Si utiliza complementos personalizados para CoralUI3 RTE, utilice `rte.coralui3` biblioteca.


1. Superposición del nodo `/libs/cq/gui/components/authoring/editors/clientlibs/core` bajo `/apps`y haga lo siguiente:

   * Reemplazar `rte.coralui3` con `rte.coralui2` para la propiedad dependencies.
   * Reemplazar `cq.authoring.editor.core.inlineediting.rte.coralui3` con `cq.authoring.editor.core.inlineediting.rte.coralui2` para la propiedad embed.
   * Reemplazar `cq.authoring.rte.coralui3` con `cq.authoring.rte.coralui2` para la propiedad embed.

1. Superponer los nodos `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` y `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` bajo `/apps`.

   Quitar categoría `cq.authoring.dialog` de `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` y añadirlo a `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. Cambie cualquier otra dependencia que se incluya en la página de `rte.coralui3` hasta `rte.coralui2`. Por ejemplo, después de superponer el nodo `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` bajo `/apps`, cambie cualquier dependencia de ella de `rte.coralui3` hasta `rte.coralui2`.

1. Superposición del nodo `cq/ui/widgets` bajo `/apps`. Reemplace la dependencia `cq.rte` en el nodo `/apps/cq/ui/widgets` con `cq.coralui2.rte`.

>[!NOTE]
>
>CoralUI 2 RTE utiliza plantillas de controlador para los cuadros de diálogo de los complementos. Por lo tanto, la clientlib RTE de CoralUI 2 tenía una dependencia de la clientlib de los controladores. CoralUI 3 RTE no utiliza plantillas de handlebars y no tiene ninguna dependencia asociada. Si los complementos personalizados utilizan plantillas de handlebars, incluya handlebars clientlib en su página web.

## Información adicional {#further-information}

Para obtener más información sobre la configuración de RTE, consulte la [AEM API de Widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) Referencia de.

En particular, para ver los complementos y las opciones relacionadas disponibles:

* El [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) proporciona un campo de formulario para editar información de texto con estilo (texto enriquecido). Para conocer todos los parámetros disponibles para el formulario de texto enriquecido, consulte las Opciones de configuración.
* El componente Texto enriquecido proporciona una amplia gama de funcionalidades mediante los complementos que se enumeran en [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). Para cada complemento:

   * consulte las Características para obtener detalles sobre la funcionalidad que se puede habilitar (o deshabilitar)
   * Consulte las Opciones de configuración para todos los parámetros disponibles para obtener una configuración detallada del complemento correspondiente

* También hay disponible más información sobre las Reglas del HTML para los vínculos.

Se pueden utilizar para ampliar y personalizar su propio RTE. Por ejemplo, para enumerar los anclajes disponibles en la página al crear un vínculo, puede proporcionar su propia implementación de la variable `LinkPlugin`.

## Limitaciones conocidas {#known-limitations}

AEM La capacidad de RTE tiene las siguientes limitaciones:

* AEM Las funcionalidades de RTE solo son compatibles en los cuadros de diálogo de componentes de. RTE no es compatible con asistentes o formularios base como [Propiedades de página](/help/sites-developing/page-properties-views.md) y [Andamiaje](/help/sites-authoring/scaffolding.md) en la IU táctil.

* AEM no funciona en la [Dispositivos híbridos](/help/release-notes/release-notes.md).

* No asigne un nombre al nodo de configuración RTE `config`. De lo contrario, la configuración de RTE se aplica solo para los administradores y no para los usuarios del grupo `content-author`.

* RTE no admite marcos en línea o iframes para incrustar contenido.

## Prácticas recomendadas y sugerencias {#best-practices-and-tips}

* Habilite solo los complementos sin ventana emergente para un cuadro de diálogo flotante. Los complementos sin ventanas emergentes son de menor tamaño y son los más adecuados para un cuadro de diálogo flotante.
* Habilite los complementos con ventanas emergentes de mayor tamaño, como `Paste` complemento, solo en el modo de diálogo de pantalla completa o en el modo de pantalla completa. Los complementos con ventanas emergentes grandes necesitan más espacio en la pantalla para proporcionar una buena experiencia de creación.
* Si utiliza complementos personalizados para CoralUI3 RTE, utilice `rte.coralui3` biblioteca.

## Solución de problemas frecuentes con RTE {#troubleshoot-issues-with-aem-rich-text-editor}

**¿Cómo se seleccionan varias celdas de la tabla?**

Para seleccionar varias celdas de una tabla, presione `Ctrl` o `Cmd` y, a continuación, haga clic en las celdas de la tabla una por una.

Ahora realice la operación en la selección, por ejemplo, establezca las propiedades de las celdas seleccionadas.

**Los hipervínculos se pierden al editar un componente con el botón Configurar**

Agregue un hipervínculo en un componente de texto editándolo con el botón Configurar. Puede perder el hipervínculo al editarlo de nuevo y validarlo por segunda vez.

Una solución consiste en hacer clic en el componente de texto cuando el cuadro de diálogo de edición se muestre por segunda vez y, a continuación, ejecutar la validación del vínculo.

AEM Este problema se resuelve en la versión 6.3 y posteriores de la versión de.

**El contenido del HTML añadido en el modo de edición de código fuente se pierde**

No agregue un HTML propenso a XSS. AEM La, y no el RTE, puede eliminar parte del contenido del HTML para adherirse a las reglas de antisamía XSS.

Para comprobar que el HTML pegado está guardado, compruebe el contenido guardado en CRXDE (en el nodo de contenido).

Si no se guarda, RTE debe haber eliminado el HTML, ya que no se adhirió a las reglas del RTE.

Si se guarda en CRXDE pero no se representa en la página (para comprobar la renderización, consulte la página [previsualización](/help/sites-authoring/editing-content.md#preview-mode)AEM , se elimina mediante reglas XSS de.

**El componente multicampo no funciona como se esperaba**

Para crear un componente de varios campos, utilice CoralUI 3 exclusivamente. No utilice los cuadros de diálogo de componentes de CoralUI 2.

Compruebe también que el código de implementación de varios campos y la estructura de nodos son correctos.

**La configuración disponible para los administradores no está disponible para los autores**

Si las actualizaciones de las configuraciones de interfaz se reflejan para los administradores, pero no para las cuentas de autor, asegúrese de que el nodo de configuración no tenga nombre `config`. Utilice el [`configPath` propiedad](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [Configuración de complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Uso del Editor de texto enriquecido para la creación](../sites-authoring/rich-text-editor.md)
>* [Configuración de RTE para sitios accesibles](rte-accessible-content.md)
>* [Paridad de características de IU táctil e IU clásica](../release-notes/touch-ui-features-status.md)
>* [Muestra de tutorial para crear un componente compuesto de varios campos](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

