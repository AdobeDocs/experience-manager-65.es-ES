---
title: Prácticas recomendadas para monitorizar [!DNL Assets] implementación
description: Prácticas recomendadas para monitorizar el entorno y el rendimiento de su [!DNL Adobe Experience Manager] después de implementarse.
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 1%

---

# Prácticas recomendadas para monitorizar [!DNL Adobe Experience Manager Assets] implementación {#assets-monitoring-best-practices}

En el [!DNL Experience Manager Assets] Desde el punto de vista, la supervisión debe incluir la observación y la presentación de informes sobre los siguientes procesos y tecnologías:

* CPU del sistema
* Uso de memoria del sistema
* Tiempo de espera de E/S y E/S del disco del sistema
* Sistema de E/S de red
* MBeans de JMX para la utilización de montículos y procesos asincrónicos, como flujos de trabajo
* Comprobaciones de estado de la consola OSGi

Normalmente, [!DNL Experience Manager Assets] pueden ser monitorizados de dos maneras, monitorización en vivo y monitorización a largo plazo.

## Supervisión en directo {#live-monitoring}

Debe realizar monitorización en vivo durante la fase de prueba de rendimiento de su desarrollo o durante situaciones de carga alta para comprender las características de rendimiento de su entorno. Normalmente, la monitorización en vivo debe realizarse con un conjunto de herramientas. Estas son algunas recomendaciones:

