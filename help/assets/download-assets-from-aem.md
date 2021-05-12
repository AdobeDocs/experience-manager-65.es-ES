---
title: Descargar recursos
description: Obtenga información sobre cómo descargar recursos de [!DNL Adobe Experience Manager] y habilitar o deshabilitar la funcionalidad de descarga.
contentOwner: AG
role: Business Practitioner
feature: Administración de recursos,Distribución de recursos
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 92983232216a5c7c563ebddc3baf6fcd81aaa4e2
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 3%

---

# Descargar recursos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puede descargar recursos, incluidas representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados están agrupados en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 activos totales por trabajo de exportación.

>[!NOTE]
>
>Los destinatarios de los correos electrónicos deben ser miembros del grupo `dam-users` para acceder al vínculo de descarga ZIP en el mensaje de correo electrónico. Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que permitan la descarga de recursos.

Los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel no se pueden descargar.

Para descargar recursos, siga estos pasos:

1. En la esquina superior izquierda, haga clic en el logotipo . En el carril izquierdo, haga clic en **[!UICONTROL Navegación]**.
1. En la página [!UICONTROL Navegación], haga clic en **[!UICONTROL Recursos]** > **[!UICONTROL Archivos.]**
1. Vaya a una carpeta que contenga los recursos que desee descargar.
1. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Descargar.]**

   ![Opciones disponibles al descargar recursos desde Recursos de Experience Manager](/help/assets/assets/asset-download1.png)

   *Figura: Opciones disponibles en el cuadro de diálogo de descarga.*

1. En el cuadro de diálogo Descargar, seleccione las opciones de descarga que desee.

   | Opción de exportación o descarga | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir cada recurso que descargue, incluidos los recursos de carpetas secundarias anidadas en la carpeta principal del recurso, en una carpeta del equipo local. Cuando esta opción no está seleccionada, de forma predeterminada, la jerarquía de carpetas se ignora y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Se envía una notificación por correo electrónico al usuario. Las plantillas de correos electrónicos estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que personalice durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recursos]** | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representaciones]** | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso que seleccione. La opción está disponible si el recurso tiene representaciones. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado desde AEM. Se crea y descarga un archivo zip con las representaciones de Recorte inteligente en el equipo local. |
   | **[!UICONTROL Representaciones dinámicas]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Al seleccionar esta opción, también puede seleccionar las representaciones que desea crear dinámicamente seleccionando una de las [Ajustes preestablecidos de imagen](image-presets.md). <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como invertir la imagen. La opción solo está disponible si tiene [!DNL Dynamic Media] habilitado. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar.]**.

Cuando selecciona una carpeta para descargar, se descarga la jerarquía completa de recursos de la carpeta. Para incluir cada recurso que descargue (incluidos los recursos de carpetas secundarias anidadas en la carpeta principal) en una carpeta individual, seleccione **[!UICONTROL Crear carpeta independiente para cada recurso]**.

## Habilitar el servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado en [!DNL Experience Manager] permite que los usuarios autenticados emitan solicitudes de descarga concurrentes y arbitrariamente grandes para crear archivos ZIP de recursos visibles para ellos que puedan sobrecargar el servidor y la red. Para mitigar los posibles riesgos de DoS causados por esta función, el componente OSGi `AssetDownloadServlet` está deshabilitado de forma predeterminada para las instancias de publicación.

Para permitir la descarga de recursos de su DAM, por ejemplo, al usar algo como Asset Share Commons u otra implementación similar a un portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda configurar el tamaño de descarga permisible lo más bajo posible sin afectar a los requisitos de descarga diarios. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombres dirigida al modo de ejecución de publicación (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir las propiedades de configuración para un modo de ejecución, consulte [Run Modes](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. En la carpeta de configuración, cree un archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente: Establece un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El siguiente ejemplo configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

De forma predeterminada, para las `GET` solicitudes de descarga de archivos, [!DNL Experience Manager] impone un límite de 50 MB en el tamaño de descarga del archivo ZIP. Las descargas iniciadas mediante solicitudes `POST` o la interfaz de usuario no se ven afectadas por este límite.

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede deshabilitar en instancias de publicación [!DNL Experience Manager] actualizando la configuración de Dispatcher para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede deshabilitar manualmente a través de la consola OSGi directamente.

1. Para bloquear las solicitudes de descarga de recursos a través de una configuración de Dispatcher, edite la configuración `dispatcher.any` y añada una regla a la sección [filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Para deshabilitar el componente OSGi en una instancia de publicación, acceda a la consola OSGi en `http://[aem_server]:[port]/system/console/components`. Busque `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` y haga clic en **[!UICONTROL Disable]**.

>[!MORELIKETHIS]
>
>* [Descargar recursos mediante Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Descargar recursos protegidos con DRM](drm.md).
>* [Descargue recursos mediante la aplicación de escritorio de Experience Manager en Win o Mac local](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Descargue recursos mediante el vínculo de recursos de Adobe desde las aplicaciones](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) de Adobe Creative Cloud compatibles.

