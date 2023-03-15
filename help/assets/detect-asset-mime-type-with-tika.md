---
title: Detección del tipo MIME de los recursos mediante Apache Tika
description: Habilite Apache Tika para ayudarle [!DNL Experience Manager Assets] detecte el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión de archivo.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Detectar tipo MIME de recursos mediante [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta el tipo MIME de los recursos que carga desde su extensión de archivo.

Si utiliza [!DNL Apache Tika] para cargar recursos, [!DNL Assets] detecta su tipo MIME del flujo de contenido durante la operación de carga en lugar de la extensión de archivo.

Esta función está desactivada de forma predeterminada. Para habilitar la función, configure el **[!UICONTROL Tipo MIME de CQ DAM del día]** servicio desde [!UICONTROL Administrador de configuración].

>[!NOTE]
>
>Detección de tipo MIME con [!DNL Apache Tika] es una operación que consume muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, busque **[!UICONTROL Servicio Day CQ DAM Mime Type]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccione el **[!UICONTROL Detectar MIME del contenido]** opción para habilitar el análisis de los recursos cargados para determinar su tipo MIME al ignorar las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.
