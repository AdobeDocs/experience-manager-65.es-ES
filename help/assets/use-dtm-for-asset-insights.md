---
title: Habilitar Assets Insights mediante DTM
description: Aprenda a utilizar la Dynamic Tag Management (DTM) de Adobe para habilitar Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Habilitar Assets Insights mediante DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management es una herramienta que activa sus herramientas de marketing digital. Se proporciona de forma gratuita a los clientes de Adobe Analytics. Puede personalizar el código de seguimiento para permitir que las soluciones de CMS de terceros utilicen Assets Insights o puede utilizar DTM para insertar etiquetas de Assets Insights. Las perspectivas solo son compatibles y se proporcionan para las imágenes.

>[!CAUTION]
>
>La DTM de Adobe está en desuso a favor de [!DNL Adobe Experience Platform] y pronto llegarán a [fin de vida útil](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). El Adobe recomienda que [use [!DNL Adobe Experience Platform] para perspectivas de recursos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Siga estos pasos para habilitar Assets Insights mediante DTM.

1. Haga clic en el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuración de perspectivas]**.
1. [Configuración de la implementación del Experience Manager con el Cloud Service DTM](/help/sites-administering/dtm.md)

   El token de API debe estar disponible una vez que inicie sesión en [https://dtm.adobe.com](https://dtm.adobe.com/) y visita **[!UICONTROL Configuración de cuenta]** en el perfil de usuario. Este paso no es necesario desde el punto de vista de Assets Insights, ya que la integración de Experience Manager Sites con Assets Insights aún está en proceso.

1. Iniciar sesión en [https://dtm.adobe.com](https://dtm.adobe.com/)y seleccione una empresa, según corresponda.
1. Crear o abrir una propiedad web existente

   * Seleccione el **[!UICONTROL Propiedades web]** y haga clic en **[!UICONTROL Añadir propiedad]**.

   * Actualice los campos según corresponda y haga clic en **[!UICONTROL Crear propiedad]**. Consulte [documentación](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es).

   ![Crear y editar propiedad web](assets/Create-edit-web-property.png)

1. En el **[!UICONTROL Reglas]** pestaña, seleccione **[!UICONTROL Reglas de carga de página]** en el panel de navegación y haga clic en **[!UICONTROL Crear nueva regla]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expandir **[!UICONTROL Etiquetas de JavaScript/terceros]**. Luego haga clic en **[!UICONTROL Agregar nuevo script]** en el **[!UICONTROL HTML secuencial]** para abrir el cuadro de diálogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Haga clic en el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.
1. Clic **[!UICONTROL Rastreador de página de perspectivas]**, copie el código de seguimiento y péguelo en el cuadro de diálogo Script que abrió en el paso 6. Guarde los cambios.

   >[!NOTE]
   >
   >* `AppMeasurement.js` se ha eliminado. Se espera que esté disponible a través de la herramienta Adobe Analytics de DTM.
   >* La llamada a `assetAnalytics.dispatcher.init()` se ha eliminado. Se espera llamar a la función una vez que la herramienta Adobe Analytics de DTM termine de cargarse.
   >* Según la ubicación en la que esté alojado el rastreador de páginas de perspectivas de recursos (por ejemplo, Experience Manager, CDN, etc.), el origen del origen del script puede requerir cambios.
   >* Para el rastreador de páginas alojado por el Experience Manager, el origen debe apuntar a una instancia de publicación utilizando el nombre de host de la instancia de Dispatcher.

1. Acceso `https://dtm.adobe.com`. Clic **[!UICONTROL Información general]** en la propiedad web y haga clic en **[!UICONTROL Agregar herramienta]** o abra una herramienta Adobe Analytics existente. Al crear la herramienta, puede establecer **[!UICONTROL Método de configuración]** hasta **[!UICONTROL Automático]**.

   ![Agregar la herramienta Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Seleccione los grupos de informes Ensayo/Producción, según corresponda.

1. Expandir **[!UICONTROL Administración de biblioteca]**, y asegúrese de que **[!UICONTROL Cargar biblioteca en]** se establece en **[!UICONTROL Principio de página]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expandir **[!UICONTROL Personalizar código de página]** y haga clic en **[!UICONTROL Abrir editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Pegue el siguiente código en la ventana:

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * La regla de carga de página en la DTM solo incluye la variable `pagetracker.js` código. Cualquiera `assetAnalytics` Los campos de se consideran anulaciones de los valores predeterminados. No son necesarias de forma predeterminada.
   * El código llama a `assetAnalytics.dispatcher.init()` después de asegurarse de que `_satellite.getToolsByType('sc')[0].getS()` se inicializa y `assetAnalytics,dispatcher.init` está disponible. Por lo tanto, puede omitir agregarlo en el paso 11.
   * Como se indica en los comentarios dentro del código de rastreador de páginas de perspectivas (**[!UICONTROL Herramientas > Recursos > Rastreador de página de perspectivas]**), cuando el Rastreador de páginas no cree un `AppMeasurement` , los tres primeros argumentos (RSID, Servidor de seguimiento y Espacio de nombres del visitante) son irrelevantes. En su lugar, se pasan cadenas vacías para resaltar esto.\
     Los argumentos restantes corresponden a lo que se configura en la página Configuración de perspectivas (**[!UICONTROL Herramientas > Recursos > Configuración de perspectivas]**).
   * El objeto de AppMeasurement se recupera consultando `satelliteLib` para todos los motores de SiteCatalyst disponibles. Si hay varias etiquetas configuradas, cambie el índice del selector de matriz correctamente. Las entradas de la matriz se ordenan según las herramientas de SiteCatalyst disponibles en la interfaz de DTM.

1. Guarde y cierre la ventana Editor de código y, a continuación, guarde los cambios en la configuración de la herramienta.
1. En el **[!UICONTROL Aprobaciones]** pestaña, apruebe las aprobaciones pendientes. La etiqueta DTM está lista para insertarse en la página web.
