---
title: Aplicar servicios de traducción en la nube a las carpetas
description: Aplicar servicios de traducción en la nube a las carpetas
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 43%

---


# Aplicar servicios de traducción en la nube a las carpetas {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager le permite utilizar los servicios de traducción basados en la nube del proveedor de traducción que elija para garantizar que los recursos se traducen según sus necesidades.

Puede aplicar el servicio de traducción en la nube directamente a la carpeta de recursos para que se puedan utilizar durante los flujos de trabajo de traducción.

## Aplicar los servicios de traducción {#applying-the-translation-services}

La aplicación de servicios de traducción en la nube directamente a la carpeta de recursos elimina la necesidad de configurar servicios de traducción al crear o actualizar flujos de trabajo de traducción.

1. En la interfaz de usuario de Recursos, seleccione la carpeta a la que desea aplicar los servicios de traducción.
1. From the toolbar, click the **[!UICONTROL Properties]** icon to display the **[!UICONTROL Folder Properties]** page.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vaya a la pestaña **[!UICONTROL Cloud Services]**.
1. En la lista Cloud Service Configurations, elija el proveedor de traducción deseado. Por ejemplo, si desea utilizar los servicios de traducción de Microsoft, elija **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Elija el conector para el proveedor de traducción.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. From the toolbar, click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the dialog.The translation service is applied to the folder.

## Aplicar conector de traducción personalizada  {#applying-custom-translation-connector}

Si desea aplicar un conector personalizado para los servicios de traducción que desea utilizar en los flujos de trabajo de traducción. Para aplicar un conector personalizado, primero instale el conector desde el Administrador de paquetes. A continuación, configure el conector desde la consola de Cloud Services. Después de configurar el conector, estará disponible en la lista de conectores de la pestaña Cloud Services que se describe en [Aplicación de los serviciosde traducción](transition-cloud-services.md#applying-the-translation-services). Después de aplicar el conector personalizado y ejecutar los flujos de trabajo de traducción, el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción muestra los detalles del conector en los encabezados **[!UICONTROL Proveedor]** y **[!UICONTROL Método]**.

1. Instale el conector desde el Administrador de paquetes.
1. Haga clic en el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas > Implementación > Servicios]** de nube.
1. Coloque el conector que instaló en **[!UICONTROL Servicios de terceros]** en la página **[!UICONTROL Cloud Services]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Haga clic en el vínculo **[!UICONTROL Configurar ahora]** para abrir el cuadro de diálogo **[!UICONTROL Crear configuración]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specify a title and a name for the connector, and then click **[!UICONTROL Create]**. El conector personalizado está disponible en la lista de conectores de la pestaña **[!UICONTROL Cloud Services]** que se describe en el paso 5 de [Aplicación de los servicios de traducción](#applying-the-translation-services).
1. Ejecute cualquier flujo de trabajo de traducción descrito en [Creación de proyectos de traducción](translation-projects.md) después de aplicar el conector personalizado. Compruebe los detalles del conector en el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción en la consola **[!UICONTROL Proyectos]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
