---
title: Vista previa de un formulario
seo-title: Vista previa de un formulario
description: Puede obtener una vista previa de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de vista previa pueden variar según los tipos de formulario admitidos.
seo-description: Puede obtener una vista previa de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de vista previa pueden variar según los tipos de formulario admitidos.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Vista previa de un formulario {#previewing-a-form}

## Información general {#overview}

En AEM Forms, puede obtener una vista previa de los formularios y documentos presentes en el repositorio. La vista previa ayuda a conocer exactamente el aspecto y el comportamiento de los formularios cuando se lanzan a los usuarios finales.

Al obtener una vista previa de los formularios, se procesan en la interfaz interactiva y el usuario puede rellenar los formularios con datos. Al obtener una vista previa de los documentos, se procesan en modo no interactivo y el usuario solo puede ver el documento. Para los formularios, hay disponible una opción adicional de Vista previa personalizada. Con esta opción, puede obtener una vista previa del formulario utilizando datos de un archivo XML. Los datos rellenan algunos o todos los campos del formulario que se está previsualizando.

En la tabla siguiente se muestran las opciones de vista previa disponibles para los distintos tipos de formularios admitidos:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong><br /> </td>
   <td><strong>Opciones de vista previa disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Vista previa de PDF</td>
  </tr>
  <tr>
   <td>Formulario PDF</td>
   <td>Vista previa de PDF y Vista previa con datos<br /> </td>
  </tr>
  <tr>
   <td>formulario adaptable</td>
   <td>Vista previa HTML y vista previa HTML con datos</td>
  </tr>
  <tr>
   <td>Plantilla de formulario</td>
   <td>vista previa de PDF, vista previa de PDF con datos, vista previa de HTML, vista previa de HTML con datos<br /> </td>
  </tr>
 </tbody>
</table>

## Vista previa de un formulario {#previewing-a-form-1}

1. Seleccione el recurso cuya vista previa desee obtener y haga clic en Vista previa de ![aem6forms_preview](assets/aem6forms_preview.png) en la barra de herramientas de acciones.

   >[!NOTE]
   >
   >Para seleccionar un recurso, cambie a la vista Lista desde la vista de tarjeta predeterminada. Haga clic en ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para cambiar de vista.

1. Al hacer clic en Vista previa se muestran las posibles opciones de vista previa aplicables al tipo de recurso seleccionado. Haga clic en la opción que desee para procesar el recurso seleccionado en una nueva ficha.

   Sus opciones son:

   * Vista previa como HTML
   * Vista previa con datos
   * Vista previa como PDF (disponible para plantillas de formulario)

## Vista previa con datos {#preview-with-data}

Al seleccionar **Vista previa con datos**, puede ver el aspecto del formulario con los datos reales introducidos en él. La opción Vista previa con datos permite cargar un XML que contiene datos de usuario de ejemplo. Los datos de usuario de ejemplo se utilizan para rellenar el formulario de vista previa en el formato que elija.

1. Seleccione un recurso, haga clic en Vista previa de ![aem6forms_preview](assets/aem6forms_preview.png)y seleccione **Vista previa con datos**.
1. En el cuadro de diálogo Vista previa del formulario, proporcione FormData como archivo XML. Haga clic en Vista previa para procesar el formulario con los datos combinados de XML.

