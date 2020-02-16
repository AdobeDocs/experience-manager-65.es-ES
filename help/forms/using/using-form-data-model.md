---
title: Usar modelo de datos de formulario
seo-title: Usar modelo de datos de formulario
description: Aprenda a utilizar el modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
seo-description: Aprenda a utilizar el modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Usar modelo de datos de formulario{#use-form-data-model}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms le permite utilizar orígenes de datos de servidor dispares para crear un modelo de datos de formulario que puede utilizar como esquema en varios formularios adaptables y flujos de trabajo de comunicaciones interactivas. Requiere configurar orígenes de datos y crear un modelo de datos de formulario basado en objetos del modelo de datos y servicios disponibles en orígenes de datos. Para obtener más información, consulte:

* [Integración de datos de AEM Forms](../../forms/using/data-integration.md)
* [Configurar orígenes de datos](../../forms/using/configure-data-sources.md)
* [Crear modelo de datos de formulario](../../forms/using/create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md)

Un modelo de datos de formulario es una extensión del esquema JSON que puede utilizar para:

* [Creación de formularios y fragmentos adaptables](#create-af)
* [Crear comunicaciones interactivas y bloques de creación como fragmentos de texto, lista y condición](#create-ic)
* [Previsualizar comunicaciones interactivas con datos de muestra](#preview-ic)
* [Rellenar formularios adaptables y comunicaciones interactivas](#prefill)
* [Volver a escribir los datos de formularios adaptables enviados en orígenes de datos](#write-af)
* [Invocar servicios mediante reglas de formulario adaptables](#invoke-services)

## Creación de formularios y fragmentos adaptables {#create-af}

Puede crear formularios [](../../forms/using/creating-adaptive-form.md) adaptables y fragmentos [de formulario](../../forms/using/adaptive-form-fragments.md) adaptables basados en un modelo de datos de formulario. Para utilizar un modelo de datos de formulario al crear un formulario adaptable o un fragmento de formulario adaptable, haga lo siguiente:

1. En la ficha Modelo de formulario de la pantalla Agregar propiedades, seleccione Modelo **[!UICONTROL de datos de]** formulario en la lista desplegable **[!UICONTROL Seleccionar desde]** .

   ![create-af-1-1](assets/create-af-1-1.png)

1. Puntee para expandir **[!UICONTROL Seleccionar modelo]** de datos de formulario. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (Solo **** fragmentos de formulario adaptables) Puede crear un fragmento de formulario adaptable basado en un solo objeto de modelo de datos en un modelo de datos de formulario. Desplegable Expandir definiciones **[!UICONTROL del modelo de datos de]** formulario. Muestra una lista con todos los objetos del modelo de datos del formulario especificado. Seleccione un objeto de modelo de datos de la lista.

   ![create-af-3](assets/create-af-3.png)

Una vez creado el formulario adaptable o fragmento de formulario adaptable basado en un modelo de datos de formulario, los objetos del modelo de datos de formulario aparecen en la ficha Objetos **[!UICONTROL del modelo de]** datos del navegador de contenido en el editor de formularios adaptable.

>[!NOTE] {graybox=&quot;true&quot;}
>
>Para un fragmento de formulario adaptable, solo el objeto de modelo de datos seleccionado en el momento de la creación y los objetos de modelo de datos asociados aparecen en la ficha Objetos del modelo de datos.

![data-model-Objects-tab](assets/data-model-objects-tab.png)

Puede arrastrar y soltar objetos del modelo de datos en el formulario o fragmento adaptable para agregar campos de formulario. Los campos de formulario agregados conservan las propiedades de metadatos y el enlace con las propiedades de objeto del modelo de datos. El enlace garantiza que los valores de los campos se actualicen en los orígenes de datos correspondientes al envío del formulario y se rellenen previamente cuando se procesa el formulario.

## Crear comunicaciones interactivas {#create-ic}

Puede crear una comunicación interactiva basada en un modelo de datos de formulario que puede utilizar para rellenar previamente la comunicación interactiva con datos de orígenes de datos configurados. Además, los componentes básicos de una comunicación interactiva, como fragmentos de documento de texto, lista y condición, pueden basarse en un modelo de datos de formulario.

Puede elegir un modelo de datos de formulario al crear una comunicación interactiva o un fragmento de documento. La siguiente imagen muestra la ficha General del cuadro de diálogo Crear comunicación interactiva.

![create-ic](assets/create-ic.png)

Ficha General del cuadro de diálogo Crear comunicación interactiva

Para obtener más información, consulte:

[Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)

[Texto en comunicaciones interactivas](/help/forms/using/texts-interactive-communications.md)

[Condiciones de las comunicaciones interactivas](/help/forms/using/conditions-interactive-communications.md)

[Lista de fragmentos](/help/forms/using/lists.md)

## Vista previa con datos de muestra {#preview-ic}

El editor del modelo de datos de formulario permite generar y editar datos de ejemplo para objetos del modelo de datos en el modelo de datos de formulario. Puede utilizar estos datos para obtener una vista previa y probar las comunicaciones interactivas y los formularios adaptables. Debe generar los datos de ejemplo antes de realizar la vista previa como se describe en [Trabajar con el modelo](../../forms/using/work-with-form-data-model.md#sample)de datos de formulario.

Para obtener una vista previa de una comunicación interactiva con datos del modelo de datos de formulario de ejemplo:

1. En la instancia de creación de AEM, vaya a **[!UICONTROL Formularios > Formularios y documentos]**.
1. Seleccione una comunicación interactiva y toque **[!UICONTROL Vista previa]** en la barra de herramientas para seleccionar Canal **** Web, Canal **[!UICONTROL de]** impresión o **[!UICONTROL Ambos canales]** para obtener una vista previa de la comunicación interactiva.
1. En el cuadro de diálogo [*Canal*] de vista previa, asegúrese de que está seleccionada la opción **[!UICONTROL Probar datos del modelo]** de datos de formulario y toque **[!UICONTROL Vista previa]**.

La comunicación interactiva se abre con datos de ejemplo precargados.

![vista previa web](assets/web-preview.png)

Del mismo modo, para obtener una vista previa de un formulario adaptable con datos de ejemplo, abra el formulario adaptable en modo de autor y toque **[!UICONTROL Vista previa]**.

## Rellenar previamente mediante el servicio de modelo de datos de formulario {#prefill}

AEM Forms proporciona el servicio de cumplimentación previa del modelo de datos de formulario incorporado que puede activar para formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario. El servicio de relleno previo consulta los orígenes de datos para los objetos del modelo de datos en el formulario adaptable y la comunicación interactiva y, en consecuencia, antepone los datos al procesar el formulario o la comunicación.

Para habilitar el servicio de cumplimentación previa del modelo de datos de formulario para un formulario adaptable, abra las propiedades del contenedor de formulario adaptable y seleccione el servicio **[!UICONTROL de cumplimentación previa del modelo de datos de]** formulario en la lista desplegable Servicio **[!UICONTROL de]** cumplimentación previa del acordeón Básico. A continuación, guarde las propiedades.

![prefill-service](assets/prefill-service.png)

Para configurar el servicio de cumplimentación previa del modelo de datos de formulario en una comunicación interactiva, puede seleccionar Servicio de cumplimentación previa del modelo de datos de formulario en la lista desplegable Servicio de cumplimentación previa al crearlo o posteriormente modificando las propiedades.

![edit-ic-props](assets/edit-ic-props.png)

Cuadro de diálogo Editar propiedades para una comunicación interactiva

## Escribir datos de formularios adaptables enviados en orígenes de datos {#write-af}

Cuando un usuario envía un formulario basado en un modelo de datos de formulario, se puede configurar el formulario para escribir los datos enviados para un objeto de modelo de datos en sus orígenes de datos. Para conseguir este caso de uso, AEM Forms proporciona una acción [de envío del modelo de datos de](../../forms/using/configuring-submit-actions.md)formulario, disponible de forma predeterminada solo para formularios adaptables basados en un modelo de datos de formulario. Escribe los datos enviados para un objeto de modelo de datos en su origen de datos.

Para configurar la acción de envío del modelo de datos de formulario, abra las propiedades del contenedor de formulario adaptable y seleccione **[!UICONTROL Enviar con el modelo]** de datos de formulario en la lista desplegable Enviar acción en el acordeón Envío. A continuación, busque y seleccione un objeto de modelo de datos en la lista desplegable **[!UICONTROL Nombre del objeto de modelo de datos para enviar]** . Guarde las propiedades.

Al enviar el formulario, los datos del objeto del modelo de datos configurado se escriben en el origen de datos correspondiente.

![envío de datos](assets/data-submission.png)

También puede enviar archivos adjuntos de formulario a un origen de datos mediante la propiedad object del modelo de datos binario. Para enviar archivos adjuntos a un origen de datos JDBC, haga lo siguiente:

1. Agregue un objeto de modelo de datos que incluya una propiedad binaria al modelo de datos de formulario.
1. En el formulario adaptable, arrastre y suelte el componente **[!UICONTROL Archivo adjunto]** del navegador Componentes en el formulario adaptable.
1. Toque para seleccionar el componente agregado y toque ![settings_icon](assets/settings_icon.png) para abrir el navegador de propiedades del componente.
1. En el campo Referencia de enlace, toque ![foldersearch_18](assets/foldersearch_18.png) y desplácese hasta seleccionar la propiedad binaria agregada en el modelo de datos de formulario. Configure otras propiedades según corresponda.

   Toque ![el botón](assets/check-button.png) de verificación para guardar las propiedades. El campo de datos adjuntos ahora está enlazado a la propiedad binaria del modelo de datos de formulario.

1. En la sección Envío de las propiedades del contenedor de formulario adaptable, habilite **[!UICONTROL Enviar datos adjuntos]** de formulario. Envía los datos adjuntos en el campo de propiedad binaria al origen de datos al enviar el formulario.

## Invocar servicios en formularios adaptables mediante reglas {#invoke-services}

En un formulario adaptable basado en un modelo de datos de formulario, puede [crear reglas](../../forms/using/rule-editor.md) para invocar servicios configurados en el modelo de datos de formulario. La operación **[!UICONTROL Invocar servicios]** de una regla enumera todos los servicios disponibles en el modelo de datos de formulario y le permite seleccionar campos de entrada y salida para el servicio. También puede utilizar el tipo de regla **Definir valor** para invocar un servicio de modelo de datos de formulario y establecer el valor de un campo en el resultado devuelto por el servicio.

Por ejemplo, la regla siguiente invoca un servicio get que toma Id. de empleado como entrada y los valores devueltos se rellenan en los campos Id. dependiente, Apellido, Nombre y Género correspondientes del formulario.

![invoke-service](assets/invoke-service.png)

Además, puede utilizar la `guidelib.dataIntegrationUtils.executeOperation` API para escribir un JavaScript en el editor de código del editor de reglas. Para obtener más información sobre API, consulte [API para invocar el servicio](/help/forms/using/invoke-form-data-model-services.md)del modelo de datos de formulario.
