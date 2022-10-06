---
title: Guardado de un formulario de HTML 5 como borrador
seo-title: Saving an HTML5 form as a draft
description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo en una etapa posterior.
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# Guardado de un formulario de HTML 5 como borrador {#saving-an-html-form-as-a-draft}

Se puede guardar un formulario de HTML5 como borrador y seguir rellenándolo en una etapa posterior. Forms Portal permite a cualquier usuario guardar y restaurar un formulario de HTML5. Para habilitar la funcionalidad Guardar como borrador , agregue las siguientes configuraciones al nodo de perfil:

## Perfil personalizado para permitir la función Guardar como borrador {#custom-profile-to-allow-save-as-draft-feature}

De serie, AEM Forms proporciona un **Guardar como borrador** perfil. Puede procesar un formulario con el perfil Guardar como borrador para habilitar la funcionalidad de borrador para un formulario HTML5. Puede especificar el perfil de renderización del HTML para un formulario en [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar la funcionalidad Guardar como borrador para las [perfil personalizado](/help/forms/using/custom-profile.md), agregue las siguientes propiedades al nodo de perfil personalizado:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Cadena</td>
   <td>true</td>
   <td><p>Habilita la función Guardar como borrador</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Cadena</td>
   <td>true</td>
   <td><p>Permite cargar archivos adjuntos</p> <p>con este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Almacenamiento y lista de borradores {#drafts-storage-and-listing}

Después de activar la función Guardar como borrador en un formulario; cuando se guarda el formulario, aparece en la lista [Componente Borradores y Presentación](/help/forms/using/draft-submission-component.md). Puede recuperar y comenzar a rellenar el formulario guardado desde el componente Borrador y envío.

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
   <td>true</td>
   <td>Para permitir que los borradores y formularios se incluyan en<br /> Componente Borradores y envíos del portal de Forms después del envío</td>
  </tr>
 </tbody>
</table>

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el nodo /content/forms/fp de la instancia de publicación. Puede agregar su proveedor de almacenamiento personalizado; para obtener más información, consulte [Almacenamiento personalizado para el componente Borradores y envíos](/help/forms/using/adding-custom-storage-provider-forms.md).
