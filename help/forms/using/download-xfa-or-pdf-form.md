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
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Descargar una plantilla de formulario XFA o PDF {#download-an-xfa-or-a-pdf-form-template}

La operación de descarga, como su nombre indica, permite exportar formularios desde el repositorio al sistema local. En combinación con la operación de carga, esta operación le ayuda a migrar los formularios de un repositorio a otro.

En AEM Forms, la operación de descarga es compatible con los siguientes tipos de recursos:

* Plantillas de formulario (XFA Forms)
* PDF forms
* Documentos (archivos PDF planos)

AEM Forms admite la descarga de estos tipos de formulario de forma individual o en una carpeta que contenga uno o varios formularios admitidos.

Además de estos recursos, puede descargar el tipo de recurso `Resource` si está presente en una carpeta. Esta funcionalidad se proporciona para permitirle descargar el recurso al que hace referencia un formulario XFA junto con el formulario.

## Descargar uno o varios formularios {#download-one-or-more-forms}

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.

1. Navegue a la ubicación del recurso que desee descargar.

1. Seleccione el recurso. Haga clic en el icono **[!UICONTROL Download]** ![aem6forms_download](assets/aem6forms_download.png) de la barra de herramientas.

   >[!NOTE]
   >
   >Solo puede seleccionar un formulario para descargarlo. Si desea descargar varios formularios, debe descargarlos como una carpeta.

1. En el cuadro de diálogo que aparece, haga clic en **[!UICONTROL Descargar]**.

   AEM Forms genera un archivo ZIP que contiene el archivo seleccionado o la carpeta seleccionada.

   Si descarga una carpeta, los recursos admitidos dentro de la carpeta se descargarán en su jerarquía existente.

   El archivo ZIP se guarda en la carpeta `Downloads` del sistema.

## Consideraciones relacionadas con la operación de carga {#related-considerations-for-the-upload-operation}

* Puede cargar el archivo ZIP en cualquier otra ubicación del mismo repositorio u otro repositorio
* La jerarquía de los recursos de una carpeta se conserva durante la operación de carga
* Cualquier cambio de metadatos realizado en los recursos descargados antes de la descarga se refleja en la carga
