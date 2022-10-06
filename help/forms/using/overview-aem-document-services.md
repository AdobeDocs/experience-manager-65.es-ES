---
title: Descripción general de AEM Document Services
seo-title: Overview of AEM Document Services
description: AEM Document Services son un conjunto de OSGi Services para crear, ensamblar y asegurar documentos PDF.
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 1%

---

# Descripción general de AEM Document Services{#overview-of-aem-document-services}

AEM Document Services son un conjunto de OSGi Services para crear, ensamblar y asegurar documentos PDF. Los servicios de documentos contienen los siguientes servicios:

## Servicio de salida {#output-service}

El servicio Output permite crear documentos en diferentes formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Printer Control Language (PCL). La siguiente lista especifica los formatos de impresora de etiquetas:

* Zebra (ZPL)
* Intertypes (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Un documento se puede enviar a una impresora de red, a una impresora local o a un archivo del sistema de archivos. El servicio Output combina los datos de formulario XML con un diseño de formulario para generar un documento. El servicio Output puede generar un documento sin combinar los datos de formulario XML en el documento. Sin embargo, el flujo de trabajo principal es combinar datos en el documento.

>[!NOTE]
>
>Normalmente, un diseño de formulario se crea mediante Designer. Para obtener información sobre la creación de diseños de formulario para el servicio Output, consulte la Ayuda de Designer.

Cuando se utiliza el servicio Output para combinar datos XML con un diseño de formulario, el resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en los campos. Por el contrario, puede utilizar el servicio Forms para crear un formulario de PDF interactivo que permita a los usuarios introducir datos en sus campos.

Las cuatro operaciones de servicio de salida siguientes están disponibles para su uso:

* **generatePDFOuput**: Combina un diseño de formulario con datos para generar un documento de PDF
* **generatePrintedOutput**: Combina un diseño de formulario con datos de formulario para generar un documento que se enviará a un láser o a una impresora de red de etiquetas

* **generatePDFOutputBatch**: Combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de archivos de PDF. También existe la opción de generar un solo PDF combinando todos los PDF
* **generatePrintedOutputBatch**: Combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de documentos de impresión (PS, PCL, ZPL, DPL, IPL, TPCL). También existe la opción de generar un solo documento de impresión.

## Servicio del ensamblador {#assembler-service}

El servicio Assembler permite combinar, reorganizar y aumentar documentos PDF y XDP, así como obtener información sobre documentos PDF. Cada trabajo enviado al servicio Assembler incluye un documento XML de descripción de documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). El documento DDX proporciona instrucciones sobre cómo utilizar los documentos de origen para producir un conjunto de documentos resultantes.

Además de las capacidades mencionadas anteriormente, el servicio Assembler:

* Convierte los documentos PDF en estándar PDF/A.
* Transforma PDF forms, formularios XML (creados en Designer) y PDF forms (creados en Acrobat) a PDF/A-1b, PDF/A-2b y PDFA/A-3b.
* Convierte documentos PDF firmados o no firmados (se requieren firmas digitales).
* Valida la conformidad de un archivo PDF/A y lo convierte si es necesario.

### Acerca de DDX {#about-ddx}

Cuando utilice el servicio Assembler, utilice un lenguaje basado en XML llamado Document Description XML (DDX) para describir la salida que desee. DDX es un lenguaje declarativo de marcado cuyos elementos representan componentes básicos de los documentos. Estos componentes básicos incluyen documentos de PDF, documentos XDP, fragmentos de formulario XDP y otros elementos, como comentarios, marcadores y texto con estilo.

El documento DDX puede especificar documentos resultantes con estas características:

* PDF documento que se monta a partir de varios documentos PDF
* Varios documentos de PDF separados de un solo documento de PDF
* Portfolio del PDF que incluye una interfaz de usuario independiente y varios documentos PDF y no PDF
* Documento XDP montado a partir de varios documentos XDP
* Documento XDP que contiene fragmentos XML insertados dinámicamente en un documento XDP
* PDF documento que empaqueta un documento XDP
* Archivos XML que informan de las características de un documento PDF. Las características de los informes incluyen texto, comentarios, datos de formulario, archivos adjuntos, archivos utilizados en Portfolio de PDF, marcadores y propiedades de PDF. Las propiedades del PDF incluyen propiedades de formulario, rotación de página y autor del documento.

Puede utilizar DDX para aumentar los documentos del PDF como parte del ensamblaje o desmontaje del documento. Puede especificar cualquier combinación de los siguientes efectos:

