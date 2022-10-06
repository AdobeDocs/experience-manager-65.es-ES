---
title: Servicio de salida
seo-title: Output Service
description: Describe Output Service, que forma parte de AEM Document Services
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 10%

---

# Servicio de salida{#output-service}

## Información general {#overview}

El servicio de salida es un servicio OSGi que forma parte de AEM Document Services. El servicio de salida admite varios formatos de salida y funciones de diseño de salida de AEM Forms Designer. El servicio de salida puede convertir plantillas XFA y datos XML para generar documentos de impresión en varios formatos.

El servicio Output le permite crear aplicaciones con las que puede hacer lo siguiente:

* Generar formularios finales al rellenar archivos de plantilla con datos XML.
* Genere formularios de salida en varios formatos, incluidos los flujos de impresión no interactivos PDF, PostScript, PCL y ZPL.
* Generar PDF de impresión a partir de PDF de formularios XFA.
* Genere documentos de PDF, PostScript, PCL y ZPL de forma masiva combinando varios conjuntos de datos con las plantillas proporcionadas.

>[!NOTE]
>
>El servicio de salida es una aplicación de 32 bits. En Microsoft Windows, una aplicación de 32 bits puede utilizar un máximo de 2 GB de memoria. El límite también se aplica al servicio de salida.

## Creación de documentos de formulario no interactivos {#creating-non-interactive-form-documents}

![uso de output_modified](assets/usingoutput_modified.png)

Normalmente, las plantillas se crean mediante AEM Forms Designer. La variable `generatePDFOutput` y `generatePrintedOutput` Las API del servicio Output permiten convertir directamente estas plantillas a varios formatos, incluidos PDF, PostScript, ZPL y PCL.

La variable `generatePDFOutput` la operación genera PDF, mientras que la variable `generatePrintedOutput` genera los formatos PostScript, ZPL y PCL. El primer parámetro de ambas operaciones acepta el nombre del archivo de plantilla (por ejemplo `ExpenseClaim.xdp`) o un objeto Document que contenga la plantilla. Cuando especifique el nombre del archivo de plantilla, especifique también la raíz del contenido como la ruta a la carpeta que contiene la plantilla. Puede especificar la raíz de contenido mediante la variable `PDFOutputOptions` o `PrintedOutputOptions` parámetro. Consulte Javadoc para obtener más información sobre otras opciones que puede especificar mediante estos parámetros.

El segundo parámetro acepta un documento XML que se combina con la plantilla al generar el documento de salida.

La variable `generatePDFOutput` La operación también puede aceptar un formulario de PDF basado en XFA como entrada y devolver una versión no interactiva del formulario de PDF como salida.

## Generación de documentos de formulario no interactivos {#generating-non-interactive-form-documents}

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML en cada plantilla.

Utilice la variable `generatePDFOutputBatch` y `generatePrintedOutputBatch` operaciones del servicio Output para generar un documento de impresión para cada registro.

También puede combinar los registros en un solo documento. Ambas operaciones toman cuatro parámetros.

El primer parámetro es un mapa que contiene una cadena arbitraria como clave y el nombre del archivo de plantilla como valor.

El segundo parámetro es un mapa diferente cuyo valor es un objeto Document que contiene datos XML. La clave es la misma que la especificada para el primer parámetro.

El tercer parámetro de `generatePDFOutputBatch` o `generatePrintedOutputBatch` es de tipo `PDFOutputOptions` o `PrintedOutputOptions` respectivamente.

Los tipos de parámetros son los mismos que los tipos de parámetros para la variable `generatePDFOutput` y `generatePrintedOutput` y tienen el mismo efecto.

El cuarto parámetro es de tipo `BatchOptions`, que se utiliza para especificar si se puede generar un archivo independiente para cada registro. El valor predeterminado de este parámetro es false.

Ambas `generatePrintedOutputBatch` y `generatePDFOutputBatch` devolver un valor de tipo `BatchResult`. El valor contiene una lista de documentos generados. También contiene un documento de metadatos en formato XML que contiene información relacionada con cada documento generado.
