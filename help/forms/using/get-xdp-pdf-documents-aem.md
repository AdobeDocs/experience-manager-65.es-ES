---
title: Obtención de documentos XDP y PDF en AEM Forms
seo-title: Obtención de documentos XDP y PDF en AEM Forms
description: AEM Forms permite cargar formularios y recursos admitidos para su uso con formularios adaptables. También puede cargar formularios de forma masiva y recursos relacionados como ZIP.
seo-description: AEM Forms permite cargar formularios y recursos admitidos para su uso con formularios adaptables. También puede cargar formularios de forma masiva y recursos relacionados como ZIP.
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Obtención de documentos XDP y PDF en AEM Forms{#getting-xdp-and-pdf-documents-in-aem-forms}

## Información general {#overview}

Puede importar los formularios desde el sistema de archivos local al repositorio de CRX cargándolos en AEM Forms. La operación de carga es compatible con los siguientes tipos de recursos:

* Plantillas de formulario (formularios XFA)
* Formularios PDF
* Documento (documentos PDF planos)

Puede cargar los tipos de recurso admitidos individualmente o como archivo ZIP. Puede cargar un recurso del tipo `Resource`, solo junto con un formulario XFA en un archivo ZIP.

>[!NOTE]
>
>Asegúrese de que es miembro del `form-power-users` grupo para poder cargar archivos XDP. Póngase en contacto con el administrador para convertirse en miembro del grupo.

## Carga de formularios {#uploading-forms}

1. Para iniciar sesión en la interfaz de usuario de AEM Forms, acceda a `https://'[server]:[port]'/aem/forms.html`.
1. Vaya a la carpeta en la que desea cargar el formulario o la carpeta que contiene los formularios.
1. En la barra de herramientas de acciones, toque **Crear > Carga** de archivos.

   ![Archivos de la opción de almacenamiento local en Crear](assets/step.png)

1. El cuadro de diálogo Cargar formularios o paquetes le permite examinar y elegir el archivo que desea cargar. El explorador de archivos solo muestra los formatos de archivo admitidos (ZIP, XDP y PDF).

   >[!NOTE]
   >
   >Un nombre de archivo solo puede contener caracteres alfanuméricos, guiones o guiones bajos.

1. Haga clic en Cargar después de seleccionar el archivo para cargar los archivos o haga clic en &#39;Cancelar&#39; para cancelar la carga. Una ventana emergente lista los recursos que se agregan y los recursos que se actualizan en la ubicación actual.

   >[!NOTE]
   >
   >Para un archivo ZIP, se muestran las rutas relativas de todos los recursos admitidos. Los recursos no admitidos dentro del ZIP se omiten y no aparecen en la lista. Sin embargo, si el archivo ZIP contiene solo los recursos no admitidos, se muestra un mensaje de error en lugar del cuadro de diálogo emergente.

   ![Cuadro de diálogo de carga al cargar un formulario XFA](assets/upload-scr.png)

1. Si uno o varios recursos tienen un nombre de archivo no válido, se muestra un error. Corrija los nombres de archivo resaltados en rojo y vuelva a cargarlos.

   ![Mensaje de error al cargar un formulario XFA](assets/upload-scr-err.png)

Una vez completada la carga, un flujo de trabajo en segundo plano genera miniaturas para cada recurso, según la previsualización del recurso. Las versiones más recientes de los recursos, si se cargan, anulan los recursos existentes.

### Modo protegido {#protected-mode}

El servidor de AEM Forms permite ejecutar código JavaScript. Un código JavaScript malintencionado puede dañar un entorno de AEM Forms. El modo protegido restringe el uso de AEM Forms para ejecutar archivos XDP solo desde ubicaciones y recursos de confianza. Todos los XDP disponibles en la interfaz de usuario de AEM Forms se consideran recursos de confianza.

El modo protegido está activado de forma predeterminada. Si es necesario, puede desactivar el modo protegido:

1. Inicie sesión en AEM Web Console como administrador. La dirección URL es https://&#39;[server]:[port]&#39;/system/console/configMgr
1. Abra Configuraciones de formularios móviles para editarlas.
1. Anule la selección de la opción Modo protegido y haga clic en **Guardar**. El modo protegido está desactivado.

## Actualización de formularios XFA a los que se hace referencia {#updating-referenced-xfa-forms}

En AEM Forms, una plantilla de formulario XFA puede ser referida por un formulario adaptable u otra plantilla de formulario XFA. Además, una plantilla puede hacer referencia a un recurso u otra plantilla XFA.

Un formulario adaptable que hace referencia a un XFA tiene sus campos enlazados con los campos disponibles en el XFA. Al actualizar una plantilla de formulario, el formulario adaptable asociado intenta sincronizarse con el XFA. Para obtener más información, consulte [Sincronización de formularios adaptables con el XFA](../../forms/using/synchronizing-adaptive-forms-xfa.md)asociado.

La eliminación de una plantilla de formulario daña el formulario adaptable o la plantilla de formulario dependientes. Este tipo de formulario adaptable se conoce a veces informalmente como un formulario sucio. En la interfaz de usuario de AEM Forms, puede encontrar los formularios sucios de las dos formas siguientes.

* Se muestra un icono de advertencia en la miniatura del formulario adaptable de la lista de recursos y el siguiente mensaje aparece al pasar el puntero sobre el icono de advertencia.\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![Advertencia para un formulario adaptable sin sincronizar después de actualizar el XFA asociado](assets/dirtyaf.png)

Se mantiene un indicador para indicar si un formulario adaptable está sucio. Esta información está disponible en la página de propiedades del formulario, junto con los metadatos del formulario. Solo para formularios adaptables sucios, una propiedad de metadatos `Model Refresh` muestra `Recommended` el valor.

![Indicación de que un formulario adaptable no está sincronizado con el modelo XFA](assets/model-refresh.png)

