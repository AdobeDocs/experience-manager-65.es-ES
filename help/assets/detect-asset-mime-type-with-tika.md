---
title: Detectar tipo MIME de recursos con Apache Tika
description: Active Apache Tika para ayudar a [!DNL Experience Manager Assets] detectar el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Detectar el tipo MIME de los recursos mediante [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta el tipo MIME de los recursos que se cargan desde su extensión de archivo.

Si utiliza [!DNL Apache Tika] para cargar recursos, [!DNL Assets] detecta su tipo MIME del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.

Esta función está deshabilitada de forma predeterminada. Para habilitar la función, configure el servicio **[!UICONTROL Day CQ DAM Mime Type]** desde [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La detección de tipo MIME que utiliza la biblioteca [!DNL Apache Tika] es una operación que utiliza muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, ubique **[!UICONTROL Servicio de tipo Mime CQ DAM]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccione la opción **[!UICONTROL Detectar MIME del contenido]** para habilitar el análisis de los recursos cargados para determinar su tipo MIME mientras se omiten las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.
