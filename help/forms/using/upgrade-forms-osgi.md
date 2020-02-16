---
title: Actualización a AEM 6.5 Forms
seo-title: Actualización a AEM 6.5 Forms
description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
seo-description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 0a7c243589b410a671674b85d27fad158fe96b2a

---


# Actualización a AEM 6.5 Forms en OSGi {#upgrade-to-aem-forms-osgi}

Puede realizar una actualización directa de AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

No está disponible la ruta de actualización directa de **AEM 6.0 Forms, AEM 6.1 Forms** y **AEM 6.2 Forms** a AEM 6.5 Forms. Realice una [actualización intermedia a AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [actualice a AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)o [actualice a AEM 6.4 Forms](/help/forms/using/upgrade.md) y, a continuación, actualice AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms.

Para actualizar AEM 6.3 Forms o AEM 6.4 Forms a AEM 6.5 Forms, haga lo siguiente:

1. Actualice la instancia de AEM existente a AEM 6.5. Los pasos se enumeran a continuación:

   1. Instale el Service Pack y los parches más recientes para AEM 6.3 Forms o AEM 6.4 Forms. Para obtener más información, consulte [AEM Sustenance Hub](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).
   1. Prepare la instancia de origen para la actualización. Para obtener más información, consulte [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Descargue el inicio rápido de [AEM 6.5](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Solo instalaciones basadas en Unix/Linux)** Si utiliza UNIX o Linux como sistema operativo subyacente, abra la ventana de terminal, navegue a la carpeta que contenga crx-quickstart y ejecute el siguiente comando:

      `chmod -R 755 ../crx-quickstart`

   1. Actualice su instancia de AEM a AEM 6.3. Para obtener instrucciones paso a paso, consulte [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md).

      Antes de continuar con los siguientes pasos, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTER dejen de aparecer en el archivo &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Una vez que el servidor está en funcionamiento, algunos paquetes de AEM Forms permanecen en estado de instalación. El número de paquetes puede variar para cada instalación. Puede ignorar con seguridad el estado de estos paquetes. Los paquetes se muestran en https://[server]:[port]/system/console/.

1. Instale el paquete de complementos de AEM Forms.  Los pasos se enumeran a continuación:

   1. Inicie sesión en el servidor de AEM como administrador y abra el recurso compartido de paquetes. La dirección URL predeterminada del recurso compartido de paquetes es `https://[server]:[port]/crx/packageshare`.
   1. En el uso compartido de paquetes, busque paquetes **de AEM 6.5 Forms, haga clic en el paquete aplicable a su sistema operativo y, a continuación, haga clic en** Descargar ****. Lea y acepte el contrato de licencia y haga clic en **Aceptar**. Se inicia la descarga. Una vez descargado, la palabra **Descargado** aparece junto al paquete.

      También puede utilizar los hipervínculos enumerados en las versiones [de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms para descargar manualmente un paquete.

   1. Una vez completada la descarga, haga clic en **Descargado**. Se le redirige al administrador de paquetes. En el administrador de paquetes, busque el paquete descargado y haga clic en **Instalar**.

      Si descarga manualmente el paquete mediante el vínculo directo que aparece en las versiones [de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)AEM Forms, abra el Administrador de paquetes de AEM, haga clic en **Cargar paquete**, seleccione el paquete descargado y haga clic en Cargar. Después de cargar el paquete, haga clic en el nombre del paquete y, a continuación, en **Instalar.**

      >[!NOTE]
      >
      >Después de instalar el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga inmediatamente el servidor.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTRARED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo &lt;crx-repository>/error.log y el registro sea estable. Además, algunos paquetes pueden permanecer en el estado de instalación. Puede ignorar con seguridad el estado de estos paquetes.

   1. Reinicie la instancia de AEM.

1. Realizar actividades posteriores a la instalación.

   * **Ejecutar la utilidad de migración**

      La utilidad de migración hace que los formularios adaptables y los recursos de gestión de correspondencia de versiones anteriores sean compatibles con los formularios de AEM 6.5. Puede descargar la utilidad desde el recurso compartido de paquetes de AEM. Para obtener información paso a paso sobre cómo configurar y utilizar la utilidad de migración, consulte Utilidad [de](../../forms/using/migration-utility.md)migración.

      Si utiliza [Sample para integrar borradores y componentes](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) de envíos con la base de datos y actualizar desde una versión anterior, ejecute las siguientes consultas SQL después de realizar la actualización:

      ```
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar Adobe Sign**

      Si tenía Adobe Sign configurado en la versión anterior de AEM Forms, vuelva a configurar Adobe Sign desde los servicios de AEM Cloud. Para obtener más información, consulte [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Compatibilidad con jQuery**

      En AEM 6.5 Forms, la versión de jQuery se actualiza a 3.2.1 y la versión de la interfaz de usuario de jQuery se actualiza a 1.12.1. AEM Form utiliza JQuery en modo **sin conflicto** . Por lo tanto, si utiliza cualquier otra versión de jQuery, no se mostrará ningún problema al realizar una actualización. Sin embargo, al actualizar a AEM 6.5 Forms:

      * Asegúrese de que los componentes personalizados, si los hay, sean compatibles con las versiones de jQuery admitidas.
      * Elimine las API no compatibles de los componentes personalizados. Consulte la guía [de](https://jquery.com/upgrade-guide/3.0/) actualización para ver la lista de API eliminadas. Por ejemplo, se elimina la compatibilidad con las API load(), .unload() y .error(). Utilice el método .on() en lugar de las API mencionadas. Por ejemplo, cambie $(&quot;img&quot;).load(fn) a $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar los análisis y los informes**

      En AEM 6.4 Forms, no están disponibles las variables de tráfico para el origen y el evento de éxito para impresión. Por lo tanto, al actualizar desde AEM 6.2 Forms o versiones anteriores, AEM Forms deja de enviar datos al servidor de Adobe Analytics y los informes de análisis para formularios adaptables no están disponibles. Además, AEM 6.4 Forms introduce la variable de tráfico para la versión del análisis de formularios y el evento de éxito para la cantidad de tiempo empleado en un campo. Por lo tanto, vuelva a configurar los análisis y los informes para su entorno de AEM Forms. Para ver los pasos detallados, consulte [Configuración de análisis e informes](../../forms/using/configure-analytics-forms-documents.md).


1. Compruebe que el servidor se ha actualizado correctamente, que todos los datos también se han migrado correctamente y que puede funcionar con normalidad.

   * **** Compruebe el estado de los paquetes: Asegúrese de que todos los paquetes están en estado activo.
   * **** Verificar replicación y replicación inversa: Publique, rellene y envíe algunos formularios migrados. Compruebe también los datos enviados.
   * **** Verificar el acceso a las interfaces de usuario de administrador y desarrollador: Inicie sesión en una instancia de AEM desde una cuenta de administrador y compruebe que tiene acceso a las siguientes direcciones URL:

      * `https://[server]:[port]/crx/packmgr`
      * `https://[server]:[port]/crx/de`
      * `https://[server]:[port]/aem/forms.html/content/dam/formsanddocuments`
   >[!NOTE]
   En AEM 6.4 Forms, la estructura del repositorio crx ha cambiado. Si actualiza de 6.3 Forms a AEM 6.5 Forms, utilice las rutas modificadas para la personalización que vuelva a crear. Para obtener la lista completa de las rutas cambiadas, consulte Reestructuración del repositorio de [formularios en AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

