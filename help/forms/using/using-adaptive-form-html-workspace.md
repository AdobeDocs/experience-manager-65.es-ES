---
title: Uso de un formulario adaptable en HTML Workspace
seo-title: Using an adaptive form in HTML Workspace
description: Uso de un formulario adaptable en HTML Workspace
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Uso de un formulario adaptable en HTML Workspace{#using-an-adaptive-form-in-html-workspace}

AEM Forms en JEE ofrece la capacidad de utilizar un formulario adaptable en HTML Workspace.

Como se puede seleccionar un XDP durante el diseño del proceso, se ha añadido la capacidad de examinar desde un formulario adaptable existente AEM repositorio. La capacidad permite al diseñador de procesos configurar un formulario adaptable tanto en el punto de inicio como en la tarea.

## Experiencia en diseño de procesos {#process-design-experience}

Realice las siguientes acciones para permitir que los formularios adaptables se utilicen en el diseño de procesos:

* En Asignar tarea y punto de inicio, puede buscar un recurso de formulario adaptable en el repositorio CRX al asignar un recurso de formulario a una tarea.
* En la hoja de propiedades Asignar tarea/Iniciar punto de trabajo, puede ocultar la barra de herramientas global/de nivel superior de un formulario adaptable.
* Puede utilizar nuevos perfiles de acción para las acciones de procesamiento y envío en los formularios adaptables.

### exportación e importación de aplicaciones de LiveCycle {#livecycle-application-export-and-import}

Dado que los formularios adaptables están en el repositorio de AEM, la exportación de la aplicación de LiveCycle contiene solo las referencias para los formularios adaptables utilizados. Por lo tanto, la exportación e importación de la aplicación de LiveCycle es un proceso de dos pasos. La aplicación de LiveCycle incluye definiciones de procesos, etc. Un paquete independiente que contiene formularios adaptables se exporta como archivo ZIP desde AEM. Durante la importación, la aplicación de LiveCycle se importa mediante Workbench y los formularios adaptables se importan mediante AEM.

## Experiencia del usuario en formularios adaptables en HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace proporciona algunos controles adaptables específicos de formularios, además de los controles disponibles para formularios móviles. Un usuario puede agregar archivos adjuntos, guardar, firmar, enviar y navegar por los formularios adaptables en HTML Workspace cuando abre una tarea o un punto de inicio. Los siguientes son los detalles específicos:

1. Para adjuntar archivos, utilice archivos adjuntos de tarea, como ocurrió en Mobile Forms. Cualquier botón de tipo Archivo adjunto del formulario adaptable está oculto.

1. Para guardar un formulario adaptable, haga clic en **Guardar**, como ocurrió en Mobile Forms. Cualquier botón de tipo Guardar del formulario adaptable está oculto.

1. Para enviar un formulario adaptable, utilice el **Submit** acciones de ruta o botón disponibles, como ocurrió en Mobile Forms. Cualquier botón de tipo Submit del formulario adaptable está oculto.

1. **Visibilidad de la barra de herramientas de Formulario adaptable Global**: Si el diseñador de procesos oculta la barra de herramientas global/de nivel superior, la barra de herramientas y los botones no aparecen en los formularios adaptables.

1. **Controles de navegación de Workspace para Forms adaptable**: Los botones Siguiente/Anterior están disponibles junto con los botones Guardar, Enviar y Acción de ruta para un formulario adaptable en HTML Workspace. Haga clic en los botones Siguiente/Anterior para desplazarse por los paneles de formularios adaptables en HTML Workspace. Los botones Siguiente/Anterior proporcionan una navegación profunda, similar a los controles de navegación de la vista Móvil de los formularios adaptables.

1. **Servicios de eSign y componente de resumen del formulario adaptable**: El componente Resumen no es operativo en HTML Workspace. En otras palabras, si un formulario adaptable tiene un componente Resumen, no es visible en el espacio de trabajo. En lugar de Enviar automáticamente en el componente Diseño, el usuario del espacio de trabajo hace clic en Enviar o en una acción de ruta en HTML Workspace. Una vez firmado un documento, se puede ver como un documento con firma plana. Haga clic en **Submit** o una acción de ruta para cerrar o completar la tarea o el punto de inicio.\
   El documento firmado se recopila del servidor de eSign services y el archivo xml de datos se reenvía al siguiente paso del proceso.

## Pasos para utilizar formularios adaptables en el diseño del proceso {#steps-to-use-adaptive-forms-in-process-design}

1. Abra Adobe Experience Manager Forms Workbench.

1. Vaya a **Archivo > Nuevo > Aplicación** o utilice la aplicación existente para crear una aplicación.

   ![Crear nueva aplicación](assets/create_new_appl.png)

   Crear nueva aplicación

1. Cree un proceso o utilice un proceso existente en la aplicación.

   ![Crear nuevo proceso](assets/create_new_process.png)

   Crear nuevo proceso

1. Cree un punto de inicio o asigne una tarea y haga doble clic en ella.
1. En el **[!UICONTROL Presentación y datos]** , seleccione **[!UICONTROL usar un recurso CRX]** y haga clic en los puntos suspensivos antes del recurso.

   ![Usar un recurso CRX](assets/use_crx_asset.png)

   Usar un recurso CRX

1. Seleccione el formulario adaptable creado a través de la interfaz de usuario de Administrar recursos y haga clic en **[!UICONTROL OK]**.

   ![Seleccionar un formulario adaptable](assets/selecting_form.png)

   Seleccionar un formulario adaptable

   >[!NOTE]
   >
   >Para obtener más información sobre la creación de un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Para obtener más información sobre cómo crear un proceso, consulte [Creación y administración de procesos](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
