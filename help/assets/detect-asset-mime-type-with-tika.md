---
title: Detectar tipo MIME de recursos con Apache Tika
description: Active Apache Tika para ayudar a Experience Manager Assets a detectar el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión de archivo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, Recursos Adobe Experience Manager detecta el tipo MIME de los recursos que se cargan desde su extensión de archivo.

Si utiliza Apache Tika para cargar recursos, Assets detecta su tipo MIME del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.

Esta función está deshabilitada de forma predeterminada. Para habilitar la función, configure el servicio **[!UICONTROL Day CQ DAM Mime Type]** desde [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La detección de tipo MIME mediante la biblioteca Apache Tika es una operación que utiliza muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, localice el servicio **[!UICONTROL Day CQ DAM Mime Type y haga clic en]** Editar ****.

1. Seleccione la opción **[!UICONTROL Detectar MIME del contenido]** para permitir el análisis de los recursos cargados para determinar su tipo MIME mientras se omiten las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
