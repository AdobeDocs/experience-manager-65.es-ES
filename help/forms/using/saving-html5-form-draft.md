---
title: Guardado de un formulario HTML5 como borrador
seo-title: Guardado de un formulario HTML5 como borrador
description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo en una etapa posterior.
seo-description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo en una etapa posterior.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# Guardado de un formulario HTML5 como borrador {#saving-an-html-form-as-a-draft}

Se puede guardar un formulario HTML5 como borrador y volver a rellenarlo en una etapa posterior. Forms Portal permite que cualquier usuario guarde y restaure un formulario HTML5. Para habilitar la funcionalidad Guardar como borrador , agregue las siguientes configuraciones al nodo de perfil:

## Perfil personalizado para permitir la función Guardar como borrador {#custom-profile-to-allow-save-as-draft-feature}

De serie, AEM Forms proporciona un perfil **Guardar como borrador**. Puede procesar un formulario con el perfil Guardar como borrador para activar la funcionalidad de borrador en un formulario HTML5. Puede especificar el perfil de renderización HTML para un formulario en [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar la funcionalidad Guardar como borrador para su [perfil personalizado](/help/forms/using/custom-profile.md) existente, agregue las siguientes propiedades al nodo de perfil personalizado:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Value</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Cadena</td>
   <td>verdadero</td>
   <td><p>Habilita la función Guardar como borrador</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Cadena</td>
   <td>verdadero</td>
   <td><p>Permite cargar archivos adjuntos</p> <p>con este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Almacenamiento de borradores y listado {#drafts-storage-and-listing}

Después de activar la función Guardar como borrador en un formulario; cuando se guarda el formulario, aparece en el componente [Borradores y envío](/help/forms/using/draft-submission-component.md). Puede recuperar y comenzar a rellenar el formulario guardado desde el componente Borrador y envío.

Para habilitar la lista de formularios para el componente Borrador y envío, agregue la siguiente propiedad al nodo de perfil:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Cadena</td>
   <td>verdadero</td>
   <td>Para permitir que los borradores y formularios se incluyan en el componente <br /> Borradores y envíos del portal de Forms después del envío</td>
  </tr>
 </tbody>
</table>

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el nodo /content/forms/fp de la instancia de publicación. Puede agregar su proveedor de almacenamiento personalizado; para obtener más información, consulte [Almacenamiento personalizado para el componente Borradores y envíos](/help/forms/using/adding-custom-storage-provider-forms.md).
