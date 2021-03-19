---
title: Detectar el tipo MIME de los recursos que utilizan Apache Tika
description: Habilite Apache Tika para ayudar [!DNL Experience Manager Assets] a detectar el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.
contentOwner: AG
role: Administrador, Arquitecto
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Detectar el tipo MIME de los recursos utilizando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta el tipo MIME de los recursos que se cargan desde su extensión de archivo.

Si utiliza [!DNL Apache Tika] para cargar recursos, [!DNL Assets] detecta su tipo MIME del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.

Esta función está deshabilitada de forma predeterminada. Para habilitar la función, configure el servicio **[!UICONTROL Day CQ DAM Mime Type]** desde [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La detección de tipo MIME que utiliza la biblioteca [!DNL Apache Tika] es una operación que consume muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, localice **[!UICONTROL Day CQ DAM Mime Type Service]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccione la opción **[!UICONTROL Detect MIME from content]** para habilitar el análisis de los recursos cargados para determinar su tipo MIME e ignorar las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.
