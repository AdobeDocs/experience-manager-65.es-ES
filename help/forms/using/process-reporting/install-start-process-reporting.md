---
title: Introducción a la creación de informes de procesos
seo-title: Getting Started with Process Reporting
description: Los pasos que debe seguir para empezar a utilizar AEM Forms en los informes de procesos JEE
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# Introducción a la creación de informes de procesos{#getting-started-with-process-reporting}

La creación de informes de procesos permite a los usuarios de AEM Forms consultar información sobre los procesos de AEM Forms definidos actualmente en la implementación de AEM Forms. Sin embargo, Process Reporting no accede a los datos directamente desde el repositorio de AEM Forms. Los datos se publican primero en el repositorio de informes de procesos de forma programada (*por el servicio ProcessDataPublisher y ProcessDataStorage* s). A continuación, los informes y las consultas de Process Reporting se generan a partir de los datos de Process Reporting publicados en el repositorio. Process Reporting se instala como parte del módulo del Forms Workflow.

Este artículo detalla los pasos para habilitar la publicación de datos de AEM Forms en el repositorio de informes de procesos. Después de lo cual, podrá usar Informes de procesos para ejecutar informes y consultas. El artículo también cubre las opciones disponibles para configurar los servicios de Process Reporting.

## Requisitos previos de informes de procesos {#process-reporting-pre-requisites}

### Purgar procesos no esenciales {#purge-non-essential-processes}

Si está utilizando Forms Workflow, la base de datos de AEM Forms puede contener una gran cantidad de datos

Los servicios de publicación de Process Reporting publicarán todos los datos de AEM Forms disponibles actualmente en la base de datos. Esto implica que si la base de datos contiene datos heredados sobre los que no desea ejecutar informes y consultas, todos esos datos también se publicarán en el repositorio aunque no se requieran para realizar informes. Se recomienda depurar estos datos antes de ejecutar los servicios para publicar los datos en el repositorio de Process Reporting. Esto mejorará el rendimiento tanto del servicio de editor como del servicio que consulta los datos para los informes.

