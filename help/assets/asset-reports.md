---
title: Informes sobre el uso y uso compartido de recursos
description: Informes sobre los recursos en [!DNL Adobe Experience Manager Assets] que le ayudan a comprender el uso, la actividad y el uso compartido de los recursos digitales.
contentOwner: AG
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 9%

---


# Informes de Asset {#asset-reports}

El informe de recursos permite evaluar la utilidad de la implementación [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets], puede generar varios informes para sus recursos digitales. Los informes proporcionan información útil sobre el uso de su sistema, cómo interactúan los usuarios con los recursos y qué recursos se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave con el fin de medir la adopción de [!DNL Assets] dentro de su empresa y por parte de los clientes.

El marco de informes [!DNL Assets] utiliza [!DNL Sling] trabajos para procesar de forma asincrónica las solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficacia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a informes archivados y ver estados de ejecución de informes (éxito, error y cola).

Cuando se genera un informe, se le notifica mediante un correo electrónico (opcional) y una notificación en la bandeja de entrada. Puede ver, descargar o eliminar un informe desde la página de lista de informes, donde se muestran todos los informes generados anteriormente.

## Requisitos previos {#prerequisite-for-reporting}

Para generar informes, haga lo siguiente:

* Habilite el servicio [!UICONTROL Day CQ DAM Event Recorder] desde **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
* Seleccione las actividades o los eventos sobre los que desee crear informes. Por ejemplo, para generar un informe sobre los recursos descargados, seleccione [!UICONTROL Recurso descargado (DESCARGADO)].

![Habilitar los informes de recursos en la consola web](assets/reports-config-day-cq-dam-event-recorder.png)

## Generar informes {#generate-reports}

[!DNL Experience Manager Assets] genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] instancias de publicación
* Uso del disco
* Archivos
* Vínculos compartidos

[!DNL Adobe Experience Manager] los administradores pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. En la interfaz [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

   ![Página Herramientas para navegar por el informe Recursos](assets/AssetsReportNavigation.png)

1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

   >[!NOTE]
   >
   >De forma predeterminada, los fragmentos de contenido y los vínculos compartidos se incluyen en el informe Recurso [!UICONTROL Descargar]. Seleccione la opción adecuada para crear un informe de vínculos compartidos o para excluir fragmentos de contenido del informe de descarga.

   >[!NOTE]
   >
   >El informe [!UICONTROL Download] muestra detalles de solo los recursos que se descargan después de seleccionarlos individualmente o de descargarlos mediante Acción rápida. Sin embargo, no incluye los detalles de los recursos que se encuentran dentro de una carpeta descargada.

1. Configure los detalles del informe como título, descripción, miniatura y ruta de carpeta en el repositorio CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo considera un informe que se generará al instante.

   Los campos de configuración pueden variar según el tipo de informe que cree. Por ejemplo, el informe **[!UICONTROL Uso del disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco utilizado por los recursos. Puede elegir incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página Detalles del informe Uso del disco](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Files]**, puede incluir/excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe Archivos](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde [!DNL Assets]. Incluye los ID de correo electrónico del usuario que ha compartido los recursos, los ID de correo electrónico de los usuarios con los que se comparten los recursos, la fecha de uso compartido y la fecha de caducidad del vínculo. Las columnas no se pueden personalizar.

   El informe **[!UICONTROL Compartir vínculos]** no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![Página de detalles del informe Compartir vínculos](assets/link_share.png)

1. Haga clic en **[!UICONTROL Next]** en la barra de herramientas.

1. En la página **[!UICONTROL Configurar columnas]**, se seleccionan algunas columnas para que aparezcan en el informe de forma predeterminada. Puede seleccionar más columnas. Cancelar la selección de una columna para excluirla en el informe.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos bajo el nodo `jcr:content` en CRX. También puede agregarlo mediante el selector de rutas de propiedad.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/custom_columns.png)

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.
1. En la página [!UICONTROL Informes de recursos], el estado de generación de informes se basa en el estado actual del trabajo del informe, por ejemplo [!UICONTROL Éxito], [!UICONTROL Fallido], [!UICONTROL En cola] o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones. Para ver la página del informe, haga clic en el vínculo del informe. Como alternativa, seleccione el informe y haga clic en **[!UICONTROL Ver]** en la barra de herramientas.

   ![Un informe generado](assets/report_page.png)

   Haga clic en **[!UICONTROL Descargar]** desde la barra de herramientas para descargar el informe en formato CSV.

## Agregar columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus necesidades personalizadas:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] instancias de publicación
* Archivos

Para agregar columnas personalizadas a estos informes, siga estos pasos:

1. En [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especificar el nombre de la columna personalizada del informe](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad bajo el nodo `jcr:content` en CRXDE utilizando el selector de rutas de la propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignación de la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Agregar]** y repita los pasos 5 y 6.

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.

## Configurar el servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesita, configure el servicio Depuración de informes de DAM desde la consola web para depurar los informes existentes en función de su cantidad y edad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL DAM Report Purge Service]**.
1. Especifique la frecuencia (intervalo de tiempo) para el servicio de depuración en el campo `scheduler.expression.name`. También puede configurar la edad y el umbral de cantidad de los informes.
1. Guarde los cambios.

## Información, sugerencias y limitaciones de resolución de problemas {#best-practices-and-limitations}

* Si algunos informes o números de los informes no están disponibles o no están disponibles, asegúrese de que el servicio [!UICONTROL Grabador de eventos de CQ DAM de día] esté habilitado.

* Elimine los informes que ya no sean necesarios. Utilice las opciones de configuración del servicio Depuración de informes de DAM para configurar los criterios de depuración de informes.

* Si el Informe de uso del disco no se genera y está utilizando [!DNL Dynamic Media], asegúrese de que todos los recursos se realicen correctamente. Para resolverlo, vuelva a procesar los recursos y, a continuación, vuelva a generar el informe.
