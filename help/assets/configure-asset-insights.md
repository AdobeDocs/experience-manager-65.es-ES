---
title: Configure las perspectivas de recursos para obtener análisis.
description: Configuración de perspectivas de recursos en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 6%

---

# Configurar perspectivas de recursos {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] obtiene datos de uso de recursos digitales utilizados por sitios web de terceros de [!DNL Adobe Analytics]. Para permitir que Assets Insights recupere estos datos y genere perspectivas, configure primero la función para integrarla con [!DNL Adobe Analytics]. Para utilizar esta función en una instalación on-premise, compre [!DNL Adobe Analytics] licencia por separado. Clientes en [!DNL Managed Services] recibir [!DNL Analytics] licencia incluida en [!DNL Experience Manager]. Consulte [Descripción del producto de Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para las imágenes.

1. Entrada [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione las credenciales, incluido el nombre de su organización, el nombre de usuario y el secreto compartido.

   ![Configuración de Adobe Analytics para las perspectivas de recursos en Experience Manager](assets/insights_config2.png)

   *Figura: Configurar [!DNL Adobe Analytics] para las perspectivas de recursos en [!DNL Experience Manager].*

1. Clic **[!UICONTROL Autenticar]**.
1. Después [!DNL Experience Manager] autentica sus credenciales, desde el **[!UICONTROL Grupo de informes]** , elija una [!DNL Adobe Analytics] grupo de informes de donde desee que Assets Insights obtenga datos. Clic **[!UICONTROL Añadir]**.
1. Después [!DNL Experience Manager] Para configurar el grupo de informes, haga clic en **[!UICONTROL Listo]**.

## Rastreador de página {#page-tracker}

Después de configurar su [!DNL Adobe Analytics] , se generará el código de seguimiento de página para usted. Para permitir el seguimiento de Assets Insights [!DNL Experience Manager] Los recursos utilizados en sitios web de terceros incluyen el código de rastreador de páginas en el código del sitio web. Utilice el [!UICONTROL Rastreador de página] utilidad en [!DNL Experience Manager Assets] para generar el código de rastreador de página. Para obtener más información sobre cómo incluir el código de rastreador de páginas en páginas web de terceros, consulte [Usar el rastreador de páginas y el código incrustado en las páginas web](/help/assets/use-page-tracker.md).

1. Entrada [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Clic **[!UICONTROL Descargar]** para descargar el código de rastreador de página.
