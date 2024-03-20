---
title: Configurar restricciones de carga de recursos
description: Restringir el tipo de recursos (archivos) que los usuarios pueden cargar
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 18%

---

# Configurar restricciones de carga de recursos {#configuring-asset-upload-restrictions}

Puede configurar [!DNL Adobe Experience Manager Assets] para restringir el tipo de recursos que los usuarios pueden cargar. Ayuda a evitar cargas accidentales de archivos malintencionados y formatos no deseados. El `Day CQ DAM Asset Upload Restriction` Este servicio permite controlar el tipo de archivos que pueden cargar los usuarios. De forma predeterminada, [!DNL Assets] permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para restringir el acceso de los usuarios únicamente a la carga de archivos de tipos MIME específicos.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Restricción de carga de recursos de CQ DAM por día]** en el modo de edición. De forma predeterminada, la variable **Permitir todos los MIME** está seleccionada la opción, que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir el acceso de los usuarios solo a archivos de ciertos tipos de MIME, anule la selección de **[!UICONTROL Permitir todos los MIME]** y especifique los tipos MIME permitidos en la **[!UICONTROL Recursos MIME permitidos (regex)]** campos que utilizan expresiones regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios. Si especifica cadenas MIME para los tipos de MIME permitidos, la operación de carga falla con cualquier recurso que tenga un tipo de MIME que no coincida con las cadenas MIME configuradas en estos campos.