Para obtener más información sobre la depuración de datos de procesos de AEM Forms, consulte [Depuración de datos de proceso](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Para obtener sugerencias y trucos de Purge Utility, consulte el artículo de Adobe Developer Connection sobre [Depuración de procesos y trabajos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuración de los servicios de informes de procesos {#configuring-process-reporting-services}

### Programar la publicación de datos de proceso {#schedule-process-data-publishing}

Los servicios de Process Reporting publican los datos de la base de datos de AEM Forms en el repositorio de Process Reporting de forma programada.

Esta operación puede requerir muchos recursos y puede afectar al rendimiento de los servidores de AEM Forms. Se recomienda programarlo fuera de los espacios horarios ocupados del servidor de AEM Forms.

De forma predeterminada, la publicación de datos está programada para ejecutarse todos los días a las 2 de la mañana.

Siga estos pasos para cambiar la programación de publicación:

>[!NOTE]
>
>Si está ejecutando la implementación de AEM Forms en un clúster, realice los siguientes pasos en cada nodo del clúster.

1. Detenga la instancia del servidor de AEM Forms.
1. &#x200B;

   * (Para Windows) Abra el `[JBoss root]/bin/run.conf.bat` en un editor.
   * (Para Linux, AIX y Solaris) `[JBoss root]/bin/run.conf.sh` en un editor.

1. Añadir el argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Ejemplo: La siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Guarde y cierre el archivo `run.conf.bat`.

1. Reinicie la instancia del servidor de AEM Forms.

1. Detenga la instancia del servidor de AEM Forms.
1. Inicie sesión en la Consola Administrativa de WebSphere. En el árbol de navegación, haga clic en **Servidores** > **Servidores de aplicaciones** y, a continuación, en el panel derecho, haga clic en el nombre del servidor.

1. En Infraestructura de servidor, haga clic en **Java y administración de procesos** > **Definición del proceso**.

1. En Propiedades adicionales, haga clic en **Máquina virtual Java**.

   En el cuadro Argumentos genéricos de JVM, añada el argumento `-Dreporting.publisher.cron = <expression>.`

   **Ejemplo**: La siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Aplicar**, haga clic en Aceptar y, a continuación, haga clic en **Guardar directamente en la configuración maestra**.
1. Reinicie la instancia del servidor de AEM Forms.
1. Detenga la instancia del servidor de AEM Forms.
1. Inicie sesión en la consola de administración de WebLogic. La dirección predeterminada de la Consola de administración de WebLogic es `https://[hostname]:[port]/console`.
1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura del dominio, haga clic en **Entorno** > **Servidores** y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en el botón **Configuración** pestaña > **Inicio del servidor** pestaña .
1. En el cuadro Argumentos, añada el argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Ejemplo**: La siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Guardar** y haga clic en **Activar cambios**.
1. Reinicie la instancia del servidor de AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servicio ProcessDataStorage {#processdatastorage-service}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

En cada ciclo de publicación, los datos se guardan en subcarpetas de una carpeta raíz predefinida.

Puede utilizar la consola de administración para configurar la raíz (**default**: `/content/reporting/pm`) ubicación y subcarpeta (**default**: `/yyyy/mm/dd/hh/mi/ss`) formato de jerarquía en el que se almacenarían los datos de proceso.

#### Para configurar las ubicaciones del repositorio de Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Iniciar sesión en **Consola de administración** con credenciales de administrador. La dirección URL predeterminada de la Consola de administración es `https://'[server]:[port]'/adminui`
1. Vaya a **Página principal** > **Servicios** > **Aplicaciones y servicios** >**Administración de servicios** y abra el **ProcessDataStorageProvider** servicio.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **CarpetaRaíz**

   Ubicación CRX dentro de la cual se almacenarán los datos del proceso para la creación de informes.

   `Default`: `/content/reporting/pm`

   **Jerarquía de carpetas**

   La jerarquía de carpetas dentro de la cual se almacenarán los datos de proceso en función del tiempo de creación del proceso.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Haga clic en **Guardar**.

### Servicio ReportConfiguration {#reportconfiguration-service}

Process Reporting utiliza el servicio ReportConfiguration para configurar el servicio de consulta de informes de procesos.

#### Para configurar el servicio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Iniciar sesión en **Administrador de configuración** con credenciales de administrador CRX. La dirección URL predeterminada del Administrador de configuración es `https://'[server]:[port]'/lc/system/console/configMgr`
1. Abra el **Configuración de informes** servicio.
1. **Número de registros**

   Al ejecutar una consulta en el repositorio, un resultado puede contener potencialmente un gran número de registros. Si el conjunto de resultados es grande, la ejecución de la consulta puede consumir recursos del servidor.

   Para gestionar grandes conjuntos de resultados, el servicio ReportConfiguration divide el procesamiento de consultas en lotes de registros. Esto reduce la carga del sistema.

   `Default`: `1000`

   **Ruta de almacenamiento CRX**

   Ubicación CRX dentro de la cual se almacenarán los datos del proceso para la creación de informes.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Esta es la misma ubicación que se especifica en la opción de configuración ProcessDataStorage **Carpeta raíz**.
   >
   >
   >Si actualiza la opción Carpeta raíz en la configuración de ProcessDataStorage, debe actualizar la ubicación de Ruta de almacenamiento CRX en el servicio ReportConfiguration.

1. Haga clic en **Guardar** y cerrar **Administrador de configuración CQ**.

### Servicio ProcessDataPublisher {#processdatapublisher-service}

El servicio ProcessDataPublisher importa datos de proceso de la base de datos de AEM Forms y publica los datos en el servicio ProcessDataStorageProvider para su almacenamiento.

#### Para configurar el servicio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Iniciar sesión en **Consola de administración** con credenciales de administrador.

   El URL predeterminado es `https://'server':port]/adminui/`.

1. Vaya a **Página principal** > **Servicios** > **Aplicaciones y servicios** >**Administración de servicios** y abra el **ProcessDataPublisher** servicio.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar datos**

Active esta opción para iniciar el proceso de publicación de datos. De forma predeterminada, la opción está desactivada.

Habilite Informes de procesos solo cuando todas las configuraciones relacionadas con los componentes de Informes de procesos estén correctamente configuradas.

También puede utilizar esta opción para desactivar la publicación de datos de proceso cuando ya no sea necesaria.

`Default`: `Off`

**Intervalo de lotes (s)**

Cada vez que se ejecuta el servicio ProcessDataPublisher, el servicio divide por primera vez el tiempo desde la última ejecución del servicio por el intervalo de lotes. A continuación, el servicio procesa cada intervalo de datos de AEM Forms por separado.

Esto ayuda a controlar el tamaño de los datos que el editor procesa de principio a fin durante cada ejecución (por lotes) dentro de un ciclo.

Por ejemplo, si el editor se ejecuta todos los días, en lugar de procesar todos los datos durante un día en una sola ejecución, de forma predeterminada divide el procesamiento en 24 lotes de una hora cada uno.

`Default`: `3600`

`Unit`: `Seconds`

**Tiempo de espera de bloqueo (s)**

El servicio de editor adquiere un bloqueo cuando comienza a procesar datos para que varias instancias del editor no empiecen a ejecutar y procesar datos simultáneamente.

Si un servicio de editor que ha adquirido un bloqueo está inactivo durante el número de segundos definido por el valor Bloquear tiempo de espera, se libera su bloqueo para que otras instancias del servicio de editor puedan continuar procesándose.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar datos de**

El entorno de AEM Forms contiene datos desde el momento en que se configuró el entorno.

De forma predeterminada, el servicio ProcessDataPublisher importa todos los datos de la base de datos de AEM Forms.

Según sus necesidades de creación de informes, si planea ejecutar informes y consultas sobre datos después de una fecha y hora determinadas, se recomienda especificar la fecha y la hora. El servicio de publicación publicará la fecha a partir de ese momento.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acceso a la interfaz de usuario de Process Reporting {#accessing-the-process-reporting-user-interface}

La interfaz de usuario de Informes de procesos se basa en el explorador.

Después de configurar los informes de procesos, puede empezar a trabajar con ellos en la siguiente ubicación de la instalación de AEM Forms:

`https://<server>:<port>/lc/pr`

### Inicio de sesión en Informes de procesos {#log-in-to-process-reporting}

Cuando vaya a la URL de informes de proceso (https://)&lt;server>:&lt;port>/lc/pr), se muestra la pantalla de inicio de sesión.

Especifique las credenciales para iniciar sesión en el módulo Informes de procesos.

>[!NOTE]
>
>Para iniciar sesión en la interfaz de usuario de Process Reporting, necesita el siguiente permiso de AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Inicio de sesión en Informes de procesos](assets/capture1_new.png)

Cuando inicia sesión en Informes de procesos, la variable **[!UICONTROL Página principal]** se abre.

### Pantalla principal de Informes de procesos {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Vista del árbol de informes de procesos:** La vista de árbol a la izquierda de la pantalla principal contiene los elementos para los módulos de Process Reporting.

La vista de árbol consta de los siguientes elementos de nivel superior:

**Informes:** Este elemento contiene los informes predeterminados que se envían con los informes de procesos.

Para obtener más información sobre los informes predefinidos, consulte [Informes predefinidos en proceso de informes](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Consultas ad hoc:** Este elemento contiene opciones para realizar búsquedas basadas en filtros para procesos y tareas.

Para obtener más información sobre consultas ad hoc, consulte [Informes de consultas ad hoc en proceso](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** El nodo Personalizado muestra los informes personalizados que ha creado.

Para ver el procedimiento para crear y mostrar informes personalizados, consulte [Informes personalizados en proceso de informes](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título de Procesamiento de informes:** La barra de título Procesamiento de informes contiene algunas opciones genéricas que puede utilizar al trabajar en la interfaz de usuario.

**Título de los informes de proceso:** El título Informes de procesos se muestra en la esquina izquierda de la barra de título.

Haga clic en el título en cualquier momento para volver a la pantalla de inicio.

**Hora de la última actualización:** Los datos de proceso se publican desde la base de datos de AEM Forms en el repositorio de informes de procesos de forma programada.

La hora de la última actualización muestra la última fecha y hora hasta la que se insertaron las actualizaciones de datos en el repositorio de informes de procesos.

Para obtener más información sobre el servicio de publicación de datos y cómo programar este servicio, consulte [Programar la publicación de datos de proceso](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) en el artículo Introducción a los informes de procesos .

**Usuario de Process Reporting:** El nombre de usuario que ha iniciado sesión se muestra a la derecha de Última actualización.

**Lista desplegable de la barra de título del sistema de informes de procesos:** La lista desplegable situada en la esquina derecha de la barra de título Procesar informes contiene las siguientes opciones:

* **[!UICONTROL Sincronización]**: Sincronice el repositorio de informes de procesos incrustado con la base de datos de AEM Forms.
* **[!UICONTROL Ayuda]**: Vea la documentación de ayuda sobre los informes de procesos.
* **[!UICONTROL Cerrar sesión]**: Cerrar sesión en Informes de procesos
