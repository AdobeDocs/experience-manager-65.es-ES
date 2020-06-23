---
title: Descargue recursos digitales desde [!DNL Adobe Experience Manager].
description: Obtenga información sobre cómo descargar recursos [!DNL Adobe Experience Manager] desde y habilitar o deshabilitar la funcionalidad de descarga.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 3%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puede descargar recursos, incluidas las representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados se incluyen en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 recursos totales por trabajo de exportación.

>[!NOTE]
>
>Destinatarios de correos electrónicos deben ser miembros del `dam-users` grupo para acceder al vínculo de descarga ZIP del mensaje de correo electrónico. Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que activen la descarga de recursos.

No se pueden descargar los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel.

**Para descargar recursos,**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Navigation]** (Compass icon).
1. En la página Navegación, toque **[!UICONTROL Recursos > Archivos.]**
1. Vaya a una carpeta que contenga los recursos que desee descargar.
1. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta.
1. En la barra de herramientas, toque **[!UICONTROL Descargar.]**

   ![Opciones disponibles al descargar recursos de Recursos Experience Manager](/help/assets/assets/asset-download1.png)

   *Opciones del cuadro de diálogo Descargar.*

1. En el cuadro de diálogo Descargar, seleccione las opciones de descarga que desee.

   | Opción de descarga | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir cada recurso que descargue, incluidos los recursos de carpetas secundarias anidados en la carpeta principal del recurso, en una carpeta del equipo local. Cuando esta opción *no está* seleccionada, de forma predeterminada se ignora la jerarquía de carpetas y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Seleccione esta opción para que se envíe una notificación por correo electrónico al destinatario. Las plantillas de correo electrónico estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que se personalizan durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recursos]** | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representaciones]** | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado desde AEM. Se crea un archivo zip con las representaciones de recorte inteligente y se descarga en el equipo local. |
   | **[!UICONTROL Representaciones dinámicas]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Al seleccionar esta opción, también puede seleccionar las representaciones que desea crear dinámicamente seleccionando una de las que aparecen en la lista Ajuste preestablecido [de](image-presets.md) imagen. <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como invertir la imagen. La opción solo está disponible si se ha [!DNL Dynamic Media] activado. |

1. En el cuadro de diálogo, toque **[!UICONTROL Descargar.]**.

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado en [!DNL Experience Manager] permite a los usuarios autenticados emitir solicitudes de descarga concurrentes y arbitrariamente grandes para crear archivos ZIP de recursos visibles para ellos que pueden sobrecargar el servidor y la red. Para mitigar los posibles riesgos de DoS causados por esta función, el componente `AssetDownloadServlet` OSGi está deshabilitado de forma predeterminada para las instancias de publicación.

Para permitir la descarga de recursos de su DAM, por ejemplo, cuando se utiliza algo como Asset Share Commons u otra implementación similar al portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda que el tamaño de descarga permitido sea lo más bajo posible sin afectar a los requisitos de descarga diaria. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombre que destinatario el modo de ejecución de publicación (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir las propiedades de configuración de un modo de ejecución, consulte [Ejecutar modos](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).

1. En la carpeta de configuración, cree un archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Define un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El ejemplo siguiente configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede deshabilitar en instancias de [!DNL Experience Manager] publicación actualizando la configuración del despachante para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede desactivar manualmente directamente mediante la consola OSGi.

1. Para bloquear las solicitudes de descarga de recursos mediante una configuración de distribuidor, edite la `dispatcher.any` configuración y agregue una regla a la sección [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtro. `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Deshabilite el componente OSGi en una instancia de Publish navegando a la consola OSGi en `http://[aem_server]:[port]/system/console/components`. Busque `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` y haga clic en **[!UICONTROL Deshabilitar]**.

>[!MORELIKETHIS]
>
>* [Descargar recursos](drm.md)protegidos con DRM.
>* [Descargue recursos mediante la aplicación de escritorio Experience Manager en el escritorio](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)de Windows o Mac.
>* [Descargue recursos mediante Adobe Assets Link desde las aplicaciones](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)compatibles de Adobe Creative Cloud.