* [VM visual](https://visualvm.github.io/): Visual VM le permite ver información detallada sobre Java VM, incluyendo uso de CPU, uso de memoria Java. Además, permite realizar muestras y evaluar el código que se ejecuta en una implementación.
* [Superior](https://man7.org/linux/man-pages/man1/top.1.html): Top es un comando Linux que abre un tablero, que muestra estadísticas de uso, incluyendo CPU, memoria y uso de E/S. Proporciona información general de alto nivel sobre lo que está sucediendo en una instancia.
* [Htop](https://hisham.hm/htop/): La parte superior es un visualizador de procesos interactivo. Proporciona un uso detallado de la CPU y la memoria además de lo que Top puede proporcionar. Htop puede instalarse en la mayoría de los sistemas Linux usando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop es un tablero detallado para el uso de IO de disco. Muestra barras y medidores que representan los procesos que utilizan E/S de disco y la cantidad que utilizan. Iotop puede instalarse en la mayoría de los sistemas Linux usando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop muestra información detallada sobre el uso de ethernet/network. Iftop muestra las estadísticas por canal de comunicación en las entidades que utilizan ethernet y la cantidad de ancho de banda que utilizan. Iftop puede instalarse en la mayoría de los sistemas Linux usando `yum install iftop` o `apt-get install iftop`.

* Grabador de vuelo Java (JFR): Herramienta comercial de Oracle que se puede utilizar libremente en entornos que no sean de producción. Para obtener más información, consulte [Cómo usar el registrador de vuelos Java para diagnosticar problemas de tiempo de ejecución de CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` archivo: Puede investigar el [!DNL Experience Manager] `error.log` para obtener más información sobre los errores registrados en el sistema. Uso del comando `tail -F quickstart/logs/error.log` para identificar los errores que se van a investigar.
* [Consola de flujo de trabajo](/help/sites-administering/workflows.md): Aproveche la consola de flujo de trabajo para monitorizar los flujos de trabajo que se quedan atrás o se quedan atascados.

Normalmente, estas herramientas se utilizan juntas para obtener una idea completa del rendimiento de su [!DNL Experience Manager] implementación.

>[!NOTE]
>
>Estas herramientas son herramientas estándar y no son compatibles directamente con el Adobe. No requieren licencias adicionales.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitorización en vivo con la herramienta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Seguimiento a largo plazo {#long-term-monitoring}

Monitorización a largo plazo de un [!DNL Experience Manager] la implementación implica supervisar durante más tiempo las mismas partes que se supervisan en directo. También incluye la definición de alertas específicas del entorno.

### Agregación de registros y sistema de informes {#log-aggregation-and-reporting}

Hay varias herramientas disponibles para agregar registros, por ejemplo Splunk(TM) y Elastic Search, Logstash y Kabana (ELK). Para evaluar el tiempo de actividad de su [!DNL Experience Manager] , es importante que entienda los eventos de registro específicos de su sistema y cree alertas basadas en ellos. Un buen conocimiento de las prácticas de desarrollo y operaciones puede ayudarle a comprender mejor cómo ajustar el proceso de agregación de registros para generar alertas críticas.

### Monitorización del entorno {#environment-monitoring}

La monitorización del entorno incluye la monitorización de lo siguiente:

* Rendimiento de red
* IO de disco
* Memoria
* Utilización de la CPU
* JMX MBeans
* Sitios web externos

Necesita herramientas externas, como NewRelic(TM) y AppDynamics(TM) para supervisar cada elemento. Con estas herramientas, puede definir las alertas específicas de su sistema, por ejemplo, una alta utilización del sistema, una copia de seguridad del flujo de trabajo, errores de comprobación de estado o un acceso no autenticado a su sitio web. Adobe no recomienda ninguna herramienta en particular sobre otras. Encuentre la herramienta que funciona y aproveche esta herramienta para monitorizar los elementos discutidos.

#### Supervisión interna de las aplicaciones {#internal-application-monitoring}

La supervisión interna de las aplicaciones incluye la monitorización de los componentes de la aplicación que conforman la variable [!DNL Experience Manager] pila, incluyendo JVM, el repositorio de contenido y monitorización a través del código de aplicación personalizado creado en la plataforma. En general, se realiza a través de Java Mbeans que pueden ser monitoreados directamente por muchas soluciones de monitoreo populares, como SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM), etc. Para los sistemas que no admiten una conexión directa con JMX, puede escribir secuencias de comandos shell para extraer los datos JMX y exponerlos a estos sistemas en un formato que entiendan de forma nativa.

El acceso remoto a los JavaScript de JMX no está habilitado de forma predeterminada. Para obtener más información sobre la monitorización mediante JMX, consulte [Monitorización y administración utilizando tecnología JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

En muchos casos, se requiere una base de referencia para monitorizar de forma eficaz una estadística. Para crear una línea de base, observe el sistema en condiciones de trabajo normales durante un período predeterminado y luego identifique la métrica normal.

**Monitorización de JVM**

Como con cualquier pila de aplicaciones basada en Java, [!DNL Experience Manager] depende de los recursos que se le proporcionan a través de la máquina virtual Java subyacente. Puede monitorizar el estado de muchos de estos recursos a través de Platform MXBeans que son expuestos por JVM. Para obtener más información sobre MXBeans, consulte [Uso del servidor MBean de Platform y de la plataforma MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Estos son algunos parámetros de línea de base que puede monitorizar para JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instancias: Todos los servidores
* Umbral de alarma: Cuando la utilización de memoria en pilas o sin memoria en pilas excede el 75% de la memoria máxima correspondiente.
* Definición de alarma: La memoria del sistema es insuficiente o hay una fuga de memoria en el código. Analice un volcado de subprocesos para llegar a una definición.

>[!NOTE]
>
>La información proporcionada por este bean se expresa en bytes.

Subprocesos

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instancias: Todos los servidores
* Umbral de alarma: Cuando el número de subprocesos es bueno al 150% de la línea base.
* Definición de alarma: O bien hay un proceso de fuga activo, o bien una operación ineficiente consume una gran cantidad de recursos. Analice un volcado de subprocesos para llegar a una definición.

**Monitorización[!DNL Experience Manager]**

[!DNL Experience Manager] también expone un conjunto de estadísticas y operaciones a través de JMX. Esto puede ayudar a evaluar el estado del sistema e identificar posibles problemas antes de que afecten a los usuarios. Para obtener más información, consulte [documentación](/help/sites-administering/jmx-console.md) en [!DNL Experience Manager] JMX MBeans.

Estos son algunos parámetros de línea de base que puede monitorizar [!DNL Experience Manager]:

Agentes de replicación

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Instancias: Un Autor y todas las instancias de publicación (para agentes de vaciado)
* Umbral de alarma: Cuando el valor de `QueueBlocked` es `true` o el valor de `QueueNumEntries` es bueno al 150% del valor basal.

* Definición de alarma: Presencia de una cola bloqueada en el sistema que indica que el destino de replicación está inactivo o no se puede acceder a él. A menudo, los problemas de red o infraestructura hacen que se pongan en cola entradas excesivas, lo que puede afectar negativamente al rendimiento del sistema.

>[!NOTE]
>
>Para los parámetros MBean y URL, reemplace `<AGENT_NAME>` con el nombre del agente de replicación que desea monitorizar.

Contador de sesión

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Estadísticas de OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Instancias: Todos los servidores
* Umbral de alarma: Cuando las sesiones abiertas superan la línea de base en más del 50%.
* Definición de alarma: Las sesiones se pueden abrir a través de un código y nunca cerrar. Esto puede suceder lentamente con el tiempo y eventualmente causar pérdidas de memoria en el sistema. Si bien el número de períodos de sesiones debe fluctuar en un sistema, no debe aumentar continuamente.

Comprobación del estado

Comprobaciones de estado disponibles en la variable [panel de operaciones](/help/sites-administering/operations-dashboard.md#health-reports) tienen MBeans de JMX correspondientes para monitorización. Sin embargo, puede escribir comprobaciones de estado personalizadas para exponer estadísticas adicionales del sistema.

Estas son algunas comprobaciones de estado integradas que son útiles para monitorizar:

* Comprobaciones del sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instancias: Un autor, todos los servidores de publicación
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es ADVERTENCIA o CRÍTICA. Consulte el atributo log para obtener más información sobre la causa del problema.

* Cola de replicación

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instancias: Un autor, todos los servidores de publicación
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es ADVERTENCIA o CRÍTICA. Compruebe el atributo log para obtener más información sobre la cola que provocó el problema.

* Rendimiento de la respuesta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instancias: Todos los servidores
   * Duración de la alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es WARN o CRITICAL . Compruebe el atributo log para obtener más información sobre la cola que provocó el problema.

* Rendimiento de consultas

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Instancias: Un autor, todos los servidores de publicación
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: Una o más consultas que se ejecutan lentamente en el sistema. Consulte el atributo log para obtener más información sobre las consultas que causaron el problema.

* Paquetes activos

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Instancias: Todos los servidores
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: Presencia de paquetes OSGi inactivos o no resueltos en el sistema. Compruebe el atributo log para obtener más información sobre los paquetes que causaron el problema.

* Errores de registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instancias: Todos los servidores
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: Hay errores en los archivos de registro. Consulte el atributo log para obtener más información sobre la causa del problema.

## Cuestiones y resoluciones comunes  {#common-issues-and-resolutions}

En el proceso de monitorización, si se producen problemas, estas son algunas tareas de resolución de problemas que puede realizar para resolver problemas comunes con [!DNL Experience Manager] implementaciones:

* Si utiliza TarMK, ejecute la compactación de Tar con frecuencia. Para obtener más información, consulte [Mantener el repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Marque `OutOfMemoryError` registros. Para obtener más información, consulte [Analizar problemas de memoria](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html).

* Compruebe los registros para cualquier referencia a consultas no indexadas, traveralles de árbol o traveralles de índice. Indican consultas no indexadas o consultas inadecuadamente indexadas. Para conocer las prácticas recomendadas sobre optimización del rendimiento de indexación y consultas, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilice la consola de flujo de trabajo para comprobar que los flujos de trabajo funcionan según lo esperado. Si es posible, condense varios flujos de trabajo en un único flujo de trabajo.
* Vuelva a realizar la monitorización en vivo y busque cuellos de botella adicionales o grandes consumidores de cualquier recurso específico.
* Investigue los puntos de salida de la red del cliente y los puntos de entrada a la [!DNL Experience Manager] red de implementación, incluido el despachante. A menudo, son áreas de cuello de botella. Para obtener más información, consulte [Consideraciones sobre la red de recursos](/help/assets/assets-network-considerations.md).
* Aumente el tamaño de su [!DNL Experience Manager] servidor. Es posible que tenga un tamaño inadecuado para su [!DNL Experience Manager] implementación. El servicio de asistencia al cliente de Adobe puede ayudarle a identificar si el servidor no tiene el tamaño adecuado.
* Examine el `access.log` y `error.log` archivos para entradas alrededor del tiempo de algo salió mal. Busque patrones que puedan indicar anomalías de código personalizado. Añádalos a la lista de eventos que supervise.
