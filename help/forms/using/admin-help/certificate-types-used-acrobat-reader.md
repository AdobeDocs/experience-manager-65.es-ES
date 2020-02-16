---
title: Tipos de certificados utilizados por las extensiones de Acrobat Reader DC
seo-title: Tipos de certificados utilizados por las extensiones de Acrobat Reader DC
description: Obtenga información sobre los tipos de certificados que utilizan las extensiones de Acrobat Reader DC.
seo-description: Obtenga información sobre los tipos de certificados que utilizan las extensiones de Acrobat Reader DC.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Tipos de certificados utilizados por las extensiones de Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

El visor de certificados proporciona la siguiente información sobre el certificado:

* Nombre &quot;práctico&quot; del certificado
* Perfiles de certificado
* Período de validez
* Derechos de uso de extensiones de Acrobat Reader DC

## Nombre &quot;práctico&quot; del certificado {#certificate-friendly-name}

El nombre &quot;práctico&quot; de un certificado de extensiones de Acrobat Reader DC es una cadena que describe las propiedades del certificado, como en el siguiente ejemplo:

ARE 2D Barcode Full Production V6.1 P8 0002054

La cadena contiene los siguientes elementos:

**** Tipo de certificado: Describe los módulos de formularios de AEM que activa el certificado y el nivel de activación, como, por ejemplo, ARE 2D Barcode Full. Para obtener una lista de los tipos de certificado disponibles, consulte la columna Tipo en la tabla de la sección Perfiles de certificado.

**** Tipo de implementación: Indica el uso previsto del certificado, como Producción. El valor puede ser Evaluación o Producción. Para obtener una lista de los tipos de implementación asociados con cada tipo de certificado, consulte la columna Tipo de implementación en la tabla de la sección Perfiles de certificado.

**** Versión de derechos de uso: Describe la versión del algoritmo de derechos de uso para el que se puede utilizar el certificado, como V6.1. Esta versión no significa la versión de las extensiones de Acrobat o Acrobat Reader DC.

**** Código de perfil: El código de perfil es una descripción breve de las propiedades completas del certificado, como P8. Para obtener una lista de los códigos de perfil asociados a cada tipo de archivo, consulte la columna Código de perfil en la tabla de la sección Perfiles de certificado.

**** Número de serie: Se asigna un número de serie a cada certificado emitido por Adobe, como 0002054. La asistencia técnica para empresas de Adobe o un representante de cuentas de Adobe Enterprise pueden utilizar este número de serie para rastrear el certificado en un pedido de producto específico o en una relación con OEM.

## Perfiles de certificado {#certificate-profiles}

En la tabla siguiente se muestran los perfiles de certificado que puede encontrar al analizar los certificados de extensiones de Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Código de perfil</p></th>
   <th><p>Tipo</p></th>
   <th><p>Período de validez</p></th>
   <th><p>Tipo de implementación</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>Producción de SAP</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>Prueba interna de SAP</p></td>
   <td><p>2 años</p></td>
   <td><p>Evaluación y ensayo</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensiones de Acrobat Reader DC, producción</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensiones de Acrobat Reader DC, uso interno de Adobe</p></td>
   <td><p>2 años</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensiones de Acrobat Reader DC, integración de socios</p></td>
   <td><p>2 años</p></td>
   <td><p>Evaluación y ensayo</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensiones de Acrobat Reader DC, evaluación</p></td>
   <td><p>60 días</p></td>
   <td><p>Evaluación</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Formularios, producción</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, Producción</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Formularios; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Formularios; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Firma solamente; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Comentarios sin conexión solamente; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Sólo comentarios; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Permisos completos; puede ser utilizado por OEM</p></td>
   <td><p>Máximo</p></td>
   <td><p>Producción y evaluación</p></td>
  </tr>
 </tbody>
</table>

## Período de validez {#validity-period}

Los certificados de evaluación se emiten a clientes y desarrolladores para que puedan evaluar y desarrollar aplicaciones de muestra para productos. El período de validez de estos certificados es de entre 60 y 90 días. Expiran al final del segundo mes siguiente a los datos de emisión.

Los certificados de integración de socios se entregan a los socios comerciales de Adobe para apoyar el desarrollo, la integración, la creación de prototipos y la demostración de software. Estos certificados son válidos durante dos años a partir de la fecha de expedición.

Los certificados de uso interno de Adobe se utilizan en Adobe para admitir el desarrollo, la integración, la creación de prototipos y la demostración de software. Estos certificados son válidos durante dos años a partir de la fecha de expedición.

Los certificados de producción se emiten a los clientes que compraron extensiones de Acrobat Reader DC. Estos certificados son válidos durante el período máximo permitido por la autoridad de certificación (CA), que se muestra como *Máx* en la tabla Perfiles de certificados.

## Derechos de uso de extensiones de Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Al examinar el certificado de extensiones de Acrobat Reader DC en el visor de certificados, puede seleccionar el elemento de derechos de uso en la ficha Detalles (si está configurado) para ver una lista detallada de los derechos de uso de Adobe Reader que el certificado puede habilitar. Los derechos de uso activados en un documento determinado pueden ser un subconjunto de los activados por el certificado.

Si se requieren comentarios en línea en un entorno que no sea de colaboración, póngase en contacto con el servicio de asistencia técnica de Adobe para obtener más información. La propiedad Mode coincide con el tipo de implementación y es *de producción* o *evaluación*.

Los derechos de uso de extensiones de Acrobat Reader DC permitidos constan de uno o más elementos específicos. Estos elementos se utilizan en diferentes combinaciones para lograr variedades de funcionalidad de productos con licencia.

<table>
 <thead>
  <tr>
   <th><p>Elemento Derechos de uso</p></th>
   <th><p>Capacidad habilitada en Adobe Reader al visualizar un documento PDF con derechos activados</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Rellene los campos del formulario y guarde los archivos localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importe y exporte datos de formulario como archivos FDF, XFDF, XML y XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Agregue, cambie o elimine campos y propiedades de campo en el formulario PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Enviar datos, por correo electrónico o sin conexión, a un servidor cuando no se esté ejecutando en una sesión del explorador.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Cree páginas a partir de páginas de plantilla dentro del mismo formulario PDF.</p></td>
  </tr>
  <tr>
   <td><p>Firma</p></td>
   <td><p>Firma y guarda digitalmente documentos PDF y borra firmas digitales.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Cree y modifique anotaciones de documento como comentarios.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Guarde anotaciones como comentarios en un archivo de datos independiente y cargue comentarios desde un archivo.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Imprima un documento con códigos de barras de datos de formulario en un formulario sin cifrar que no requiera software de servidor con licencia para descodificar.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Cargue y descargue anotaciones, como comentarios, en un servidor de comentarios y revisión de documentos en línea.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Conéctese a servicios Web o bases de datos que estén definidos en un formulario PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifique los objetos de archivo incrustados asociados al documento PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los derechos de uso de las extensiones de Acrobat Reader DC solo se pueden licenciar desde Adobe en determinadas combinaciones que funcionan juntas. No es posible licenciar estas capacidades de forma independiente. Para obtener información sobre las combinaciones disponibles de derechos de uso, póngase en contacto con un representante de cuentas de formularios de AEM.

