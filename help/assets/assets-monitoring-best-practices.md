---
title: Prácticas recomendadas a monitorizar [!DNL Assets] implementación
description: Prácticas recomendadas para monitorizar el entorno y el rendimiento de su [!DNL Adobe Experience Manager] implementación después de implementarla.
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 1%

---

# Prácticas recomendadas a monitorizar [!DNL Adobe Experience Manager Assets] implementación {#assets-monitoring-best-practices}

Desde el [!DNL Experience Manager Assets] Desde este punto de vista, el seguimiento debe incluir la observación y la presentación de informes sobre los siguientes procesos y tecnologías:

* CPU del sistema
* Uso de memoria del sistema
* Tiempo de espera de E/S del disco del sistema
* E/S de red del sistema
* MBean de JMX para el uso de la pila y los procesos asincrónicos, como flujos de trabajo
* Comprobaciones de estado de la consola OSGi

Normalmente, [!DNL Experience Manager Assets] puede monitorizarse de dos maneras: monitorización en vivo y monitorización a largo plazo.

## Monitorización en directo {#live-monitoring}

Debe realizar la monitorización en directo durante la fase de prueba de rendimiento del desarrollo o durante situaciones de alta carga para comprender las características de rendimiento del entorno. Normalmente, la monitorización en directo debe realizarse con un conjunto de herramientas. Estas son algunas recomendaciones:

