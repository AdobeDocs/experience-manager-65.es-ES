---
title: Configure el Editor de texto enriquecido para crear sitios y páginas web accesibles.
description: Configure el Editor de texto enriquecido para crear sitios y páginas web accesibles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Configure RTE para crear páginas web y sitios accesibles {#configure-rte-for-accessibility}

Adobe Experience Manager admite muchas funciones de accesibilidad estándar de acuerdo con diversos estándares de accesibilidad. Además, los desarrolladores pueden personalizar o ampliar para proporcionar funciones que ayuden a crear contenido accesible mediante componentes de Experience Manager que utilicen el editor de texto enriquecido (RTE).

Al diseñar páginas web y añadir contenido a las páginas, los desarrolladores y autores de contenido pueden utilizar las funciones de RTE para proporcionar información relacionada con la accesibilidad. Por ejemplo, agregue información estructural a través de encabezados y elementos de párrafo.

Para configurar y personalizar estas características, [configure los complementos RTE](#configure-the-plugin-features) para el componente. Por ejemplo, el complemento `paraformat` permite agregar elementos semánticos de nivel de bloque adicionales, incluida la ampliación del número de niveles de encabezado admitidos más allá de los `H1`, `H2` y `H3` básicos proporcionados de manera predeterminada.

RTE está disponible en una variedad de componentes para la interfaz de usuario táctil y la interfaz de usuario clásica. Sin embargo, el componente principal para utilizar RTE es el componente **Texto** que está disponible para ambas interfaces. Las siguientes imágenes muestran el RTE con un rango de complementos habilitados, incluido `paraformat`:

![Componente de texto (RTE) en modo de pantalla completa en la IU táctil.](assets/chlimage_1-206.png)

*Figura: Componente Texto en la interfaz de usuario táctil.*

![Cuadro de diálogo de edición (RTE) del componente de texto en la IU clásica.](assets/chlimage_1-207.png)

*Figura: El componente Texto de la interfaz de usuario de Classic.*

Para ver las diferencias entre las características RTE disponibles en las distintas interfaces, consulte [Complementos y sus características](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurar las características del complemento {#configure-the-plugin-features}

Para obtener las instrucciones completas para configurar RTE, consulte [configurar la página Editor de texto enriquecido](/help/sites-administering/rich-text-editor.md). Esto abarca todos los problemas, incluidos los pasos clave:

* [Los complementos y las funciones](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Ubicaciones](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations) de configuración.
* [Active un complemento y configure la propiedad](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins) features.
* [Configure otras funcionalidades de RTE](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Al configurar un complemento dentro de la subrama `rtePlugins` apropiada en el CRXDE Lite, puede activar todas las características o características específicas para ese complemento.

![CRXDE Lite que muestra un ejemplo de rtePlugin.](assets/chlimage_1-208.png)

### Ejemplo: especifique los formatos de párrafo disponibles en el campo de selección RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Los nuevos formatos de bloque semántico pueden estar disponibles para su selección mediante:

1. Según el RTE, determine y navegue a la [ubicación de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilite el campo](/help/sites-administering/rich-text-editor.md) de selección Párrafos; al  [activar el complemento](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique los formatos que desea que estén disponibles en el campo](/help/sites-administering/rich-text-editor.md) de selección Párrafos.
1. Los formatos de párrafo están disponibles para el autor del contenido desde los campos de selección en RTE. Se puede acceder a ellos:

   * Uso del icono de almohadilla de párrafo en la IU táctil.
   * Uso del campo **Formato** (selector emergente) en la IU clásica.

Con los elementos estructurales disponibles en RTE mediante las opciones de formato de párrafo, AEM ofrece una buena base para el desarrollo de contenido accesible. Los autores de contenido no pueden utilizar RTE para dar formato al tamaño de fuente o a los colores u otros atributos relacionados, lo que impide la creación de formato en línea. En su lugar, deben seleccionar los elementos estructurales adecuados, como encabezados y utilizar estilos globales seleccionados en la opción Estilos. Esto garantiza la limpieza de las opciones de marcado buenas para los usuarios que exploran con sus propias hojas de estilo y contenido correctamente estructurado.

## Uso de la función de edición de origen {#use-of-the-source-edit-feature}

En algunos casos, los autores de contenido encontrarán necesario examinar y ajustar el código fuente HTML creado mediante RTE. Por ejemplo, un fragmento de contenido creado dentro del editor de texto enriquecido puede requerir un marcado adicional para garantizar el cumplimiento de WCAG 2.0. Esto se puede hacer con la opción [de edición de origen](/help/sites-administering/rich-text-editor.md#aboutplugins) de RTE. Puede especificar la función [ `sourceedit` en el complemento `misctools`](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilice la función `sourceedit` con cuidado. Los errores de escritura y/o las funciones no compatibles pueden provocar más problemas.

## Añada la compatibilidad con más elementos y atributos HTML {#add-support-for-more-html-elements-and-attributes}

Para ampliar aún más las características de accesibilidad de AEM, es posible ampliar los componentes existentes basados en el RTE (como los componentes **Text** y **Table**) con elementos y atributos adicionales.

El siguiente procedimiento ilustra cómo extender el componente **Tabla** con un elemento **Rótulo** que proporciona información sobre una tabla de datos a los usuarios de tecnología de asistencia:

### Ejemplo: agregue el rótulo al cuadro de diálogo Propiedades de tabla {#example-adding-the-caption-to-the-table-properties-dialog}

En el constructor de `TablePropertiesDialog`, agregue un campo de entrada de texto adicional que se utilice para editar el rótulo. Tenga en cuenta que `itemId` debe configurarse en `caption` (es decir, el nombre del atributo DOM) para administrar automáticamente su contenido.

En **Tabla**, establezca explícitamente o elimine el atributo del elemento DOM. El valor se pasa por el cuadro de diálogo en el objeto `config`. Tenga en cuenta que los atributos DOM deben configurarse o eliminarse utilizando los métodos `CQ.form.rte.Common` correspondientes ( `com` es un método abreviado para `CQ.form.rte.Common`) a fin de evitar obstáculos comunes con las implementaciones del explorador.

>[!NOTE]
>
>Este procedimiento solo es adecuado para la interfaz de usuario clásica.

### Ejemplo: crear HTML accesible al usar énfasis en el texto {#create-accessible-html-for-text}

RTE puede utilizar etiquetas `strong` y `em` en lugar de `b` y `i`. Añada el siguiente nodo como un elemento secundario en los nodos `uiSettings` y `rtePlugins` del cuadro de diálogo.

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

1. Inicio CRXDE Lite. Por ejemplo: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   hasta:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Es posible que deba crear carpetas intermedias si no existen.

1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   hasta:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Abra el siguiente archivo para editarlo (ábralo con doble-clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. En el método `constructor`, antes de la lectura de la línea:

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

1. Añada el siguiente código al final del método `transferConfigToTable`:

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

1. Guarde los cambios con **Guardar todo...**

>[!NOTE]
>
>Un campo de texto sin formato no es el único tipo de entrada permitido para el valor del elemento de rótulo. Puede utilizar cualquier utilidad ExtJS que proporcione el valor del rótulo a través de su método `getValue()`.
>
>Para agregar capacidades de edición para otros elementos y atributos adicionales, asegúrese de que ambos:
>
>* La propiedad `itemId` de cada campo correspondiente se establece en el nombre del atributo DOM correspondiente (`TablePropertiesDialog`).
>* El atributo se establece y/o elimina explícitamente en el elemento DOM (`Table`).


>[!MORELIKETHIS]
>
>* [Guía rápida de WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creación de contenido accesible (conformidad con WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

