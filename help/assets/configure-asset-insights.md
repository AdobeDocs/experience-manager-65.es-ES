---
title: Configure Asset Insights para obtener análisis.
description: Configure Asset Insights en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Asset Insights,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 7%

---


# Configurar Asset Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recupera los datos de uso relacionados con los recursos digitales utilizados por sitios web de terceros desde  [!DNL Adobe Analytics]. Para permitir que Asset Insights recupere estos datos y genere perspectivas, configure primero la función para integrarla con Adobe Analytics.

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
1. Después de que [!DNL Experience Manager] autentique sus credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes [!DNL Adobe Analytics] desde el que desea que Asset Insights recupere datos. Haga clic en **[!UICONTROL Agregar]**.
1. Una vez [!DNL Experience Manager] configurado el grupo de informes, haga clic en **[!UICONTROL Listo]**.

## Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de [!DNL Adobe Analytics], se genera el código del rastreador de páginas. Para permitir que Assets Insights rastree los [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad [!UICONTROL Page Tracker] de [!DNL Experience Manager Assets] para generar el código de seguimiento de páginas. Para obtener más información sobre cómo incluir el código del rastreador de páginas en páginas web de terceros, consulte [Uso del rastreador de páginas e incrustar código en páginas web](/help/assets/use-page-tracker.md).

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.
