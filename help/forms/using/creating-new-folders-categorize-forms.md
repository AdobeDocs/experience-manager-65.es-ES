---
title: Crear nuevas carpetas para aplicar categorías a los formularios
seo-title: Crear nuevas carpetas para aplicar categorías a los formularios
description: Utilice carpetas para organizar las plantillas de formulario, los PDF, los recursos y los formularios adaptables.
seo-description: Utilice carpetas para organizar las plantillas de formulario, los PDF, los recursos y los formularios adaptables.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Crear nuevas carpetas para aplicar categorías a los formularios {#create-new-folders-to-categorize-forms}

Puede organizar mejor los recursos mediante carpetas. Dado que AEM Forms admite varios tipos de recursos (plantillas de formulario, PDF, documentos, recursos y formularios adaptables, con varios metadatos), puede utilizar carpetas para clasificar los formularios según los criterios deseados.

AEM Forms permite cambiar el título de una carpeta. El título no es el mismo que el nombre del nodo en el que se almacena la carpeta en el repositorio. En su lugar, el título se mantiene como metadatos para la carpeta. Si cambia el título de una carpeta, la ruta de cualquier recurso presente dentro de la carpeta no se verá afectada.

## Cree una carpeta  . {#create-a-folder}

Puede crear una carpeta en AEM Forms de una de las siguientes maneras:

* Cargue un archivo ZIP que contenga recursos en la estructura de carpetas deseada (consulte [Obtención de documentos XDP y PDF en AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Crear una nueva carpeta vacía

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.
1. Desplácese a la ubicación en la que desea crear una carpeta.
1. Haga clic en el icono ![aem6forms_add](assets/aem6forms_add.png) de la barra de herramientas y, a continuación, seleccione **[!UICONTROL Crear carpeta]**.

1. Introduzca los siguientes detalles:

   * **Título:** Mostrar nombre para la carpeta
   * **Nombre:** *(obligatorio)* El nombre del nodo en el que desea almacenar la carpeta en el repositorio.

   >[!NOTE]
   >
   >De forma predeterminada, el valor del campo de nombre se rellena automáticamente desde el título. El nombre solo puede contener caracteres alfanuméricos o caracteres especiales de guion (-) y guion bajo (_). Cualquier otro carácter especial introducido en el título se sustituye automáticamente por un guión y se le solicita que confirme el nuevo nombre. Puede elegir continuar con el nombre sugerido o editarlo más adelante.

1. Haga clic en **[!UICONTROL Enviar].**

   Se muestra una nueva carpeta con el título que haya definido en la ubicación actual de la lista de recursos.

   Si existe una carpeta con el nombre especificado, el envío falla con un error. Puede ver el mensaje de error pasando el cursor sobre el icono de error ![aem6forms_error_alert](assets/aem6forms_error_alert.png) que aparece junto al campo de nombre.

### Editar el título de la carpeta {#edit-the-folder-title-br}

1. Seleccione la carpeta cuyo título desee editar.
1. Haga clic en el icono editar ![aem6forms_edit](assets/aem6forms_edit.png) de la barra de herramientas.
1. Introduzca el nuevo título. El campo de texto se rellena previamente con el valor actual del título de la carpeta. Puede cambiarlo a un nuevo valor.
1. Haga clic en **[!UICONTROL Enviar].**
