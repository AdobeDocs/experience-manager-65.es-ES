---
title: Descarga de recursos de AEM
description: Obtenga información sobre cómo descargar recursos de AEM y activar o desactivar la funcionalidad de descarga.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Descarga de recursos de AEM {#download-assets-from-aem}

Puede descargar recursos, incluidas las representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde Recursos AEM. Los recursos descargados se incluyen en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 recursos totales por trabajo de exportación.

>[!NOTE]
>
>Los destinatarios de los mensajes de correo electrónico deben ser miembros del `dam-users` grupo para acceder al vínculo de descarga ZIP del mensaje de correo electrónico. Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que activen la descarga de recursos.

Para descargar recursos, navegue hasta un recurso, selecciónelo y toque **[!UICONTROL Descargar]** en la barra de herramientas. En el cuadro de diálogo resultante, especifique las opciones de descarga.

No se pueden descargar los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel.

![Opciones disponibles al descargar recursos de Recursos AEM](assets/asset_download_dialog.png)

*Figura: Opciones disponibles al descargar recursos de Recursos AEM*

Las siguientes son las opciones de exportación y descarga. Las representaciones dinámicas son exclusivas de Dynamic Media y permiten generar representaciones sobre la marcha además del recurso seleccionado; esta opción solo está disponible si tiene Dynamic Media activado.

| Opciones de exportación o descarga | Descripciones |
|---|---|
| [!UICONTROL Assets] | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación. |
| [!UICONTROL Representaciones] | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
| [!UICONTROL Representaciones dinámicas] | Una representación dinámica genera otras representaciones sobre la marcha. Cuando selecciona esta opción, también selecciona las representaciones que desea crear dinámicamente seleccionando una de la lista Ajustes preestablecidos [de](image-presets.md) imagen. <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen (por ejemplo, para invertir la imagen) |
| [!UICONTROL Correo electrónico] | Se envía una notificación por correo electrónico al usuario. Las plantillas de correo electrónico estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Las plantillas que personalice durante la implementación deben estar presentes en estas ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en estas ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
| [!UICONTROL Crear una carpeta independiente para cada recurso] | Seleccione esta opción para conservar la jerarquía de carpetas al descargar recursos. De forma predeterminada, la jerarquía de carpetas se ignora y todos los recursos se descargan en una carpeta del sistema local. |

La opción Representaciones está disponible si el recurso tiene representaciones. La opción de subrecursos está disponible si el recurso incluye subrecursos.

Cuando selecciona una carpeta para descargar, se descarga la jerarquía completa de recursos bajo la carpeta. Para incluir cada recurso que descargue (incluidos los recursos de las carpetas secundarias anidadas en la carpeta principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado de AEM permite a los usuarios autenticados emitir solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos visibles para ellos que pueden sobrecargar el servidor y la red. Para mitigar los posibles riesgos de DoS causados por esta función, el componente `AssetDownloadServlet` OSGi está deshabilitado de forma predeterminada para las instancias de publicación.

Para permitir la descarga de recursos de su DAM, por ejemplo, cuando se utiliza algo como Asset Share Commons u otra implementación similar al portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda que el tamaño de descarga permitido sea lo más bajo posible sin afectar a los requisitos de descarga diaria. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombre que se dirija al modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

   Para definir las propiedades de configuración de un modo de ejecución, consulte [Ejecutar modos](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode) para obtener más información.

1. En la carpeta config, cree un nuevo archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Define un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El ejemplo siguiente configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede desactivar en instancias de AEM Publish actualizando la configuración del despachante para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede desactivar manualmente directamente mediante la consola OSGi.

1. Para bloquear las solicitudes de descarga de recursos mediante una configuración de distribuidor, edite la `dispatcher.any` configuración y agregue una nueva regla a la sección [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtros.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Puede deshabilitar manualmente el componente OSGi en una instancia de Publish, navegando a la consola OSGi en `<aem-host>/system/console/components`. Busque `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` y haga clic en **[!UICONTROL Deshabilitar]**.

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos DRM](drm.md)
>* [Descargar recursos con la aplicación de escritorio AEM en Windows o Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Descargar recursos mediante Adobe Assets Link desde las aplicaciones compatibles de Adobe Creative Cloud](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)