---
title: Informes sobre sus recursos digitales
description: Conozca los informes sobre sus recursos en Recursos AEM que le ayudarán a comprender el uso, la actividad y el uso compartido de sus recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Informes del recurso {#asset-reports}

Los informes de recursos son una herramienta clave para evaluar la utilidad de la implementación de Recursos Adobe Experience Manager (AEM). Con Recursos AEM, puede generar varios informes para sus recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, la forma en que los usuarios interactúan con los recursos y los recursos que se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave a fin de medir la adopción de Recursos AEM en su empresa y por parte de los clientes.

El marco de informes de AEM Assets utiliza trabajos de Sling para procesar de forma asíncrona las solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficiencia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles detallados para acceder a los informes archivados y ver los estados de ejecución de los informes (exitosos, fallidos y en cola).

Cuando se genera un informe, se le notifica mediante un mensaje de correo electrónico (opcional) y una notificación de bandeja de entrada. Puede ver, descargar o eliminar un informe desde la página con la lista de informes, donde se muestran todos los informes generados previamente.

## Generar informes {#generate-reports}

Recursos AEM genera los siguientes informes estándar:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de Brand Portal
* Uso del disco
* Archivos
* Vínculos compartidos

Los administradores de AEM pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.

![Navegar por el informe de activos](assets/AssetsReportNavigation.png)

1. En la página Informes de recursos, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y toque o haga clic en **[!UICONTROL Siguiente]**.

   ![select_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Antes de generar un informe de descarga **[!UICONTROL de]** recursos, asegúrese de que el servicio de descarga de recursos está habilitado. En la consola web (`https://[aem_server]:[port]/system/console/configMgr`), abra la configuración del grabador **[!UICONTROL de eventos de CQ DAM]** de **[!UICONTROL día y seleccione la opción]** Recurso descargado (DESCARGADO)en Tipos de eventos si no está seleccionada.

   >[!NOTE]
   >
   >De forma predeterminada, los fragmentos de contenido y los recursos compartidos de vínculos se incluyen en el informe Descarga de recursos. Seleccione la opción adecuada para crear un informe de recursos compartidos de vínculos o para excluir fragmentos de contenido del informe de descarga.

1. Configure los detalles del informe, como título, descripción, miniatura y ruta de carpeta, en el repositorio de CRX donde se almacena el informe. De forma predeterminada, la ruta de la carpeta es */content/dam*. Puede especificar una ruta diferente.

   ![report_configuration](assets/report_configuration.png)

   Elija el intervalo de fechas del informe.

   Puede elegir generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no especifica ningún valor, el motor de informes lo trata como un informe que se va a generar instantáneamente.

   Los campos de configuración pueden diferir según el tipo de informe que cree. Por ejemplo: el informe Uso del **[!UICONTROL disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco que utilizan los recursos. Puede optar por incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe Uso del **[!UICONTROL disco]** no incluye campos de intervalo de fechas porque sólo indica el uso actual del espacio en disco.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Archivos]** , puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![files_report](assets/files_report.png)

   El informe Compartir **** vínculos muestra las direcciones URL de los recursos que se comparten con usuarios externos desde Recursos AEM. Incluye los ID de correo electrónico del usuario que ha compartido los recursos, los ID de correo electrónico de los usuarios con los que se comparten los recursos, la fecha de uso compartido y la fecha de caducidad del vínculo. Las columnas no se pueden personalizar.

   El informe Compartir **** vínculos no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![link_share](assets/link_share.png)

1. Toque o haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

1. En la página **[!UICONTROL Configurar columnas]** , se seleccionan algunas columnas para que aparezcan en el informe de forma predeterminada. Puede seleccionar más columnas. Anule la selección de una columna seleccionada para excluirla del informe.

   ![configure_columns](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de propiedad, configure las propiedades del binario de recursos en el nodo jcr:content en CRX. También puede agregarla mediante el selector de rutas de propiedad.

   ![custom_columns](assets/custom_columns.png)

1. Toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas. Un mensaje notifica que se ha iniciado la generación de informes.
1. En la página Informes de recursos, el estado de generación de informes se basa en el estado actual del trabajo del informe, por ejemplo, Éxito, Fallido, En cola o Programado. El mismo estado aparece en la bandeja de entrada de notificaciones.Para ver la página del informe, toque o haga clic en el vínculo del informe. Como alternativa, seleccione el informe y toque **[!UICONTROL Ver]** en la barra de herramientas.

   ![report_page](assets/report_page.png)

   Toque **[!UICONTROL Descargar]** desde la barra de herramientas para descargar el informe en formato CSV.

## Agregar columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos según sus requisitos personalizados:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de Brand Portal
* Archivos

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página Informes de recursos, toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]** , elija el informe que desee crear y toque o haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como título, descripción, miniatura, ruta de carpeta e intervalo de fechas, según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna en debajo de Columnas **** personalizadas.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Agregue la ruta de acceso de propiedad debajo del `jcr:content` nodo en CRXDE mediante el selector de rutas de propiedad. 
También puede escribir la ruta en el campo de ruta de la propiedad.

   ![property_picker](assets/property_picker.png)

   Para agregar más columnas personalizadas, toque o haga clic en **[!UICONTROL Agregar]** y repita los pasos 5 y 6.

1. Toque o haga clic en **[!UICONTROL Crear]** desde la barra de herramientas. Un mensaje notifica que se ha iniciado la generación de informes.

## Configurar el servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesite, configure el servicio Depuración de informes DAM desde la consola web para purgar los informes existentes en función de su cantidad y antigüedad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración del servicio **[!UICONTROL de depuración de informes]** DAM.
1. Especifique la frecuencia (intervalo de tiempo) del servicio de depuración en el `scheduler.expression.name` campo. También puede configurar la edad y el umbral de cantidad para los informes.
1. Guarde los cambios.
