---
title: Importación y exportación de archivos de configuración de PDF Generator
seo-title: Importación y exportación de archivos de configuración de PDF Generator
description: Obtenga información sobre cómo importar y exportar archivos de configuración de PDF Generator.
seo-description: Obtenga información sobre cómo importar y exportar archivos de configuración de PDF Generator.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: Generador de PDF
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Importación y exportación de archivos de configuración de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

El archivo de configuración contiene la información de conversión del Generador de PDF, que incluye el PDF, el tipo de archivo y la configuración de seguridad.

>[!NOTE]
>
>No puede cambiar la configuración de tiempo de espera para PDF Generator mediante la importación de un archivo nativo2pdfconfig.xml personalizado. La configuración de tiempo de espera de ese archivo es solo para fines informativos y muestra la configuración actual en PDF Generator. Para cambiar la configuración de tiempo de espera, consulte &quot;Configuración de los parámetros de rendimiento del generador de PDF&quot; en [Instalación e implementación de AEM formularios](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Exporte el archivo de configuración actual {#export-your-current-configuration-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Para exportar la configuración, seleccione la opción adecuada:

   * Para exportar todos los ajustes asignados, seleccione Descargar toda la configuración.
   * Para exportar solo una configuración de Adobe PDF, configuración de seguridad o configuración de tipo de archivo, seleccione Descargar configuración mínima.

      Si va a exportar una configuración mínima, seleccione la configuración de Adobe PDF, seguridad y tipo de archivo que desea exportar.

1. Haga clic en Descargar y guarde el archivo XML en una ubicación adecuada.

## Importar un archivo de configuración {#import-a-configuration-file}

>[!NOTE]
>
>El sistema se reconfigurará según la información del archivo importado.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Importar Un Archivo De Configuración Existente.
1. Para especificar la ubicación del archivo en el cuadro Archivo de configuración, haga clic en Examinar para buscar y seleccionar el archivo y, a continuación, haga clic en **Importar**.

## Conversión de todas las capas dentro de archivos de AutoCAD {#convert-all-layers-within-autocad-files}

De forma predeterminada, PDF Generator convierte sólo la capa predeterminada de los archivos de AutoCAD a PDF en lugar de todas las capas dentro del archivo. Para convertir todas las capas, siga este procedimiento.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Seleccione Descargar toda la configuración y haga clic en Descargar.
1. En un editor de texto, abra el archivo descargado y, en la etiqueta `AutoCAD` dentro de la etiqueta `PDFMaker`, añada el texto `convertAllPages="true"`.
1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Importar un archivo de configuración existente, especifique el archivo actualizado y haga clic en Importar.

   Todos los archivos de AutoCAD convertidos utilizando el fichero de configuración modificado tendrán todas las capas convertidas.

## Restablezca la configuración a la configuración original instalada con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Restablecer configuración a configuración predeterminada y haga clic en Importar.

