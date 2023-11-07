---
title: Vista previa de un formulario
seo-title: Previewing a form
description: Puede obtener una vista previa de los formularios antes de publicarlos o activarlos para asegurarse de que cumplen las expectativas. Las opciones de vista previa pueden variar según los tipos de formulario admitidos.
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 85%

---

# Vista previa de un formulario {#previewing-a-form}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>

## Información general {#overview}

En AEM Forms, puede obtener una vista previa de los formularios y los documentos presentes en el repositorio. La vista previa permite saber exactamente qué aspecto tienen los formularios y cómo se comportan cuando se entregan a los usuarios finales.

Al obtener una vista previa de los formularios, estos se representan en la interfaz interactiva, y el usuario puede rellenarlos con datos. Al obtener una vista previa de los documentos, estos se representan en el modo no interactivo, y el usuario únicamente puede ver el documento. En el caso de los formularios, hay disponible una opción adicional de vista previa personalizada. Con esta opción, puede obtener una vista previa del formulario utilizando datos de un archivo XML. Los datos rellenan algunos o todos los campos del formulario que se está previsualizando.

La siguiente tabla muestra las opciones de vista previa disponibles para los distintos tipos de formularios admitidos:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de recurso</strong><br /> </td>
   <td><strong>Opciones de vista previa disponibles</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Vista previa del PDF</td>
  </tr>
  <tr>
   <td>Formulario PDF</td>
   <td>Vista previa del PDF y vista previa con datos<br /> </td>
  </tr>
  <tr>
   <td>formulario adaptable</td>
   <td>Vista previa del HTML y vista previa del HTML con datos</td>
  </tr>
  <tr>
   <td>Plantilla de formulario</td>
   <td>Vista previa del PDF, vista previa del PDF con datos, vista previa del HTML, vista previa del HTML con datos<br /> </td>
  </tr>
 </tbody>
</table>

## Vista previa de un formulario {#previewing-a-form-1}

1. Seleccione el recurso que desea previsualizar y haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png) en la barra de herramientas de acciones.

   >[!NOTE]
   >
   >Para seleccionar un recurso, cambie a la vista Lista en la vista Tarjeta predeterminada. Haga clic en ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para cambiar de vista.

1. Al hacer clic en Vista previa, se muestran las posibles opciones de vista previa aplicables al tipo de recurso seleccionado. Haga clic en la opción que desee para representar el recurso seleccionado en una nueva pestaña.

   Las opciones son las siguientes:

   * Vista precia como HTML
   * Vista previa con datos
   * Vista previa como PDF (disponible para plantillas de formulario)

## Vista previa con datos {#preview-with-data}

Al seleccionar **Vista previa con datos**, puede ver el aspecto que tendrá el formulario una vez que se introduzcan datos reales en él. La opción Vista previa con datos permite cargar un XML con datos de usuario de ejemplo. Los datos de usuario de ejemplo se utilizan para rellenar el formulario de vista previa en el formato que elija.

1. Seleccione un recurso, haga clic en Vista previa ![aem6forms_preview](assets/aem6forms_preview.png) y seleccione **Vista previa con datos**.
1. En el cuadro de diálogo Vista previa de formulario, proporcione FormData como el archivo XML. Haga clic en Vista previa para representar el formulario con los datos combinados del XML.
