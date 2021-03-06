---
title: Configurar restricciones de carga de recursos
description: 'Restringir el tipo de recursos (archivos) que los usuarios pueden cargar '
contentOwner: AG
role: Developer, Admin, Architect
feature: Administración de recursos,Cargar
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---

# Configurar restricciones de carga de recursos {#configuring-asset-upload-restrictions}

Puede configurar [!DNL Adobe Experience Manager Assets] para restringir el tipo de recursos que los usuarios pueden cargar. Ayuda a evitar cargas accidentales de formatos no deseados y archivos malintencionados. El servicio `Day CQ DAM Asset Upload Restriction` permite controlar el tipo de archivos que los usuarios pueden cargar. De forma predeterminada, [!DNL Assets] permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para restringir el acceso de los usuarios solo a archivos de tipos MIME específicos.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en el modo de edición. De forma predeterminada, la opción **Allow all MIME** está seleccionada, lo que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir el acceso de los usuarios solo a archivos de ciertos tipos de MIME, desmarque la opción **[!UICONTROL Allow all MIME]** y especifique los tipos de MIME permitidos en los campos **[!UICONTROL Allowed Asset MIMEs (regex)]** utilizando expresiones regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios. Si especifica cadenas MIME para los tipos de MIME permitidos, la operación de carga falla con cualquier recurso que tenga un tipo de MIME que no coincida con las cadenas MIME configuradas en estos campos.
