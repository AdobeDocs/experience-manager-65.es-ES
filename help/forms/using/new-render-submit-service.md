---
title: Nuevo servicio de renderización y envío
seo-title: New render and submit service
description: Defina los servicios de renderización y envío en Workbench para procesar el formulario XDP como HTML o PDF según el dispositivo desde el que se acceda.
seo-description: Define render and submit services in Workbench to render XDP form as HTML or PDF depending on the device it is accessed from.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Nuevo servicio de renderización y envío{#new-render-and-submit-service}

## Introducción {#introduction}

En Workbench, al definir una `AssignTask` especifique un formulario concreto (formulario XDP o PDF). Especifique también un conjunto de servicios de procesamiento y envío mediante un perfil de acción.

Un XDP se puede procesar como formulario de PDF o de HTML. Las nuevas funciones incluyen la capacidad de:

* Representar y enviar un formulario XDP como HTML
* Representar y enviar un formulario XDP como PDF en el escritorio y como HTML en dispositivos móviles (por ejemplo, un iPad)

### Nuevo servicio de HTML Forms {#new-html-forms-service}

El nuevo servicio Forms de HTML aprovecha la nueva función de Forms para admitir la representación del formulario XDP como HTML. El nuevo servicio Forms de HTML expone los siguientes métodos:

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Puede encontrar más información sobre los perfiles de formularios móviles en [Creación de un perfil personalizado](/help/forms/using/custom-profile.md).

## Nuevos procesos de procesamiento y envío de formularios del HTML {#new-html-form-render-amp-submit-processes}

Para cada operación &#39;AssignTask&#39;, especifique un proceso de procesamiento y un proceso de envío con el formulario. TaskManager llama a estos procesos `renderForm`y `submitForm`API para permitir la administración personalizada. Semántica de estos procesos para el nuevo formulario de HTML:

### Representar un nuevo formulario de HTML {#render-a-new-html-form}

El nuevo proceso para procesar el HTML, como todos los procesos de procesamiento, tiene los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outFormDoc`

Este método simula el comportamiento exacto de `renderHTMLForm` API de NewHTMLFormsService. Llama a la función `generateFormURL` para obtener la URL de la representación de HTML del formulario. A continuación, rellena runtimeMap con las siguientes claves o valores:

nuevo formulario html = true

newHTMLFormURL = la URL devuelta después de llamar a `generateFormURL` API.

### Enviar un nuevo formulario de HTML {#submit-a-new-html-form}

Este proceso para enviar un nuevo formulario de HTML funciona con los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outputDocument`

El proceso define la variable `outputDocument`a `inputDocument`recuperado de `taskContext`.

## Procesos de procesamiento o envío predeterminados y perfiles de acción {#default-render-or-submit-processes-and-action-profiles}

Los servicios de procesamiento y envío predeterminados permiten que los PDF se representen en un equipo de escritorio y que el HTML en dispositivos móviles (iPad).

### Formulario de procesamiento predeterminado {#default-render-form}

Este proceso procesa un formulario XDP en varias plataformas sin problemas. El proceso recupera el agente de usuario de `taskContext`y utiliza los datos para llamar al proceso para procesar el HTML o el PDF.

![default-render-form](assets/default-render-form.png)

### Formulario de envío predeterminado {#default-submit-form}

Este proceso envía un formulario XDP en varias plataformas sin problemas. Recupera el agente de usuario de `taskContext`y utiliza los datos para llamar al proceso y enviar el HTML o el PDF.

![default-submit-form](assets/default-submit-form.png)

## Cambiar la renderización de formularios móviles de PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Los navegadores están retirando gradualmente la compatibilidad con los complementos basados en NPAPI, incluidos los complementos para Adobe Acrobat y Adobe Acrobat Reader. Puede cambiar la renderización de formularios móviles de PDF a HTML siguiendo los pasos siguientes:

1. Inicie sesión en Workbench como usuario válido.
1. Select **Archivo** > **Obtener aplicaciones**.

   Aparece el cuadro de diálogo Obtener aplicaciones .

1. Seleccione las aplicaciones para las que desea cambiar la renderización del formulario móvil y haga clic en **OK**.
1. Abra el proceso para el que desee cambiar la renderización.
1. Abra el punto de inicio o la tarea de destino, vaya a la sección Presentación y datos y haga clic en **Administrar perfiles de acción**.

   Aparece el cuadro de diálogo Administrar perfiles de acción .
1. Cambie las configuraciones de perfil de procesamiento predeterminado de PDF a HTML y haga clic en **OK**.
1. Compruebe en el proceso.
1. Repita los pasos para cambiar la renderización para otros procesos.
1. Implemente la aplicación correspondiente a los procesos que haya cambiado.

### Perfil de acción predeterminado {#default-action-profile}

El perfil de acción predeterminado representaba el formulario XDP como PDF. Este comportamiento se ha cambiado para utilizar los procesos Formulario de procesamiento predeterminado y Formulario de envío predeterminado.

Algunas de las preguntas más frecuentes sobre los perfiles de acción son las siguientes:

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué procesos de procesamiento/envío estarán disponibles de forma predeterminada?**

* Guía de procesamiento (las guías están en desuso)
* Guía de renderización de formularios
* Formulario de PDF de procesamiento
* Formulario de HTML de procesamiento
* Renderizar nuevo formulario de HTML (nuevo)
* Formulario de procesamiento predeterminado (nuevo)

Y, procesos de envío equivalentes.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué perfiles de acción estarán disponibles de forma predeterminada?**

Para XDP Forms:

* Predeterminado (procesar/enviar con los nuevos procesos &quot;Procesamiento/Enviar predeterminado&quot;)

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un equipo de escritorio?**

Nada. El perfil de acción predeterminado se elige automáticamente y el modo de renderización también se cuida automáticamente.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué se debe hacer para permitir que el formulario se procese en HTML en un escritorio?**

El usuario debe seleccionar el botón de opción HTML para el perfil predeterminado.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Habrá algún impacto de actualización en el cambio del comportamiento predeterminado del perfil de acción?**

Sí, dado que los servicios de procesamiento y envío anteriores asociados al perfil de acción predeterminado eran diferentes, se tratan como una personalización de los formularios existentes. Al hacer clic en **Restaurar valores predeterminados**, los servicios de renderización y envío predeterminados se establecen en su lugar.

Si ha modificado los servicios de formulario de PDF de envío o procesamiento existentes o ha creado servicios personalizados (por ejemplo, personalizado1), y desea utilizar la misma funcionalidad para la representación de HTML. Debe replicar el nuevo servicio de renderización o envío (como custom2) y aplicar personalizaciones similares a las de . Ahora, modifique el perfil de acción para que su XDP empiece a utilizar los servicios custom2, en lugar del custom1 para renderizar o enviar.

¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un equipo de escritorio?
¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un equipo de escritorio?
