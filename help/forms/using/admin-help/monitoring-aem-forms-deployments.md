---
title: Supervisar las implementaciones de AEM Forms
seo-title: Monitoring AEM forms deployments
description: AEM Puede monitorizar las implementaciones de formularios de desde el nivel del sistema y desde un nivel interno. AEM Obtenga más información sobre la monitorización de implementaciones de formularios en el documento.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# Supervisar las implementaciones de AEM Forms {#monitoring-aem-forms-deployments}

AEM Puede monitorizar las implementaciones de formularios de desde el nivel del sistema y desde un nivel interno. Puede utilizar herramientas de administración especializadas como HP OpenView, IBM Tivoli, CA UniCenter y un monitor JMX de terceros llamado *JConsole* para monitorizar específicamente la actividad de Java. AEM La implementación de una estrategia de monitorización mejora la disponibilidad, la fiabilidad y el rendimiento de las implementaciones de los formularios de la.

AEM Para obtener más información sobre la monitorización de las implementaciones de formularios en la aplicación, consulte [AEM Una guía técnica para monitorizar las implementaciones de formularios en la](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## Monitorización mediante MBeans {#monitoring-using-mbeans}

AEM Los formularios de proporcionan dos MBeans registrados que proporcionan información estadística y de navegación. Estos son los únicos MBeans compatibles con la integración y la inspección:

* **Estadísticas de servicio:** Este MBean proporciona información sobre el nombre del servicio y su versión.
* **Estadísticas de operación:** Este MBean proporciona las estadísticas de cada servicio del servidor de Forms. Aquí es donde los administradores pueden obtener información sobre un servicio en particular, como el tiempo de invocación, el número de errores, etc.

### Interfaces públicas de ServiceStatisticsMbean {#servicestatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas del MBean ServiceStatistics para realizar pruebas:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas de OperationStatisticsMbean {#operationstatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas del MBean OperationStatistics para realizar pruebas:

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

### Estadísticas de árbol y funcionamiento de MBean {#mbean-tree-operation-statistics}

Mediante una consola JMX (JConsole), las estadísticas del MBean OperationStatistics están disponibles. Estas estadísticas son atributos de MBean y se pueden navegar en el siguiente árbol de jerarquías:

**Árbol MBean**

**Nombre de dominio de Adobe:** Depende del servidor de aplicaciones. Si Application Server no define el dominio, el valor predeterminado es adobe.com.

**Tipo de servicio:** AdobeService es el nombre que se utiliza para enumerar todos los servicios.

**AdobeServiceName:** Nombre o ID del servicio.

**Versión:** Versión del servicio.

**Estadísticas de operación**

**Hora de invocación:** Tiempo empleado para la ejecución del método. Esto no incluye el tiempo en que la solicitud se serializa, se transfiere del cliente al servidor y se deserializa.

**Recuento de invocaciones:** El número de veces que se invoca el servicio.

**Tiempo medio de invocación:** Tiempo promedio de todas las invocaciones que se han ejecutado desde que se inició el servidor.

**Tiempo máximo de invocación:** La duración de la invocación más larga que se ha ejecutado desde que se inició el servidor.

**Tiempo mínimo de invocación:** La duración de la invocación más corta que se ha ejecutado desde que se inició el servidor.

**Recuento de excepciones:** Número de invocaciones que han dado lugar a errores.

**Mensaje de excepción:** El mensaje de error de la última excepción que se produjo.

**Hora de la última fecha de muestreo:** La fecha de la última invocación.

**Unidad de tiempo:** El valor predeterminado es milisegundo.

Para habilitar la monitorización JMX, los servidores de aplicaciones suelen necesitar alguna configuración. Consulte la documentación del servidor de aplicaciones para conocer los detalles específicos.

### Ejemplos de cómo configurar el acceso JMX abierto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configurar el inicio de JVM**

Para ver MBeans desde JConsole, configure los parámetros de inicio de JVM del servidor de aplicaciones JBoss. Asegúrese de que JBoss se inicia desde el archivo run.bat/sh.

1. Edite el archivo run.bat ubicado en InstallJBoss/bin.
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
>Para WebLogic, puede acceder al MBean mediante Remote o IIOP.

**Acceder al MBean de forma remota**

1. Inicie JConsole para una nueva conexión y haga clic en la pestaña remota.
1. Introduzca el nombre de host y el puerto (9088, el número que especifique durante las opciones de inicio de JVM).

**Websphere 6.1: configurar el inicio de JVM**

1. En Admin Console (Servidor de aplicaciones > server1 > Definición de procesos > JVM), añada la siguiente línea al campo Argumento de JVM genérico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Añada o quite los comentarios de las tres líneas siguientes en el archivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie WebSphere.
