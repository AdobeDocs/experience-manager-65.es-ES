---
title: Aplicar servicios de nube de traducción a carpetas
description: Aplicar servicios de nube de traducción a carpetas
contentOwner: AG
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 44%

---


# Aplicar servicios de nube de traducción a carpetas {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager] permite utilizar los servicios de traducción basados en la nube del proveedor de traducción que elija para garantizar que los recursos se traduzcan según sus necesidades.

Puede aplicar el servicio de nube de traducción directamente a la carpeta de recursos para que se puedan utilizar durante los flujos de trabajo de traducción.

## Aplique los servicios de traducción {#applying-the-translation-services}

La aplicación de servicios de traducción en la nube directamente a la carpeta de recursos elimina la necesidad de configurar servicios de traducción al crear o actualizar flujos de trabajo de traducción.

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta a la que desea aplicar los servicios de traducción.
1. En la barra de herramientas, haga clic en **[!UICONTROL Properties]** para mostrar la página **[!UICONTROL Folder Properties]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vaya a la pestaña **[!UICONTROL Cloud Services]**.
1. En la lista Configuraciones del Cloud Service , elija el proveedor de traducción deseado. Por ejemplo, si desea utilizar servicios de traducción de Microsoft, elija **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Seleccione el conector para el proveedor de traducción.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Save]** y, a continuación, haga clic en **[!UICONTROL OK]** para cerrar el cuadro de diálogo. El servicio de traducción se aplica a la carpeta.

## Aplicar conector de traducción personalizado {#applying-custom-translation-connector}

Si desea aplicar un conector personalizado para los servicios de traducción que desea utilizar en los flujos de trabajo de traducción. Para aplicar un conector personalizado, primero instale el conector desde el Administrador de paquetes. A continuación, configure el conector desde la consola de Cloud Services. Después de configurar el conector, estará disponible en la lista de conectores de la pestaña Cloud Services que se describe en [Aplicación de los serviciosde traducción](transition-cloud-services.md#applying-the-translation-services). Después de aplicar el conector personalizado y ejecutar los flujos de trabajo de traducción, el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción muestra los detalles del conector en los encabezados **[!UICONTROL Proveedor]** y **[!UICONTROL Método]**.

1. Instale el conector desde el Administrador de paquetes.
1. Haga clic en el logotipo [!DNL Experience Manager] y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Coloque el conector que instaló en **[!UICONTROL Servicios de terceros]** en la página **[!UICONTROL Cloud Services]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Haga clic en el enlace **[!UICONTROL Configure now]** para abrir el cuadro de diálogo **[!UICONTROL Create Configuration]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique un título y un nombre para el conector y, a continuación, haga clic en **[!UICONTROL Crear]**. El conector personalizado está disponible en la lista de conectores de la pestaña **[!UICONTROL Cloud Services]** que se describe en el paso 5 de [Aplicación de los servicios de traducción](#applying-the-translation-services).
1. Ejecute cualquier flujo de trabajo de traducción descrito en [Creación de proyectos de traducción](translation-projects.md) después de aplicar el conector personalizado. Compruebe los detalles del conector en el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción en la consola **[!UICONTROL Proyectos]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
