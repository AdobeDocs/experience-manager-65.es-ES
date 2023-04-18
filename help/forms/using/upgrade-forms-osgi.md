---
title: Actualizar a AEM 6.5 Forms en OSGi
description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 99%

---

# Actualizar a AEM 6.5 Forms en OSGi {#upgrade-to-aem-forms-osgi}

Puede realizar una actualización directa de AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

La ruta de actualización directa desde **AEM 6.0 Forms, AEM 6.1 Forms** y **AEM 6.2 Forms** a AEM 6.5 Forms no está disponible. Realizar una [actualización intermedia a AEM 6.2 Forms](https://helpx.adobe.com/es/experience-manager/6-2/forms/using/upgrade.html), [actualización a AEM 6.3 Forms](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/upgrade.html) o [actualización a AEM 6.4 Forms](/help/forms/using/upgrade.md) y, a continuación, actualizar de AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Haga lo siguiente para actualizar de AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms:

1. Actualice la instancia de AEM existente a AEM 6.5. Los pasos se enumeran a continuación:

   1. Instale el Service Pack y los parches más recientes para AEM 6.3 Forms o AEM 6.4 Forms. Para obtener más información, consulte [Centro de soporte de AEM](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html).
   1. Prepare la instancia de origen para la actualización. Para ver los pasos detallados, consulte [Actualizar a AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Descargue [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Solo instalaciones basadas en Unix/Linux)** Si utiliza UNIX o Linux como sistema operativo subyacente, abra la ventana de terminal, vaya a la carpeta que contiene crx-quickstart y ejecute el siguiente comando:

      `chmod -R 755 ../crx-quickstart`

   1. Actualizar la instancia de AEM a AEM 6.3. Para obtener instrucciones paso a paso, consulte [Actualizar a AEM 6.5](/help/sites-deploying/upgrade.md).

      Antes de continuar con los siguientes pasos, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Una vez que el servidor esté en funcionamiento, algunos paquetes de AEM Forms permanecen en estado de instalación. El número de paquetes puede variar para cada instalación. Puede ignorar de forma segura el estado de estos paquetes. Los paquetes se enumeran en https://&#39;[server]:[port]&#39;/system/console/.

1. Instalar el paquete de complementos para AEM Forms. A continuación se detallan los pasos que debe seguir:

   1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
   1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
   1. En la sección **[!UICONTROL Filtros]**:
      1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
      1. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
   1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y pulse **[!UICONTROL Descargar]**.
   1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
   1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

      También puede descargar el paquete utilizando el vínculo directo que aparece en el artículo [Versiones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

      >[!NOTE]
      >
      >Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo &lt;crx-repository>/error.log y el registro esté estable. Tenga en cuenta también que algunos paquetes pueden permanecer en el estado instalado. Puede ignorar de forma segura el estado de estos paquetes.

1. Reinicie la instancia de AEM.

1. Realice actividades posteriores a la instalación.

   * **Ejecutar la utilidad de migración**

      La utilidad de migración hace que los recursos de administración de correspondencia y formularios adaptables de versiones anteriores sean compatibles con los formularios de AEM 6.5. Puede descargar la utilidad desde la distribución de software de AEM. Para obtener información paso a paso sobre cómo configurar y utilizar la utilidad de migración, consulte [utilidad de migración](../../forms/using/migration-utility.md).

      Si utiliza [Ejemplo para integrar el componente borradores y envíos](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con la base de datos y la actualización de una versión anterior, ejecute las siguientes consultas SQL tras realizar la actualización:

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar Adobe Sign**

      Si tenía Adobe Sign configurado en la versión anterior de AEM Forms, vuelva a configurar Adobe Sign desde AEM Cloud Services. Para obtener más información, consulte [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Compatibilidad con jQuery**

      En AEM 6.5 Forms, la versión de jQuery se actualiza a la 3.2.1 y la versión de la interfaz de usuario de jQuery se actualiza a la 1.12.1. AEM Forms utiliza JQuery en modo **noConflict**. Por lo tanto, si utiliza cualquier otra versión de jQuery, no se muestran problemas al realizar una actualización. Sin embargo, al actualizar a AEM 6.5 Forms:

      * Asegúrese de que los componentes personalizados, si los hay, sean compatibles con las versiones de jQuery admitidas.
      * Elimine las API no compatibles de los componentes personalizados. Consulte la [guía de actualización](https://jquery.com/upgrade-guide/3.0/) para ver la lista de API quitadas. Por ejemplo, se quita la compatibilidad con las API load(), .unload() y .error(). Utilice el método .on() en lugar de las API mencionadas. Por ejemplo, cambie $(&quot;img&quot;).load(fn) a $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar los análisis e informes**

      En AEM 6.4 Forms, la variable de tráfico para el origen y el evento de éxito para la impresión no están disponibles. Por lo tanto, al actualizar desde AEM 6.2 Forms o versiones anteriores, AEM Forms deja de enviar datos al servidor de Adobe Analytics y los informes de análisis para los formularios adaptables no están disponibles. Además, AEM 6.4 Forms introduce una variable de tráfico para la versión del análisis de formularios y el evento de éxito para la cantidad de tiempo invertido en un campo. Por lo tanto, vuelva a configurar los análisis y los informes para su entorno de AEM Forms. Para ver los pasos detallados, consulte [Configurar análisis e informes](../../forms/using/configure-analytics-forms-documents.md).


1. Compruebe que el servidor se haya actualizado correctamente, que todos los datos también se hayan migrado correctamente y que puede funcionar con normalidad.

   * **Compruebe el estado de los paquetes:** Asegúrese de que todos los paquetes estén en estado activo.
   * **Compruebe la replicación y replicación inversa:** Publique, rellene y envíe algunos formularios migrados. Compruebe también los datos enviados.
   * **Compruebe el acceso a las interfaces de usuario de administrador y desarrollador:** Inicie sesión en la instancia de AEM desde una cuenta de administrador y compruebe que tiene acceso a las siguientes direcciones URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   En AEM 6.4 Forms, la estructura del repositorio crx ha cambiado. Si actualiza de Forms 6.3 a AEM 6.5 Forms, utilice las rutas modificadas para la personalización que cree de nuevo. Para obtener la lista completa de las rutas cambiadas, consulte [Reestructurar el repositorio de Forms en AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
