---
title: Guardar un formulario HTML5 como borrador
seo-title: Guardar un formulario HTML5 como borrador
description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo más adelante.
seo-description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo más adelante.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---


# Guardar un formulario HTML5 como borrador {#saving-an-html-form-as-a-draft}

Puede guardar un formulario HTML5 como borrador y volver a rellenarlo más adelante. Forms Portal permite a cualquier usuario guardar y restaurar un formulario HTML5. Para habilitar la funcionalidad Guardar como borrador, agregue las configuraciones siguientes al nodo perfil:

## Perfil personalizado para permitir la función Guardar como borrador {#custom-profile-to-allow-save-as-draft-feature}

De forma predeterminada, AEM Forms proporciona un perfil **Guardar como borrador**. Puede procesar un formulario con el perfil Guardar como borrador para activar la funcionalidad de borrador en un formulario HTML5. Puede especificar el perfil de procesamiento HTML para un formulario en [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar la funcionalidad Guardar como borrador para el [perfil personalizado](/help/forms/using/custom-profile.md) existente, agregue las siguientes propiedades al nodo de perfil personalizado:

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
   <td><p>Permite guardar como función de borrador</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Cadena</td>
   <td>verdadero</td>
   <td><p>Permite cargar archivos adjuntos</p> <p>con este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Borradores almacenamiento y listado {#drafts-storage-and-listing}

Después de activar la funcionalidad Guardar como borrador para un formulario; cuando se guarda el formulario, aparece en el componente [Borradores y envío](/help/forms/using/draft-submission-component.md). Puede recuperar y rellenar en inicio el formulario guardado desde el componente Borrador y envío.

Para habilitar la lista de formularios para el componente Borrador y envío, agregue la siguiente propiedad al nodo perfil:

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
   <td>Para permitir que los borradores y formularios se incluyan en el componente Borradores y envíos de Forms Portal después del envío<br /></td>
  </tr>
 </tbody>
</table>

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el nodo /content/forms/fp de la instancia de Publish. Puede agregar su proveedor de almacenamiento personalizado; para obtener más información, consulte [almacenamiento personalizado para borradores y envíos, componente](/help/forms/using/adding-custom-storage-provider-forms.md).
