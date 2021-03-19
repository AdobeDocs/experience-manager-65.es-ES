---
title: Diferenciación de características entre formularios HTML5 y PDF forms
seo-title: Diferenciación de características entre formularios HTML5 y PDF forms
description: Funcionalidad admitida en formularios y PDF forms HTML5
seo-description: Funcionalidad admitida en formularios y PDF forms HTML5
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 3%

---


# Diferenciación de características entre formularios HTML5 y PDF forms {#feature-differentiation-between-html-forms-and-pdf-forms}

La siguiente tabla especifica la compatibilidad de funciones proporcionada para los formularios y PDF forms HTML5:

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Formularios HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Códigos de barras<br /> </td>
   <td>No disponible en el nivel de interfaz de usuario. </td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Campo de firma<br /> </td>
   <td><strong>Las </strong> firmas digitales no son compatibles, pero se agrega un nuevo  <strong>campo de firma </strong> manuscrita para el papel, como las firmas. Se puede garabatear su firma en el formulario utilizando el campo <strong>Scribble Signature</strong>. La firma se guarda en el formulario como una imagen. Puede guardar la información de geolocalización en el campo <strong>Scribble Signature</strong>.</td>
   <td>Campo de firma disponible para <strong>firmas digitales</strong>.</td>
  </tr>
  <tr>
   <td>Combinación de datos</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Imágenes</td>
   <td>El esquema de URI de datos se utiliza para mostrar imágenes. Todas las versiones modernas de los navegadores admiten este esquema, pero hay diferencias en el rango de formatos de imagen que admite cada navegador.<br /> </td>
   <td>Los formatos .gif, .png, .jpeg, .bmp y .tiff son compatibles.</td>
  </tr>
  <tr>
   <td>Paginación<br /> </td>
   <td><p>Un formulario HTML5 se divide en paneles y cuadros para que tenga un aspecto similar al de los PDF forms. El tamaño de la página se calcula dinámicamente. Si se elimina o se marca oculto todo el contenido de una página de un formulario HTML5, la página en blanco se oculta y no se muestra ningún espacio vacío (espacio en blanco) entre las páginas que aparecen encima y debajo de la página en blanco.</p> <p>Si la combinación de datos o las secuencias de comandos agregan contenido a una página, la longitud de la página se amplía para dar cabida al contenido recién agregado. No se agregan nuevas páginas al formulario para dar cabida al contenido recién agregado. </p> <p><strong>Nota:</strong> Cuando se elimina o marca todo el contenido de una página en un formulario HTML5 oculto, la página en blanco (espacio en blanco) permanece visible entre la primera y la segunda página, pero no entre ninguna otra página.</p> </td>
   <td>La paginación en PDF depende del contenido de los datos fusionado o del contenido del usuario, y el recuento de páginas se incrementa/reduce en función de él.</td>
  </tr>
  <tr>
   <td>Encabezados/pies de página </td>
   <td>Compatible. <br /> <br /> Como los formularios móviles HTML5 no admiten saltos de página, los encabezados y pies de página aparecen solo una vez. Sin embargo, puede configurarlas en la presentación para que aparezcan en varios lugares de la vista previa de formularios móviles.<br /> </td>
   <td>Compatible.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>Se pueden personalizar utilidades para mejorar la experiencia del usuario en dispositivos móviles.<br /> </td>
   <td>Todos los widgets están bloqueados y no se puede conectar ningún widget personalizado.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Admite las construcciones de scripts XFA más utilizadas. Para obtener más información sobre las construcciones compatibles, consulte <a href="/help/forms/using/scripting-support.md">compatibilidad con secuencias de comandos</a>.</td>
   <td>Admite todas las construcciones de scripts XFA.</td>
  </tr>
  <tr>
   <td>API de Acrobat Script </td>
   <td>Los formularios HTML5 admiten las API más utilizadas. Para obtener más información, consulte <a href="/help/forms/using/scripting-support.md">compatibilidad con secuencias de comandos</a>.</td>
   <td>Si el archivo PDF se abre dentro de Acrobat o Reader, también admite todas las API de script que proporciona Acrobat.</td>
  </tr>
  <tr>
   <td>Compatibilidad con idiomas de derecha a izquierda </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
