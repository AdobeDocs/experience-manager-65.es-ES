---
title: Configurar restricciones de carga de recursos
description: 'Restringir el tipo de recursos (archivos) que los usuarios pueden cargar '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# Configurar restricciones de carga de recursos {#configuring-asset-upload-restrictions}

Puede configurar [!DNL Adobe Experience Manager Assets] para restringir el tipo de recursos que los usuarios pueden cargar. Ayuda a evitar cargas accidentales de formato no deseado y archivos malintencionados. El `Day CQ DAM Asset Upload Restriction` servicio le permite controlar el tipo de archivos que los usuarios pueden cargar. De forma predeterminada, [!DNL Assets] permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para que restrinja a los usuarios la carga de archivos de tipos MIME específicos solamente.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en modo de edición. De forma predeterminada, está seleccionada la opción **Permitir todo MIME** , que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click **[!UICONTROL Save]** to save the changes. Si especifica cadenas MIME para los tipos de MIME permitidos, la operación de carga falla con cualquier recurso que tenga un tipo de MIME que no coincida con las cadenas MIME configuradas en estos campos.
