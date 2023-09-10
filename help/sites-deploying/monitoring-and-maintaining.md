---
title: Supervisión y mantenimiento de su Adobe Experience Manager instancia
description: AEM Obtenga información sobre cómo monitorizar los.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: Configuring
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '5933'
ht-degree: 1%

---

# Supervisión y mantenimiento de la instancia de Adobe Experience Manager{#monitoring-and-maintaining-your-aem-instance}

AEM Una vez implementadas las instancias de, debe monitorizar y mantener su funcionamiento, rendimiento e integridad.

Un factor clave aquí es que para reconocer posibles problemas, debe saber cómo se ve y se comporta su sistema en condiciones normales. La mejor manera de conseguir esta capacidad es supervisar el sistema y recopilar información a lo largo del tiempo.

| Comprobación | Consideraciones | Comentario/acciones |
|---|---|---|
| Plan de respaldo. |  | Consulte cómo [Haga una copia de seguridad de su instancia](/help/sites-deploying/monitoring-and-maintaining.md#backups). |
| Plan de recuperación ante desastres. | Directrices de recuperación ante desastres de su empresa. |  |
| Hay disponible un sistema de seguimiento de errores para informar de problemas. | Por ejemplo, [Bugzilla](https://www.bugzilla.org/), [Jira](https://www.atlassian.com/software/jira), o uno de muchos otros. |  |
| Se están monitorizando los sistemas de archivos. | El repositorio CRX se &quot;bloquea&quot; si no hay suficiente espacio en disco. Se reanuda después de que haya espacio disponible. | &quot; `*ERROR* LowDiskSpaceBlocker`Los mensajes &quot; se pueden ver en el archivo de registro cuando hay poco espacio disponible. |
| [Archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) están siendo monitorizados. |  |  |
| La monitorización del sistema se está ejecutando (constantemente) en segundo plano. | Incluyendo uso de CPU, memoria, disco y red. Utilizando, por ejemplo, iostat / vmstat / perfmon. | Los datos registrados se visualizan y se pueden utilizar para rastrear problemas de rendimiento. También se puede acceder a los datos sin procesar. |
| [AEM Se está monitorizando el rendimiento de la](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | Incluyendo [Contadores de solicitudes](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) para controlar los niveles de tráfico. | Si se observa una pérdida de rendimiento significativa o a largo plazo, debe realizarse una investigación detallada. |
| Está monitorizando su [Agentes de replicación](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents). |  |  |
| Purgue instancias de flujo de trabajo con regularidad. | Tamaño del repositorio y rendimiento del flujo de trabajo. | Consulte [Depuración regular de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances). |

## Copias de seguridad {#backups}

Es recomendable realizar copias de seguridad de:

* Instalación del software: antes o después de realizar cambios significativos en la configuración
* El contenido incluido en el repositorio: con regularidad

Es probable que su compañía tenga una directiva de copia de seguridad que usted siga. Entre las consideraciones adicionales sobre qué y cuándo realizar copias de seguridad se incluyen las siguientes:

* qué tan críticos son el sistema y los datos.
* la frecuencia con la que se realizan cambios en el software o en los datos.
* volumen de datos; la capacidad puede ser ocasionalmente un problema, al igual que el tiempo para realizar la copia de seguridad.
* si la copia de seguridad se puede realizar mientras los usuarios están en línea y, si es posible, cuál es el impacto en el rendimiento.
* la distribución geográfica de los usuarios; es decir, ¿cuándo es el mejor momento para realizar copias de seguridad (para minimizar el impacto)?
* su política de recuperación ante desastres; ¿existen directrices sobre dónde deben almacenarse los datos de copia de seguridad (por ejemplo, fuera del sitio y en un medio específico)?

A menudo, se realiza una copia de seguridad completa a intervalos regulares (por ejemplo, diaria, semanal o mensual), con copias de seguridad incrementales intermedias (por ejemplo, por hora, diaria o semanal).

>[!CAUTION]
>
>Al implementar copias de seguridad de las instancias de producción, haga pruebas *debe* para garantizar que la copia de seguridad se pueda restaurar correctamente.
>
>Sin esta prueba, la copia de seguridad es potencialmente inútil (en el peor de los casos).

>[!NOTE]
>
>Para obtener más información sobre el rendimiento de las copias de seguridad, lea la [Rendimiento de backup](/help/sites-deploying/configuring-performance.md#backup-performance) sección.

### Copia de seguridad de la instalación del software {#backing-up-your-software-installation}

Después de la instalación o cambios significativos en la configuración, cree un copia de seguridad de la instalación del software.

Para llevar a cabo este tarea, [haga una copia de seguridad de todo su repositorio](#backing-up-your-repository) y luego:

1. Parada AEM.
1. Realizar copia de seguridad de todo `<cq-installation-dir>` desde el sistema de archivos.

>[!CAUTION]
>
>Si utiliza un servidor de aplicaciones de terceros, las carpetas adicionales pueden estar en una ubicación diferente y también se debe realizar una copia de seguridad de las mismas. Consulte [AEM Cómo instalar el servidor de aplicaciones con un servidor de aplicaciones de manera que se pueda instalar](/help/sites-deploying/application-server-install.md) para obtener información sobre la instalación de servidores de aplicaciones.

>[!CAUTION]
>
>Se admite la copia de seguridad incremental del almacén de datos de archivos; cuando utilice la copia de seguridad incremental para otros componentes (como el índice Lucene), asegúrese de que los archivos eliminados también estén marcados como eliminados en la copia de seguridad.

>[!NOTE]
>
>La duplicación de discos también se puede utilizar como mecanismo de copia de seguridad.

### Copia de seguridad del repositorio {#backing-up-your-repository}

El [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md) Esta sección de la documentación de CRX cubre todos los problemas relacionados con las copias de seguridad del repositorio CRX.

Para obtener más información sobre cómo realizar una copia de seguridad en línea &quot;activa&quot;, consulte [Creación de una copia de seguridad en línea](/help/sites-administering/backup-and-restore.md#online-backup).

## Depuración de versiones {#version-purging}

El **Purgar versiones** está diseñada para depurar las versiones de un nodo o una jerarquía de nodos en el repositorio. Su propósito principal es ayudarle a reducir el tamaño del repositorio eliminando las versiones antiguas de los nodos.

AEM Esta sección trata sobre las operaciones de mantenimiento relacionadas con la función de control de versiones de las versiones de los informes de la aplicación de. El **Purgar versión** está diseñada para depurar las versiones de un nodo o una jerarquía de nodos en el repositorio. Su propósito principal es ayudarle a reducir el tamaño del repositorio eliminando las versiones antiguas de los nodos.

### Información general {#overview}

El **Purgar versiones** está disponible como tarea de mantenimiento semanal. Antes de usar por primera vez, debe añadirse y luego configurarse. Después, se puede ejecutar bajo petición o de forma semanal.

### Depuración de versiones de un sitio Web {#purging-versions-of-a-web-site}

Para purgar versiones de un sitio web, siga estos pasos:

1. Vaya a **[Herramientas](/help/sites-administering/tools-consoles.md)** **consolar**, seleccione **Operación**, **Mantenimiento**, entonces **Ventana de mantenimiento semanal**.

1. Seleccionar **+ Agregar** en la barra de herramientas superior.

   ![Agregar purga de versión](assets/version-purge-add.png)

1. Seleccionar **Depuración de versión** en la lista desplegable de la **Añadir nueva tarea** diálogo. Entonces **Guardar**.

   ![Agregar purga de versión](assets/version-purge-add-new-task.png)

1. El **Depuración de versión** se ha añadido la tarea. Utilice las acciones de tarjeta para lo siguiente:
   * Seleccionar: muestra acciones adicionales en la barra de herramientas superior
   * Ejecutar: para ejecutar la depuración configurada inmediatamente
   * Configurar: para configurar la tarea de depuración semanal

   ![Acciones de purga de versiones](assets/version-purge-actions.png)

1. Seleccione el **Configurar** acción para abrir la consola web de **Tarea de depuración de versión de CQ WCM por día**, donde puede configurar:

   ![Configuración de purga de versiones](assets/version-purge-configuration.png)

   * **Purga de rutas**
Defina la ruta de inicio del contenido que se va a depurar; por ejemplo, `/content/wknd`.

     >[!CAUTION]
     >
     >El Adobe recomienda definir varias rutas para cada uno de los sitios web.
     >
     >La definición de una ruta con demasiados hijos puede alargar significativamente el tiempo para realizar la depuración.

   * **Purgar versiones de forma recursiva**

      * Anule la selección si solo desea depurar el nodo definido por la ruta.
      * Seleccione si desea depurar el nodo definido por la ruta y sus descendientes.

   * **Número máximo de versiones**
Establezca el número máximo de versiones (para cada nodo) que desea conservar. Dejar vacío para no utilizar esta configuración.

   * **Número mínimo de versiones**
Establezca el número mínimo de versiones (para cada nodo) que desea conservar. Dejar vacío para no utilizar esta configuración.

   * **Página de versión máxima**
Establezca la antigüedad máxima de la versión en días (para cada nodo) que desea mantener. Dejar vacío para no utilizar esta configuración.

   Entonces **Guardar**.

1. Navegar/volver a **Ventana de mantenimiento semanal** y seleccione **Ejecutar** para iniciar el proceso inmediatamente.

>[!CAUTION]
>
>Puede utilizar el cuadro de diálogo IU clásica para realizar una [Ejecución en seco](#analyzing-the-console) de la configuración:
>
>* http://localhost:4502/etc/versioning/purge.html
>
>Los nodos purgados no se pueden revertir sin restaurar el repositorio. Tenga cuidado con la configuración realizando siempre una ejecución en seco antes de purgar.

#### Ejecución en seco: Análisis de la consola {#analyzing-the-console}

La IU clásica proporciona un **Ejecución en seco** opción de:

* http://localhost:4502/etc/versioning/purge.html

El proceso enumera todos los nodos que se han procesado. Durante el proceso, un nodo puede tener uno de los siguientes estados:

* `ignore (not versionnable)`: el nodo no admite el control de versiones y se ignora durante el proceso.

* `ignore (no version)`: el nodo no tiene ninguna versión y se ignora durante el proceso.

* `retained`: el nodo no se depura.
* `purged`: el nodo se purga.

Además, la consola proporciona información útil sobre las versiones:

* `V 1.0`: el número de versión.
* `V 1.0.1`&#42;: la estrella indica que la versión es la versión actual (base) y que no se puede depurar.

* `Thu Mar 15 2012 08:37:32 GMT+0100`: la fecha de la versión.

En el ejemplo siguiente:

* Las **[!DNL Shirts]** versiones se depuran porque su antigüedad es superior a dos días.
* El **[!DNL Tonga Fashions!]** las versiones se purgan porque su número de versiones es mayor que 5.

![global_version_screenshot](assets/global_version_screenshot.png)

## Trabajar con registros de auditoría y archivos de registro {#working-with-audit-records-and-log-files}

Los registros de auditoría y los archivos de registro relacionados con Adobe Experience Manager AEM () se encuentran en varias ubicaciones. A continuación se proporciona una descripción general de lo que puede encontrar y dónde puede encontrarlo.

### Uso de registros {#working-with-logs}

AEM WCM registra registros detallados. Después de desempaquetar e iniciar Quickstart, podrá encontrar los registros en:

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### Rotación de archivo de registro {#log-file-rotation}

La rotación del archivo de registro hace referencia al proceso que limita el crecimiento del archivo creando un archivo periódicamente. AEM En, un archivo de registro llamado: `error.log` se gira una vez al día según las reglas dadas:

* El `error.log` se cambia el nombre del archivo según el patrón {original_filename} `.yyyy-MM-dd`. Por ejemplo, el 11 de julio de 2010, se cambia el nombre del archivo de registro actual `error.log-2010-07-10`, luego un nuevo `error.og` se ha creado.

* Los archivos de registro anteriores no se eliminan, por lo que es responsabilidad suya limpiar los archivos de registro antiguos periódicamente para limitar el uso del disco.

>[!NOTE]
>
>AEM AEM Si actualiza la instalación de la, cualquier archivo de registro existente que ya no utilice el usuario permanecerá en el disco. Puede eliminarlos sin riesgo. Todas las nuevas entradas de registro se escriben en los nuevos archivos de registro.

### Búsqueda de los archivos de registro {#finding-the-log-files}

AEM Varios archivos de registro se guardan en el servidor de archivos donde instaló la instalación de la siguiente manera:

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
AEM Todas las solicitudes de acceso al WCM de la y al repositorio se registran aquí.

   * `audit.log`
Las acciones de moderación se registran aquí.

   * `error.log`
Los mensajes de error (de diferentes niveles de gravedad) se registran aquí.

   * [`ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
Este registro solo se utiliza si [!DNL Dynamic Media] está activada. Proporciona estadísticas e información analítica utilizada para analizar el comportamiento del proceso interno de ImageServer.

   * `request.log`
Cada solicitud de acceso se registra aquí junto con la respuesta.

   * [`s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
Este registro solo se utiliza si [!DNL Dynamic Media] está activada. El registro de acceso de s7 registra cada solicitud realizada a [!DNL Dynamic Media] mediante `/is/image` y `/is/content`.

   * `stderr.log`
Contiene mensajes de error, de distinto nivel de gravedad, generados durante el inicio. De forma predeterminada, el nivel de registro se establece en `Warning` ( `WARN`)

   * `stdout.log`
Contiene mensajes de registro que indican eventos durante el inicio.

   * `upgrade.log`
Proporciona un registro de todas las operaciones de actualización que se ejecutan desde el `com.day.compat.codeupgrade` y `com.adobe.cq.upgradesexecutor` paquetes.

* `<cq-installation-dir>/crx-quickstart/repository/segmentstore`

   * `journal.log`
Información de diario de revisión.

>[!NOTE]
>
>Los registros de acceso de ImageServer y s7 no se incluyen en el paquete **Descargar ** completo&quot; generado desde la página **system/console/status-Bundlelist **. Para fines de soporte, si tiene [!DNL Dynamic Media] Cuando se produzcan problemas, añada los registros de acceso de ImageServer y s7 al ponerse en contacto con Asistencia al cliente.

### Activación del nivel de registro de depuración {#activating-the-debug-log-level}

El nivel de registro predeterminado ([Configuración de registro de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)) es Information, por lo que los mensajes de depuración no se registran.

Para activar el nivel de registro de depuración para un registrador, establezca la propiedad `org.apache.sling.commons.log.level` para depurar en el repositorio. Por ejemplo, el `/libs/sling/config/org.apache.sling.commons.log.LogManager` para configurar el [Registro global de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration).

>[!CAUTION]
>
>No deje el registro en el nivel de registro de depuración más tiempo del necesario, ya que genera numerosas entradas de registro que consumen recursos.

Una línea del archivo de depuración suele comenzar con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. AEM La instalación continúa, pero una parte de WCM no se instaló correctamente y no funciona. |
| 2 | Advertencia | La acción se realizó correctamente pero se encontraron problemas. AEM La WCM puede funcionar o no correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

### Crear un archivo de registro personalizado {#create-a-custom-log-file}

>[!NOTE]
>
>Al trabajar con Adobe Experience Manager, existen varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

En determinadas circunstancias, es posible que desee crear un archivo de registro personalizado con un nivel de registro diferente. En el repositorio, haga lo siguiente:

1. Si no existe, cree una carpeta de configuración ( `sling:Folder`) para su proyecto `/apps/<project-name>/config`.
1. En `/apps/<project-name>/config`, cree un nodo para el nuevo [Configuración del registrador de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration):

   * Nombre: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`

     Donde `<identifier>` se sustituye por texto libre que se debe introducir para identificar la instancia (no se puede omitir esta información).

     Por ejemplo, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Tipo: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Aunque no es un requisito técnico, es recomendable hacer `<identifier>` único.

1. Establezca las siguientes propiedades en este nodo:

   * Nombre: `org.apache.sling.commons.log.file`

     Tipo: cadena

     Value: especifique el archivo de registro; por ejemplo, `logs/myLogFile.log`

   * Nombre: `org.apache.sling.commons.log.names`

     Tipo: cadena[] (Cadena + Múltiple)

     Valor: especifique los servicios OSGi para los que el registrador va a registrar mensajes; por ejemplo, todos los siguientes:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`

   * Nombre: `org.apache.sling.commons.log.level`

     Tipo: cadena

     Value: especifique el nivel de registro requerido ( `debug`, `info`, `warn`, o `error`); por ejemplo, `debug`

   * Configure los demás parámetros según sea necesario:

      * Nombre: `org.apache.sling.commons.log.pattern`

        Tipo: `String`

        Value: especifique el patrón del mensaje de registro según sea necesario; por ejemplo,

        `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` admite hasta seis argumentos.
   >
   >{0} Marca de tiempo del tipo `java.util.Date`
   >
   >{1} el marcador de registro
   >
   >{2} el nombre del subproceso actual
   >
   >{3} el nombre del registrador
   >
   >{4} el nivel de registro
   >
   >{5} el mensaje de registro
   >
   >Si la llamada de registro incluye un `Throwable`, el stacktrace se anexa al mensaje.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names debe tener un valor.

   >[!NOTE]
   >
   >Las rutas de escritura de registros son relativas a `crx-quickstart` ubicación.
   >
   >Por lo tanto, un archivo de registro especificado como:
   >
   >`logs/thelog.log`
   >
   >escribe a:
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`.
   >
   >Y un archivo de registro especificado como:
   >
   >`../logs/thelog.log`
   >
   >escribe en un directorio:
   >
   >`<cq-installation-dir>/logs/`\
   >(es decir, junto a `<cq-installation-dir>/crx-quickstart/`)

1. Este paso sólo es necesario cuando se requiere un nuevo Writer (es decir, con una configuración distinta de la predeterminada Writer).

   >[!CAUTION]
   >
   >Solo se requiere una nueva configuración de Escritor de registro cuando el valor predeterminado existente no es adecuado.
   >
   >Si no se configura ningún objeto Writer explícito, el sistema genera automáticamente un objeto Writer implícito basado en el valor predeterminado.

   En `/apps/<project-name>/config`, cree un nodo para el nuevo [Configuración del escritor de registro de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration):

   * Nombre: `org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` (a Escritor)

     Como con el Logger, `<identifier>` se sustituye por texto libre que se debe introducir para identificar la instancia (no se puede omitir esta información). Por ejemplo, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Tipo: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Aunque no es un requisito técnico, es aconsejable hacer lo siguiente `<identifier>` único.

   Establezca las siguientes propiedades en este nodo:

   * Nombre: `org.apache.sling.commons.log.file`

     Tipo: `String`

     Value: especifique el archivo de registro para que coincida con el archivo especificado en el registrador;

     para este ejemplo, `../logs/myLogFile.log`.

   * Configure los demás parámetros según sea necesario:

      * Nombre: `org.apache.sling.commons.log.file.number`

        Tipo: `Long`

        Value: especifique el número de archivos de registro que desea conservar; por ejemplo, `5`

      * Nombre: `org.apache.sling.commons.log.file.size`

        Tipo: `String`

        Valor: especifique según sea necesario para controlar la rotación del archivo por tamaño/fecha; por ejemplo, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controla la rotación del archivo de registro estableciendo:
   >
   >* un tamaño de archivo máximo
   >* una programación de fecha y hora
   >
   >para indicar cuándo se crea un nuevo archivo (y el nombre del archivo existente cambia según el patrón de nombre).
   >
   >* Se puede especificar un límite de tamaño con un número. Si no se proporciona ningún indicador de tamaño, se toma como número de bytes o puede agregar uno de los indicadores de tamaño: `KB`, `MB`, o `GB` (se ignora mayúsculas y minúsculas).
   >* Como patrón se puede especificar una programación de fecha/hora `java.util.SimpleDateFormat` . Define el período de tiempo tras el cual se rota el archivo. Además, el sufijo anexado al archivo girado (para su identificación).
   >
   >El valor predeterminado es &#39;.&#39;aaaa-MM-dd (para rotación diaria de registros).
   >
   >Por ejemplo, a medianoche del 20 de enero de 2010 (o cuando se produce el primer mensaje de registro posterior a esta fecha para ser preciso), .. /logs/error.log se renombra a.. /logs/error.log.2010-01-20. El registro del 21 de enero se genera en (nuevo y vacío) .. /logs/error.log hasta que se transfiere al cambio de día.
   >
   >| `'.'yyyy-MM` | Rotación al comienzo de cada mes |
   >|---|---|
   >| `'.'yyyy-ww` | Rotación el primer día de cada semana (depende de la configuración regional). |
   >| `'.'yyyy-MM-dd` | Rotación a medianoche cada día. |
   >| `'.'yyyy-MM-dd-a` | Rotación a medianoche y mediodía de cada día. |
   >| `'.'yyyy-MM-dd-HH` | Rotación al principio de cada hora. |
   >| `'.'yyyy-MM-dd-HH-mm` | Rotación al principio de cada minuto. |
   >
   >Nota: Al especificar una hora/fecha:
   >
   >1. Debe &quot;escapar&quot; el texto literal dentro de un par de comillas simples (&quot; &#39;);
   >
   >    Evita que ciertos caracteres se interpreten como letras de patrón.
   >
   >1. Utilice solo los caracteres permitidos para un nombre de archivo válido en cualquier parte de la opción.

1. Lea el nuevo archivo de registro con la herramienta elegida.

   El archivo de registro creado por este ejemplo es `../crx-quickstart/logs/myLogFile.log`.

La consola Felix también proporciona información sobre la compatibilidad de registros de Sling en `../system/console/slinglog`; por ejemplo, `https://localhost:4502/system/console/slinglog`.

### Búsqueda de registros de auditoría {#finding-the-audit-records}

Los registros de auditoría se mantienen para proporcionar un registro de quién hizo qué y cuándo. AEM Se generan diferentes registros de auditoría para los eventos WCM y OSGi de la.

#### AEM Registros de auditoría de WCM mostrados durante la creación de páginas {#aem-wcm-audit-records-shown-when-page-authoring}

1. Abra una página.
1. En la barra de tareas, puede seleccionar la pestaña con el icono de candado y, a continuación, hacer doble clic **Registro de auditoría...**
1. Se abre una nueva ventana que muestra la lista de registros de auditoría de la página actual.

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. Clic **OK** cuando desee cerrar la ventana.

#### AEM Registros de auditoría de WCM dentro del repositorio {#aem-wcm-auditing-records-within-the-repository}

Dentro de `/var/audit` carpeta, los registros de auditoría se mantienen según el recurso. Puede explorar en profundidad hasta que vea los registros individuales y la información que contienen.

Estas entradas contienen la misma información que se muestra al editar una página.

#### Registros de auditoría OSGi de la consola web {#osgi-audit-records-from-the-web-console}

Los eventos OSGi también generan registros de auditoría que se pueden ver desde el **Estado de configuración** pestaña -> **Archivos de registro** AEM en la consola web de la:

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## Supervisión de los agentes de replicación {#monitoring-your-replication-agents}

Puede supervisar su [colas de replicación](/help/sites-deploying/replication.md) para detectar cuándo una cola está caída o bloqueada, lo que a su vez podría indicar un problema con una instancia de publicación o un sistema externo:

* ¿están habilitadas todas las colas necesarias?
* ¿sigue siendo necesaria alguna cola deshabilitada?
* todo `enabled` las colas deben tener el estado `idle` o `active`, que indican un funcionamiento normal; no se deben crear colas `blocked`, que a menudo es un signo de problemas en el lado del receptor.

* si el tamaño de la cola aumenta con el tiempo, puede indicar una cola bloqueada.

Para supervisar un agente de replicación:

1. Acceda a la **Herramientas** AEM pestaña en la lista de.
1. Clic **Replicación**.
1. Haga doble clic en el vínculo a los agentes para el entorno adecuado (el panel izquierdo o el derecho); por ejemplo, **Agentes en el autor**.

   La ventana resultante muestra una descripción general de todos los agentes de replicación para el entorno de creación, incluidos su destino y estado.

1. Haga clic en el nombre del agente apropiado (que es un vínculo) para mostrar información detallada sobre ese agente:

   ![chlimage_1](assets/chlimage_1.jpeg)

   Aquí puede hacer lo siguiente:

   * Compruebe si el agente está activado.
   * Consulte el objetivo de cualquier replicación.
   * Ver si la cola de replicación está activa (habilitada).
   * Ver si hay algún elemento en la cola.
   * **Actualizar** o **Borrar** para actualizar la visualización de entradas de cola. Al hacerlo, puede ver los elementos que entran y salen de la cola.
   * **Ver registro** para acceder al registro de cualquier acción realizada por el agente de replicación.
   * **Probar conexión** a la instancia de target.
   * **Forzar reintento** en cualquier elemento en cola, si es necesario.

   >[!CAUTION]
   >
   >No utilice el vínculo &quot;Probar conexión&quot; para la bandeja de salida de replicación inversa en una instancia de publicación.
   >
   >Si se realiza una prueba de replicación para una cola de Bandeja de salida, los elementos anteriores a la replicación de prueba se vuelven a procesar con cada replicación inversa.
   >
   >Si estos elementos existen en cola, se pueden encontrar con la siguiente consulta JCR XPath y deben eliminarse.
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

De nuevo, puede desarrollar una solución para detectar todos los agentes de replicación (ubicados en `/etc/replication/author` o `/etc/replication/publish`) y, a continuación, compruebe el estado del agente ( `enabled`, `disabled`) y la cola subyacente ( `active`, `idle`, `blocked`).

## Monitorización del rendimiento {#monitoring-performance}

[Optimización del rendimiento](/help/sites-deploying/configuring-performance.md) es un proceso interactivo que recibe atención durante el desarrollo. Después de la implementación, se revisa después de intervalos o eventos específicos.

Los métodos utilizados al recopilar información para la optimización también se pueden utilizar para la monitorización continua.

>[!NOTE]
>
>Específico [configuraciones disponibles para mejorar el rendimiento](/help/sites-deploying/configuring-performance.md#configuring-for-performance) también se puede comprobar.

A continuación se enumeran los problemas comunes de rendimiento que se producen, junto con propuestas sobre cómo detectarlos y contrarrestarlos.

| Área | Síntoma | Para aumentar la capacidad... | Para reducir el volumen... |
|---|---|---|---|
| Cliente | Alto uso de CPU del cliente. | Instale una CPU de cliente con mayor rendimiento. | Simplificar el diseño (para HTML). |
|   | Uso de CPU del servidor bajo. | Actualice a un explorador más rápido. | Mejore la caché del lado del cliente. |
|   | Algunos clientes rápido, otros lento. |  |  |
| Servidor |  |  |  |
| Red | Uso de CPU bajo en servidores y clientes. | Elimine los cuellos de botella de red. | Mejore/optimice la configuración de la caché del cliente. |
|   | La exploración local en el servidor es (comparativamente) rápida. | Aumentar el ancho de banda de red. | Reduzca el &quot;peso&quot; de sus páginas web (por ejemplo, menos imágenes, HTML optimizado). |
| Web-server | El uso de CPU en el servidor web es alto. | Agrupe los servidores web. | Reduzca las visitas por página (visita). |
|   |  | Utilice un equilibrador de carga de hardware. |  |
| Aplicación | El uso de CPU del servidor es alto. | AEM Clúster las instancias de la. | Busque y elimine bloques de CPU y memoria (utilice la salida de revisión de código y temporización). |
|   | Alto consumo de memoria. |  | Mejore el almacenamiento en caché en todos los niveles. |
|   | Tiempos de respuesta bajos. |  | Optimizar plantillas y componentes (por ejemplo, estructura y lógica). |
| Repositorio |  |  |  |
| Caché |  |  |  |

Los problemas de rendimiento pueden provenir de varias causas que no tienen nada que ver con su sitio web, incluidas las ralentizaciones temporales en la velocidad de conexión, la carga de la CPU y muchas más.

También puede afectar a todos los visitantes o solo a un subconjunto de ellos.

Toda esta información debe obtenerse, ordenarse y analizarse antes de optimizar el rendimiento general o resolver problemas específicos.

* Antes de experimentar un problema de rendimiento:

   * recopilar la mayor cantidad de información posible para adquirir un buen conocimiento práctico del sistema en circunstancias normales.

* Cuando experimenta un problema de rendimiento:

   * intente replicarlo con un navegador web estándar (o preferiblemente más), en un cliente diferente que sepa que tiene un buen rendimiento general o en el propio servidor (si es posible)
   * compruebe si algo (relacionado con el sistema) ha cambiado en un espacio de tiempo adecuado y si alguno de estos cambios podría haber afectado al rendimiento
   * haga preguntas como:

      * ¿el problema solo se produce en momentos específicos?
      * ¿el problema solo se produce en páginas específicas?
      * ¿se ven afectadas otras solicitudes?

   * recopile la mayor cantidad de información posible para compararla con su conocimiento del sistema en circunstancias normales:

### Herramientas para monitorizar y analizar el rendimiento {#tools-for-monitoring-and-analyzing-performance}

A continuación se ofrece una breve descripción general de algunas de las herramientas disponibles para supervisar y analizar el rendimiento.

Algunas de estas herramientas dependen del sistema operativo.

<table>
 <tbody>
  <tr>
   <td>Herramienta</td>
   <td>Se usa para analizar...</td>
   <td>Uso / Más información...</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>Tiempos de respuesta y concurrencia.</td>
   <td><a href="#interpreting-the-request-log">Interpretación de request.log</a>.</td>
  </tr>
  <tr>
   <td>armadura/traza</td>
   <td>Cargas de página</td>
   <td><p>Comandos Unix/Linux para rastrear llamadas y señales del sistema. Aumente el nivel de registro a <code>INFO</code>.</p> <p>Analice la cantidad de cargas de página por solicitud y qué páginas.</p> </td>
  </tr>
  <tr>
   <td>Volcados de hilos</td>
   <td>Observe los hilos de JVM. Identificar contenciones, bloqueos y operadores de larga duración.</td>
   <td><p>En función del sistema operativo:<br /> - Unix/Linux: <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows (modo consola): Ctrl-Break<br /> </p> <p>También hay herramientas de análisis disponibles, como <a href="https://github.com/irockel/tda">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>Volcados de pila</td>
   <td>Problemas de falta de memoria que causan un rendimiento lento.</td>
   <td><p>Añada el:<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> AEM a la llamada de Java™ que va a la interfaz de usuario de.</p> <p>Consulte la <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/prepapp002.html#CEGBHDFH">Página Opciones/Indicadores para Resolución de Problemas de JVM</a>.</p> </td>
  </tr>
  <tr>
   <td>Llamadas del sistema</td>
   <td>Identificar problemas de temporización.</td>
   <td><p>Llamadas a <code>System.currentTimeMillis()</code> o <code>com.day.util</code>. La temporización se utiliza para generar marcas de tiempo a partir del código o mediante <a href="#html-comments">HTML-comentarios</a>.</p> <p><strong>Nota:</strong> Implemente estos elementos para que se puedan activar o desactivar según sea necesario; cuando un sistema se ejecuta sin problemas, no se necesita la sobrecarga de recopilación de estadísticas.</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>Identifique las fugas de memoria y analice selectivamente el tiempo de respuesta.</td>
   <td><p>el uso básico es:</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>Consulte <a href="#apache-bench">Apache Bench</a> y el <a href="https://httpd.apache.org/docs/2.4/programs/ab.html">página de comando man ab</a> para obtener información detallada.</p> </td>
  </tr>
  <tr>
   <td>Análisis de búsqueda</td>
   <td> </td>
   <td>Ejecute consultas de búsqueda sin conexión, identifique el tiempo de respuesta de la consulta, pruebe y confirme el conjunto de resultados.<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>Pruebas de carga y funcionales.</td>
   <td><a href="https://jmeter.apache.org/">https://jmeter.apache.org/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>Perfiles exhaustivos de CPU y memoria.</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>Java™ Flight Recorder</td>
   <td>Java™ Flight Recorder (JFR) es una herramienta para recopilar datos de diagnóstico y perfil sobre una aplicación Java™ en ejecución.</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>Observe las métricas y los hilos de JVM.</td>
   <td><p>Uso: jconsole</p> <p>Consulte <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html">jconsole</a> y <a href="#monitoring-performance-using-jconsole">Monitorización del rendimiento con JConsole</a>.</p> <p><strong>Nota:</strong> Con JDK 1.8, JConsole es extensible con complementos; por ejemplo, Top o TDA (Thread Dump Analyzer).</p> </td>
  </tr>
  <tr>
   <td>Java™ VisualVM</td>
   <td>Observe las métricas, los hilos, la memoria y los perfiles de JVM.</td>
   <td><p>Uso: visualvm o visualvm<br /> </p> <p>Consulte <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/">visualvm</a> y <a href="#monitoring-performance-using-j-visualvm">Monitorización del rendimiento con (J)VisualVM</a>.</p> <p><strong>Nota:</strong> Con JDK 1.8, VisualVM se puede ampliar con complementos. VisualVM se interrumpe después de JDK 9. En su lugar, utilice Java™ Flight Recorder.</p> </td>
  </tr>
  <tr>
   <td>armadura/escalera, lsof</td>
   <td>Llamada al núcleo y análisis de procesos detallados (UNIX®).</td>
   <td>Comandos Unix/Linux.</td>
  </tr>
  <tr>
   <td>Estadísticas de temporización</td>
   <td>Consulte Estadísticas temporales para la renderización de páginas.</td>
   <td><p>Para ver las estadísticas de tiempo de la renderización de la página, puede utilizar <strong>Ctrl-Mayús-U</strong> junto con <code>?debugClientLibs=true</code> se establece en la dirección URL.</p> </td>
  </tr>
  <tr>
   <td>Herramienta de perfil de CPU y memoria<br /> </td>
   <td><a href="#interpreting-the-request-log">Se utiliza al analizar solicitudes lentas durante el desarrollo</a>.</td>
   <td>Por ejemplo, <a href="https://www.yourkit.com/">Su kit</a>. o el <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">Java™ Flight Recorder</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">Recopilación de información</a></td>
   <td>El estado actual de la instalación.</td>
   <td>Conocer en la medida de lo posible su instalación también puede ayudarle a rastrear qué podría haber causado un cambio en el rendimiento y si estos cambios están justificados. Recopile estas métricas a intervalos regulares para poder ver fácilmente cambios significativos.</td>
  </tr>
 </tbody>
</table>

### Interpretación de request.log {#interpreting-the-request-log}

AEM Este archivo registra información básica acerca de cada solicitud realizada a la persona que lo ha solicitado De esto se pueden extraer valiosas conclusiones.

El `request.log` ofrece una forma integrada de obtener información sobre cuánto tiempo tardan las solicitudes. A efectos de desarrollo, resulta útil `tail -f` el `request.log` y observe los tiempos de respuesta lentos. Para analizar un `request.log`, el Adobe recomienda el [uso de `rlog.jar` que permite ordenar y filtrar los tiempos de respuesta](#using-rlog-jar-to-find-requests-with-long-duration-times).

El Adobe recomienda aislar las páginas &quot;lentas&quot; del `request.log`y luego ajustarlos individualmente para obtener un mejor rendimiento. Incluya métricas de rendimiento por componente o utilice una herramienta de perfil de rendimiento como ` [yourkit](https://www.yourkit.com/)`.

#### Monitorización del tráfico en el sitio web {#monitoring-traffic-on-your-website}

El registro de solicitudes registra cada solicitud realizada, junto con la respuesta obtenida:

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

Al sumar todas las entradas de GET dentro de períodos específicos (por ejemplo, en varios períodos de 24 horas), puede realizar declaraciones sobre el tráfico promedio en el sitio web.

#### Monitorización de los tiempos de respuesta con request.log {#monitoring-response-times-with-the-request-log}

Un buen punto de partida para el análisis del rendimiento es el registro de solicitudes:

`<cq-installation-dir>/crx-quickstart/logs/request.log`

El registro tiene el siguiente aspecto (las líneas se abrevian para simplificar):

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

Este registro tiene una línea por solicitud o respuesta:

* La fecha en la que se realizó cada solicitud o respuesta.
* El número de la solicitud, entre corchetes. Este número coincide con la solicitud y la respuesta de.
* Una flecha que indica si es una solicitud (flecha que señala a la derecha) o una respuesta (flecha a la izquierda).
* Para las solicitudes, la línea contiene:

   * el método (normalmente, GET, HEAD o POST)
   * la página solicitada
   * el protocolo

* Para las respuestas, la línea contiene:

   * el código de estado (200 significa &quot;correcto&quot;, 404 significa &quot;página no encontrada&quot;)
   * el tipo MIME
   * el tiempo de respuesta

Mediante pequeños scripts, puede extraer la información necesaria del archivo de registro y combinar las estadísticas que desee. Desde estas estadísticas, puede ver qué páginas o tipos de páginas son lentos y si el rendimiento general es satisfactorio.

#### Monitorización de los tiempos de respuesta de búsqueda con el request.log {#monitoring-search-response-times-with-the-request-log}

Las solicitudes de búsqueda también se registran en el archivo de registro:

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

Por lo tanto, como se ha indicado anteriormente, puede utilizar secuencias de comandos para extraer la información relevante y crear estadísticas.

Sin embargo, una vez que haya determinado el tiempo de respuesta, analice por qué la solicitud está tardando en responder y qué se puede hacer para mejorarla.

#### Monitorización del número y el impacto de usuarios simultáneos {#monitoring-the-number-and-impact-of-concurrent-users}

De nuevo, la `request.log` puede utilizarse para controlar la concurrencia y la reacción del sistema a ella.

Se deben realizar pruebas para determinar cuántos usuarios simultáneos puede manejar el sistema antes de que se vea un impacto negativo. De nuevo, se pueden utilizar secuencias de comandos para extraer los resultados del archivo de registro:

* monitorice cuántas solicitudes se realizan en un lapso de tiempo específico, como un minuto.
* pruebe los efectos de un número específico de usuarios que realizan las mismas solicitudes al mismo tiempo (lo más cerca posible). Por ejemplo, 30 usuarios haciendo clic en **Guardar** al mismo tiempo.

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### Uso de log.jar para buscar solicitudes con tiempos de larga duración {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM La incluye varias herramientas de ayuda en lo siguiente:
`<cq-installation-dir>/crx-quickstart/opt/helpers`

Una de estas herramientas, `rlog.jar`, se puede utilizar para ordenar rápidamente `request.log` de modo que las solicitudes se muestren por duración, desde la más larga a la más corta.

El siguiente comando muestra los posibles argumentos:

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

Por ejemplo, puede ejecutarlo especificando `request.log` como parámetro y mostrar las diez primeras solicitudes que tienen la duración más larga:

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

Concatenar al individuo `request.log` archivos si debe realizar esta operación en una muestra de datos de gran tamaño.

### Apache Bench {#apache-bench}

Para minimizar el impacto de los casos especiales (como la recolección de basura), se recomienda utilizar una herramienta como `apachebench` (por ejemplo, [ab](https://httpd.apache.org/docs/2.4/programs/ab.html) para obtener más documentación) para ayudar a identificar las fugas de memoria y analizar selectivamente el tiempo de respuesta.

Apache Bench se puede utilizar de la siguiente manera:

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

Los números anteriores se toman de un portátil MAcBook Pro estándar (mediados de 2010) que accede a la página de la empresa de Geometrixx AEM, tal como se incluye en una instalación predeterminada de la. La página es sencilla, pero no está optimizada para el rendimiento.

El `apachebench` también muestra el tiempo por solicitud como media en todas las solicitudes simultáneas; consulte `Time per request: 54.595 [ms]` (media, en todas las solicitudes simultáneas). Puede cambiar el valor del parámetro de concurrencia `-c` (número de solicitudes múltiples que se realizan a la vez) para ver cualquier efecto.

### Contadores de solicitudes {#request-counters}

La información sobre el tráfico de la solicitud (número de solicitudes durante un período de tiempo específico) le proporciona una indicación de la carga de la instancia. Esta información se puede extraer de [request.log](#interpreting-the-request-log), aunque el uso de contadores automatiza la recopilación de datos para que pueda ver lo siguiente:

* diferencias significativas en la actividad (es decir, diferenciar entre &quot;muchas solicitudes&quot; y &quot;baja actividad&quot;)
* cuando no se está utilizando una instancia
* cualquier reinicio (los contadores se restablecen a 0)

Para automatizar la recopilación de información, también puede instalar un RequestFilter para incrementar un contador en cada solicitud. Se pueden usar varios contadores para diferentes periodos de tiempo.

La información recopilada se puede utilizar para indicar:

* cambios significativos en la actividad
* una instancia redundante
* cualquier reinicio (contador restablecido en 0)

### Comentarios del HTML {#html-comments}

Se recomienda que cada proyecto incluya `html comments` para el rendimiento del servidor. Se pueden encontrar muchos buenos ejemplos públicos. Seleccione una página, abra el origen de la página para verlo y desplácese hasta la parte inferior. Se pueden ver códigos como los siguientes:

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### Monitorización del rendimiento con JConsole {#monitoring-performance-using-jconsole}

El comando herramienta `jconsole` está disponible con el JDK de.

1. AEM Inicie la instancia de.
1. Ejecución `jconsole.`
1. AEM Seleccione la instancia de la y **Connect**.

1. Desde dentro de `Local` aplicación, doble clic `com.day.crx.quickstart.Main`; la Información general se muestra de forma predeterminada:

   ![chlimage_1-1](assets/chlimage_1-1.png)

   Ahora puede seleccionar otras opciones.

### Supervisión del rendimiento mediante (J)VisualVM {#monitoring-performance-using-j-visualvm}

Para JDK 6-8, el comando tool `visualvm` está disponible. Después de instalar un JDK, puede hacer lo siguiente:

1. AEM Inicie la instancia de.

   >[!NOTE]
   >
   >Si utiliza Java™ 5, puede añadir la variable `-Dcom.sun.management.jmxremote` a la línea de comandos de Java™ que inicia la JVM. JMX está habilitado de forma predeterminada con Java™ 6.

1. Ejecute una de estas acciones:

   * `jvisualvm`: en la carpeta JDK bin 1.6 (versión probada)
   * `visualvm`: se puede descargar desde [VisualVM](https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/) (versión de borde sangrante)

1. Desde dentro de `Local` aplicación, doble clic `com.day.crx.quickstart.Main`. La Información general se muestra como predeterminada:

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Ahora puede seleccionar otras opciones, incluido Monitor:

   ![chlimage_1-3](assets/chlimage_1-3.png)

Puede utilizar esta herramienta para generar volcados de hilos y volcados de cabezales de memoria. El equipo de soporte técnico suele solicitar esta información.

### Recopilación de información {#information-collection}

Conocer en la medida de lo posible su instalación puede ayudarle a averiguar qué puede haber causado un cambio en el rendimiento y si estos cambios están justificados. Recopile estas métricas a intervalos regulares para poder ver fácilmente cambios significativos.

La siguiente información puede resultar útil:

* [¿Cuántos autores están trabajando con el sistema?](#how-many-authors-are-working-with-the-system)
* [¿Cuál es el número promedio de activaciones de página por día?](#what-is-the-average-number-of-page-activations-per-day)
* [¿Cuántas páginas mantiene actualmente en este sistema?](#how-many-pages-do-you-currently-maintain-on-this-system)
* [Si usa MSM, ¿cuál es el número promedio de despliegues por mes?](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [¿Cuál es el número promedio de Live Copies por mes?](#what-is-the-average-number-of-live-copies-per-month)
* [Si utiliza AEM Assets, ¿cuántos recursos mantiene actualmente en Assets?](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [¿Cuál es el tamaño promedio de los recursos?](#what-is-the-average-size-of-the-assets)
* [¿Cuántas plantillas se están utilizando actualmente?](#how-many-templates-are-currently-used)
* [¿Cuántos componentes se utilizan actualmente?](#how-many-components-are-currently-used)
* [¿Cuántas solicitudes por hora tiene en el sistema de creación en la hora de mayor actividad?](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [¿Cuántas solicitudes por hora tiene en el sistema de publicación en las horas de mayor actividad?](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### ¿Cuántos autores están trabajando con el sistema? {#how-many-authors-are-working-with-the-system}

Para ver el número de autores que han utilizado el sistema desde la instalación, utilice la línea de comandos:

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

Para ver el número de autores que trabajan en una fecha determinada:

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### ¿Cuál es el número promedio de activaciones de página por día? {#what-is-the-average-number-of-page-activations-per-day}

Para ver el número total de activaciones de página desde la instalación del servidor, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`

* **Ruta** `/`

* **Consulta** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

A continuación, calcule el número de días transcurridos desde la instalación para calcular la media.

#### ¿Cuántas páginas mantiene actualmente en este sistema? {#how-many-pages-do-you-currently-maintain-on-this-system}

Para ver el número de páginas que hay actualmente en el servidor, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`

* **Ruta** `/`

* **Consulta** `//element(*, cq:Page)`

#### Si usa MSM, ¿cuál es el número promedio de despliegues por mes? {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

Para determinar el número total de despliegues desde la instalación, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`

* **Ruta** `/`

* **Consulta** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

Calcule el número de meses transcurridos desde la instalación para calcular la media.

#### ¿Cuál es el número promedio de Live Copies por mes? {#what-is-the-average-number-of-live-copies-per-month}

Para determinar el número total de Live Copies realizadas desde la instalación, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`

* **Ruta** `/`

* **Consulta** `//element(*, cq:LiveSyncConfig)`

Utilice de nuevo el número de meses transcurridos desde la instalación para calcular la media.

#### Si utiliza AEM Assets, ¿cuántos recursos mantiene actualmente en Assets? {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

Para ver cuántos recursos DAM mantiene actualmente, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`
* **Ruta** `/`
* **Consulta** `/jcr:root/content/dam//element(*, dam:Asset)`

#### ¿Cuál es el tamaño promedio de los recursos? {#what-is-the-average-size-of-the-assets}

Para determinar el tamaño total del `/var/dam` carpeta:

1. Utilice WebDAV para asignar el repositorio al sistema de archivos local.

1. Utilice la línea de comandos:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   Para obtener el tamaño promedio, divida el tamaño global por el número total de recursos en `/var/dam` (obtenido anteriormente).

#### ¿Cuántas plantillas se están utilizando actualmente? {#how-many-templates-are-currently-used}

Para ver el número de plantillas que hay actualmente en el servidor, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`
* **Ruta** `/`
* **Consulta** `//element(*, cq:Template)`

#### ¿Cuántos componentes se utilizan actualmente? {#how-many-components-are-currently-used}

Para ver el número de componentes que hay actualmente en el servidor, utilice una consulta del repositorio; a través de CRXDE - Herramientas - Consulta:

* **Tipo** `XPath`
* **Ruta** `/`
* **Consulta** `//element(*, cq:Component)`

#### ¿Cuántas solicitudes por hora tiene en el sistema de creación en la hora de mayor actividad? {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

Para determinar las solicitudes por hora que tiene en el sistema de creación en la hora de mayor actividad:

1. Para determinar el número total de solicitudes desde la instalación, utilice la línea de comandos:

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. Para determinar las fechas de inicio y finalización:

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   Utilice estos valores para calcular la cantidad de horas que han transcurrido desde la instalación y, a continuación, el número promedio de solicitudes por hora.

#### ¿Cuántas solicitudes por hora tiene en el sistema de publicación en las horas de mayor actividad? {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

Repita el procedimiento anterior en la instancia de publicación.

## Análisis de escenarios específicos {#analyzing-specific-scenarios}

A continuación se muestra una lista de sugerencias sobre qué comprobar si comienza a experimentar ciertos problemas de rendimiento. La lista (lamentablemente) no es completa.

>[!NOTE]
>
Consulte también los siguientes artículos para obtener más información:
>
* [Volcados de hilos](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=es)
* [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=es)
* [Analizar con el generador de perfiles integrado](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17499.html?lang=es)
* [Analizar procesos lentos y bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
>

### CPU al 100% {#cpu-at}

Si la CPU del sistema se ejecuta constantemente al 100%, consulte lo siguiente:

* Base de conocimiento:

   * [Analizar procesos lentos y bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### Memoria insuficiente {#out-of-memory}

Aunque estos errores deben detectarse durante el desarrollo y la prueba, algunos escenarios pueden saltarse.

Si el sistema se está quedando sin memoria, este problema se puede ver de varias maneras, incluida la degradación del rendimiento y los mensajes de error, incluido el subtexto:

`java.lang.OutOfMemoryError`

En estos casos, compruebe:

* La configuración de JVM utilizada para [AEM inicio de la](/help/sites-deploying/deploy.md#getting-started)
* Base de conocimiento:

   * [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=es)

### E/S de disco {#disk-i-o}

Si el sistema se está quedando sin espacio en disco o nota que se ha golpeado el disco, consulte:

* Si ha deshabilitado la recopilación de información de depuración, puede configurarse en varias ubicaciones, incluidas las siguientes:

   * [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Controlador de JavaScript Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Configuración de registro de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [Administrador de bibliotecas HTML de CQ](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [Filtrar de depuración de CQ Gestión de contenidos web](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [Registradores](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)

* Si ha configurado Versión purga de y cómo lo ha hecho [](/help/sites-deploying/version-purging.md)
* Base de conocimiento:

   * [Demasiados archivos abiertos](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17470.html?lang=es)
   * [El diario consume demasiado espacio en disco](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### Degradación regular del rendimiento {#regular-performance-degradation}

Si ve que el rendimiento de su instancia se deteriora después de cada reinicio (a veces una semana o más tarde), se puede comprobar lo siguiente:

* [Memoria insuficiente](#outofmemory)
* Base de conocimiento:

   * [Sesiones sin cerrar](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### Ajuste de JVM {#jvm-tuning}

La máquina virtual Java™ (JVM) ha mejorado en cuanto a la optimización (especialmente desde Java™ 7). Por lo tanto, a menudo resulta adecuado especificar un tamaño de JVM fijo razonable y utilizar los valores predeterminados.

Si la configuración predeterminada no es adecuada, es importante establecer un método para supervisar y evaluar el rendimiento de GC. Hágalo antes de intentar ajustar la JVM. Este proceso puede incluir factores de monitorización, como el tamaño de la pila, el algoritmo y otros aspectos.

Algunas opciones comunes son:

* VerboseGC:

  ```
  -verbose:gc \
   -Xloggc:$LOGS/verbosegc.log \
   -XX:+PrintGCDetails \
   -XX:+PrintGCDateStamps
  ```

El registro resultante se puede ingerir mediante un visualizador GC como:

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

O JConsole:

* Esta configuración es para una conexión JMX &quot;totalmente abierta&quot;:

  ```
  -Dcom.sun.management.jmxremote \
   -Dcom.sun.management.jmxremote.port=8889 \
   -Dcom.sun.management.jmxremote.authenticate=false \
   -Dcom.sun.management.jmxremote.ssl=false
  ```

* A continuación, conéctese a JVM con JConsole; consulte lo siguiente:
  ` [https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html)`

Puede ver cuánta memoria se está utilizando, qué algoritmos de GC se están utilizando, cuánto tardan en ejecutarse y qué efecto tiene este proceso en el rendimiento de la aplicación. Sin él, la sintonización es solo &quot;perillas giratorias aleatoriamente&quot;.

>[!NOTE]
>
Para la VM de Oracle, también hay información en:
>
[https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html)
