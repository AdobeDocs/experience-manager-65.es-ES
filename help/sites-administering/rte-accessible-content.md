---
title: Configure el Editor de texto enriquecido para crear sitios y páginas web accesibles.
description: Configure el Editor de texto enriquecido para crear sitios y páginas web accesibles.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Configuración de RTE para crear páginas web y sitios accesibles {#configure-rte-for-accessibility}

Adobe Experience Manager admite muchas funciones de accesibilidad estándar de acuerdo con varios estándares de accesibilidad. Además, los desarrolladores pueden personalizar o ampliar para proporcionar funciones que ayuden a crear contenido accesible mediante componentes de Experience Manager que utilicen el Editor de texto enriquecido (RTE).

Al diseñar páginas web y añadir contenido a las páginas, los desarrolladores y autores de contenido pueden utilizar las funciones de RTE para proporcionar información relacionada con la accesibilidad. Por ejemplo, agregue información estructural a través de encabezados y elementos de párrafo.

Para configurar y personalizar estas funciones, [configuración de los complementos RTE](#configure-the-plugin-features) para el componente. Por ejemplo, la variable `paraformat` complemento le permite añadir elementos semánticos de nivel de bloque adicionales, incluida la ampliación del número de niveles de encabezado admitidos más allá del `H1`, `H2`y `H3` proporcionado de forma predeterminada.

El RTE está disponible en una variedad de componentes para la interfaz de usuario táctil y la interfaz de usuario clásica. Sin embargo, el componente principal para utilizar RTE es el **Texto** componente que está disponible para ambas interfaces. Las siguientes imágenes muestran el RTE con una gama de complementos habilitados, incluyendo `paraformat`:

![Componente de texto (RTE) en modo de pantalla completa en la IU táctil.](assets/chlimage_1-206.png)

*Figura: Componente Texto en la interfaz de usuario táctil.*

![Cuadro de diálogo de edición (RTE) del componente de texto en la IU clásica.](assets/chlimage_1-207.png)

*Figura: Componente Texto en la interfaz de usuario de Classic.*

Para ver las diferencias entre las características de RTE disponibles en las distintas interfaces, consulte [Los complementos y sus funciones](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configuración de las características del complemento {#configure-the-plugin-features}

Para obtener instrucciones completas para configurar el RTE, consulte [configurar el editor de texto enriquecido](/help/sites-administering/rich-text-editor.md) página. Esto cubre todos los problemas, incluidos los pasos clave:

* [Complementos y funciones](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Ubicaciones de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Activar un complemento y configurar la propiedad de funciones](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configurar otras funcionalidades del RTE](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un complemento dentro de los `rtePlugins` en CRXDE Lite, puede activar todas las funciones o características específicas de ese complemento.

![CRXDE Lite que muestra un ejemplo rtePlugin.](assets/chlimage_1-208.png)

### Ejemplo: especifique los formatos de párrafo disponibles en el campo de selección RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Se pueden hacer disponibles nuevos formatos de bloque semántico para su selección mediante:

1. En función de su RTE, determine y vaya a la [ubicación de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilitar el campo de selección Párrafos](/help/sites-administering/rich-text-editor.md); por [activación del complemento](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique los formatos que desea que estén disponibles en el campo de selección Párrafos](/help/sites-administering/rich-text-editor.md).
1. Los formatos de párrafo están disponibles para el autor de contenido desde los campos de selección en RTE. Se puede acceder a ellas:

   * Uso del icono de almohadilla del párrafo en la IU táctil.
   * Al usar la variable **Formato** campo (selector emergente) en la IU clásica.

Con los elementos estructurales disponibles en RTE a través de las opciones de formato de párrafo, AEM ofrece una buena base para el desarrollo de contenido accesible. Los autores de contenido no pueden usar el RTE para dar formato al tamaño de fuente o a los colores u otros atributos relacionados, lo que impide la creación de formato en línea. En su lugar, deben seleccionar los elementos estructurales adecuados, como encabezados y utilizar estilos globales elegidos en la opción Estilos. Esto garantiza una limpieza del marcado y buenas opciones para los usuarios que exploran con sus propias hojas de estilo y contenido correctamente estructurado.

## Uso de la función de edición de fuentes {#use-of-the-source-edit-feature}

En algunos casos, los autores de contenido encontrarán necesario examinar y ajustar el código fuente del HTML creado mediante RTE. Por ejemplo, un fragmento de contenido creado dentro de RTE puede requerir un marcado adicional para garantizar el cumplimiento de WCAG 2.0. Esto se puede hacer con la variable [editar fuente](/help/sites-administering/rich-text-editor.md#aboutplugins) de RTE. Puede especificar la variable [ `sourceedit` en la función `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilice la variable `sourceedit` con cuidado. Escribir errores o funciones no admitidas puede provocar más problemas.

## Agregar compatibilidad para más elementos y atributos del HTML {#add-support-for-more-html-elements-and-attributes}

Para ampliar aún más las características de accesibilidad de AEM, es posible ampliar los componentes existentes basados en el RTE (como el **Texto** y **Tabla** componentes) con elementos y atributos adicionales.

El siguiente procedimiento ilustra cómo ampliar el **Tabla** componente con un **Pie de ilustración** elemento que proporciona información sobre una tabla de datos para los usuarios de tecnología de asistencia:

### Ejemplo: añadir el rótulo al cuadro de diálogo Propiedades de tabla {#example-adding-the-caption-to-the-table-properties-dialog}

En el constructor del `TablePropertiesDialog`, agregue un campo de entrada de texto adicional que se utilizará para editar el rótulo. Tenga en cuenta que `itemId` debe estar configurado como `caption` (es decir, el nombre del atributo DOM) para gestionar automáticamente su contenido.

En **Tabla**, establezca explícitamente o elimine el atributo en/desde el elemento DOM. El cuadro de diálogo pasa el valor en la variable `config` objeto. Tenga en cuenta que los atributos DOM deben configurarse o eliminarse utilizando la variable correspondiente `CQ.form.rte.Common` métodos ( `com` es un método abreviado para `CQ.form.rte.Common`) para evitar obstáculos comunes con las implementaciones de exploradores.

>[!NOTE]
>
>Este procedimiento solo es adecuado para la interfaz de usuario clásica.

### Ejemplo: creación de un HTML accesible al utilizar énfasis en el texto {#create-accessible-html-for-text}

RTE puede utilizar `strong` y `em` etiquetas en lugar de `b` y `i`. Agregue el siguiente nodo como un elemento secundario al `uiSettings` y `rtePlugins` en el cuadro de diálogo.

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
   >Es posible que tenga que crear carpetas intermedias si no existen.

1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   hasta:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Abra el siguiente archivo para editarlo (ábralo con doble clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. En el `constructor` antes de la lectura de línea:

   ```
   var dialogRef = this;
   ```

   Agregue el siguiente código:

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

1. Guarde los cambios utilizando **Guardar todo...**

>[!NOTE]
>
>Un campo de texto sin formato no es el único tipo de entrada permitido para el valor del elemento de rótulo. Puede utilizar cualquier utilidad ExtJS que proporcione el valor del rótulo a través de su `getValue()` método.
>
>Para añadir funciones de edición para otros elementos y atributos adicionales, asegúrese de que ambos:
>
>* La variable `itemId` para cada campo correspondiente se establece en el nombre del atributo DOM apropiado (`TablePropertiesDialog`).
>* El atributo se establece o elimina explícitamente en el elemento DOM (`Table`).


>[!MORELIKETHIS]
>
>* [Guía rápida de WCAG 2.0](/help/managing/qg-wcag.md)
>* [Crear contenido accesible (conformidad con WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

