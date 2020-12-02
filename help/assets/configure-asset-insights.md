---
title: Configure las perspectivas de recursos para obtener análisis.
description: Configure Asset Insights en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# Configurar perspectivas de recursos {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] recoge datos de uso de recursos digitales utilizados por sitios web de terceros desde  [!DNL Adobe Analytics]. Para habilitar Asset Insights para recuperar estos datos y generar perspectivas, primero configure la función para integrarla con Adobe Analytics.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluido el nombre de su organización, el nombre de usuario y Shared Secret.

   ![Configuración de Adobe Analytics para Assets Insights en Experience Manager](assets/insights_config2.png)

   *Figura: Configurar  [!DNL Adobe Analytics] para perspectivas de recursos en  [!DNL Experience Manager].*

1. Haga clic en **[!UICONTROL Autenticar]**.
1. Después de que [!DNL Experience Manager] autentique las credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes [!DNL Adobe Analytics] desde donde desee que Asset Insights recopile datos. Haga clic en **[!UICONTROL Agregar]**.
1. Después de que [!DNL Experience Manager] configure el grupo de informes, haga clic en **[!UICONTROL Listo]**.

## Rastreador de páginas {#page-tracker}

Después de configurar su cuenta [!DNL Adobe Analytics], se genera el código del rastreador de páginas. Para permitir que Assets Insights rastree [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad [!UICONTROL Rastreador de páginas] de [!DNL Experience Manager Assets] para generar el código del rastreador de páginas. Para obtener más información sobre cómo incluir el código del rastreador de páginas en páginas web de terceros, consulte [Uso del rastreador de páginas y código incrustado en páginas web](/help/assets/use-page-tracker.md).

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.
