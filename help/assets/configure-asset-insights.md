---
title: Configure Assets Insights para obtener análisis.
description: Configure Assets Insights en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Información sobre Assets, Informes de Asset
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 6%

---

# Configuración de Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera los datos de uso relacionados con los recursos digitales utilizados por sitios web de terceros desde  [!DNL Adobe Analytics]. Para permitir que Assets Insights recupere estos datos y genere perspectivas, configure primero la función para integrarla con [!DNL Adobe Analytics]. Para utilizar esta función en una instalación local, compre la licencia [!DNL Adobe Analytics] por separado. Los clientes de [!DNL Managed Services] reciben [!DNL Analytics] licencia incluida con [!DNL Experience Manager]. Consulte [Descripción del producto de Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Las perspectivas solo se admiten y se proporcionan para imágenes.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluidos el nombre de su organización, el nombre de usuario y el secreto compartido.

   ![Configuración de Adobe Analytics para Assets Insights en Experience Manager](assets/insights_config2.png)

   *Figura: Configure  [!DNL Adobe Analytics] para Assets Insights en  [!DNL Experience Manager].*

1. Haga clic en **[!UICONTROL Autenticar]**.
1. Después de que [!DNL Experience Manager] autentique sus credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes [!DNL Adobe Analytics] desde el que desea que Assets Insights recupere datos. Haga clic en **[!UICONTROL Agregar]**.
1. Una vez [!DNL Experience Manager] configurado el grupo de informes, haga clic en **[!UICONTROL Listo]**.

## Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de [!DNL Adobe Analytics], se genera el código del rastreador de páginas. Para permitir que Assets Insights rastree los [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad [!UICONTROL Page Tracker] de [!DNL Experience Manager Assets] para generar el código de seguimiento de páginas. Para obtener más información sobre cómo incluir el código del rastreador de páginas en páginas web de terceros, consulte [Uso del rastreador de páginas e incrustar código en páginas web](/help/assets/use-page-tracker.md).

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.