* Agregue o quite marcas de agua o fondos en páginas seleccionadas.
* Agregue o elimine encabezados y pies de página en páginas seleccionadas.
* Elimina la estructura y las capacidades de navegación de un Portfolio de PDF o paquete de PDF. El resultado es un solo archivo PDF.
* Renumérense las etiquetas de página. Las etiquetas de página generalmente se utilizan para la numeración de páginas.
* Importar metadatos de otro documento de origen.
* Agregue o elimine archivos adjuntos, marcadores, vínculos, comentarios y JavaScript.
* Defina las características de la vista inicial y optimice la visualización en la web.
* Establezca permisos para el PDF cifrado.
* Rotar páginas o rotar y desplazar contenido en páginas.
* Cambie el tamaño de las páginas seleccionadas.
* Combine datos con un PDF basado en XFA.

Puede utilizar un mapa de entrada simple para especificar las ubicaciones de los documentos de origen y los documentos resultantes. También puede utilizar los siguientes tipos de URL de datos externos:

* Archivo
* FTP
* HTTP/HTTPS

## Doc Assurance Service {#doc-assurance-service}

El servicio de control de documentos le ayuda a cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y añadir firmas digitales a sus documentos. Los usuarios pueden interactuar fácilmente con los PDF forms y documentos, mientras que su organización mejora la seguridad, el archiving y el cumplimiento de normas.

El servicio Doc Assurance contiene tres servicios: firma, cifrado y extensión de lector.

### Servicio de firmas {#signature-service}

El servicio Signature le permite trabajar con firmas digitales y documentos en el servidor de AEM. Por ejemplo, el servicio de firma se suele utilizar en las siguientes situaciones:

* El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra con Acrobat o Adobe Reader.
* El servidor de AEM valida una firma que se agregó a un formulario mediante Acrobat o Adobe Reader.
* El servidor de AEM firma un formulario en nombre de un notario público.

El servicio de firma accede a los certificados y credenciales almacenados en el almacén de confianza.

### Servicio de cifrado {#encryption-service}

El servicio Encryption permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Puede cifrar todo el documento del PDF (incluido su contenido, metadatos y archivos adjuntos), todo lo que no sea sus metadatos o solo los archivos adjuntos. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña de apertura antes de que el documento se pueda ver en Adobe Reader o Acrobat. Si un documento de PDF está cifrado con un certificado, el usuario debe descifrar el documento de PDF con una clave privada (certificado). La clave privada utilizada para descifrar el documento del PDF debe corresponder a la clave pública utilizada para cifrarlo.

### Servicio de extensión de Reader {#reader-extension-service}

El servicio de Extensiones de Reader permite a su organización compartir fácilmente documentos de PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio Reader Extensions funciona con Adobe Reader 7.0 o posterior. El servicio agrega derechos de uso a un documento de PDF. Esta acción activa funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Los usuarios de terceros no requieren software ni complementos adicionales para trabajar con documentos habilitados para derechos.

Cuando se agregan los derechos de uso correspondientes a los documentos del PDF, los destinatarios pueden realizar las siguientes actividades desde Adobe Reader:

* Lleve a cabo documentos y formularios PDF en línea o sin conexión, lo que permite a los destinatarios guardar copias localmente para sus registros y mantener intacta la información añadida
* Guarde los documentos del PDF en un disco duro local para conservar el documento original y los comentarios, datos o archivos adjuntos adicionales
* Adjuntar archivos y clips multimedia a documentos del PDF
* Firme, certifique y autentique documentos PDF mediante la aplicación de firmas digitales mediante tecnologías estándar de infraestructura de claves públicas (PKI)
* Enviar documentos de PDF completados o anotados electrónicamente
* Utilizar documentos y formularios PDF como un front-end de desarrollo intuitivo para bases de datos y servicios web internos
* Comparta documentos PDF con otros para que los revisores puedan agregar comentarios mediante herramientas de marcado intuitivas. Estas herramientas incluyen notas adhesivas electrónicas, sellos, resaltados y tachado de texto. Las mismas funciones están disponibles en Acrobat.
* Admite la descodificación de formularios con códigos de barras.

Estas funciones especiales del usuario se activan automáticamente cuando se abre un documento PDF con derechos activados en Adobe Reader. Cuando el usuario ha terminado de trabajar con un documento con derechos activados, esas funciones se desactivan de nuevo en Adobe Reader. Permanecen deshabilitados hasta que el usuario reciba otro documento de PDF con derechos activados.

De serie, el servicio DocAssurance no está disponible para su uso. Para configurar el servicio DocAssurance, consulte [Instalación y configuración de servicios de documentos](../../forms/using/install-configure-document-services.md).

## Enviar al servicio de impresora {#send-to-printer-service}

Send To Printer Service proporciona API para enviar documentos a una impresora especificada para su impresión.
