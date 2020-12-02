---
title: Personalización de plantillas para componentes del portal de formularios
seo-title: Personalización de plantillas para componentes del portal de formularios
description: Mostrar metadatos personalizados en la lista de formularios
seo-description: Mostrar metadatos personalizados en la lista de formularios
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# Personalización de plantillas para componentes del portal de formularios{#customizing-templates-for-forms-portal-components}

## Requisitos previos {#prerequisites}

[Administración de metadatos de formulario](../../forms/using/manage-form-metadata.md)

Conocimientos prácticos sobre HTML y CSS

## Información general {#overview}

La interfaz de usuario de AEM Forms permite agregar metadatos a cualquier formulario. Los metadatos personalizados pueden mejorar la experiencia del usuario mientras enumera y busca los formularios de su organización.

Forms Portal le permite utilizar metadatos personalizados en los listados de formularios. Al crear plantillas personalizadas para recursos, puede modificar su diseño y utilizar metadatos personalizados con el conjunto de estilos CSS.

Siga estos pasos para crear una plantilla personalizada para varios componentes de Forms Portal.

## Creación de una plantilla personalizada {#creating-a-nbsp-custom-template}

1. Creación de un nodo sling:Folder en /apps

   Añada una propiedad &quot;fpContentType&quot;. Especifique los valores adecuados para la propiedad en función del componente para el que esté definiendo la plantilla personalizada.

   * Componente Búsqueda y listado: &quot;/libs/fd/fp/formTemplate&quot;
   * Componente Borradores y envíos:

      * Sección Borradores: /libs/fd/fp/DraftTemplate
      * Sección de Envíos: /libs/fd/fp/submitTemplate
   * Componente de vínculo: /libs/fd/fp/linkTemplate

   Añada un título que desee que se muestre al seleccionar plantillas de diseño.

   >[!NOTE]
   >
   >El título puede ser diferente del nombre de nodo de sling:Folder que ha creado.

   La siguiente imagen muestra la configuración del componente Buscar y listado.
   ![Creación de una sling:Folder](assets/1.png)

1. Cree un archivo template.html en esta carpeta para que sirva de plantilla personalizada.
1. Escriba la plantilla personalizada y utilice los metadatos personalizados como se describe a continuación.

## Ejemplo práctico {#working-example}

A continuación se muestra una implementación de muestra de una plantilla personalizada en la que Forms Portal adquiere un diseño de tarjeta de gobierno de Geometrixx personalizado para el componente Buscar y listar.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## Especificaciones técnicas para plantillas personalizadas {#technical-specifications-for-custom-templates}

Una plantilla personalizada para cualquier componente de Forms Portal incluye entradas repetibles y no repetibles. Las entradas repetibles son entidades básicas para la cotización. Ejemplos de entradas repetibles son los componentes Buscar y listado, Borradores y envíos y Vínculo.

Forms Portal proporciona una sintaxis para que los marcadores de posición muestren metadatos personalizados/OTB. Los marcadores de posición se rellenan después de mostrar los resultados de formularios, borradores o envíos.

Para incluir una entrada repetible, configure el valor del atributo **data-repetible** en **true**.

*En el ejemplo analizado, hay dos elementos Div presentes en la parte superior de la plantilla personalizada. La primera, con la clase CSS &quot;__FP_boxes-contenedor&quot;, funciona como un elemento de contenedor para los formularios que se muestran. El segundo, con la clase CSS &quot;__FP_boxes&quot;, es una plantilla para las entidades básicas, en este caso un formulario. El atributo **repetible de datos**presente en el elemento Div tiene el valor **true**.*

Cada marcador de posición tiene un conjunto exclusivo de metadatos OTB. Para mostrar metadatos personalizados en un lugar determinado del formulario, agregue la propiedad **${metadata_prop}** en el lugar.

*En el ejemplo, la propiedad metadata se utiliza en varias instancias. Por ejemplo, se utiliza en **description**,**name**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**y &lt;a11. 2/>path **de la manera prescrita.***

## Metadatos predeterminados {#out-of-the-box-metadata}

Varios componentes de Forms Portal proporcionan conjuntos exclusivos de metadatos OOTB que puede utilizar para la lista.

### Componente Búsqueda y listado {#search-amp-lister-component}

* **Título:** Título del formulario
* **name**: Nombre del formulario (en su mayoría es el mismo que el título)
* **descripción**: Descripción del formulario
* **formUrl**: URL para procesar el formulario como HTML
* **pdfUrl**: URL para procesar el formulario como PDF
* **assetType**: Tipo del recurso. Los valores válidos incluyen **Formulario**,**Formulario PDF**, **Formulario de impresión** y **Formulario adaptable**

* **htmlStyle** y  **pdfStyle**: Estilo de visualización para los iconos HTML y PDF, respectivamente, utilizados para la representación. Los valores válidos son &quot;**__FP_display_none**&quot; o blank.

>[!NOTE]
>
>Recuerde utilizar la clase __FP_display_none en la hoja de estilo personalizada.

