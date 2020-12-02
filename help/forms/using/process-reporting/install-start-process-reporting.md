---
title: Introducción a Process Sistema de informes
seo-title: Introducción a Process Sistema de informes
description: Los pasos que debe seguir para empezar a usar AEM Forms en el Sistema de informes de procesos JEE
seo-description: Los pasos que debe seguir para empezar a usar AEM Forms en el Sistema de informes de procesos JEE
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Introducción a Process Sistema de informes{#getting-started-with-process-reporting}

El Sistema de informes de procesos permite a los usuarios de AEM Forms obtener información de consulta sobre los procesos de AEM Forms que se definen actualmente en la implementación de AEM Forms. Sin embargo, Process Sistema de informes no accede a los datos directamente desde el repositorio de AEM Forms. Los datos se publican primero en el repositorio de Process Sistema de informes de forma programada (*por el servicio ProcessDataPublisher y ProcessDataStorage* s). Los informes y consultas en el Sistema de informes de proceso se generan a partir de los datos de Sistema de informes de proceso publicados en el repositorio. El Sistema de informes de procesos se instala como parte del módulo Forms Workflow.

Este artículo detalla los pasos para habilitar la publicación de datos de AEM Forms en el repositorio de Process Sistema de informes. Después de lo cual, podrá utilizar Process Sistema de informes para ejecutar informes y consultas. El artículo también cubre las opciones disponibles para configurar los servicios de Sistema de informes de procesos.

## Requisitos previos de Sistema de informes de procesos {#process-reporting-pre-requisites}

### Purgar procesos no esenciales {#purge-non-essential-processes}

Si actualmente está utilizando Forms Workflow, la base de datos de AEM Forms puede contener una gran cantidad de datos

Los servicios de publicación de Process Sistema de informes publicarán todos los datos de AEM Forms disponibles actualmente en la base de datos. Esto implica que, si la base de datos contiene datos heredados sobre los que no desea ejecutar informes y consultas, todos esos datos también se publicarán en el repositorio aunque no sean necesarios para el sistema de informes. Se recomienda depurar estos datos antes de ejecutar los servicios para publicar los datos en el repositorio de Process Sistema de informes. Esto mejorará el rendimiento tanto del servicio del editor como del servicio que consulta los datos para el sistema de informes.

Para obtener más información sobre la depuración de datos de procesos de AEM Forms, consulte [Depuración de datos de procesos](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Para obtener sugerencias y trucos de la utilidad de depuración, consulte el artículo de Adobe Developer Connection sobre [Depuración de procesos y trabajos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuración de los servicios de Sistema de informes de procesos {#configuring-process-reporting-services}

### Programar la publicación de datos del proceso {#schedule-process-data-publishing}

Los servicios de Sistema de informes de procesos publican datos de la base de datos de AEM Forms en el repositorio de Process Sistema de informes de forma programada.

Esta operación puede requerir muchos recursos y puede afectar al rendimiento de los servidores AEM Forms. Se recomienda programar esto fuera de los espacios de tiempo ocupados del servidor de AEM Forms.

De forma predeterminada, la publicación de datos está programada para ejecutarse todos los días a las 2:00 a.m.

Realice los siguientes pasos para cambiar la programación de publicación:

>[!NOTE]
>
>Si está ejecutando la implementación de AEM Forms en un clúster, lleve a cabo los siguientes pasos en cada nodo del clúster.

1. Detenga la instancia del servidor de AEM Forms.
1. &#x200B;

   * (Para Windows) Abra el archivo `[JBoss root]/bin/run.conf.bat` en un editor.
   * (Para Linux, AIX y Solaris) `[JBoss root]/bin/run.conf.sh` en un editor.

1. Añadir el argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Ejemplo: La siguiente expresión cron hace que Process Sistema de informes publique datos de AEM Forms en el repositorio de Process Sistema de informes cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Guarde y cierre el archivo `run.conf.bat`.

1. Reinicie la instancia del servidor de AEM Forms.

1. Detenga la instancia del servidor de AEM Forms.
1. Inicie sesión en la Consola administrativa de WebSphere. En el árbol de navegación, haga clic en **Servidores** > **Servidores de aplicaciones** y, a continuación, en el panel derecho, haga clic en el nombre del servidor.

1. En Infraestructura de servidor, haga clic en **Administración de procesos y Java** > **Definición de proceso**.

1. En Propiedades adicionales, haga clic en **Máquina virtual Java**.

   En el cuadro de argumentos JVM genérico, agregue el argumento `-Dreporting.publisher.cron = <expression>.`

   **Ejemplo**: La siguiente expresión cron hace que Process Sistema de informes publique datos de AEM Forms en el repositorio de Process Sistema de informes cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Aplicar**, haga clic en Aceptar y, a continuación, haga clic en **Guardar directamente en la configuración maestra**.
1. Reinicie la instancia del servidor de AEM Forms.
1. Detenga la instancia del servidor de AEM Forms.
1. Inicie sesión en la Consola de administración de WebLogic. La dirección predeterminada de la Consola de administración de WebLogic es `https://[hostname]:[port]/console`.
1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura de dominio, haga clic en **Entorno** > **Servidores** y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la pantalla siguiente, haga clic en la ficha **Configuración** > **Inicio del servidor**.
1. En el cuadro Argumentos, agregue el argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Ejemplo**: La siguiente expresión cron hace que Process Sistema de informes publique datos de AEM Forms en el repositorio de Process Sistema de informes cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Guardar** y, a continuación, haga clic en **Activar cambios**.
1. Reinicie la instancia del servidor de AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servicio ProcessDataStorage {#processdatastorage-service}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Sistema de informes.

En cada ciclo de publicación, los datos se guardan en subcarpetas de una carpeta raíz predefinida.

Puede utilizar la consola de administración para configurar la raíz (**default**: `/content/reporting/pm`) ubicación y subcarpeta (**predeterminado**: `/yyyy/mm/dd/hh/mi/ss`) formato de jerarquía donde se almacenarían los datos del proceso.

#### Para configurar las ubicaciones del repositorio de Process Sistema de informes {#to-configure-the-process-reporting-repository-locations}

1. Inicie sesión en **Consola de administración** con credenciales de administrador. La dirección URL predeterminada de la Consola de administración es `https://'[server]:[port]'/adminui`
1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** >**Administración de servicios** y abra el servicio **ProcessDataStorageProvider**.

   ![process-data-almacenamiento-service](assets/process-data-storage-service.png)

   **CarpetaRaíz**

   Ubicación de CRX dentro de la cual se almacenarán los datos del proceso para su sistema de informes.

   `Default`: `/content/reporting/pm`

   **Jerarquía de carpetas**

   La jerarquía de carpetas dentro de la cual se almacenarán los datos del proceso en función del tiempo de creación del proceso.

   `Default`::  `/yyyy/mm/dd/hh/mi/ss`

1. Haga clic en **Guardar**.

### Servicio ReportConfiguration {#reportconfiguration-service}

Process Sistema de informes utiliza el servicio ReportConfiguration para configurar el servicio de consulta de sistema de informes de procesos.

#### Para configurar el servicio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Inicie sesión en **Configuration Manager** con las credenciales de administrador de CRX. La dirección URL predeterminada de Configuration Manager es `https://'[server]:[port]'/lc/system/console/configMgr`
1. Abra el servicio **ReportingConfiguration**.
1. **Número de registros**

   Al ejecutar una consulta en el repositorio, un resultado puede contener un gran número de registros. Si el conjunto de resultados es grande, la ejecución de la consulta puede consumir recursos del servidor.

   Para administrar grandes conjuntos de resultados, el servicio ReportConfiguration divide el procesamiento de consultas en lotes de registros. Esto reduce la carga del sistema.

   `Default`::  `1000`

   **Ruta de Almacenamiento CRX**

   Ubicación de CRX dentro de la cual se almacenarán los datos del proceso para su sistema de informes.

   `Default`::  `/content/reporting/pm`

   >[!NOTE]
   >
   >Es la misma ubicación que se especifica en la opción de configuración ProcessDataStorage **Carpeta raíz**.
   >
   >
   >Si actualiza la opción Carpeta raíz en la configuración ProcessDataStorage, debe actualizar la ubicación de Ruta de Almacenamiento CRX en el servicio ReportConfiguration.

1. Haga clic en **Guardar** y cierre **CQ Configuration Manager**.

### Servicio ProcessDataPublisher {#processdatapublisher-service}

El servicio ProcessDataPublisher importa datos de proceso de la base de datos de AEM Forms y publica los datos en el servicio ProcessDataStorageProvider para almacenamiento.

#### Para configurar el servicio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Inicie sesión en **Consola de administración** con credenciales de administrador.

   La dirección URL predeterminada es `https://'server':port]/adminui/`.

1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** >**Administración de servicios** y abra el servicio **ProcessDataPublisher**.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar datos**

Active esta opción para inicio de datos del proceso de publicación. De forma predeterminada, la opción está desactivada.

Active Procesar Sistema de informes sólo cuando todas las configuraciones relacionadas con los componentes de Process Sistema de informes estén configuradas correctamente.

Como alternativa, utilice esta opción para desactivar la publicación de datos de proceso cuando ya no sea necesario.

`Default`::  `Off`

**Intervalo de lote (s)**

Cada vez que se ejecuta el servicio ProcessDataPublisher, el servicio divide por primera vez el tiempo transcurrido desde la última ejecución del servicio mediante el intervalo de lotes. A continuación, el servicio procesa cada intervalo de datos de AEM Forms por separado.

Esto ayuda a controlar el tamaño de los datos que el editor procesa de punta a punta durante cada ejecución (por lotes) dentro de un ciclo.

Por ejemplo, si el editor se ejecuta todos los días, en lugar de procesar todos los datos durante un día en una sola ejecución, se divide de forma predeterminada el procesamiento en 24 lotes de una hora cada uno.

`Default`::  `3600`

`Unit`::  `Seconds`

**Tiempo de espera de bloqueo (s)**

El servicio de editor adquiere un bloqueo cuando inicio el procesamiento de datos para que varias instancias del editor no inicio la ejecución y el procesamiento simultáneo de datos.

Si un servicio de publicador ha adquirido un bloqueo, permanece inactivo durante el número de segundos definido por el valor de tiempo de espera de bloqueo, se libera el bloqueo para que otras instancias del servicio de publicador puedan continuar el procesamiento.

`Default`::  `3600`

`Unit`::  `Seconds`

**Publicar datos de**

AEM Forms entorno contiene datos del momento en que se configuró el entorno.

De forma predeterminada, el servicio ProcessDataPublisher importa todos los datos de la base de datos de AEM Forms.

Según las necesidades de su sistema de informes, si planea ejecutar informes y consultas en datos después de una fecha y hora determinadas, se recomienda especificar la fecha y la hora. El servicio de publicación publicará la fecha a partir de ese momento.

`Default`::  `01-01-1970 00:00:00`

`Format`::  `dd-MM-yyyy HH:mm:ss`

## Acceso a la interfaz de usuario de Process Sistema de informes {#accessing-the-process-reporting-user-interface}

La interfaz de usuario de Process Sistema de informes se basa en el explorador.

Después de configurar Process Sistema de informes, puede realizar inicios para trabajar con Process Sistema de informes en la siguiente ubicación de la instalación de AEM Forms:

`https://<server>:<port>/lc/pr`

### Inicie sesión en Process Sistema de informes {#log-in-to-process-reporting}

Cuando se desplaza a la URL de Process Sistema de informes (https://&lt;servidor>:&lt;puerto>/lc/pr), se muestra la pantalla de inicio de sesión.

Especifique las credenciales para iniciar sesión en el módulo Sistema de informes de procesos.

>[!NOTE]
>
>Para iniciar sesión en la interfaz de usuario de Process Sistema de informes, necesita el siguiente permiso de AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Iniciar sesión en el Sistema de informes de proceso](assets/capture1_new.png)

Cuando inicia sesión en Process Sistema de informes, se muestra la pantalla **[!UICONTROL Inicio]**.

### Pantalla inicial de Sistema de informes de procesos {#process-reporting-home-screen}

![process-sistema de informes-home-screen](assets/process-reporting-home-screen.png)

**Vista de árbol de Sistema de informes de proceso:** la vista de árbol en el lado izquierdo de la pantalla de inicio contiene los elementos para los módulos de Sistema de informes de proceso.

La vista de árbol consta de los siguientes elementos de nivel superior:

**Informes:** Este elemento contiene los informes predeterminados que se envían con Sistema de informes de proceso.

Para obtener más información sobre los informes predefinidos, consulte [Informes predefinidos en el Sistema de informes de proceso](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Consultas ad hoc:** Este elemento contiene opciones para realizar búsquedas basadas en filtros para procesos y tareas.

Para obtener más información sobre consultas ad hoc, consulte [Consultas ad-hoc en el Sistema de informes de procesos](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** El nodo Personalizado muestra los informes personalizados que se crean.

Para ver el procedimiento para crear y mostrar informes personalizados, consulte [Sistema de informes Informes personalizados en proceso](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título de Sistema de informes de proceso:** La barra de título de Sistema de informes de proceso contiene algunas opciones genéricas que puede utilizar al trabajar en la interfaz de usuario.

**Título del Sistema de informes de proceso:** el título del Sistema de informes de proceso se muestra en la esquina izquierda de la barra de título.

Haga clic en el título en cualquier momento para volver a la pantalla de inicio.

**Hora de la última actualización:** los datos del proceso se publican desde la base de datos de AEM Forms en el repositorio de Process Sistema de informes de forma programada.

La hora de la última actualización muestra la última fecha y hora hasta la cual se insertaron las actualizaciones de datos en el repositorio de Process Sistema de informes.

Para obtener más información sobre el servicio de publicación de datos y cómo programar este servicio, consulte [Programar la publicación de datos del proceso](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) en el artículo Introducción a Process Sistema de informes.

**Usuario de Sistema de informes de procesos:** El nombre de usuario que ha iniciado sesión se muestra a la derecha de la hora de la última actualización.

**Lista desplegable de la barra de título del Sistema de informes de procesos:** La lista desplegable situada en la esquina derecha de la barra de título del Sistema de informes de procesos contiene las siguientes opciones:

* **[!UICONTROL Sincronizar]**: Sincronice el repositorio de Process Sistema de informes incrustado con la base de datos de AEM Forms.
* **[!UICONTROL Ayuda]**: Vista de la documentación de la Ayuda sobre el Sistema de informes de procesos.
* **[!UICONTROL Cerrar sesión]**: Cerrar sesión de Sistema de informes de proceso