* [Visual VM](https://visualvm.github.io/): Visual VM le permite ver información detallada de Java VM, incluido el uso de CPU y el uso de memoria Java. Además, permite tomar muestras y evaluar el código que se ejecuta en una implementación.
* [Superior](https://man7.org/linux/man-pages/man1/top.1.html): Top es un comando de Linux que abre un tablero, que muestra estadísticas de uso, incluido el uso de CPU, memoria e IO. Proporciona una descripción general de alto nivel de lo que está sucediendo en una instancia.
* [Htop](https://hisham.hm/htop/): La visita es un visualizador de procesos interactivo. Proporciona un uso detallado de la CPU y la memoria, además de lo que Top puede proporcionar. Htop se puede instalar en la mayoría de los sistemas Linux utilizando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop es un tablero detallado para el uso de E/S de disco. Muestra las barras y los medidores que muestran los procesos que utilizan E/S de disco y la cantidad que utilizan. Iotop se puede instalar en la mayoría de los sistemas Linux utilizando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop muestra información detallada sobre el uso de Ethernet/red. Iftop muestra estadísticas por canal de comunicación sobre las entidades que utilizan Ethernet y la cantidad de ancho de banda que utilizan. Iftop se puede instalar en la mayoría de los sistemas Linux utilizando `yum install iftop` o `apt-get install iftop`.

* Java Flight Recorder (JFR): Una herramienta comercial de Oracle que puede utilizar libremente en entornos que no sean de producción. Para obtener más información, consulte [Cómo utilizar el registrador de vuelo Java para diagnosticar problemas de tiempo de ejecución de CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` Archivo: Puede investigar el [!DNL Experience Manager] `error.log` para obtener más información sobre los errores registrados en el sistema. Utilice el comando `tail -F quickstart/logs/error.log` para identificar los errores que se deben investigar.
* [Consola Flujo trabajo](/help/sites-administering/workflows.md): aproveche la consola de flujos de trabajo para monitorizar los flujos de trabajo que se retrasan o se quedan atascados.

Normalmente, estas herramientas se utilizan juntas para obtener una idea completa sobre el rendimiento de su [!DNL Experience Manager] implementación.

>[!NOTE]
>
>Estas herramientas son herramientas estándar y no son compatibles directamente con Adobe. No requieren licencias adicionales.

![chlimage_1-33](assets/chlimage_1-143.png)

*Imagen: supervisión en directo con la herramienta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitorización a largo plazo {#long-term-monitoring}

Monitorización a largo plazo de un [!DNL Experience Manager] la implementación implica monitorizar durante un periodo más largo las mismas partes que se monitorizan en directo. También incluye la definición de alertas específicas para su entorno.

### Agregación de registros e informes {#log-aggregation-and-reporting}

Hay varias herramientas disponibles para agregar registros, por ejemplo, Splunk(TM) y Elastic Search, Logstash y Kabana (ELK). Para evaluar el tiempo de actividad de su [!DNL Experience Manager] En la implementación de, es importante comprender los eventos de registro específicos del sistema y crear alertas basadas en ellos. Un buen conocimiento de las prácticas de desarrollo y operaciones puede ayudarle a comprender mejor cómo ajustar el proceso de agregación de registros para generar alertas críticas.

### Monitorización del entorno {#environment-monitoring}

La monitorización del entorno incluye monitorizar lo siguiente:

* Rendimiento de red
* E/S de disco
* Memoria
* Utilización de CPU
* MBeans de JMX
* Sitios web externos

Necesita herramientas externas, como NewRelic(TM) y AppDynamics(TM) para supervisar cada elemento. Con estas herramientas, puede definir alertas específicas del sistema, por ejemplo, alta utilización del sistema, copia de seguridad del flujo de trabajo, errores de comprobación de estado o acceso no autenticado al sitio web. El Adobe no recomienda ninguna herramienta en particular sobre otras. Busque la herramienta que mejor se adapte a sus necesidades y utilícela para supervisar los elementos analizados.

#### Monitorización de aplicaciones internas {#internal-application-monitoring}

La monitorización de aplicaciones internas incluye la monitorización de los componentes de la aplicación que conforman el [!DNL Experience Manager] pila, incluida JVM, el repositorio de contenido y monitorización a través del código de aplicación personalizado creado en la plataforma. En general, se realiza a través de Mbeans JMX que pueden ser monitoreados directamente por muchas soluciones de monitoreo populares, como SolarWinds (TM), HP OpenView (TM), Hyperic (TM), Zabbix (TM) y otras. En el caso de los sistemas que no admiten una conexión directa a JMX, puede escribir scripts de shell para extraer los datos JMX y exponerlos a estos sistemas en un formato que comprendan de forma nativa.

El acceso remoto a los Mbeans de JMX no está habilitado de forma predeterminada. Para obtener más información sobre la monitorización mediante JMX, consulte [Monitorización y administración con tecnología JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

En muchos casos, se requiere una línea de base para monitorizar una estadística de forma eficaz. Para crear una línea de base, observe el sistema en condiciones normales de trabajo durante un período predeterminado y luego identifique la métrica normal.

**Monitorización JVM**

Al igual que con cualquier pila de aplicaciones basadas en Java, [!DNL Experience Manager] depende de los recursos que se le proporcionan a través de la máquina virtual Java subyacente. Puede monitorizar el estado de muchos de estos recursos a través de Platform MXeans que expone JVM. Para obtener más información sobre MXBeans, consulte [Uso del servidor MBean de Platform y de Platform MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Estos son algunos parámetros de línea de base que puede monitorizar para JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instancias: todos los servidores
* Umbral de alarma: cuando la utilización de la memoria (pila o no pila) supera el 75% de la memoria máxima correspondiente.
* Definición de alarma: la memoria del sistema es insuficiente o hay una fuga de memoria en el código. Analice un volcado de hilos para llegar a una definición.

>[!NOTE]
>
>La información proporcionada por este bean se expresa en bytes.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instancias: todos los servidores
* Umbral de alarma: cuando el número de hilos es mayor que el 150% de la línea de base.
* Definición de alarma: o bien hay un proceso de fuga activo, o una operación ineficiente consume una gran cantidad de recursos. Analice un volcado de hilos para llegar a una definición.

**Monitor[!DNL Experience Manager]**

[!DNL Experience Manager] también expone un conjunto de estadísticas y operaciones a través de JMX. Esto puede ayudar a evaluar el estado del sistema e identificar posibles problemas antes de que afecten a los usuarios. Para obtener más información, consulte [documentación](/help/sites-administering/jmx-console.md) el [!DNL Experience Manager] MBeans de JMX.

Estos son algunos parámetros de línea de base que puede monitorizar [!DNL Experience Manager]:

Agentes de replicación

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Instancias: un autor y todas las instancias de publicación (para los agentes de vaciado)
* Umbral de alarma: Cuando el valor de `QueueBlocked` es `true` o el valor de `QueueNumEntries` es mayor que el 150 % del valor basal.

* Definición de alarma: presencia de una cola bloqueada en el sistema que indica que el destino de replicación está inactivo o no se puede acceder a él. A menudo, los problemas de red o infraestructura hacen que se pongan en cola entradas excesivas, lo que puede afectar negativamente al rendimiento del sistema.

>[!NOTE]
>
>Para los parámetros MBean y URL, sustituya `<AGENT_NAME>` con el nombre del agente de replicación que desea supervisar.

Contador de sesión

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Estadísticas de OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Instancias: todos los servidores
* Umbral de alarma: cuando las sesiones abiertas superan la línea de base en más del 50%.
* Definición de alarma: las sesiones pueden abrirse a través de un fragmento de código y nunca cerrarse. Esto puede ocurrir lentamente con el tiempo y, finalmente, causar fugas de memoria en el sistema. Aunque el número de sesiones debería fluctuar en un sistema, no deberían aumentar continuamente.

Comprobación del estado

Comprobaciones de estado disponibles en el [panel de operaciones](/help/sites-administering/operations-dashboard.md#health-reports) tienen los MBeans de JMX correspondientes para la monitorización. Sin embargo, puede escribir comprobaciones de estado personalizadas para exponer estadísticas de sistema adicionales.

Estas son algunas comprobaciones de estado listas para usar que son útiles para monitorizar:

* Comprobaciones del sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o CRÍTICA. Compruebe el atributo de registro para obtener más información sobre la causa del problema.

* Cola de replicación

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o CRÍTICA. Compruebe el atributo de registro para obtener más información sobre la cola que provocó el problema.

* Rendimiento de la respuesta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instancias: todos los servidores
   * Duración de la alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o ESTADO CRÍTICO. Compruebe el atributo de registro para obtener más información sobre la cola que provocó el problema.

* Rendimiento de consultas

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: una o más consultas que se ejecutan lentamente en el sistema. Consulte el atributo de registro para obtener más información sobre las consultas que causaron el problema.

* Paquetes activos

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Instancias: todos los servidores
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: presencia de paquetes OSGi inactivos o sin resolver en el sistema. Consulte el atributo de registro para obtener más información sobre los paquetes que causaron el problema.

* Errores de registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instancias: todos los servidores
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: hay errores en los archivos de registro. Compruebe el atributo de registro para obtener más información sobre la causa del problema.

## Problemas y resoluciones comunes  {#common-issues-and-resolutions}

En el proceso de monitorización, si encuentra problemas, estas son algunas tareas de resolución de problemas que puede realizar para resolver problemas comunes con [!DNL Experience Manager] implementaciones:

* Si usa TarMK, ejecute la compactación de Tar con frecuencia. Para obtener más información, consulte [Mantener el repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Marque `OutOfMemoryError` registros. Para obtener más información, consulte [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* Consulte en los registros cualquier referencia a consultas sin indexar, recorridos de árbol o recorridos de índice. Indican consultas no indexadas o consultas indexadas inadecuadamente. Para conocer las prácticas recomendadas sobre la optimización del rendimiento de consultas e indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilice la consola de flujo de trabajo para comprobar que los flujos de trabajo funcionan según lo esperado. Si es posible, condense varios flujos de trabajo en uno solo.
* Vuelva a realizar la monitorización en directo y busque cuellos de botella adicionales o grandes consumidores de cualquier recurso específico.
* Investigue los puntos de salida de la red de clientes y los puntos de entrada a la [!DNL Experience Manager] red de implementación, incluido Dispatcher. Con frecuencia, estas son áreas de cuello de botella. Para obtener más información, consulte [Consideraciones de red de Assets](/help/assets/assets-network-considerations.md).
* Aumente el tamaño de su [!DNL Experience Manager] servidor. Es posible que tenga un tamaño inadecuado de su [!DNL Experience Manager] implementación. La Asistencia al cliente de Adobe puede ayudarle a identificar si el tamaño del servidor es inferior al esperado.
* Examine la `access.log` y `error.log` archivos para entradas en el momento en que algo salió mal. Busque motivos que puedan indicar anomalías de código personalizado. Añádalos a la lista de eventos que supervisa.