* **downloadUrl**: URL para descargar un recurso.

Compatibilidad con la localización, clasificación y uso de las propiedades de configuración en la interfaz de usuario (solo Search &amp; Lister):

1. **Compatibilidad** con localizaciones: Para localizar cualquier texto estático, utilice el atributo  `${localize-YOUR_TEXT}` y haga que el valor localizado esté disponible, si no existe ya.
   *En el ejemplo analizado, los atributos  `${localize-Apply}` y  `${localize-Download}` se utilizan para localizar el texto Aplicar y Descargar.*

1. **Compatibilidad con la ordenación**: Haga clic en el elemento HTML para ordenar los resultados de búsqueda. Para implementar la ordenación en un diseño tabulado, agregue el atributo &quot;data-sortKey&quot; en el encabezado de tabla concreto. Además, añada su valor como metadatos para los que desea ordenar.
Por ejemplo, para el encabezado &quot;Título&quot; en la vista de cuadrícula, el valor del encabezado &quot;data-sortKey&quot; es &quot;título&quot;. Haga clic en el encabezado para ordenar los valores de una columna en particular.

1. **Uso de las propiedades** de configuración: El componente Búsqueda y listado tiene varias configuraciones que puede utilizar en la interfaz de usuario. Por ejemplo, para mostrar texto de información sobre herramientas HTML guardado a través del cuadro de diálogo de edición, utilice el atributo `${config-htmlLinkText}`. **Del mismo modo, para el texto de información del objeto PDF, utilice** `${config-pdfLinkText}` el atributo .

### Componente de vínculo {#link-component}

* **Título:** Título del formulario
* **formUrl**: URL para procesar el formulario como HTML
* **destinatario**: Destinatario del vínculo. Los valores válidos son &quot;_blank&quot; y &quot;_self&quot;.
* **linkText**: Rótulo de vínculo

### Componente Borradores y envíos {#drafts-amp-submissions-component}

* **Ruta**: Ruta del nodo de metadatos de borradores/envíos. Utilícelo con la extensión .HTML como URL para abrir un borrador o envío.
* **contextPath**: Ruta de contexto de la instancia de AEM
* **firstLetter**: Primera letra (mayúscula) del título del formulario adaptable, que se guardó como borrador o se envió.
* **formName**: Título del formulario adaptable, que se guardó como borrador o se envió.
* **draftID**: ID del borrador que se muestra (se utiliza solo en la plantilla de la sección Borrador).
* **submitID**: ID del envío que se muestra (se utiliza solo en la plantilla de la sección Envío).
* **estado**: Estado del formulario enviado. (Se utiliza solo en la plantilla de la sección Envío).
* **descripción**: Descripción del formulario adaptable asociado con el borrador o el envío.
* **diffTime**: Diferencia entre la hora actual y la última acción de guardar del borrador. Alternativamente, la diferencia entre la hora actual y la última acción de envío para el envío.
* **iconClass**: Clase CSS utilizada para mostrar la primera letra del borrador/envío. Forms Portal incluye las siguientes clases, que proporcionan distintos fondos de color.
* **propietario**: Usuario que creó el borrador/envío.
* **Hoy**: Fecha de creación del borrador o envío en formato DD:MM:AAAA.
* **TimeNow**: Hora de creación del borrador o envío en formato HH:MM:SS de 24 horas

*Nota:*

1. Para la opción Eliminar de la sección Borradores del componente Borradores y envíos, asigne a la clase CSS el nombre &quot;__FP_deleteDraft&quot;. Además, incluya el atributo &quot;draftID&quot; con el valor **${draftID}**, que es el identificador de borrador del borrador correspondiente.

1. Al crear vínculos para abrir borradores y envíos, puede especificar **${path}.html** como el valor del atributo **href** para la etiqueta de anclaje.

![Nodo Borradores y envío](assets/raw-image-with-index.png)

**A**. Elemento contenedor

**B.**  Metadatos de &quot;ruta&quot; con una jerarquía fija para obtener la miniatura almacenada para cada formulario.

**C.Atributo** repetible de datos utilizado para la sección de plantilla para cada formulario

**D.** Para localizar la cadena &quot;Aplicar&quot;

**E.** Uso de la propiedad de configuración pdfLinkText

**F.** Uso de los metadatos &quot;pdfUrl&quot;

## Sugerencias, trucos y problemas conocidos {#tips-tricks-and-known-issues}

1. No utilice comillas simples (&#39;) en ninguna plantilla personalizada.
1. Para metadatos personalizados, almacene esta propiedad solo en el nodo **jcr:content/metadata**. Si lo almacena en cualquier otro lugar, Forms Portal no puede mostrar los metadatos.
1. Asegúrese de que el nombre de los metadatos personalizados o los metadatos existentes no incluya dos puntos ( : ). Si lo hace, no puede mostrarlo en la interfaz de usuario.
1. **los datos** repetitivos no tienen importancia para un  **** componente de Linkcomponent. Adobe recomienda evitar el uso de esta propiedad en la plantilla de un componente de vínculo.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)