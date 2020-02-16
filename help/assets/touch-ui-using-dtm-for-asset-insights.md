---
title: Activar perspectivas de recursos mediante DTM
description: Obtenga información sobre cómo utilizar la administración dinámica de etiquetas (DTM) de Adobe para activar las perspectivas de recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Activar perspectivas de recursos mediante DTM {#enable-asset-insights-through-dtm}

La administración dinámica de etiquetas de Adobe es una herramienta que activa las herramientas de marketing digital. Se proporciona de forma gratuita a los clientes de Adobe Analytics.

Aunque puede personalizar el código de seguimiento para permitir que las soluciones de CMS de terceros utilicen Asset Insights, Adobe recomienda utilizar DTM para insertar etiquetas de Asset Insights.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

Siga estos pasos para habilitar las perspectivas de recursos a través de la DTM.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Configuración **[!UICONTROL de]** perspectivas.
1. [Configurar la instancia de AEM con el servicio de nube de DTM](/help/sites-administering/dtm.md)

   El testigo API debe estar disponible una vez que inicie sesión en [https://dtm.adobe.com](https://dtm.adobe.com/) y visite Configuración **[!UICONTROL de cuenta]** desde el icono Perfil. Este paso no es necesario desde el punto de vista de las perspectivas de recursos, ya que la integración de los sitios de AEM con las perspectivas de recursos sigue en marcha.

1. Inicie sesión en [https://dtm.adobe.com](https://dtm.adobe.com/)y seleccione una empresa, según corresponda.
1. Crear/abrir una propiedad web existente

   * Seleccione la ficha Propiedades **** web y, a continuación, toque o haga clic en **[!UICONTROL Agregar propiedad]**.

   * Actualice los campos según corresponda y toque o haga clic en **[!UICONTROL Crear propiedad]**. Consulte [la documentación](https://helpx.adobe.com/experience-manager/using/dtm.html).
   ![Crear, editar propiedad web](assets/Create-edit-web-property.png)

1. En la ficha **[!UICONTROL Reglas]** , seleccione **[!UICONTROL Reglas]** de carga de página en el panel de navegación y toque o haga clic en **[!UICONTROL Crear nueva regla]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expanda **[!UICONTROL Etiquetas]** Javascript/de terceros. A continuación, toque o haga clic en **[!UICONTROL Agregar nueva secuencia de comandos]** en la ficha HTML **** secuencial para abrir el cuadro de diálogo Secuencia de comandos.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Recursos]**.
1. Toque o haga clic en **[!UICONTROL Rastreador]** de páginas de perspectivas, copie el código del rastreador y péguelo en el cuadro de diálogo Script que abrió en el paso 6. Guarde los cambios.

   >[!NOTE]
   >
   > * `AppMeasurement.js` se elimina. Se espera que esté disponible a través de la herramienta Adobe Analytics de la DTM.
   > * Se elimina la llamada a `assetAnalytics.dispatcher.init`(). Se espera que se llame a la función una vez que la herramienta Adobe Analytics de la DTM termine de cargarse.
   > * Según el lugar en el que esté alojado el rastreador de páginas de perspectivas de recursos (por ejemplo, AEM, CDN, etc.), el origen del origen de la secuencia de comandos puede requerir cambios.
   > * Para el rastreador de páginas alojado en AEM, el origen debe apuntar a una instancia de publicación utilizando el nombre de host de la instancia de despachante.


1. Acceso `https://dtm.adobe.com`. Haga clic en **[!UICONTROL Información general]** en la propiedad web y haga clic en **[!UICONTROL Agregar herramienta]** o abra una herramienta Adobe Analytics existente. Al crear la herramienta, puede establecer el método **** de configuración en **[!UICONTROL Automático]**.

   ![Agregar la herramienta Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Seleccione los grupos de informes Ensayo/Producción, según corresponda.

1. Amplíe Administración **** de biblioteca y asegúrese de que **[!UICONTROL Cargar biblioteca en está]** configurada en Principio **[!UICONTROL de]** página.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expanda **[!UICONTROL Personalizar código]** de página y toque o haga clic en **[!UICONTROL Abrir editor]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, please include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
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

   * La regla de carga de página en la DTM solo incluye el código pagetracker.js. Los `assetAnalytics` campos se consideran anulaciones para los valores predeterminados. No son obligatorios de forma predeterminada.
   * El código llama `assetAnalytics.dispatcher.init`() después de asegurarse de que `_satellite.getToolsByType('sc')[0].getS`() se inicializa y `assetAnalytics,dispatcher.init` está disponible. Por lo tanto, puede omitir agregarla en el paso 11.
   * Como se indica en los comentarios dentro del código Rastreador de páginas de perspectivas (**[!UICONTROL Herramientas > Recursos > Rastreador]** de páginas de perspectivas), cuando el Rastreador de páginas no crea un `AppMeasurement` objeto, los tres primeros argumentos (RSID, Servidor de seguimiento y Espacio de nombres de visitantes) son irrelevantes. En su lugar, se pasan cadenas vacías para resaltar esto.\
      Los argumentos restantes corresponden a lo que se configura en la página Configuración de perspectivas (**[!UICONTROL Herramientas > Recursos > Configuración]** de perspectivas).
   * El objeto AppMeasurement se recupera consultando `satelliteLib` todos los motores de SiteCatalyst disponibles. Si hay varias etiquetas configuradas, cambie el índice del selector de matrices de forma adecuada. Las entradas de la matriz se ordenan según las herramientas de SiteCatalyst disponibles en la interfaz de la DTM.

1. Guarde y cierre la ventana Editor de código y, a continuación, guarde los cambios en la configuración de la herramienta.
1. En la ficha **[!UICONTROL Aprobaciones]** , apruebe ambas aprobaciones pendientes. La etiqueta DTM está lista para insertarla en la página web. Para obtener más información sobre cómo insertar etiquetas de DTM en páginas web, consulte [Integración de DTM en plantillas](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)de página personalizadas.
