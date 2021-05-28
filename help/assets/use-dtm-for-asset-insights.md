---
title: Habilitar Assets Insights a través de DTM
description: Aprenda a utilizar Adobe Dynamic Tag Management (DTM) para habilitar Assets Insights.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Información sobre Assets, Informes de Asset
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Habilitar Assets Insights a través de DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management es una herramienta que activa las herramientas de marketing digital. Se proporciona de forma gratuita a los clientes de Adobe Analytics. Puede personalizar el código de seguimiento para permitir que las soluciones de CMS de terceros utilicen Assets Insights o puede utilizar DTM para insertar etiquetas de Assets Insights. Las perspectivas solo se admiten y se proporcionan para imágenes.

>[!CAUTION]
>
>Adobe DTM está en desuso en favor de [!DNL Adobe Experience Platform Launch] y pronto llegará al [fin de vida](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe recomienda utilizar [para perspectivas de recursos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html). [!DNL Launch] 

Siga estos pasos para habilitar Assets Insights mediante DTM.

1. Haga clic en el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Insights Configuration]**.
1. [Configuración de la implementación del Experience Manager con el Cloud Service de DTM](/help/sites-administering/dtm.md)

   El token de API debe estar disponible una vez que inicie sesión en [https://dtm.adobe.com](https://dtm.adobe.com/) y visite **[!UICONTROL Configuración de la cuenta]** en el perfil del usuario. Este paso no es necesario desde el punto de vista de Assets Insights, ya que la integración de Experience Manager Sites con Assets Insights aún está en funcionamiento.

1. Inicie sesión en [https://dtm.adobe.com](https://dtm.adobe.com/) y seleccione una empresa, según corresponda.
1. Crear o abrir una propiedad web existente

   * Seleccione la pestaña **[!UICONTROL Web Properties]** y haga clic en **[!UICONTROL Add Property]**.

   * Actualice los campos según corresponda y haga clic en **[!UICONTROL Crear propiedad]**. Consulte [documentación](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Crear editar propiedad web](assets/Create-edit-web-property.png)

1. En la pestaña **[!UICONTROL Rules]**, seleccione **[!UICONTROL Page Load Rules]** en el panel de navegación y haga clic en **[!UICONTROL Crear nueva regla]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expanda **[!UICONTROL Etiquetas de JavaScript/terceros]**. A continuación, haga clic en **[!UICONTROL Agregar nuevo script]** en la pestaña **[!UICONTROL HTML secuencial]** para abrir el cuadro de diálogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Haga clic en el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.
1. Haga clic en **[!UICONTROL Rastreador de páginas de perspectivas]**, copie el código del rastreador y péguelo en el cuadro de diálogo Script que abrió en el paso 6. Guarde los cambios.

   >[!NOTE]
   >
   >* `AppMeasurement.js` se elimina. Se espera que esté disponible a través de la herramienta Adobe Analytics de DTM.
   >* Se ha eliminado la llamada a `assetAnalytics.dispatcher.init()`. Se espera que se llame a la función una vez que la herramienta Adobe Analytics de DTM termine de cargarse.
   >* Dependiendo de dónde esté alojado el rastreador de páginas de Assets Insights (por ejemplo, Experience Manager, CDN, etc.), el origen de la secuencia de comandos puede requerir cambios.
   >* Para el rastreador de páginas alojado por el Experience Manager, el origen debe señalar a una instancia de publicación utilizando el nombre de host de la instancia de Dispatcher.


1. Acceso `https://dtm.adobe.com`. Haga clic en **[!UICONTROL Información general]** en la propiedad web y haga clic en **[!UICONTROL Agregar herramienta]** o abra una herramienta Adobe Analytics existente. Mientras crea la herramienta, puede establecer **[!UICONTROL Método de configuración]** en **[!UICONTROL Automático]**.

   ![Agregar la herramienta Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Seleccione los grupos de informes Ensayo/Producción, según corresponda.

1. Expanda **[!UICONTROL Administración de biblioteca]** y asegúrese de que **[!UICONTROL Cargar biblioteca en]** esté configurado como **[!UICONTROL Principio de página]**.

   ![climage_1-61](assets/chlimage_1-197.png)

1. Expanda **[!UICONTROL Personalizar código de página]** y haga clic en **[!UICONTROL Abrir editor]**.

   ![imagen_1-62](assets/chlimage_1-198.png)

1. Pegue el siguiente código en la ventana :

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * La regla de carga de página en la DTM solo incluye el código `pagetracker.js`. Los campos `assetAnalytics` se consideran anulaciones para los valores predeterminados. No son obligatorios de forma predeterminada.
   * El código llama a `assetAnalytics.dispatcher.init()` después de asegurarse de que `_satellite.getToolsByType('sc')[0].getS()` se inicializa y que `assetAnalytics,dispatcher.init` está disponible. Por lo tanto, puede omitir agregarla en el paso 11.
   * Como se indica en los comentarios del código Rastreador de páginas de perspectivas (**[!UICONTROL Herramientas > Assets > Rastreador de páginas de perspectivas]**), cuando el rastreador de páginas no crea un objeto `AppMeasurement`, los tres primeros argumentos (RSID, Servidor de seguimiento y Área de nombres de visitantes) son irrelevantes. Se pasan cadenas vacías en su lugar para resaltarlo.\
      Los argumentos restantes corresponden a lo que está configurado en la página Configuración de perspectivas (**[!UICONTROL Tools > Assets > Insights Configuration]**).
   * El objeto AppMeasurement se recupera consultando `satelliteLib` para todos los motores de SiteCatalyst disponibles. Si hay varias etiquetas configuradas, cambie el índice del selector de matriz de la forma adecuada. Las entradas de la matriz se ordenan según las herramientas de SiteCatalyst disponibles en la interfaz de DTM.

1. Guarde y cierre la ventana Editor de código y, a continuación, guarde los cambios en la configuración de la herramienta.
1. En la pestaña **[!UICONTROL Approvals]**, apruebe ambas aprobaciones pendientes. La etiqueta DTM está lista para su inserción en la página web. Para obtener más información sobre cómo insertar etiquetas DTM en páginas web, consulte [Integrar DTM en plantillas de página personalizadas](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
