---
title: Visión general de AEM servicios de Documento
seo-title: Visión general de AEM servicios de Documento
description: Los servicios de Documento de AEM son un conjunto de servicios de OSGi para crear, montar y asegurar Documentos PDF.
seo-description: Los servicios de Documento de AEM son un conjunto de servicios de OSGi para crear, montar y asegurar Documentos PDF.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# Información general sobre AEM servicios de Documento{#overview-of-aem-document-services}

Los servicios de Documento de AEM son un conjunto de servicios de OSGi para crear, montar y asegurar Documentos PDF. Los servicios de documento contienen los siguientes servicios:

## Servicio de salida {#output-service}

El servicio Output permite crear documentos en diferentes formatos, incluidos PDF, formatos de impresora láser y formatos de impresora de etiquetas. Los formatos de impresora láser son PostScript y Printer Control Language (PCL). La siguiente lista especifica los formatos de impresora de etiquetas:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TechToshiba (TPCL)

Se puede enviar un documento a una impresora de red, una impresora local o un archivo del sistema de archivos. El servicio Output combina los datos de formulario XML con un diseño de formulario para generar un documento. El servicio Output puede generar un documento sin combinar datos de formulario XML en el documento. Sin embargo, el flujo de trabajo principal consiste en combinar datos en el documento.

>[!NOTE]
>
>Normalmente, un diseño de formulario se crea con Designer. Para obtener información sobre la creación de diseños de formulario para el servicio Output, consulte la Ayuda de Designer.

Al utilizar el servicio Output para combinar datos XML con un diseño de formulario, el resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en sus campos. Por el contrario, puede utilizar el servicio Forms para crear un formulario PDF interactivo que permita a los usuarios introducir datos en sus campos.

Están disponibles para su uso las cuatro operaciones de servicio de salida siguientes:

* **generatePDFOuput**: Combina un diseño de formulario con datos para generar un documento PDF
* **generatePrintedOutput**: Combina un diseño de formulario con datos de formulario para generar un documento para enviarlo a una impresora láser o a una impresora de red de etiquetas

* **generatePDFOutputBatch**: Combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de archivos PDF. También existe la opción de generar un solo PDF combinando todos los archivos PDF
* **generatePrintedOutputBatch**: Combina varias plantillas con varios registros de datos en una sola invocación para generar un lote de documentos de impresión (PS,PCL,ZPL,DPL,IPL,TPCL). También existe la opción de generar un solo documento de impresión.

## Servicio del ensamblador {#assembler-service}

El servicio Ensamblador le permite combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF. Cada trabajo enviado al servicio de ensamblador incluye un documento XML de descripción de Documento (DDX), documentos de origen y recursos externos (cadenas y gráficos). El documento DDX proporciona instrucciones sobre cómo utilizar los documentos de origen para producir un conjunto de documentos resultantes.

Aparte de las capacidades mencionadas, el servicio de ensamblador:

* Convierte documentos PDF a PDF/A estándar.
* Transforma PDF forms, formularios XML (creados en Designer) y PDF forms (creados en Acrobat) a PDF/A-1b, PDF/A-2b y PDF/A-3b.
* Convierte documentos PDF firmados o sin firmar (se requieren firmas digitales).
* Valida la compatibilidad de un archivo PDF/A y lo convierte si es necesario.

### Acerca de DDX {#about-ddx}

Cuando utilice el servicio Ensamblador, utilice un lenguaje basado en XML denominado XML de descripción de Documento (DDX) para describir la salida que desee. DDX es un lenguaje de marcado declarativo cuyos elementos representan los componentes básicos de los documentos. Estos bloques de creación incluyen documentos PDF, documentos XDP, fragmentos de formulario XDP y otros elementos como comentarios, marcadores y texto con estilo.

El documento DDX puede especificar documentos resultantes con estas características:

* DOCUMENTO PDF que se monta a partir de varios documentos PDF
* Varios documentos PDF que se separan de un solo documento PDF
* Portfolio PDF que incluye una interfaz de usuario independiente y varios documentos PDF y no PDF
* Documento XDP montado a partir de varios documentos XDP
* Documento XDP que contiene fragmentos XML insertados dinámicamente en un documento XDP
* DOCUMENTO PDF que empaqueta un documento XDP
* Archivos XML que informan sobre las características de un documento PDF. Las características de los informes incluyen texto, comentarios, datos de formulario, archivos adjuntos, archivos utilizados en Portfolio PDF, marcadores y propiedades PDF. Las propiedades PDF incluyen propiedades de formulario, rotación de página y autor de documento.

Puede utilizar DDX para aumentar los documentos PDF como parte del ensamblado o desmontaje de documento. Puede especificar cualquier combinación de los siguientes efectos:

