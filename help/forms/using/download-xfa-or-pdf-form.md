---
title: Descargar una plantilla de formulario XFA o PDF
seo-title: Descargar una plantilla de formulario XFA o PDF
description: Puede exportar formularios del repositorio al sistema local y migrar los formularios descargados al nuevo repositorio.
seo-description: Puede exportar formularios del repositorio al sistema local y migrar los formularios descargados al nuevo repositorio.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Descargar una plantilla de formulario XFA o PDF {#download-an-xfa-or-a-pdf-form-template}

La operación de descarga, como su nombre indica, permite exportar formularios del repositorio al sistema local. En combinación con la operación de carga, esta operación le ayuda a migrar los formularios de un repositorio a otro.

En AEM Forms, la operación de descarga es compatible con los siguientes tipos de recursos:

* Plantillas de formulario (XFA Forms)
* PDF forms
* Documentos (archivos PDF planos)

AEM Forms admite la descarga de estos tipos de formularios individualmente o en una carpeta que contenga uno o varios formularios admitidos.

Aparte de estos recursos, puede descargar el tipo `Resource` de recurso si está presente en una carpeta. Esta funcionalidad se proporciona para permitirle descargar el recurso al que hace referencia un formulario XFA junto con el formulario.

## Descargar uno o más formularios {#download-one-or-more-forms}

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.

1. Vaya a la ubicación del recurso que desea descargar.

1. Seleccione el recurso. Haga clic en el icono **[!UICONTROL Descargar]** ![aem6formularios_descargar](assets/aem6forms_download.png) en la barra de herramientas.

   >[!NOTE]
   >
   >Solo puede seleccionar un formulario para la descarga. Si desea descargar varios formularios, debe descargarlos como una carpeta.

1. En el cuadro de diálogo que aparece, haga clic en **[!UICONTROL Descargar]**.

   AEM Forms genera un archivo ZIP que contiene el archivo seleccionado o la carpeta seleccionada.

   Si va a descargar una carpeta, los recursos admitidos dentro de la carpeta se descargarán en la jerarquía existente.

   El archivo ZIP se guarda en la carpeta `Downloads` del sistema.

## Consideraciones relacionadas para la operación de carga {#related-considerations-for-the-upload-operation}

* Puede cargar el archivo ZIP en cualquier otra ubicación del mismo repositorio o en otro repositorio
* La jerarquía de los recursos de una carpeta se conserva durante la operación de carga
* Cualquier cambio de metadatos realizado en los recursos descargados antes de la descarga se refleja en la carga

