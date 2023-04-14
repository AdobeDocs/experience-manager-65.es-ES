---
title: Supervisar las implementaciones de AEM Forms
seo-title: Monitoring AEM forms deployments
description: Puede supervisar las implementaciones de formularios AEM desde un nivel de sistema y desde un nivel interno. Obtenga más información sobre la supervisión de las implementaciones de formularios AEM en este documento.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Supervisar las implementaciones de AEM Forms {#monitoring-aem-forms-deployments}

Puede supervisar las implementaciones de formularios AEM desde un nivel de sistema y desde un nivel interno. Puede utilizar herramientas de administración especializadas como HP OpenView, IBM® Tivoli y CA UniCenter, así como un monitor JMX de terceros denominado *JConsole* para monitorizar específicamente la actividad de Java™. La implementación de una estrategia de monitorización mejora la disponibilidad, fiabilidad y rendimiento de las implementaciones de formularios AEM.

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## Monitorización con MBeans {#monitoring-using-mbeans}

AEM Forms proporciona dos MBeans registrados que proporcionan navegación e información estadística. Estas partes son los únicos MBeans compatibles con la integración y la inspección:

* **ServiceStatistics:** Este MBean proporciona información sobre el nombre del servicio y su versión.
* **OperationStatistics:** Este MBean proporciona la estadística de cada servicio del servidor de AEM Forms. Este MBean es donde los administradores pueden obtener información sobre un servicio en particular, como el tiempo de invocación y el número de errores.

### Interfaces públicas ServiceStatisticsMbean {#servicestatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas de ServiceStatistics MBean con fines de prueba:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas OperationStatisticsMbean {#operationstatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas de OperationStatistics MBean con fines de prueba:

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean Tree &amp; Operation Statistics {#mbean-tree-operation-statistics}

Con una consola JMX (JConsole), hay disponibles estadísticas de OperationStatistics MBean. Estas estadísticas son atributos de MBean y se pueden navegar bajo el siguiente árbol de jerarquía:

**árbol MBean**

**Nombre de dominio de Adobe:** Depende del servidor de aplicaciones. Si el servidor de aplicaciones no define el dominio, el valor predeterminado es adobe.com.

**ServiceType:** AdobeService es el nombre que se utiliza para enumerar todos los servicios.

**AdobeServiceName:** Nombre del servicio o ID del servicio.

**Versión:** Versión del servicio.

**Estadísticas de operación**

**Tiempo de invocación:** Tiempo necesario para la ejecución del método . Esta invocación no incluye el tiempo de serialización, transferencia de cliente a servidor y deserialización de la solicitud.

**Recuento de invocaciones:** Número de veces que se invoca el servicio.

**Tiempo promedio de invocación:** Promedio de tiempo de todas las invocaciones que se han ejecutado desde que se inició el servidor.

**Tiempo máximo de invocación:** La duración de la invocación más larga que se ha ejecutado desde que se inició el servidor.

**Tiempo mínimo de invocación:** La duración de la invocación más corta que se ha ejecutado desde que se inició el servidor.

**Recuento de excepciones:** Número de invocaciones que han resultado en errores.

**Mensaje de excepción:** Mensaje de error de la última excepción que se produjo.

**Hora de la fecha del último muestreo:** La fecha de la última invocación.

**Unidad de tiempo:** El valor predeterminado es milisegundo.

Para habilitar la monitorización JMX, los servidores de aplicaciones generalmente necesitan alguna configuración. Consulte la documentación del servidor de aplicaciones para conocer los detalles específicos.

### Ejemplos de cómo configurar el acceso JMX abierto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - configurar el inicio de JVM**

Para ver MBeans desde JConsole, configure los parámetros de inicio de JVM del servidor de aplicaciones JBoss. Asegúrese de que JBoss se inicia desde el archivo run.bat/sh.

1. Edite el archivo run.bat que se encuentra en InstallJBoss/bin.
1. Busque la línea JAVA_OPTS y añada lo siguiente:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10: configurar el inicio de JVM**

1. Edite el archivo startWebLogic.bat que se encuentra en `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Busque la línea JAVA_OPTS y añada lo siguiente:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Reinicie WebLogic.

>[!NOTE]
>
>Para WebLogic, puede acceder a MBean mediante remoto o IIOP.

**Acceso remoto a MBean**

1. Inicie JConsole para obtener una nueva conexión y haga clic en la pestaña remota .
1. Introduzca el nombre de host y el puerto (9088, el número especificado durante las opciones de inicio de JVM).

**WebSphere® 6.1: configurar el inicio de JVM**

1. En el Admin Console (Application server > server1 > Process Definition > JVM), añada la línea siguiente al campo para el Argumento genérico de JVM:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Añada o quite el comentario de las tres líneas siguientes en el archivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie WebSphere.
