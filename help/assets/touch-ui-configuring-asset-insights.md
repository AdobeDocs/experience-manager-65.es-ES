---
title: Configure las perspectivas de recursos para obtener análisis de uso de recursos digitales.
description: Configure las perspectivas de recursos en [!DNL Recursos Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Configurar perspectivas de recursos {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recoge datos de uso de recursos digitales utilizados por sitios web de terceros desde [!DNL Adobe Analytics]. Para habilitar Asset Insights para recuperar estos datos y generar perspectivas, primero configure la función para integrarla con Adobe Analytics.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluido el nombre de su organización, el nombre de usuario y Shared Secret.

   ![Configuración de Adobe Analytics para perspectivas de recursos en Experience Manager](assets/insights_config2.png)

   *Figura: Configurar[!DNL Adobe Analytics]para perspectivas de recursos en[!DNL Experience Manager].*

1. Haga clic en **[!UICONTROL Autenticar]**.
1. Después de [!DNL Experience Manager] autenticar las credenciales, en la lista Grupo **[!UICONTROL de]** informes, elija un grupo de [!DNL Adobe Analytics] informes desde donde desee que Asset Insights recopile datos. Haga clic en **[!UICONTROL Agregar]**.
1. Después de [!DNL Experience Manager] configurar el grupo de informes, haga clic en **[!UICONTROL Finalizado]**.

## Rastreador de páginas {#page-tracker}

Después de configurar su [!DNL Adobe Analytics] cuenta, se genera el código Rastreador de páginas. Para permitir que Assets Insights rastree [!DNL Experience Manager] los recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad [!UICONTROL Rastreador] de páginas en [!DNL Experience Manager Assets] para generar el código del rastreador de páginas. Para obtener más información sobre cómo incluir el código del rastreador de páginas en páginas web de terceros, consulte [Uso del rastreador de páginas y código incrustado en páginas](/help/assets/touch-ui-using-page-tracker.md)web.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.
