---
title: Incrustación del componente de vínculo en una página
seo-title: Incrustación del componente de vínculo en una página
description: Puede utilizar el componente de vínculo para vincular un documento adaptable o un formulario adaptable desde cualquier página.
seo-description: Puede utilizar el componente de vínculo para vincular un documento adaptable o un formulario adaptable desde cualquier página.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Incrustación del componente de vínculo en una página{#embedding-link-component-in-a-page}

## Requisitos previos {#prerequisites}

El componente de vínculo es un miembro de la categoría de Document Services. Asegúrese de que la categoría de Document Services esté visible en el navegador de componentes de AEM. Si la categoría no aparece en la lista, siga los pasos que se indican en [Activación de los componentes](/help/forms/using/enabling-forms-portal-components.md)del portal de formularios.

## Componente de vínculo {#link-component}

El componente Vínculo permite a los autores del portal de formularios crear un vínculo a un formulario adaptable desde cualquier lugar de una página. El componente Vínculo está disponible en la sección Document Services del navegador de componentes.

Realice los siguientes pasos para agregar un componente Vínculo a la página:

1. Arrastre el componente **Vínculo** a la página. Seleccione el componente y toque ![cmppr](assets/cmppr.png). Se abre el cuadro de diálogo Editar componente de vínculo.

   ![edit-link-component](assets/edit-link-component.png)

1. En la ficha **Mostrar** , especifique lo siguiente:

   * **Rótulo** del vínculo: Texto o rótulo del vínculo.
   * **Información del objeto** de vínculo: Información del objeto para el vínculo.
   * **Plantilla** de diseño: Plantilla para el diseño del componente Vínculo.

1. Abra la ficha Información **del** recurso y especifique el tipo de recurso. Un recurso puede ser un **formulario**. Según el tipo de recurso seleccionado, se muestran las opciones siguientes:

   * **Ruta** del recurso: Ruta del repositorio donde se almacena el recurso.

   * **Tipo** de procesamiento: El formato de procesamiento: PDF, HTML o Automático. El tipo de procesamiento automático detecta el entorno de usuario y, en consecuencia, procesa el formulario como HTML o PDF. Por ejemplo, si se accede al formulario desde un dispositivo móvil, el tipo de procesamiento automático procesa el formulario en HTML.
   * **** Enviar URL:  Dirección URL del servlet donde se envían los datos del formulario.
   * **Perfil** HTML: Perfil para procesar el formulario como HTML.
   * **Perfil** PDF: Perfil para procesar el formulario como documento PDF.

1. Abra la pestaña **Avanzadas.** Puede especificar los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

   Toque **Listo** para guardar la configuración.

## Prácticas recomendadas para utilizar el componente Vínculo {#best-practices-for-using-link-component-br}

* Asegúrese de seleccionar PDF como tipo de procesamiento si la ruta especificada en Ruta de formulario apunta a un documento que tiene PDF como formato de procesamiento permitido.
* La dirección URL de envío de un formulario se puede especificar en varios lugares y su orden de prioridad es el siguiente:

   1. La dirección URL de envío incrustada en el formulario (en el botón de envío) tiene la prioridad más alta.
   1. La dirección URL de envío mencionada en Forms Manager tiene la prioridad media.
   1. La dirección URL de envío mencionada en el portal de formularios tiene la prioridad más baja.
