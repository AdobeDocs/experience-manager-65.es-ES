---
title: Importar y exportar archivos de configuración del generador de PDF
seo-title: Importing and exporting PDF Generator configuration files
description: Obtenga información sobre cómo importar y exportar archivos de configuración de PDF Generator.
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 5%

---

# Importar y exportar archivos de configuración del generador de PDF {#importing-and-exporting-pdf-generator-configuration-files}

El archivo de configuración contiene la información de conversión de PDF Generator, incluido el PDF, el tipo de archivo y la configuración de seguridad.

>[!NOTE]
>
>No puede cambiar la configuración de tiempo de espera para PDF Generator importando un archivo native2pdfconfig.xml personalizado. La configuración de tiempo de espera de ese archivo es solo informativa y muestra la configuración actual en PDF Generator. Para cambiar la configuración de tiempo de espera, consulte &quot;Configuración de los parámetros de rendimiento del PDF Generator&quot; en [AEM Instalación e implementación de formularios](https://www.adobe.com/go/learn_aemforms_installJBoss_63_es).

## Exportar el archivo de configuración actual {#export-your-current-configuration-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Para exportar la configuración, seleccione la opción adecuada:

   * Para exportar todas las configuraciones con nombre, seleccione Descargar configuración completa.
   * Para exportar solo una configuración de Adobe PDF, de seguridad o de tipo de archivo, seleccione Descargar configuración mínima.

      Si va a exportar una configuración mínima, seleccione la configuración de Adobe PDF, seguridad y tipo de archivo que desea exportar.

1. Haga clic en Descargar y guarde el archivo XML en una ubicación adecuada.

## Importar un archivo de configuración {#import-a-configuration-file}

>[!NOTE]
>
>El sistema se volverá a configurar según la información contenida en el archivo importado.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Import An Existing Configuration File.
1. Para especificar la ubicación del archivo en el cuadro Archivo de configuración, haga clic en Examinar para buscar y seleccionar el archivo y, a continuación, haga clic en **Importar**.

## Convertir todas las capas de los archivos de AutoCAD {#convert-all-layers-within-autocad-files}

De forma predeterminada, PDF Generator convierte sólo la capa predeterminada de archivos de AutoCAD en PDF, en lugar de todas las capas del archivo. Para convertir todas las capas, siga este procedimiento.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Seleccione Descargar configuración completa y haga clic en Descargar.
1. En un editor de texto, abra el archivo descargado y, en `AutoCAD` dentro de la `PDFMaker` , añada el texto `convertAllPages="true"`.
1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Importar un archivo de configuración existente, especifique el archivo actualizado y haga clic en Importar.

   Todos los archivos de AutoCAD que se conviertan mediante el fichero de configuración modificado tendrán convertidas todas las capas.

## Restablezca la configuración a la configuración original instalada con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Restablecer configuración a la configuración predeterminada y haga clic en Importar.
