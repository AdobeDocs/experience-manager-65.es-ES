---
title: Configure el Editor de texto enriquecido para crear páginas web y sitios accesibles.
description: Configure el Editor de texto enriquecido para crear páginas web y sitios accesibles.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 1%

---

# Configuración de RTE para crear páginas web y sitios accesibles {#configure-rte-for-accessibility}

Adobe Experience Manager admite muchas funciones de accesibilidad estándar de acuerdo con varios estándares de accesibilidad. Además, los desarrolladores pueden personalizar o ampliar para proporcionar funciones que ayuden a crear contenido accesible mediante componentes de Experience Manager que utilicen el Editor de texto enriquecido (RTE).

Al diseñar páginas web y agregar contenido a las páginas, los desarrolladores y autores de contenido pueden utilizar las funciones de RTE para proporcionar información relacionada con la accesibilidad. Por ejemplo, agregue información estructural mediante encabezados y elementos de párrafo.

Para configurar y personalizar estas funciones, [configuración de los complementos RTE](#configure-the-plugin-features) para el componente. Por ejemplo, la variable `paraformat` El complemento permite agregar elementos semánticos de nivel de bloque adicionales, incluida la ampliación del número de niveles de encabezado admitidos más allá del nivel básico `H1`, `H2`, y `H3` proporcionadas de forma predeterminada.

El RTE está disponible en una variedad de componentes para la interfaz de usuario táctil y la interfaz de usuario clásica. Sin embargo, el componente principal para utilizar el RTE es el **Texto** que está disponible para ambas interfaces. Las siguientes imágenes muestran el RTE con una serie de complementos activados, incluidos `paraformat`:

![Componente de texto (RTE) en modo de pantalla completa en la IU táctil.](assets/chlimage_1-206.png)

*Imagen: componente Texto en la interfaz de usuario táctil.*

![Cuadro de diálogo de edición (RTE) del componente de texto en la IU clásica.](assets/chlimage_1-207.png)

*Imagen: componente Texto de la interfaz de usuario de Campaign Classic.*

Para ver las diferencias entre las funciones RTE disponibles en las distintas interfaces, consulte [Complementos y sus funciones](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configuración de las funciones del complemento {#configure-the-plugin-features}

Para obtener las instrucciones completas para configurar el RTE, consulte [configuración del Editor de texto enriquecido](/help/sites-administering/rich-text-editor.md) página. Esto cubre todos los problemas, incluidos los pasos clave:

* [Complementos y funciones](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Ubicaciones de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Activar un complemento y configurar la propiedad features](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configuración de otras funcionalidades de RTE](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Mediante la configuración de un complemento dentro del `rtePlugins` en CRXDE Lite, puede activar todas las funciones o las específicas para ese complemento.

![CRXDE Lite que muestra un ejemplo rtePlugin.](assets/chlimage_1-208.png)

### Ejemplo: especificar formatos de párrafo disponibles en el campo de selección RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Los nuevos formatos de bloque semántico pueden estar disponibles para su selección mediante:

1. Según el RTE, determine y vaya a [ubicación de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilitar el campo de selección Párrafos](/help/sites-administering/rich-text-editor.md); por [activación del complemento](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique los formatos que desea tener disponibles en el campo Selección de párrafos](/help/sites-administering/rich-text-editor.md).
1. Los formatos de párrafo están disponibles para el autor de contenido desde los campos de selección en RTE. Se puede acceder a ellas:

   * Uso del icono de fila de párrafo en la IU táctil.
   * Uso del **Formato** (selector emergente) en la IU clásica.

AEM Con los elementos estructurales disponibles en RTE a través de las opciones de formato de párrafo, el formato de párrafo proporciona una buena base para el desarrollo de contenido accesible. Los autores de contenido no pueden utilizar RTE para dar formato al tamaño de fuente, los colores u otros atributos relacionados, lo que impide la creación de formato en línea. En su lugar, deben seleccionar los elementos estructurales adecuados, como encabezados y utilizar estilos globales elegidos desde la opción Estilos. Esto garantiza un marcado limpio, buenas opciones para los usuarios que exploran con sus propias hojas de estilo y contenido correctamente estructurado.

## Uso de la función de edición de origen {#use-of-the-source-edit-feature}

En algunos casos, los autores de contenido encontrarán necesario examinar y ajustar el código fuente del HTML creado con RTE. Por ejemplo, un fragmento de contenido creado dentro de RTE puede requerir un marcado adicional para garantizar el cumplimiento de WCAG 2.0. Esto se puede hacer con la variable [edición de origen](/help/sites-administering/rich-text-editor.md#aboutplugins) de RTE. Puede especificar la variable [`sourceedit` función en la `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilice el `sourceedit` presentar cuidadosamente. Escribir errores y/o funciones no admitidas puede presentar más problemas.

## Agregar compatibilidad para más elementos y atributos del HTML {#add-support-for-more-html-elements-and-attributes}

AEM Para ampliar aún más las funciones de accesibilidad de los recursos, es posible ampliar los componentes existentes en función del RTE (como el **Texto** y **Tabla** componentes) con elementos y atributos adicionales.

El siguiente procedimiento ilustra cómo extender el **Tabla** componente con un **Rótulo** que proporciona información sobre una tabla de datos a los usuarios de tecnología de asistencia:

### Ejemplo: añadir el pie de ilustración al cuadro de diálogo Propiedades de la tabla {#example-adding-the-caption-to-the-table-properties-dialog}

En el constructor de `TablePropertiesDialog`, agregue un campo de entrada de texto adicional que se utilice para editar el pie de ilustración. Tenga en cuenta que `itemId` se debe establecer en `caption` (es decir, el nombre del atributo DOM) para gestionar automáticamente su contenido.

Entrada **Tabla**, establezca explícitamente o quite el atributo en el elemento DOM. El valor lo pasa el cuadro de diálogo en `config` objeto. Tenga en cuenta que los atributos DOM deben configurarse/eliminarse utilizando el `CQ.form.rte.Common` métodos ( `com` es un método abreviado para `CQ.form.rte.Common`) para evitar problemas comunes con las implementaciones de exploradores.

>[!NOTE]
>
>Este procedimiento solo es adecuado para la interfaz de usuario clásica.

### Ejemplo: Crear un HTML accesible al utilizar énfasis en el texto {#create-accessible-html-for-text}

RTE puede utilizar `strong` y `em` etiquetas en lugar de `b` y `i`. Agregue el siguiente nodo como elemento secundario al `uiSettings` y `rtePlugins` nodos en el cuadro de diálogo.

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### Instrucciones paso a paso {#step-by-step-instructions}

1. Iniciar CRXDE Lite. Por ejemplo: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   hasta:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Es posible que tenga que crear carpetas intermedias si aún no existen.

1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   hasta:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Abra el siguiente archivo para editarlo (ábralo haciendo doble clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. En el `constructor` método, antes de la lectura de línea:

   ```
   var dialogRef = this;
   ```

   Añada el siguiente código:

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Abra el siguiente archivo:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Agregue el siguiente código al final del `transferConfigToTable` método:

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. Guarde los cambios mediante **Guardar todo...**

>[!NOTE]
>
>Un campo de texto sin formato no es el único tipo de entrada permitido para el valor del elemento caption. Puede utilizar cualquier widget de ExtJS que proporcione el valor del pie de ilustración a través de su `getValue()` método.
>
>Para añadir funciones de edición para elementos y atributos adicionales, asegúrese de que ambos:
>
>* El `itemId` para cada campo correspondiente se establece en el nombre del atributo DOM correspondiente (`TablePropertiesDialog`).
>* El atributo se establece o se elimina explícitamente en el elemento DOM (`Table`).

>[!MORELIKETHIS]
>
>* [Guía rápida de WCAG 2.0](/help/managing/qg-wcag.md)
>* [Crear contenido accesible (conformidad con WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)
