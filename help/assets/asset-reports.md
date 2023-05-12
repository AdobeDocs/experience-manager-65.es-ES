---
title: Informes sobre el uso y uso compartido de recursos
description: Informes sobre sus recursos en [!DNL Adobe Experience Manager Assets] que le ayudan a comprender el uso, la actividad y el uso compartido de sus recursos digitales.
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 9%

---

# Informes de Asset {#asset-reports}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | Este artículo |

Los informes de recursos le permiten evaluar la utilidad de su [!DNL Adobe Experience Manager Assets] implementación. con [!DNL Assets], puede generar varios informes para los recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, la forma en que los usuarios interactúan con los recursos y los recursos que se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave para medir la adopción de [!DNL Assets] en su empresa y por clientes.

La variable [!DNL Assets] uso del marco de informes [!DNL Sling] trabajos para procesar de forma asíncrona solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficacia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a informes archivados y ver estados de ejecución de informes (éxito, error y cola).

Cuando se genera un informe, se le notifica mediante un correo electrónico (opcional) y una notificación en la bandeja de entrada. Puede ver, descargar o eliminar un informe desde la página de lista de informes, donde se muestran todos los informes generados anteriormente.

## Requisitos previos {#prerequisite-for-reporting}

Para generar informes, haga lo siguiente:

* Habilitar [!UICONTROL Grabador de eventos de CQ DAM de día] servicio desde **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
* Seleccione las actividades o los eventos sobre los que desee crear informes. Por ejemplo, para generar un informe sobre los recursos descargados, seleccione [!UICONTROL Recurso descargado (DESCARGADO)].

![Habilitar los informes de recursos en la consola web](assets/reports-config-day-cq-dam-event-recorder.png)

## Generar informes {#generate-reports}

[!DNL Experience Manager Assets] genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] publicación
* Uso del disco
* Archivos
* Vínculos compartidos

[!DNL Adobe Experience Manager] los administradores pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. En [!DNL Experience Manager] interfaz, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

   ![Página Herramientas para navegar por el informe Recursos](assets/AssetsReportNavigation.png)

1. En el [!UICONTROL Informes de recursos] página, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En el **[!UICONTROL Crear informe]** , elija el informe que desea crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

   >[!NOTE]
   >
   >De forma predeterminada, los fragmentos de contenido y los vínculos compartidos se incluyen en el recurso [!UICONTROL Descargar] informe. Seleccione la opción adecuada para crear un informe de vínculos compartidos o para excluir fragmentos de contenido del informe de descarga.

   >[!NOTE]
   >
   >La variable [!UICONTROL Descargar] El informe solo muestra los detalles de los recursos que se descargan tras seleccionarlos individualmente o que se descargan mediante Acción rápida. Sin embargo, no incluye los detalles de los recursos que se encuentran dentro de una carpeta descargada.

1. Configure los detalles del informe como título, descripción, miniatura y ruta de carpeta en el repositorio CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo considera un informe que se generará al instante.

   Los campos de configuración pueden variar según el tipo de informe que cree. Por ejemplo, la variable **[!UICONTROL Uso del disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco utilizado por los recursos. Puede elegir incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página Detalles del informe Uso del disco](assets/disk_usage_configuration.png)

   Al crear la variable **[!UICONTROL Archivos]** , puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe Archivos](assets/files_report.png)

   El informe **[!UICONTROL Compartir vínculos]** muestra las direcciones URL de los recursos que se comparten con usuarios externos desde [!DNL Assets]. Incluye los ID de correo electrónico del usuario que ha compartido los recursos, los ID de correo electrónico de los usuarios con los que se comparten los recursos, la fecha de uso compartido y la fecha de caducidad del vínculo. Las columnas no se pueden personalizar.

   La variable **[!UICONTROL Compartir vínculos]** no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![Página de detalles del informe Compartir vínculos](assets/link_share.png)

1. Haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

1. En el **[!UICONTROL Configurar columnas]** , algunas columnas están seleccionadas para aparecer en el informe de forma predeterminada. Puede seleccionar más columnas. Cancelar la selección de una columna para excluirla en el informe.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos en la sección `jcr:content` en CRX. También puede agregarlo mediante el selector de rutas de propiedad.

   ![Seleccionar o cancelar la selección de columnas de informes](assets/custom_columns.png)

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.
1. En el [!UICONTROL Informes de recursos] , el estado de generación de informes se basa en el estado actual del trabajo del informe, por ejemplo [!UICONTROL Correcto], [!UICONTROL Error], [!UICONTROL En cola]o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones. Para ver la página del informe, haga clic en el vínculo del informe. También puede seleccionar el informe y hacer clic en **[!UICONTROL Ver]** en la barra de herramientas.

   ![Un informe generado](assets/report_page.png)

   Haga clic en **[!UICONTROL Descargar]** en la barra de herramientas para descargar el informe en formato CSV.

## Añadir columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus necesidades personalizadas:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* [!DNL Brand Portal] publicación
* Archivos

Para agregar columnas personalizadas a estos informes, siga estos pasos:

1. En el [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En el [!UICONTROL Informes de recursos] página, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

1. En el **[!UICONTROL Crear informe]** , elija el informe que desea crear y haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especificar el nombre de la columna personalizada del informe](assets/custom_columns-1.png)

1. Añada la ruta de la propiedad en la sección `jcr:content` en CRXDE usando el selector de rutas de propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignación de la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Agregar]** y repita los pasos 5 y 6.

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.

## Configurar el servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesita, configure el servicio Depuración de informes de DAM desde la consola web para depurar los informes existentes en función de su cantidad y edad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Servicio de depuración de informes DAM]** configuración.
1. Especifique la frecuencia (intervalo de tiempo) del servicio de depuración en la variable `scheduler.expression.name` campo . También puede configurar la edad y el umbral de cantidad de los informes.
1. Guarde los cambios.

## Información, sugerencias y limitaciones de resolución de problemas {#best-practices-and-limitations}

* Si algunos informes o números de los informes no están disponibles o no se muestran correctamente, asegúrese de que [!UICONTROL Grabador de eventos de CQ DAM de día] está habilitado.

* Elimine los informes que ya no sean necesarios. Utilice las opciones de configuración del servicio Depuración de informes de DAM para configurar los criterios de depuración de informes.

* Si el Informe de uso del disco no se genera y está utilizando [!DNL Dynamic Media], asegúrese de que todos los recursos se realizan correctamente. Para resolverlo, vuelva a procesar los recursos y, a continuación, vuelva a generar el informe.
