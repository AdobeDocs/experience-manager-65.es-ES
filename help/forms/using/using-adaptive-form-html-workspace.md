---
title: Uso de un formulario adaptable en HTML Workspace
seo-title: Uso de un formulario adaptable en HTML Workspace
description: Uso de un formulario adaptable en HTML Workspace
seo-description: Uso de un formulario adaptable en HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# Uso de un formulario adaptable en HTML Workspace{#using-an-adaptive-form-in-html-workspace}

AEM Forms en JEE ofrece la posibilidad de utilizar un formulario adaptable en HTML Workspace.

Como se puede seleccionar un XDP durante el diseño de proceso, se ha agregado la capacidad de examinar desde un formulario adaptable existente AEM repositorio. Esta función permite al diseñador de procesos configurar un formulario adaptable tanto en el punto de inicio como en la Tarea.

## Experiencia de diseño de procesos {#process-design-experience}

Realice lo siguiente para habilitar los formularios adaptables para su uso en el diseño de procesos:

* En Asignar Tarea y punto de Inicio, puede buscar un recurso de formulario adaptable en el repositorio de CRX al asignar un recurso de formulario a una tarea.
* En la hoja de propiedades Asignar área de trabajo de Tarea/punto de Inicio, puede ocultar la barra de herramientas de nivel superior/global de un formulario adaptable.
* Puede utilizar nuevos perfiles de acción para procesar y enviar acciones en formularios adaptables.

### Exportación e importación de aplicaciones de LiveCycle {#livecycle-application-export-and-import}

Dado que los formularios adaptables se encuentran en el repositorio de AEM, la exportación de la aplicación LiveCycle solo contiene las referencias para los formularios adaptables utilizados. Por lo tanto, la exportación e importación de la aplicación de LiveCycle es un proceso de dos pasos. La aplicación LiveCycle incluye definiciones de procesos, etc. Un paquete independiente que contiene formularios adaptables se exporta como archivo ZIP desde AEM. Durante la importación, la aplicación LiveCycle se importa a través de Workbench y los formularios adaptables se importan a través de AEM.

## Experiencia del usuario en formularios adaptables en HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace proporciona algunos controles adaptables específicos del formulario, además de los controles disponibles para los formularios móviles. Un usuario puede agregar datos adjuntos, guardarlos, firmarlos, enviarlos y navegar por los formularios adaptables en el espacio de trabajo HTML cuando abre una Tarea o un punto de Inicio. Los siguientes son los detalles específicos:

1. Para adjuntar archivos, utilice archivos adjuntos de Tarea, como ocurrió en Mobile Forms. Cualquier botón de tipo Archivo adjunto del formulario adaptable está oculto.

1. Para guardar un formulario adaptable, haga clic en **Guardar**, como ocurrió en Mobile Forms. Cualquier botón Guardar tipo de formulario adaptable está oculto.

1. Para enviar un formulario adaptable, utilice el botón **Enviar** o las acciones de ruta disponibles, como ocurrió en Mobile Forms. Cualquier botón de tipo Enviar del formulario adaptable está oculto.

1. **Visibilidad** de la barra de herramientas de Formulario global adaptable: Si el diseñador de procesos oculta la barra de herramientas global o de nivel superior, la barra de herramientas y los botones no aparecen en los formularios adaptables.

1. **Controles de navegación del espacio de trabajo para Forms** adaptable: Los botones Siguiente/Anterior están disponibles junto con los botones Guardar, Enviar y Acción de ruta para un formulario adaptable en HTML Workspace. Haga clic en los botones Siguiente/Anterior para desplazarse por los paneles de formularios adaptables en HTML Workspace. Los botones Siguiente/Anterior proporcionan una navegación profunda, similar a los controles de navegación de la vista Móvil de los formularios adaptables.

1. **Servicios de eSign y componente de resumen del formulario** adaptable: El componente Resumen no funciona en el espacio de trabajo HTML. En otras palabras, si un formulario adaptable tiene un componente Resumen, no estará visible en el espacio de trabajo. En lugar de Enviar automáticamente en el componente Diseño, el usuario del espacio de trabajo hace clic en la acción Enviar o de ruta en el espacio de trabajo HTML. Después de firmar un documento, se ve como un documento con firma plana. Haga clic en **Enviar** o en una acción de ruta para cerrar o completar la tarea o el punto de Inicio.\
   El documento firmado se recopila del servidor de servicios de eSign y el archivo xml de datos se reenvía al siguiente paso del proceso.

## Pasos para utilizar formularios adaptables en el diseño de procesos {#steps-to-use-adaptive-forms-in-process-design}

1. Abra Adobe Experience Manager Forms Workbench.

1. Vaya a **Archivo > Nuevo > Aplicación** o utilice la aplicación existente para crear una aplicación.

   ![Crear nueva aplicación](assets/create_new_appl.png)

   Crear nueva aplicación

1. Cree un proceso o utilice un proceso existente en la aplicación.

   ![Crear nuevo proceso](assets/create_new_process.png)

   Crear nuevo proceso

1. Cree un punto de Inicio o asigne una Tarea y haga clic en él con el botón doble.
1. En la sección **[!UICONTROL Presentación y datos]**, seleccione **[!UICONTROL usar un recurso CRX]** y haga clic en las elipses antes del recurso.

   ![Uso de un recurso CRX](assets/use_crx_asset.png)

   Uso de un recurso CRX

1. Seleccione el formulario adaptable creado mediante la interfaz de usuario de Administrar recursos y haga clic en **[!UICONTROL Aceptar]**.

   ![Seleccionar un formulario adaptable](assets/selecting_form.png)

   Seleccionar un formulario adaptable

   >[!NOTE]
   >
   >Para obtener más información sobre la creación de un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Para obtener más información sobre cómo crear un proceso, consulte [Creación y administración de procesos](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).