* Añada o elimine marcas de agua o fondos en las páginas seleccionadas.
* Añada o elimine encabezados y pies de página en las páginas seleccionadas.
* Elimina la estructura y las funciones de navegación de un paquete PDF o Portfolio PDF. El resultado es un solo archivo PDF.
* Volver a numerar etiquetas de página. Las etiquetas de página generalmente se utilizan para la numeración de páginas.
* Importar metadatos desde otro documento de origen.
* Añada o elimine archivos adjuntos, marcadores, vínculos, comentarios y JavaScript.
* Configure las características de vista iniciales y optimice su visualización en la Web.
* Configure permisos para archivos PDF cifrados.
* Rotar páginas o rotar y desplazar contenido en páginas.
* Cambiar el tamaño de las páginas seleccionadas.
* Combina datos con un PDF basado en XFA.

Puede utilizar un mapa de entrada sencillo para especificar las ubicaciones de los documentos de origen y de origen. También puede utilizar los siguientes tipos de URL de datos externos:

* Archivo
* FTP
* HTTP/HTTPS

## Doc Assurance Service {#doc-assurance-service}

El servicio Doc Assurance le ayuda a cifrar y descifrar documentos, ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales y agregar firmas digitales a sus documentos. Los usuarios pueden interactuar fácilmente con PDF forms y documentos, mientras que su organización mejora la seguridad, el archiving y el cumplimiento de normas.

El servicio Doc Assurance contiene tres servicios: firma, cifrado y extensión de lector.

### Servicio de firma {#signature-service}

El servicio Signature le permite trabajar con firmas digitales y documentos en el servidor de AEM. Por ejemplo, el servicio Signature se suele utilizar en las siguientes situaciones:

* El servidor de AEM certifica un formulario antes de enviarlo a un usuario para que lo abra mediante Acrobat o Adobe Reader.
* El servidor de AEM valida una firma que se agregó a un formulario mediante Acrobat o Adobe Reader.
* El servidor de AEM firma un formulario en nombre de un notario público.

El servicio Signature accede a los certificados y las credenciales almacenados en el almacén de confianza.

### Servicio de cifrado {#encryption-service}

El servicio Cifrado le permite cifrar y descifrar documentos. Cuando se cifra un documento, su contenido se vuelve ilegible. Puede cifrar todo el documento PDF (incluido su contenido, metadatos y archivos adjuntos), todo lo que no sea sus metadatos o solo los archivos adjuntos. Un usuario autorizado puede descifrar el documento para obtener acceso a su contenido. Si un documento PDF está cifrado con una contraseña, el usuario debe especificar la contraseña abierta para que el documento se pueda ver en Adobe Reader o Acrobat. Si un documento PDF está cifrado con un certificado, el usuario debe descifrar el documento PDF con una clave privada (certificado). La clave privada utilizada para descifrar el documento PDF debe corresponder a la clave pública utilizada para cifrarlo.

### Servicio de extensión de Reader {#reader-extension-service}

El servicio Extensiones de Reader permite a su organización compartir fácilmente documentos PDF interactivos al ampliar la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio Reader Extensions funciona con Adobe Reader 7.0 o posterior. El servicio agrega derechos de uso a un documento PDF. Esta acción activa funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Los usuarios de terceros no necesitan software o complementos adicionales para trabajar con documentos habilitados para derechos.

Cuando se agregan los derechos de uso correspondientes a los documentos PDF, los destinatarios pueden realizar las siguientes actividades desde Adobe Reader:

* Rellene los documentos y formularios PDF en línea o sin conexión, lo que permite a los destinatarios guardar copias localmente para sus registros y mantener intacta la información agregada
* Guardar documentos PDF en una unidad de disco duro local para conservar el documento original y los comentarios, datos o archivos adjuntos adicionales
* Adjuntar archivos y clips multimedia a documentos PDF
* Firmar, certificar y autenticar documentos PDF mediante la aplicación de firmas digitales mediante tecnologías de infraestructura de clave pública (PKI) estándar del sector
* Enviar documentos PDF completados o anotados electrónicamente
* Utilice los documentos y formularios PDF como un front-end de desarrollo intuitivo para las bases de datos internas y los servicios Web
* Comparta documentos PDF con otros para que los revisores puedan añadir comentarios mediante herramientas de marcado intuitivas. Estas herramientas incluyen notas adhesivas electrónicas, sellos, resaltados y tachado de texto. Las mismas funciones están disponibles en Acrobat.
* Admitir la descodificación de formularios con códigos de barras.

Estas funciones especiales de usuario se activan automáticamente cuando se abre un documento PDF con derechos activados en Adobe Reader. Cuando el usuario ha terminado de trabajar con un documento con derechos activados, estas funciones se desactivan de nuevo en Adobe Reader. Permanecen desactivados hasta que el usuario recibe otro documento PDF con derechos activados.

De forma predeterminada, el servicio DocAssurance no está disponible para su uso. Para configurar el servicio DocAssurance, consulte [Instalación y configuración de los servicios de Documento](../../forms/using/install-configure-document-services.md).

## Enviar al servicio de impresión {#send-to-printer-service}

Send To Printer Service proporciona API para enviar documentos a la impresora especificada para la impresión.
