---
title: Detectar el tipo MIME de los recursos que utilizan Apache Tika
description: Habilitar Apache Tika para ayudar [!DNL Experience Manager Assets] detecte el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión del archivo.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Detectar el tipo MIME de los recursos que utilizan [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta el tipo MIME de los recursos que se cargan desde su extensión de archivo.

Si usa [!DNL Apache Tika] para cargar recursos, [!DNL Assets] detecta su tipo MIME de la secuencia de contenido durante la operación de carga en lugar de la extensión de archivo.

Esta función está deshabilitada de forma predeterminada. Para habilitar la función, configure la variable **[!UICONTROL Tipo de Mime de Day CQ DAM]** servicio desde [!UICONTROL Administrador de configuración].

>[!NOTE]
>
>Detección de tipo MIME mediante la función [!DNL Apache Tika] es una operación que consume muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, busque **[!UICONTROL Servicio Day CQ DAM Mime Type]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccione el **[!UICONTROL Detectar MIME del contenido]** para habilitar el análisis de los recursos cargados para determinar su tipo MIME e ignorar las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.
