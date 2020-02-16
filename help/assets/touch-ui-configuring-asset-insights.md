---
title: Configurar perspectivas de recursos
description: Configuración de perspectivas de recursos en Recursos AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6d4f79c126a3c44666e2a42b2246c964813d24ab

---


# Configurar perspectivas de recursos {#configure-asset-insights}

Recursos Adobe Experience Manager (AEM) obtiene datos de uso de los recursos de AEM utilizados por sitios web de terceros desde Adobe Analytics. Para habilitar Asset Insights para recuperar estos datos y generar perspectivas, primero configure la función para integrarla con Adobe Analytics.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

1. En AEM, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta Configuración **[!UICONTROL de]** perspectivas.
1. En el asistente, seleccione un centro de datos y proporcione sus credenciales, incluido el nombre de su organización, el nombre de usuario y Shared Secret.

   ![Configuración de Adobe Analytics para perspectivas de recursos en AEM](assets/insights_config2.png)


   *Figura: Configuración de Adobe Analytics para perspectivas de recursos en AEM*

1. Toque o haga clic en **[!UICONTROL Autenticar]**.
1. Una vez que AEM haya autenticado sus credenciales, en la lista Grupo **[!UICONTROL de]** informes, elija un grupo de informes de Adobe Analytics desde el que desee que Asset Insights obtenga datos. Haga clic en **[!UICONTROL Agregar]**.
1. Una vez que AEM haya configurado el grupo de informes, toque o haga clic en **[!UICONTROL Listo]**.

## Rastreador de páginas {#page-tracker}

Después de configurar la cuenta de Adobe Analytics, se genera el código de rastreador de páginas. Para habilitar Assets Insights a fin de rastrear los recursos de AEM utilizados en sitios web de terceros, incluya el código del rastreador de páginas en el código del sitio web. Utilice la utilidad Rastreador de páginas de Recursos AEM para generar el código de seguimiento de páginas. Para obtener más información sobre cómo incluir el código del rastreador de páginas en páginas web de terceros, consulte [Uso del rastreador de páginas y código incrustado en páginas](/help/assets/touch-ui-using-page-tracker.md)web.

1. En AEM, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]** , haga clic en la tarjeta Rastreador **[!UICONTROL de páginas de]** perspectivas.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código del rastreador de páginas.
