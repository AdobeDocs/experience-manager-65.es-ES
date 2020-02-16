---
title: Configuración de RTE para la producción de sitios accesibles
description: Obtenga información sobre cómo configurar el editor de texto enriquecido de AEM para crear sitios accesibles.
uuid: 87539fee-3ecc-49f4-af3d-8dde72399c28
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ff0f006d-461c-4cc4-b6eb-d665f3f3b498
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Configuración de RTE para la producción de sitios accesibles {#configuring-rte-for-producing-accessible-sites}

AEM admite ambos:

* funciones de accesibilidad estándar, incluido texto alternativo para imágenes
* así como funciones adicionales a las que se puede acceder al crear contenido con componentes que utilizan el editor de texto enriquecido (RTE)

Los autores de contenido pueden utilizar funciones de RTE para proporcionar información de accesibilidad al añadir contenido a una página. Esto puede incluir agregar información estructural a través de encabezados y elementos de párrafo.

Puede [configurar y personalizar estas funciones configurando los complementos](#configuring-the-plugin-features) RTE para el componente. Por ejemplo, el complemento le permite agregar elementos semánticos de nivel de bloque adicionales, incluida la ampliación del número de niveles de encabezado admitidos más allá de los básicos `paraformat``H1`y `H2` `H3` proporcionados de forma predeterminada.

El RTE está disponible en una variedad de componentes, tanto de la IU táctil como de la clásica. Sin embargo, el componente principal para utilizar RTE es el componente **Texto** .

El componente **Texto** de AEM está disponible tanto para las IU táctiles como para las clásicas. Las siguientes imágenes muestran el editor de texto enriquecido con una serie de complementos activados, incluidos `paraformat`:

* Componente **Texto** en la IU táctil:

   ![Componente de texto (RTE) en modo de pantalla completa en la IU táctil.](assets/chlimage_1-206.png)

* El componente **Texto** de la IU clásica:

   ![Cuadro de diálogo de edición (RTE) del componente de texto en la IU clásica.](assets/chlimage_1-207.png)

>[!NOTE]
>
>Existen diferencias entre las funciones RTE disponibles en la IU clásica y la IU táctil. Para obtener más información, consulte
>
>* [Complementos y sus funciones](/help/sites-administering/rich-text-editor.md#aboutplugins)
>* [Complementos y sus funciones: IU táctil](/help/sites-administering/rich-text-editor.md#aboutplugins)
>



## Configuración de las funciones del complemento {#configuring-the-plugin-features}

Las instrucciones completas sobre la configuración de RTE están disponibles en la página [Configuración del editor](/help/sites-administering/rich-text-editor.md) de texto enriquecido. Esto abarca todos los problemas, incluidos los pasos clave:

* [Complementos y sus funciones](/help/sites-administering/rich-text-editor.md#aboutplugins)
* [Ubicaciones de configuración](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Activar un complemento y Configurar la propiedad de funciones](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configuración de otra funcionalidad del RTE](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Al configurar un complemento dentro de la `rtePlugins` subramificación adecuada en CRXDE Lite (ver la siguiente imagen), puede activar todas las características o específicas de ese complemento.

![CRXDE Lite muestra un ejemplo de rtePlugin.](assets/chlimage_1-208.png)

### Ejemplo: Especificación de formatos de párrafo disponibles en el campo de selección RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Los nuevos formatos de bloque semántico pueden estar disponibles para su selección mediante:

1. Según el RTE, determine y navegue a la ubicación [de](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)configuración.
1. [Habilite el campo](/help/sites-administering/rich-text-editor.md)de selección Párrafos; al [activar el complemento](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique los formatos que desea que estén disponibles en el campo](/help/sites-administering/rich-text-editor.md)de selección Párrafos.
1. Los formatos de párrafo están disponibles para el autor del contenido desde los campos de selección en RTE. Se puede acceder a ellos:

   * Uso del icono de almohadilla de párrafo en la IU táctil.
   * Uso del campo **Formato** (selector emergente) en la IU clásica.

Con los elementos estructurales disponibles en RTE mediante las opciones de formato de párrafo, AEM ofrece una buena base para el desarrollo de contenido accesible. Los autores de contenido no pueden utilizar RTE para dar formato al tamaño de fuente o a los colores u otros atributos relacionados, lo que impide la creación de formato en línea. En su lugar, deben seleccionar los elementos estructurales adecuados, como encabezados y utilizar estilos globales seleccionados en la opción Estilos. Esto garantiza la limpieza de las marcas, así como mayores opciones para los usuarios que exploran con sus propias hojas de estilo y contenido correctamente estructurado.

## Uso de la función de edición de origen {#use-of-the-source-edit-feature}

En algunos casos, los autores de contenido encontrarán necesario examinar y ajustar el código fuente HTML creado mediante RTE. Por ejemplo, un fragmento de contenido creado dentro del editor de texto enriquecido puede requerir un marcado adicional para garantizar el cumplimiento de WCAG 2.0. Esto se puede hacer con la opción de edición [de](/help/sites-administering/rich-text-editor.md#aboutplugins) origen de RTE. Puede especificar la [ función en el `sourceedit` complemento `misctools`](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilice la `sourceedit` función con cuidado. Los errores de escritura y/o las funciones no compatibles pueden provocar más problemas.

## Adición de compatibilidad con elementos y atributos HTML adicionales {#adding-support-for-additional-html-elements-and-attributes}

Para ampliar aún más las funciones de accesibilidad de AEM, es posible ampliar los componentes existentes basados en RTE (como los componentes **Texto** y **Tabla** ) con elementos y atributos adicionales.

El siguiente procedimiento ilustra cómo ampliar el componente **Tabla** con un elemento **Rótulo** que proporciona información sobre una tabla de datos a los usuarios de tecnología de asistencia:

### Ejemplo: Adición del rótulo al cuadro de diálogo Propiedades de tabla {#example-adding-the-caption-to-the-table-properties-dialog}

En el constructor del `TablePropertiesDialog`, agregue un campo de entrada de texto adicional que se utilice para editar el rótulo. Tenga en cuenta que `itemId` debe configurarse en `caption` (es decir, el nombre del atributo DOM) para gestionar automáticamente su contenido.

En la **tabla** debe establecer o eliminar explícitamente el atributo en o desde el elemento DOM. El valor se pasa por el cuadro de diálogo del `config` objeto. Tenga en cuenta que los atributos DOM deben configurarse o eliminarse utilizando los `CQ.form.rte.Common` métodos correspondientes ( `com` es un método abreviado para `CQ.form.rte.Common`) para evitar escollos comunes en las implementaciones del explorador.

>[!NOTE]
>
>Este procedimiento solo es adecuado para la IU clásica.

### Instrucciones paso a paso {#step-by-step-instructions}

1. Inicie CRXDE Lite. Por ejemplo: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

1. Abra el siguiente archivo para editarlo (ábralo con doble clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. En el `constructor` método, antes de la lectura de línea:

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

1. Guardar los cambios con **Guardar todo...**

>[!NOTE]
>
>Un campo de texto sin formato no es el único tipo de entrada permitido para el valor del elemento de rótulo. Se puede utilizar cualquier utilidad ExtJS que proporcione el valor del rótulo a través de su `getValue()` método.
>
>Para agregar capacidades de edición para otros elementos y atributos adicionales, asegúrese de que ambos:
>
>* La `itemId` propiedad de cada campo correspondiente se establece en el nombre del atributo DOM (`TablePropertiesDialog`) correspondiente.
>* El atributo se establece y/o elimina en el elemento DOM explícitamente (`Table`).


>[!MORELIKETHIS]
>
>* [Guía rápida de WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creación de contenido accesible (conformidad con WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

