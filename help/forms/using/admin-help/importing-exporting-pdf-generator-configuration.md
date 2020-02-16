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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importación y exportación de archivos de configuración de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

El archivo de configuración contiene la información de conversión del generador de PDF, incluido el PDF, el tipo de archivo y la configuración de seguridad.

>[!NOTE]
>
>No puede cambiar la configuración de tiempo de espera para el generador de PDF importando un archivo nativo2pdfconfig.xml personalizado. La configuración de tiempo de espera de ese archivo es solo para fines informativos y muestra la configuración actual en el generador de PDF. Para cambiar la configuración de tiempo de espera, consulte &quot;Configuración de los parámetros de rendimiento de PDF Generator&quot; en [Instalación e implementación de formularios](https://www.adobe.com/go/learn_aemforms_installJBoss_63)AEM.

## Exportar el archivo de configuración actual {#export-your-current-configuration-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Para exportar la configuración, seleccione la opción adecuada:

   * Para exportar todos los ajustes con nombre, seleccione Descargar toda la configuración.
   * Para exportar solo una configuración de Adobe PDF, configuración de seguridad o configuración de tipo de archivo, seleccione Descargar configuración mínima.

      Si va a exportar una configuración mínima, seleccione los ajustes de Adobe PDF, seguridad y tipo de archivo que desea exportar.

1. Haga clic en Descargar y guarde el archivo XML en una ubicación adecuada.

## Importar un archivo de configuración {#import-a-configuration-file}

>[!NOTE]
>
>El sistema se reconfigurará según la información del archivo importado.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Importar un archivo de configuración existente.
1. Para especificar la ubicación del archivo en el cuadro Archivo de configuración, haga clic en Examinar para buscar y seleccionar el archivo y, a continuación, haga clic en **Importar**.

## Conversión de todas las capas dentro de los archivos de AutoCAD {#convert-all-layers-within-autocad-files}

De forma predeterminada, PDF Generator convierte sólo la capa predeterminada de los archivos de AutoCAD a PDF en lugar de todas las capas del archivo. Para convertir todas las capas, siga este procedimiento.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Exportar configuración.
1. Seleccione Descargar toda la configuración y haga clic en Descargar.
1. En un editor de texto, abra el archivo descargado y, bajo la `AutoCAD` etiqueta dentro de la `PDFMaker` etiqueta, agregue el texto `convertAllPages="true"`.
1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Importar un archivo de configuración existente, especifique el archivo actualizado y haga clic en Importar.

   Todos los archivos de AutoCAD convertidos mediante el archivo de configuración modificado tendrán convertidas todas las capas.

## Restaure la configuración a la configuración original instalada con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Archivos de configuración > Importar configuración.
1. Seleccione Restaurar configuración a configuración predeterminada y haga clic en Importar.

