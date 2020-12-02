---
title: Servicio de salida
seo-title: Servicio de salida
description: Describe Output Service, que forma parte de AEM Documento Services
seo-description: Describe Output Service, que forma parte de AEM Documento Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Servicio de salida{#output-service}

## Información general {#overview}

El servicio de salida es un servicio OSGi que forma parte de AEM Documento Services. El servicio Output admite varios formatos de salida y funciones de diseño de salida de AEM Forms Designer. El servicio Output puede convertir plantillas XFA y datos XML para generar documentos de impresión en diversos formatos.

El servicio de salida permite crear aplicaciones que le permiten:

* Genere documentos finales de formulario rellenando archivos de plantilla con datos XML.
* Genere formularios de salida en varios formatos, incluidos los flujos de impresión PDF no interactivos, PostScript, PCL y ZPL.
* Genere archivos PDF impresos a partir de archivos PDF de formulario XFA.
* Genere documentos PDF, PostScript, PCL y ZPL de forma masiva combinando varios conjuntos de datos con las plantillas suministradas.

>[!NOTE]
>
>El servicio de salida es una aplicación de 32 bits. En Microsoft Windows, una aplicación de 32 bits puede utilizar un máximo de 2 GB de memoria. El límite también se aplica al servicio de salida.

## Creación de documentos de formulario no interactivos {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

Normalmente, las plantillas se crean con AEM Forms Designer. Las API `generatePDFOutput` y `generatePrintedOutput` del servicio Output permiten convertir directamente estas plantillas a diversos formatos, incluidos PDF, PostScript, ZPL y PCL.

La operación `generatePDFOutput` genera archivos PDF, mientras que la operación `generatePrintedOutput` genera formatos PostScript, ZPL y PCL. El primer parámetro de ambas operaciones acepta el nombre del archivo de plantilla (por ejemplo, `ExpenseClaim.xdp`) o un objeto de Documento que contiene la plantilla. Cuando especifique el nombre del archivo de plantilla, especifique también la raíz del contenido como la ruta de la carpeta que contiene la plantilla. Puede especificar la raíz del contenido mediante el parámetro `PDFOutputOptions` o el parámetro `PrintedOutputOptions`. Consulte Javadoc para obtener detalles de otras opciones que puede especificar mediante estos parámetros.

El segundo parámetro acepta un documento XML que se combina con la plantilla al generar el documento de salida.

La operación `generatePDFOutput` también puede aceptar un formulario PDF basado en XFA como entrada y devolver una versión no interactiva del formulario PDF como salida.

## Generación de documentos de formulario no interactivos {#generating-non-interactive-form-documents}

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML para cada plantilla.

Utilice las operaciones `generatePDFOutputBatch` y `generatePrintedOutputBatch` del servicio Output para generar un documento de impresión para cada registro.

También puede combinar los registros en un único documento. Ambas operaciones utilizan cuatro parámetros.

El primer parámetro es un mapa que contiene una cadena arbitraria como clave y el nombre del archivo de plantilla como valor.

El segundo parámetro es un mapa diferente cuyo valor es un objeto Documento que contiene datos XML. La clave es la misma que la especificada para el primer parámetro.

El tercer parámetro para `generatePDFOutputBatch` o `generatePrintedOutputBatch` es de tipo `PDFOutputOptions` o `PrintedOutputOptions` respectivamente.

Los tipos de parámetro son los mismos que los tipos de parámetros para las operaciones `generatePDFOutput` y `generatePrintedOutput` y tienen el mismo efecto.

El cuarto parámetro es de tipo `BatchOptions`, que se utiliza para especificar si se puede generar un archivo independiente para cada registro. El valor predeterminado de este parámetro es false.

Tanto `generatePrintedOutputBatch` como `generatePDFOutputBatch` devuelven un valor de tipo `BatchResult`. El valor contiene una lista de documentos generados. También contiene un documento de metadatos en formato XML que contiene información relacionada con cada documento que se genera.
