---
title: Vista previa de un formulario
seo-title: Vista previa de un formulario
description: Puede realizar la previsualización de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de previsualización pueden variar según los tipos de formulario admitidos.
seo-description: Puede realizar la previsualización de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de previsualización pueden variar según los tipos de formulario admitidos.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# Vista previa de un formulario {#previewing-a-form}

## Información general {#overview}

En AEM Forms, puede realizar la previsualización de los formularios y documentos presentes en el repositorio. La previsualización ayuda a conocer exactamente el aspecto y el comportamiento de los formularios cuando se envían a los usuarios finales.

Al obtener una vista previa de los formularios, se procesan en la interfaz interactiva y el usuario puede rellenar los formularios con datos. Al obtener una vista previa de documentos, se procesan en modo no interactivo y el usuario solo puede realizar la vista del documento. Para los formularios, hay disponible una opción adicional de Previsualización personalizada. Con esta opción, puede realizar la previsualización del formulario utilizando datos de un archivo XML. Los datos rellenan algunos o todos los campos del formulario que se está previsualizando.

La siguiente tabla lista las opciones de previsualización disponibles para los distintos tipos de formularios admitidos:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong><br /> </td>
   <td><strong>Opciones de previsualización disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>PREVISUALIZACIÓN PDF</td>
  </tr>
  <tr>
   <td>Formulario PDF</td>
   <td>PREVISUALIZACIÓN y Previsualización de PDF con datos<br /> </td>
  </tr>
  <tr>
   <td>formulario adaptable</td>
   <td>PREVISUALIZACIÓN HTML y previsualización HTML con datos</td>
  </tr>
  <tr>
   <td>Plantilla de formulario</td>
   <td>PREVISUALIZACIÓN PDF, previsualización PDF con datos, previsualización HTML, previsualización HTML con datos<br /> </td>
  </tr>
 </tbody>
</table>

## Vista previa de un formulario {#previewing-a-form-1}

1. Seleccione un recurso que desee previsualización y haga clic en Previsualización ![aem6forms_previsualización](assets/aem6forms_preview.png) en la barra de herramientas de acciones.

   >[!NOTE]
   >
   >Para seleccionar un recurso, cambie a vista de Lista desde la vista de tarjeta predeterminada. Haga clic en ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para cambiar de vista.

1. Al hacer clic en Previsualización, se listas las posibles opciones de previsualización aplicables al tipo de recurso seleccionado. Haga clic en la opción que desee para procesar el recurso seleccionado en una nueva ficha.

   Sus opciones son:

   * Previsualización como HTML
   * Vista previa con datos
   * Previsualización como PDF (disponible para plantillas de formulario)

## Vista previa con datos {#preview-with-data}

Cuando selecciona **Previsualización con datos**, puede ver el aspecto del formulario con los datos reales introducidos en él. La opción previsualización con datos permite cargar un XML que contiene datos de usuario de ejemplo. Los datos de usuario de ejemplo se utilizan para rellenar el formulario de previsualización en el formato que elija.

1. Seleccione un recurso, haga clic en Previsualización ![aem6forms_previsualización](assets/aem6forms_preview.png) y seleccione **Previsualización con datos**.
1. En el cuadro de diálogo Formulario de Previsualización, proporcione FormData como archivo XML. Haga clic en Previsualización para procesar el formulario con los datos combinados de XML.

