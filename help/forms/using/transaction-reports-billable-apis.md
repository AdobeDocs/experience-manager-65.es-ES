---
title: Informes de transacciones API facturables
seo-title: Informes de transacciones API facturables
description: Lista de todas las API que se contabilizan como transacciones
seo-description: Lista de todas las API que se contabilizan como transacciones
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Informes de transacciones API facturables{#transaction-reports-billable-apis}

AEM Forms proporciona varias API para enviar formularios, procesar documentos y procesar documentos. Algunas API se contabilizan como transacciones y otras son libres de usar. Este documento proporciona una lista de todas las API que se contabilizan como transacciones en un informe de transacciones. Estos son algunos casos comunes en los que se utiliza una API facturable:

* Envío de un formulario adaptable, un formulario HTML5 y un conjunto de formularios
* Representación de una versión impresa o web de una comunicación interactiva
* Conversión de un documento de un formato a otro
* Acoplamiento de un documento PDF dinámico
* Generación de un documento de registro
* Combinación de un documento PDF interactivo con otro documento PDF
* Uso del paso de tareas de asignación y los pasos de servicios de documentación de los flujos de trabajo de AEM
* Uso de formularios adaptables en formularios adaptables

Las API de facturación no tienen en cuenta el número de páginas, la longitud de un documento o formulario o el formato final del documento procesado. Un informe de transacciones divide las transacciones en dos categorías: Documentos procesados y formularios enviados.

* **** Formularios enviados: Cuando los datos se envían desde cualquier tipo de formulario creado con AEM Forms y los datos se envían a cualquier repositorio de almacenamiento de datos o base de datos, se considera el envío del formulario. Por ejemplo, el envío de un formulario adaptable, formulario HTML5, formulario PDF y conjunto de formularios se contabilizan como formularios enviados. Cada formulario de un conjunto de formularios se considera un envío. Por ejemplo, si un conjunto de formularios tiene 5 formularios, cuando se envía el conjunto, el servicio de informes de transacciones lo cuenta como 5 envíos.

* **** Documentos procesados: La generación de un documento mediante la combinación de una plantilla y datos, la firma o certificación digitales de un documento, el uso de una API de servicios de documentos facturables para document services o la conversión de un documento de un formato a otro se contabilizan como documentos procesados.

>[!NOTE]
>
>La interfaz de usuario de informes de transacciones muestra tres categorías: Formularios enviados, documentos procesados y documentos procesados. Tanto los documentos procesados como los documentos procesados se contabilizan como documentos procesados.

## API de Document Services facturables {#billable-document-services-apis}

### Generar servicio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Crea archivos PDF de Adobe a partir de tipos de archivo admitidos.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea archivos PDF de Adobe a partir de tipos de archivo admitidos.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Convierte Adobe PDF en tipos de archivo admitidos. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Convierte Adobe PDF en tipos de archivo admitidos. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Convierte Adobe PDF en tipos de archivo admitidos. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crea archivos PDF a partir de páginas HTML.</p> </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crea archivos PDF a partir de direcciones URL que apuntan a una página HTML.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crea archivos PDF a partir de direcciones URL que apuntan a una página HTML.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizarPDF</a></td>
   <td>Optimiza el PDF para reducir el tamaño del archivo eliminando metadatos innecesarios sin afectar a la calidad.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Crea archivos PDF de Adobe a partir de tipos de archivo admitidos.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea archivos PDF de Adobe a partir de tipos de archivo admitidos.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Documento de servicio de registro (servicio DoR) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">procesar</a></td>
   <td>Invoca el método de procesamiento especificado para generar un documento de registro utilizando los parámetros proporcionados.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servicio de salida {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Combina datos y plantillas para crear un conjunto de documentos PDF.</td>
   <td>Documentos procesados</td>
   <td> La API generatePDFOutputBatch combina una plantilla de formulario con un registro y genera un PDF. Al procesar un lote de registros, el servicio de informes de transacciones cuenta cada registro como una representación en PDF independiente. <br> Puede utilizar el indicador <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> para combinar varias representaciones en un único archivo PDF. Independientemente del estado del indicador, el servicio cuenta cada registro como una representación PDF independiente. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convierte documentos XDP y PDF a formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convierte documentos XDP y PDF a formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Convierte un conjunto de documentos XDP y PDF en un conjunto de formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> La API generatePDFOutputBatch combina una plantilla de formulario con un registro y genera un PDF. Al procesar un lote de registros, el servicio de informes de transacciones cuenta cada registro como una representación en PDF independiente. <br> Puede utilizar el indicador <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> para combinar varias representaciones en un único archivo PDF. Independientemente del estado del indicador, el servicio cuenta cada registro como una representación PDF independiente. </td>
  </tr>
 </tbody>
</table>

### Servicio de Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">procesarPDFForm</a></td>
   <td>Procesa el formulario PDF a partir de plantillas XDP. Las plantillas XP se crean en Forms Designer.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extrae datos de un formulario PDF o plantillas XDP</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Convertir servicio PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Convierte un documento PDF en una lista de documentos de imagen. Los formatos de imagen admitidos son JPEG, JPEG2K, PNG y TIFF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Convierte un archivo PDF plano al formato PostScript mediante las opciones especificadas en la especificación de opciones.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Descodifica todos los códigos de barras de un objeto Document y devuelve un objeto org.w3c.dom.Document que contiene datos recuperados del código de barras.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servicio del ensamblador {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invoke</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">EnsemblerResult</a> que contiene los documentos resultantes. </td>
   <td>Documentos procesados</td>
   <td>Las siguientes operaciones no se contabilizan como transacciones:
    <ul>
     <li>Creación de paquetes o portafolios</li>
     <li>Definición de varios XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invoke</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">EnsemblerResult</a> que contiene los documentos resultantes. </td>
   <td>Documentos procesados</td>
   <td>Todos los formatos de archivo de entrada compatibles con PDF Generator, Forms y Output, el servicio Ensamblador admite todos esos formatos como formatos de archivo de salida. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convierta un documento especificado a PDF/A con las opciones especificadas.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* La API de invocación del servicio de ensamblador puede llamar internamente a una API facturable de otro servicio en función de la entrada. Por lo tanto, la API de invocación se puede contabilizar como ninguna, una o varias transacciones. El número de transacciones contabilizadas depende de la entrada y de las API internas invocadas.
>* Un solo documento PDF producido mediante el servicio de ensamblador se puede contabilizar como ninguna, una sola o varias transacciones. El número de transacciones contabilizadas depende del código DDX suministrado.
>



### Servicio de utilidades de PDF {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Convierte un documento PDF en un archivo XDP. Para que un documento PDF se convierta correctamente en un archivo XDP, el documento PDF debe contener una secuencia XFA en el diccionario AcroForm.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API de captura de datos facturables {#billable-data-capture-apis}

Todos los sucesos de envío de formularios adaptables, formularios HTML5 y conjuntos de formularios se contabilizan como transacciones. De forma predeterminada, el envío de un formulario PDF no se contabiliza como una transacción. Utilice la API [de grabador de](transaction-reports-billable-apis.md#recordingbillableapisastransactionsforcustomcode) transacciones proporcionada para registrar un envío de formulario PDF como transacción.

### Formularios adaptables {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Envío de un formulario adaptable</td>
   <td>Envía un formulario adaptable a la acción de envío configurada. </td>
   <td>Formularios enviados</td>
   <td>
    <ul>
     <li>Cuenta de envíos correcta para una o dos transacciones. El número de transacciones contabilizadas depende del tipo de acción de envío utilizada para el envío. Por ejemplo, enviar archivos PDF a través de una acción de envío por correo electrónico tiene en cuenta dos recuentos de transacciones. Una transacción para el envío del formulario y otra para PDF generada mediante el servicio Documento de registro (DOR). </li>
     <li>El uso del formulario adaptable dentro de un formulario adaptable (conjunto de formularios adaptables) solo cuenta una transacción. Puede tener cualquier número de formularios adaptables dentro de un formulario adaptable.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Descripción </td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Envío de un formulario HTML5</td>
   <td>Envía un formulario HTML5 para enviar la URL configurada en el formulario.</td>
   <td>Formularios enviados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Conjunto de formularios {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Envío de un conjunto de formularios</td>
   <td>Envía el conjunto de formularios a la URL de envío configurada en el conjunto de formularios.</td>
   <td>Formularios enviados</td>
   <td>
    <ul>
     <li>El uso del formulario adaptable dentro de un formulario adaptable (conjunto de formularios adaptables) solo cuenta una transacción. Puede tener cualquier número de formularios adaptables dentro de un formulario adaptable.</li>
     <li>Cada formulario de un conjunto de formularios HTML5 Forms se cuenta como una transacción independiente. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en formularios y comunicación interactiva facturable en las API de OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Asigne pasos de tareas y servicios de documentos de flujos de trabajo de AEM centrados en formularios en OSGi y todas las representaciones de comunicación interactiva y se contabilizan como transacciones. La vista previa de una comunicación interactiva en la instancia de autor y la vista previa en la instancia de publicación mediante la interfaz de usuario del agente no se contabilizan como transacciones. Si un paso de workflow registra una transacción y el flujo de trabajo no se completa, el recuento de transacciones no se invierte.

### Comunicación interactiva - Canal web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Representación de un canal web</td>
   <td>Abre la versión web de una comunicación interactiva.</td>
   <td>Documentos procesados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">procesar</a> (convertir a PDF)</td>
   <td>Genera la versión PDF de una comunicación interactiva.</td>
   <td>Documentos procesados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Flujos de trabajo de AEM centrados en formularios en OSGi {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoría del informe de transacciones</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Envío de un paso Asignar Tarea</td>
   <td>Formularios enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envío de un punto de inicio de aplicación de flujo de trabajo </td>
   <td>Formularios enviados</td>
   <td> </td>
  </tr>
  <tr>
   <td>Envío de una comunicación interactiva (canal de impresión) desde la interfaz de usuario del agente a un flujo de trabajo</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registro de API facturables como transacciones para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Las acciones como enviar un formulario PDF, utilizar la interfaz de usuario del agente para obtener una vista previa de una comunicación interactiva, utilizar un envío de formulario no estándar y las implementaciones personalizadas no se contabilizan como transacciones. AEM Forms proporciona una API para registrar acciones como transacciones. Puede llamar a la API desde sus implementaciones personalizadas para [registrar una transacción](/help/forms/using/record-transaction-custom-implementation.md).

## Artículos relacionados {#related-articles}

* [Información general sobre los informes de transacciones](../../forms/using/transaction-reports-overview.md)
* [Visualización y comprensión de los informes de transacciones](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrar una transacción para implementaciones personalizadas](/help/forms/using/record-transaction-custom-implementation.md)

