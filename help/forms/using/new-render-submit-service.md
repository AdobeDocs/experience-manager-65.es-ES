---
title: Nuevo servicio de procesamiento y envío
seo-title: Nuevo servicio de procesamiento y envío
description: Defina los servicios de procesamiento y envío en Workbench para procesar el formulario XDP como HTML o PDF en función del dispositivo desde el que se acceda a él.
seo-description: Defina los servicios de procesamiento y envío en Workbench para procesar el formulario XDP como HTML o PDF en función del dispositivo desde el que se acceda a él.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Nuevo servicio de procesamiento y envío{#new-render-and-submit-service}

## Introducción {#introduction}

En Workbench, cuando defina una `AssignTask` operación, especifique un formulario concreto (formulario XDP o PDF). Además, especifique un conjunto de servicios de procesamiento y envío mediante un perfil de acción.

Un XDP se puede procesar como formulario PDF o HTML. Las nuevas funciones incluyen la capacidad de:

* Representar y enviar un formulario XDP como HTML
* Representar y enviar un formulario XDP como PDF en el escritorio y como HTML en dispositivos móviles (por ejemplo, un iPad)

### Nuevo servicio de formularios HTML {#new-html-forms-service}

El nuevo servicio de formularios HTML aprovecha la nueva función de Forms para admitir la representación de formularios XDP como HTML. El nuevo servicio de formularios HTML expone los siguientes métodos:

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

Para obtener más información sobre los perfiles de formulario móvil, consulte [Creación de un perfil](/help/forms/using/custom-profile.md)personalizado.

## Nuevos procesos de envío y procesamiento de formularios HTML {#new-html-form-render-amp-submit-processes}

Para cada operación &#39;Asignar tarea&#39;, especifique un proceso de procesamiento y un proceso de envío con el formulario. TaskManager `renderForm`y `submitForm`las API llaman a estos procesos para permitir la administración personalizada. Semánticos de estos procesos para Nuevo formulario HTML:

### Representar un nuevo formulario HTML {#render-a-new-html-form}

El nuevo proceso para procesar HTML, como todos los procesos de procesamiento, tiene los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outFormDoc`

Este método simula el comportamiento exacto de la `renderHTMLForm` API de NewHTMLFormsService. Llama a la `generateFormURL` API para obtener la URL para la representación HTML del formulario. A continuación, rellena RuntimeMap con las siguientes claves o valores:

nuevo formulario HTML = true

newHTMLFormURL = la URL devuelta después de llamar a `generateFormURL` API.

### Enviar un nuevo formulario HTML {#submit-a-new-html-form}

Este proceso para enviar un nuevo formulario HTML funciona con los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outputDocument`

El proceso establece el `outputDocument`en el `inputDocument`recuperado de `taskContext`.

## Procesos de procesamiento o envío predeterminados y perfiles de acción {#default-render-or-submit-processes-and-action-profiles}

Los servicios predeterminados de procesamiento y envío permiten la compatibilidad para procesar archivos PDF en un escritorio y HTML en dispositivos móviles (iPad).

### Formulario de procesamiento predeterminado {#default-render-form}

Este proceso procesa un formulario XDP en varias plataformas sin problemas. El proceso recupera el agente de usuario de `taskContext`y utiliza los datos para llamar al proceso para procesar HTML o PDF.

![default-output-form](assets/default-render-form.png)

### Formulario de envío predeterminado {#default-submit-form}

Este proceso envía un formulario XDP en varias plataformas sin problemas. Recupera el agente de usuario `taskContext`y utiliza los datos para llamar al proceso para enviar HTML o PDF.

![default-submit-form](assets/default-submit-form.png)

## Cambiar la representación de formularios móviles de PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Los navegadores están retirando gradualmente la compatibilidad con los complementos basados en NPAPI, incluidos los complementos para Adobe Acrobat y Adobe Acrobat Reader. Puede cambiar la representación de formularios móviles de PDF a HTML mediante los siguientes pasos:

1. Inicie sesión en Workbench como usuario válido.
1. Seleccione **Archivo** > **Obtener aplicaciones**.

   Aparece el cuadro de diálogo Obtener aplicaciones.

1. Seleccione las aplicaciones para las que desea cambiar la representación del formulario móvil y haga clic en **Aceptar**.
1. Abra el proceso para el que desea cambiar la representación.
1. Abra el punto de inicio o la tarea de destino, vaya a la sección Presentación y datos y haga clic en **Administrar perfiles** de acción.

   Aparece el cuadro de diálogo Administrar perfiles de acción.
1. Cambie las configuraciones de perfil de procesamiento predeterminadas de PDF a HTML y haga clic en **Aceptar**.
1. Compruebe el proceso.
1. Repita los pasos para cambiar el procesamiento de otros procesos.
1. Implemente la aplicación relevante para los procesos que haya cambiado.

### Perfil de acción predeterminado {#default-action-profile}

El perfil de acción predeterminado procesaba el formulario XDP como PDF. Este comportamiento se ha cambiado para utilizar los procesos Formulario de procesamiento predeterminado y Formulario de envío predeterminado.

Algunas de las preguntas más frecuentes sobre los perfiles de acción son las siguientes:

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué procesos de procesamiento y envío estarán disponibles de forma predeterminada?**

* Guía de procesamiento (las guías están en desuso)
* Guía de procesamiento de formularios
* Representar formulario PDF
* Representar formulario HTML
* Representar nuevo formulario HTML (nuevo)
* Formulario de procesamiento predeterminado (nuevo)

Y, procesos de envío equivalentes.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué perfiles de acción estarán disponibles de forma predeterminada?**

Para formularios XDP:

* Predeterminado (procesar/enviar mediante los nuevos procesos &#39;Predeterminado de procesamiento/envío&#39;)

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un escritorio?**

Nada. El perfil de acción predeterminado se elige automáticamente y el modo de procesamiento también se toma en consideración automáticamente.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Qué se debe hacer para permitir que el formulario se procese en HTML en un escritorio?**

El usuario debe seleccionar el botón de opción HTML para el perfil predeterminado.

![gen_question_b_20](assets/gen_question_b_20.png) **¿Tendrá algún impacto de actualización en el cambio del comportamiento predeterminado del perfil de acción?**

Sí, dado que los servicios de procesamiento y envío anteriores asociados al perfil de acción predeterminado eran diferentes, se tratan como una personalización de los formularios existentes. Al hacer clic en **Restaurar valores predeterminados**, se establecen los servicios predeterminados de procesamiento y envío.

Si ha modificado los servicios de procesamiento o envío de formulario PDF existentes o ha creado servicios personalizados (por ejemplo, personalizado1) y desea utilizar la misma funcionalidad para la representación HTML. Debe replicar el nuevo servicio de procesamiento o envío (como custom2) y aplicar personalizaciones similares a ellas. Ahora, modifique el perfil de acción del XDP para que comience a utilizar servicios personalizados2, en lugar del custom1 para procesar o enviar.

¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un escritorio?
¿Qué debe hacer el diseñador de procesos para permitir que el formulario se procese en HTML en un dispositivo y en PDF en un escritorio?  [Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
