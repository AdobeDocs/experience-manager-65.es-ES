---
title: Configurar restricciones de carga de recursos
description: 'Restringir el tipo de recursos (archivos) que los usuarios pueden cargar '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configurar restricciones de carga de recursos {#configuring-asset-upload-restrictions}

Puede configurar Recursos Adobe Experience Manager (AEM) para restringir el tipo de recursos (archivos) que los usuarios pueden cargar. Esta función le ayuda a eliminar la posibilidad de que los usuarios carguen recursos en un formato no deseado o carguen archivos maliciosos. El `Day CQ DAM Asset Upload Restriction` servicio le permite controlar el tipo de archivos que los usuarios pueden cargar. De forma predeterminada, Recursos AEM permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para que restrinja a los usuarios la carga de archivos de tipos MIME específicos solamente.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en modo de edición. De forma predeterminada, está seleccionada la opción **Permitir todo MIME** , que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir el acceso de los usuarios a archivos de ciertos tipos MIME únicamente, desactive la opción **[!UICONTROL Permitir todo tipo MIME]** y especifique los tipos MIME permitidos en los campos MIME de recursos **[!UICONTROL permitidos (regex)]** mediante expresiones regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Toque o haga clic en **[!UICONTROL Guardar]** para guardar los cambios. Si especifica cadenas MIME para tipos MIME permitidos, la operación de carga falla para cualquier recurso con tipo MIME que no coincida con las cadenas MIME configuradas en estos campos.
