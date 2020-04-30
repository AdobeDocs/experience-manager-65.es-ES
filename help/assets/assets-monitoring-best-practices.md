---
title: Prácticas recomendadas para supervisar la implementación de [!DNL Adobe Experience Manager Assets].
description: Prácticas recomendadas para supervisar el entorno y el rendimiento de la implementación de [!DNL Adobe Experience Manager] después de implementarla.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Prácticas recomendadas para supervisar la implementación [!DNL Adobe Experience Manager Assets]{#assets-monitoring-best-practices}

Desde el [!DNL Experience Manager Assets] punto de vista de la vigilancia, ésta debe incluir la observación y el sistema de informes de los siguientes procesos y tecnologías:

* CPU del sistema
* Uso de memoria del sistema
* Tiempo de espera de E/S y E/S del disco del sistema
* E/S de red del sistema
* MBeans de JMX para la utilización del montón y procesos asincrónicos, como flujos de trabajo
* Comprobaciones de estado de la consola OSGi

Generalmente, [!DNL Experience Manager Assets] se puede monitorear de dos maneras: monitoreo en vivo y monitoreo a largo plazo.

## Monitoreo en directo {#live-monitoring}

Debe realizar un monitoreo en vivo durante la fase de prueba de rendimiento de su desarrollo o durante situaciones de alta carga para comprender las características de rendimiento de su entorno. Normalmente, la supervisión en directo se debe realizar mediante un conjunto de herramientas. Estas son algunas recomendaciones:

* [VM](https://visualvm.java.net/)visual: Visual VM permite la vista de información detallada de Java VM, incluyendo el uso de CPU y de memoria Java. Además, le permite tomar muestras y evaluar el código que se ejecuta en una implementación.
* [Superior](https://man7.org/linux/man-pages/man1/top.1.html): Arriba hay un comando Linux que abre un panel, que muestra las estadísticas de uso, incluyendo el uso de CPU, memoria y E/S. Proporciona información general de alto nivel sobre lo que sucede en una instancia.
* [Superior](https://hisham.hm/htop/): Htop es un visor de procesos interactivo. Proporciona un uso detallado de la CPU y la memoria además de lo que Top puede proporcionar. Htop puede instalarse en la mayoría de los sistemas Linux usando `yum install htop` o `apt-get install htop`.

* [Iotop](https://guichaz.free.fr/iotop/): Iotop es un panel detallado para el uso de E/S de disco. Muestra barras y medidores que representan los procesos que utilizan la E/S de disco y la cantidad que utilizan. Iotop puede instalarse en la mayoría de los sistemas Linux usando `yum install iotop` o `apt-get install iotop`.

* [Ftop](https://www.ex-parrot.com/pdw/iftop/): Iftop muestra información detallada sobre el uso de Ethernet/red. Iftop muestra las estadísticas de canal de comunicaciones de las entidades que utilizan Ethernet y la cantidad de ancho de banda que utilizan. Si se puede instalar en la mayoría de los sistemas Linux usando `yum install iftop` o `apt-get install iftop`.

* Grabador de vuelos Java (JFR): Herramienta comercial de Oracle que puede utilizar libremente en entornos que no sean de producción. Para obtener más información, consulte [Cómo utilizar la grabadora de vuelos Java para diagnosticar problemas](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)de CQ Runtime.
* [!DNL Experience Manager] `error.log` archivo: Puede investigar el [!DNL Experience Manager] archivo `error.log` para obtener detalles de los errores registrados en el sistema. Utilice el comando `tail -F quickstart/logs/error.log` para identificar los errores que desea investigar.
* [Consola](/help/sites-administering/workflows.md)de flujo de trabajo: Aproveche la consola de flujo de trabajo para supervisar flujos de trabajo que se quedan atrás o se quedan atascados.

Normalmente, estas herramientas se utilizan juntas para obtener una idea completa del rendimiento de la [!DNL Experience Manager] implementación.

>[!NOTE]
>
>Estas herramientas son herramientas estándar y no son compatibles directamente con Adobe. No requieren licencias adicionales.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitoreo en vivo mediante la herramienta de VM visual.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitoreo a largo plazo {#long-term-monitoring}

La supervisión a largo plazo de una [!DNL Experience Manager] implementación implica la supervisión durante más tiempo de las mismas partes que se supervisan en directo. También incluye la definición de las alertas específicas de su entorno.

### Agregación y sistema de informes de registros {#log-aggregation-and-reporting}

Existen varias herramientas disponibles para los registros acumulados, por ejemplo Splunk(TM) y Elastic Search, Logstash y Kabana (ELK). Para evaluar el tiempo de actividad de su [!DNL Experience Manager] implementación, es importante que comprenda los eventos de registro específicos del sistema y cree alertas basadas en ellos. Un buen conocimiento de las prácticas de desarrollo y operaciones puede ayudarle a comprender mejor cómo ajustar el proceso de agregación de registros para generar alertas críticas.

### Supervisión de Entornos {#environment-monitoring}

La supervisión del Entorno incluye la supervisión de lo siguiente:

* Rendimiento de red
* E/S de disco
* Memoria
* Utilización de CPU
* MBeans de JMX
* Sitios web externos

Se requieren herramientas externas, como NewRelic(TM) y AppDynamics(TM), para supervisar cada elemento. Mediante estas herramientas, puede definir alertas específicas de su sistema, por ejemplo, alta utilización del sistema, respaldo del flujo de trabajo, errores de comprobación de estado o acceso no autenticado al sitio web. Adobe no recomienda ninguna herramienta en particular sobre otras. Encuentre la herramienta que funciona para usted y aproveche la herramienta para monitorear los elementos analizados.

#### Supervisión interna de aplicaciones {#internal-application-monitoring}

La supervisión interna de las aplicaciones incluye el monitoreo de los componentes de la aplicación que componen la [!DNL Experience Manager] pila, incluyendo JVM, el repositorio de contenido y el monitoreo a través del código de la aplicación personalizado creado en la plataforma. En general, se realiza a través de los Mbeans JMX que pueden ser monitoreados directamente por muchas soluciones de monitoreo populares, como SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) y otras. Para sistemas que no admiten una conexión directa con JMX, puede escribir secuencias de comandos de shell para extraer los datos JMX y exponerlos a estos sistemas en un formato que entiendan de forma nativa.

El acceso remoto a los mbeans de JMX no está habilitado de forma predeterminada. Para obtener más información sobre la supervisión a través de JMX, consulte [Monitoreo y administración con tecnología](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)JMX.

En muchos casos, se requiere una base de referencia para monitorear eficazmente una estadística. Para crear una línea base, observe el sistema en condiciones de trabajo normales durante un período predeterminado y luego identifique la métrica normal.

**Monitoreo de JVM**

Como con cualquier pila de aplicaciones basada en Java, [!DNL Experience Manager] depende de los recursos que se le proporcionen a través de la máquina virtual Java subyacente. Puede monitorear el estado de muchos de estos recursos a través de los MXBeans de plataforma expuestos por JVM. Para obtener más información sobre MXBeans, consulte [Uso de MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)de plataforma y servidor MBean.

Estos son algunos parámetros de línea de base que puede monitorear para JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instancias: Todos los servidores
* Umbral de alarma: Cuando la utilización de la memoria del montón o sin montón excede el 75% de la memoria máxima correspondiente.
* Definición de alarma: La memoria del sistema es insuficiente o hay una fuga de memoria en el código. Analice un volcado de subprocesos para llegar a una definición.

>[!Note]
>
>La información proporcionada por este grano se expresa en bytes.

Subprocesos

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instancias: Todos los servidores
* Umbral de alarma: Cuando el número de subprocesos es bueno a más del 150% de la línea base.
* Definición de alarma: O bien existe un proceso de fuga activo, o bien una operación ineficiente consume una gran cantidad de recursos. Analice un volcado de subprocesos para llegar a una definición.

**Monitor[!DNL Experience Manager]**

[!DNL Experience Manager] también expone un conjunto de estadísticas y operaciones a través de JMX. Esto puede ayudar a evaluar el estado del sistema e identificar los problemas potenciales antes de que afecten a los usuarios. Para obtener más información, consulte la [documentación](/help/sites-administering/jmx-console.md) sobre los MBeans de [!DNL Experience Manager] JMX.

Estos son algunos parámetros de línea de base que puede supervisar para [!DNL Experience Manager]:

Agentes de replicación

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* Instancias: Un autor y todas las instancias de publicación (para agentes de vaciado)
* Umbral de alarma: Cuando el valor de `QueueBlocked` es `true` o el valor de `QueueNumEntries` es bueno al 150% de la línea base.

* Definición de alarma: Presencia de una cola bloqueada en el sistema que indica que el destinatario de replicación está inactivo o inaccesible. A menudo, los problemas de red o infraestructura hacen que se pongan en cola entradas excesivas, lo que puede afectar negativamente al rendimiento del sistema.

>[!Note]
>
>Para los parámetros MBean y URL, reemplace `<AGENT_NAME>` por el nombre del agente de replicación que desee monitorear.

Contador de sesiones

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* Instancias: Todos los servidores
* Umbral de alarma: Cuando las sesiones abiertas superan la línea de base en más del 50 %.
* Definición de alarma: Las sesiones se pueden abrir a través de un código y nunca cerrar. Esto puede ocurrir lentamente con el tiempo y eventualmente causar pérdidas de memoria en el sistema. Si bien el número de sesiones debe fluctuar en un sistema, no debe aumentar continuamente.

Comprobación del estado

Las comprobaciones de estado disponibles en el panel [de](/help/sites-administering/operations-dashboard.md#health-reports) operaciones tienen los MBeans de JMX correspondientes para la supervisión. Sin embargo, puede escribir comprobaciones de estado personalizadas para exponer estadísticas adicionales del sistema.

Estas son algunas de las comprobaciones de estado integradas que son útiles para monitorear:

* Comprobaciones del sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instancias: Un autor, todos los servidores de publicación
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es WARN o CRITICAL. Consulte el atributo log para obtener más información sobre la causa del problema.

* Cola de replicación

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck `
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instancias: Un autor, todos los servidores de publicación
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es WARN o CRITICAL. Consulte el atributo log para obtener más información sobre la cola que provocó el problema.

* Rendimiento de la respuesta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instancias: Todos los servidores
   * Duración de la alarma: Cuando el estado no es correcto
   * Definición de alarma: El estado de una de las métricas es WARN o CRITICAL. Consulte el atributo log para obtener más información sobre la cola que provocó el problema.

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
   * Definición de alarma: Presencia de paquetes OSGi inactivos o no resueltos en el sistema. Consulte el atributo log para obtener más información sobre los paquetes que causaron el problema.

* Errores de registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instancias: Todos los servidores
   * Umbral de alarma: Cuando el estado no es correcto
   * Definición de alarma: Hay errores en los archivos de registro. Consulte el atributo log para obtener más información sobre la causa del problema.

## Cuestiones y resoluciones comunes {#common-issues-and-resolutions}

En el proceso de supervisión, si se producen problemas, se presentan algunas tareas de resolución de problemas que puede realizar para resolver problemas comunes con [!DNL Experience Manager] las implementaciones:

* Si utiliza TarMK, ejecute la compactación Tar con frecuencia. Para obtener más información, consulte [Mantener el repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Compruebe `OutOfMemoryError` los registros. Para obtener más información, consulte [Análisis de problemas](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)de memoria.

* Compruebe los registros para buscar referencias a consultas no indizadas, traverales de árbol o traverales de índice. Estos datos indican consultas no indizadas o consultas inadecuadamente indizadas. Para obtener información sobre las prácticas recomendadas para optimizar el rendimiento de consulta e indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilice la consola de flujo de trabajo para comprobar que los flujos de trabajo funcionan correctamente. Si es posible, condense varios flujos de trabajo en un único flujo de trabajo.
* Revisa el monitoreo en vivo y busca cuellos de botella adicionales o altos consumidores de cualquier recurso específico.
* Investigue los puntos de salida desde la red del cliente y los puntos de entrada a la red de implementación, incluido el despachante. [!DNL Experience Manager] A menudo, estas son áreas de cuello de botella. Para obtener más información, consulte Consideraciones [de red de](/help/assets/assets-network-considerations.md)Assets.
* Aumente el tamaño del [!DNL Experience Manager] servidor. Es posible que la implementación no tenga un tamaño adecuado [!DNL Experience Manager] . El Servicio de atención al cliente de Adobe puede ayudarle a identificar si el servidor tiene un tamaño inferior al normal.
* Examine los `access.log` archivos y `error.log` los archivos en busca de entradas en el momento en que algo salió mal. Busque patrones que puedan indicar anomalías de código personalizado. Añada a la lista de eventos que supervise.
