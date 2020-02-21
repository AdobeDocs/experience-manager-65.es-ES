---
title: Introducción a los informes de procesos
seo-title: Introducción a los informes de procesos
description: Pasos que debe seguir para empezar a utilizar AEM Forms en los informes de procesos JEE
seo-description: Pasos que debe seguir para empezar a utilizar AEM Forms en los informes de procesos JEE
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Introducción a los informes de procesos{#getting-started-with-process-reporting}

Los informes de proceso permiten a los usuarios de AEM Forms consultar información sobre los procesos de AEM Forms que están definidos actualmente en la implementación de AEM Forms. Sin embargo, Process Reporting no tiene acceso a los datos directamente desde el repositorio de AEM Forms. Los datos se publican primero en el repositorio de Process Reporting de forma programada (*por los* servicios ProcessDataPublisher y ProcessDataStorage). Los informes y las consultas de Informes de procesos se generan a partir de los datos de Informes de procesos publicados en el repositorio. Process Reporting se instala como parte del módulo Flujo de trabajo de Forms.

En este artículo se detallan los pasos para permitir la publicación de datos de AEM Forms en el repositorio de Process Reporting. Después de lo cual, podrá utilizar Informes de procesos para ejecutar informes y consultas. El artículo también cubre las opciones disponibles para configurar los servicios de informes de procesos.

## Requisitos previos de informes de procesos {#process-reporting-pre-requisites}

### Purgar procesos no esenciales {#purge-non-essential-processes}

Si actualmente utiliza Forms Workflow, la base de datos de AEM Forms puede contener una gran cantidad de datos

Los servicios de publicación de Process Reporting publicarán todos los datos de AEM Forms disponibles actualmente en la base de datos. Esto implica que si la base de datos contiene datos heredados sobre los que no desea ejecutar informes y consultas, todos esos datos también se publicarán en el repositorio aunque no se requieran para los informes. Se recomienda depurar estos datos antes de ejecutar los servicios para publicar los datos en el repositorio de informes de procesos. Esto mejorará el rendimiento tanto del servicio de publicador como del servicio que realiza la consulta de los datos para los informes.

Para obtener más información sobre la depuración de datos de proceso de AEM Forms, consulte [Depuración de datos](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)de proceso.

>[!NOTE]
>
>Para obtener sugerencias y trucos sobre la herramienta de depuración, consulte el artículo de Adobe Developer Connection sobre la [depuración de procesos y trabajos](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuración de los servicios de informes de procesos {#configuring-process-reporting-services}

### Programar la publicación de datos de proceso {#schedule-process-data-publishing}

Los servicios de informes de procesos publican datos de la base de datos de AEM Forms en el repositorio de informes de procesos de forma programada.

Esta operación puede requerir muchos recursos y puede afectar al rendimiento de los servidores de AEM Forms. Se recomienda programar esto fuera de los espacios de tiempo ocupados del servidor de AEM Forms.

De forma predeterminada, la publicación de datos está programada para ejecutarse todos los días a las 2:00 a.m.

Realice los siguientes pasos para cambiar la programación de publicación:

>[!NOTE]
>
>Si ejecuta la implementación de AEM Forms en un clúster, lleve a cabo los siguientes pasos en cada nodo del clúster.

1. Detenga la instancia de servidor de AEM Forms.
1. &#x200B;

   * (Para Windows) Abra el `[JBoss root]/bin/run.conf.bat` archivo en un editor.
   * (Para Linux, AIX y Solaris) `[JBoss root]/bin/run.conf.sh` en un editor.

1. Agregar el argumento JVM `-Dreporting.publisher.cron = <expression>.`

   Ejemplo: La siguiente expresión cron hace que Process Reporting publique datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Guarde y cierre el `run.conf.bat` archivo.

1. Reinicie la instancia de servidor de AEM Forms.

1. Detenga la instancia de servidor de AEM Forms.
1. Inicie sesión en la Consola administrativa de WebSphere. En el árbol de navegación, haga clic en **Servidores** > Servidores **** de aplicaciones y, a continuación, en el panel derecho, haga clic en el nombre del servidor.

1. En Infraestructura de servidor, haga clic en **Java y Administración** de procesos > Definición **de proceso**.

1. En Propiedades adicionales, haga clic en **Java Virtual Machine**.

   En el cuadro de argumentos JVM genérico, agregue el argumento `-Dreporting.publisher.cron = <expression>.`

   **Ejemplo**: La siguiente expresión cron hace que Process Reporting publique datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Aplicar**, en Aceptar y, a continuación, en **Guardar directamente en la configuración** maestra.
1. Reinicie la instancia de servidor de AEM Forms.
1. Detenga la instancia de servidor de AEM Forms.
1. Inicie sesión en la Consola de administración de WebLogic. La dirección predeterminada de la Consola de administración de WebLogic es `https://[hostname]:[port]/console`.
1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura de dominio, haga clic en **Entorno** > **Servidores** y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la pantalla siguiente, haga clic en la ficha **Configuración** > Inicio **** del servidor.
1. En el cuadro Argumentos, agregue el argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Ejemplo**: La siguiente expresión cron hace que Process Reporting publique datos de AEM Forms en el repositorio de Process Reporting cada 5 horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Guardar** y, a continuación, en **Activar cambios**.
1. Reinicie la instancia de servidor de AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servicio ProcessDataStorage {#processdatastorage-service}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

En cada ciclo de publicación, los datos se guardan en subcarpetas de una carpeta raíz predefinida.

Puede utilizar la consola de administración para configurar la raíz (**predeterminada**: `/content/reporting/pm`) ubicación y subcarpeta (**predeterminado**: `/yyyy/mm/dd/hh/mi/ss`) formato de jerarquía donde se almacenarán los datos del proceso.

#### Para configurar las ubicaciones del repositorio de Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Inicie sesión en **la Consola** de administración con las credenciales del administrador. La dirección URL predeterminada de la Consola de administración es `https://[server]:[port]/adminui`
1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** > Administración **** de servicios y abra el servicio **ProcessDataStorageProvider** .

   ![proceso-data-storage-service](assets/process-data-storage-service.png)

   **CarpetaRaíz**

   Ubicación de CRX dentro de la cual se almacenarán los datos del proceso para los informes.

   `Default`: `/content/reporting/pm`

   **Jerarquía de carpetas**

   La jerarquía de carpetas dentro de la cual se almacenarán los datos del proceso en función del tiempo de creación del proceso.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Haga clic en **Guardar**.

### Servicio ReportConfiguration {#reportconfiguration-service}

Process Reporting utiliza el servicio ReportConfiguration para configurar el servicio de consulta de informes de procesos.

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. Inicie sesión en **Configuration Manager** con las credenciales de administrador de CRX. La dirección URL predeterminada de Configuration Manager es `https://[server]:[port]/lc/system/console/configMgr`
1. Abra el servicio **ReportingConfiguration** .
1. **Número de registros**

   Al ejecutar una consulta en el repositorio, un resultado puede contener un gran número de registros. Si el conjunto de resultados es grande, la ejecución de la consulta puede consumir recursos del servidor.

   Para administrar grandes conjuntos de resultados, el servicio ReportConfiguration divide el procesamiento de consultas en lotes de registros. Esto reduce la carga del sistema.

   `Default`: `1000`

   **Ruta de almacenamiento CRX**

   Ubicación de CRX dentro de la cual se almacenarán los datos del proceso para los informes.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Es la misma ubicación que se especifica en la opción de configuración ProcessDataStorage **Carpeta** raíz.
   >
   >
   >Si actualiza la opción Carpeta raíz en la configuración ProcessDataStorage, debe actualizar la ubicación de Ruta de almacenamiento CRX en el servicio ReportConfiguration.

1. Haga clic en **Guardar** y cierre **CQ Configuration Manager**.

### Servicio ProcessDataPublisher {#processdatapublisher-service}

El servicio ProcessDataPublisher importa datos de proceso de la base de datos de AEM Forms y publica los datos en el servicio ProcessDataStorageProvider para almacenamiento.

#### Para configurar el servicio ProcessDataPublisher {#to-configure-processdatapublisher-service-nbsp}

1. Inicie sesión en **la Consola** de administración con las credenciales del administrador.

   La dirección URL predeterminada es `https://[server]:port]/adminui/`.

1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** >**Administración** de servicios y abra el servicio **ProcessDataPublisher** .

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publicar datos**

Active esta opción para iniciar la publicación de datos del proceso. De forma predeterminada, la opción está desactivada.

Habilite Informes de procesos sólo cuando todas las configuraciones relacionadas con los componentes de Informes de procesos estén configuradas correctamente.

Como alternativa, utilice esta opción para desactivar la publicación de datos de proceso cuando ya no sea necesario.

`Default`: `Off`

**Intervalo de lote (s)**

Cada vez que se ejecuta el servicio ProcessDataPublisher, el servicio divide por primera vez el tiempo transcurrido desde la última ejecución del servicio mediante el intervalo de lotes. A continuación, el servicio procesa cada intervalo de datos de AEM Forms por separado.

Esto ayuda a controlar el tamaño de los datos que el editor procesa de punta a punta durante cada ejecución (por lotes) dentro de un ciclo.

Por ejemplo, si el editor se ejecuta todos los días, en lugar de procesar todos los datos durante un día en una sola ejecución, se divide de forma predeterminada el procesamiento en 24 lotes de una hora cada uno.

`Default`: `3600`

`Unit`: `Seconds`

**Tiempo de espera de bloqueo (s)**

El servicio de editor adquiere un bloqueo cuando comienza a procesar datos para que varias instancias del editor no comiencen a ejecutar y a procesar datos simultáneamente.

Si un servicio de publicador ha adquirido un bloqueo, permanece inactivo durante el número de segundos definido por el valor de tiempo de espera de bloqueo, se libera el bloqueo para que otras instancias del servicio de publicador puedan continuar el procesamiento.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar datos de**

El entorno de AEM Forms contiene datos del momento en que se configuró el entorno.

De forma predeterminada, el servicio ProcessDataPublisher importa todos los datos de la base de datos de AEM Forms.

Según sus necesidades de informes, si planea ejecutar informes y consultas sobre datos después de una fecha y hora determinadas, se recomienda especificar la fecha y la hora. El servicio de publicación publicará la fecha a partir de ese momento.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acceso a la interfaz de usuario de Process Reporting {#accessing-the-process-reporting-user-interface}

La interfaz de usuario de Process Reporting se basa en el explorador.

Una vez configurados los informes de procesos, puede empezar a trabajar con ellos en la siguiente ubicación de la instalación de AEM Forms:

`https://<server>:<port>/lc/pr`

### Inicio de sesión en Process Reporting {#log-in-to-process-reporting}

Cuando se desplaza a la URL de informes de proceso (https://&lt;server>:&lt;port>/lc/pr), se muestra la pantalla de inicio de sesión.

Especifique sus credenciales para iniciar sesión en el módulo de informes de procesos.

>[!NOTE]
>
>Para iniciar sesión en la interfaz de usuario de Process Reporting, necesita el siguiente permiso de AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Informes de inicio de sesión en proceso](assets/capture1_new.png)

Cuando inicia sesión en Process Reporting, aparece la pantalla **[!UICONTROL Inicio]** .

### Pantalla de inicio de informes de procesos {#process-reporting-home-screen}

![process-reporting-home screen](assets/process-reporting-home-screen.png)

**** Vista del árbol de informes de procesos: La vista de árbol a la izquierda de la pantalla de inicio contiene los elementos para los módulos de informes de procesos.

La vista de árbol consta de los siguientes elementos de nivel superior:

**** Informes: Este elemento contiene los informes predeterminados que se envían con Informes de procesos.

Para obtener más información sobre los informes predefinidos, consulte Informes [predefinidos en informes](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)de proceso.

**** Consultas ad hoc: Este elemento contiene opciones para realizar búsquedas basadas en filtros para procesos y tareas.

Para obtener más información sobre consultas ad hoc, consulte Consultas [ad-hoc en informes](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)de procesos.

**** Personalizado: El nodo Personalizado muestra los informes personalizados que usted crea.

Para ver el procedimiento para crear y mostrar informes personalizados, consulte Informes [personalizados en informes](/help/forms/using/process-reporting/process-reporting-custom-reports.md)de proceso.

**** Barra de título de informes de procesos: La barra de título de Informes de procesos contiene algunas opciones genéricas que puede utilizar al trabajar en la interfaz de usuario.

**** Título de informe de procesos: El título Informe de procesos se muestra en la esquina izquierda de la barra de título.

Haga clic en el título en cualquier momento para volver a la pantalla de inicio.

**** Hora de la última actualización: Los datos de proceso se publican de forma programada desde la base de datos de AEM Forms al repositorio de informes de procesos.

La hora de la última actualización muestra la última fecha y hora hasta la cual se insertaron las actualizaciones de datos en el repositorio de informes de procesos.

Para obtener más información sobre el servicio de publicación de datos y cómo programar este servicio, consulte [Programar la publicación](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) de datos de procesos en el artículo Introducción a los informes de procesos.

**** Usuario de Process Reporting: El nombre de usuario que ha iniciado sesión se muestra a la derecha de la hora de la última actualización.

**** Lista desplegable de la barra de título de informes de procesos: La lista desplegable situada en la esquina derecha de la barra de título Procesar informes contiene las siguientes opciones:

* **[!UICONTROL Sincronizar]**: Sincronice el repositorio de informes de procesos incrustado con la base de datos de AEM Forms.
* **[!UICONTROL Ayuda]**: Consulte la documentación de la Ayuda sobre los informes de procesos.
* **[!UICONTROL Cerrar sesión]**: Cerrar sesión en los informes de proceso

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
