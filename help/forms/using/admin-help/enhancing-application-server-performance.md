---
title: Mejora del rendimiento del servidor de aplicaciones
seo-title: Mejora del rendimiento del servidor de aplicaciones
description: Este documento describe los ajustes opcionales que puede configurar para mejorar el rendimiento del servidor de aplicaciones de formularios AEM.
seo-description: Este documento describe los ajustes opcionales que puede configurar para mejorar el rendimiento del servidor de aplicaciones de formularios AEM.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# Mejora del rendimiento del servidor de aplicaciones{#enhancing-application-server-performance}

Este contenido describe la configuración opcional que puede configurar para mejorar el rendimiento del servidor de aplicaciones de formularios AEM.

## Configuración de las fuentes de datos del servidor de aplicaciones {#configuring-application-server-data-sources}

AEM formularios utiliza el repositorio de AEM formularios como su origen de datos. El repositorio de AEM formularios almacena los recursos de la aplicación y, en tiempo de ejecución, los servicios pueden recuperar recursos del repositorio como parte de la finalización de un proceso comercial automatizado.

El acceso al origen de datos puede ser significativo, en función del número de módulos de formularios AEM que esté ejecutando y del número de usuarios simultáneos que accedan a la aplicación. El acceso a la fuente de datos se puede optimizar mediante el agrupamiento de conexiones. *La* agrupación de conexiones es una técnica que se utiliza para evitar la sobrecarga de realizar nuevas conexiones de base de datos cada vez que una aplicación u objeto de servidor requiere acceso a la base de datos. El agrupamiento de conexiones se utiliza generalmente en aplicaciones basadas en la Web y en aplicaciones empresariales, y normalmente lo gestiona un servidor de aplicaciones, pero no se limita a él.

Es importante configurar correctamente los parámetros del grupo de conexiones para que nunca se queden sin conexiones, lo que puede ocasionar que el rendimiento de la aplicación se deteriore.

Para configurar correctamente la configuración del grupo de conexiones, es importante que el administrador del servidor de aplicaciones supervise el grupo de conexiones durante las horas punta del día. La supervisión garantiza que haya suficientes conexiones disponibles para las aplicaciones y los usuarios en todo momento. La mayoría de los servidores de aplicaciones incluyen herramientas de monitoreo.

Puede supervisar varias estadísticas para cada instancia de origen de datos JDBC en su dominio mediante la Consola de administración de WebLogic Server. Consulte la documentación de WebLogic para obtener más información.

Cuando el administrador del servidor de aplicaciones determina la configuración correcta del grupo de conexiones, esa persona debe comunicar esta información al administrador de la base de datos. El administrador de la base de datos necesita esta información porque el número de conexiones de la base de datos es igual al número de conexiones del grupo de conexiones para el origen de datos. A continuación, complete los pasos para configurar la configuración del grupo de conexiones para el servidor de aplicaciones y el tipo de fuente de datos como se describe a continuación.

### Configurar la configuración del grupo de conexiones para WebLogic para Oracle y MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. En Estructura de dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en IDP_DS.
1. En la pantalla siguiente, haga clic en la ficha Configuración > Grupo de conexiones e introduzca un valor en los cuadros siguientes:

   * Capacidad inicial
   * Capacidad máxima
   * Aumento de capacidad
   * Tamaño de caché de instrucciones

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configurar la configuración del grupo de conexiones para WebLogic para SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. En Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en EDC_DS.
1. En la pantalla siguiente, haga clic en la ficha Configuración > Grupo de conexiones e introduzca un valor en los cuadros siguientes:

   * Capacidad inicial
   * Capacidad máxima
   * Aumento de capacidad
   * Tamaño de caché de instrucciones

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configurar la configuración del grupo de conexiones para WebSphere para DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC. En el panel derecho, haga clic en el origen de datos que ha creado, ya sea DB2 Universal JDBC Driver Provider o LiveCycle - db2 - IDP_DS.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la pantalla siguiente, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Número máximo de conexiones y en el cuadro Conexiones mínimas.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

### Configurar la configuración del grupo de conexiones para WebSphere para Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC. En el panel derecho, haga clic en el origen de datos del controlador JDBC de Oracle que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la pantalla siguiente, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Número máximo de conexiones y en el cuadro Conexiones mínimas.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

### Configurar la configuración del grupo de conexiones para WebSphere para SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC y, en el panel derecho, haga clic en el origen de datos de controlador JDBC definido por el usuario que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la pantalla siguiente, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Número máximo de conexiones y en el cuadro Conexiones mínimas:
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

## Optimización de documentos en línea e impacto en la memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Si normalmente procesa documentos de un tamaño relativamente pequeño, puede mejorar el rendimiento asociado con la velocidad de transferencia de documento y el espacio de almacenamiento. Para ello, implemente las siguientes configuraciones de producto de formularios AEM:

* Aumente el tamaño de línea máximo del documento predeterminado para AEM formularios de modo que sea mayor que el tamaño de la mayoría de los documentos.
* Para procesar archivos más grandes, especifique los directorios de almacenamiento que se encuentran en un sistema de discos de alta velocidad o un disco RAM.

El tamaño de línea máximo y los directorios de almacenamiento (el directorio de archivos temporales de formularios AEM y el directorio GDS) se configuran en la consola de administración.

### Tamaño de documento y tamaño de línea máximo {#document-size-and-maximum-inline-size}

Cuando un documento enviado para su procesamiento por AEM formularios es menor o igual al tamaño en línea máximo de documento predeterminado, el documento se almacena en el servidor en línea y el documento se serializa como objeto de Documento de Adobe. El almacenamiento de documentos en línea puede tener importantes beneficios de rendimiento. Sin embargo, si utiliza el flujo de trabajo de formularios, el contenido también puede almacenarse en la base de datos para realizar un seguimiento. Por lo tanto, aumentar el tamaño de línea máximo puede afectar al tamaño de la base de datos.

Un documento mayor que el tamaño máximo en línea se almacena en el sistema de archivos local. El objeto de Documento de Adobe que se transfiere desde y hacia el servidor es sólo un puntero a ese archivo.

Cuando el contenido de documento está alineado (es decir, es menor que el tamaño en línea máximo), el contenido se almacena en la base de datos como parte de la carga útil de serialización del documento. Por lo tanto, aumentar el tamaño de línea máximo puede afectar al tamaño de la base de datos.

**Cambiar el tamaño de línea máximo**

1. En la consola de administración, haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. Introduzca un valor en el cuadro Tamaño en línea máximo de Documento predeterminado y haga clic en Aceptar.

   >[!NOTE]
   >
   >El valor de la propiedad Tamaño en línea máximo de Documento debe ser idéntico para AEM Forms en el entorno JEE y AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE. Este paso actualiza el valor solo para AEM Forms en el entorno JEE y no para AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE.

1. Reinicie el servidor de aplicaciones con la siguiente propiedad del sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La propiedad del sistema antes mencionada anula el valor de la propiedad Tamaño en línea máximo de Documento establecida para AEM Forms en el entorno JEE y AEM Forms en el paquete OSGi incluye AEM Forms en el entorno JEE.

>[!NOTE]
>
>El tamaño en línea máximo predeterminado es 65536 bytes.

### Tamaño máximo del montón JVM {#jvm-maximum-heap-size}

Un aumento en el tamaño de línea máximo requiere más memoria para almacenar los documentos serializados. Por lo tanto, generalmente también requiere un aumento en el tamaño máximo del montón JVM.

Un sistema muy cargado que procesa muchos documentos puede saturar rápidamente la memoria de montón JVM. Para evitar un OutOfMemoryError, aumente el tamaño máximo del montón JVM en una cantidad correspondiente al tamaño de los documentos en línea multiplicados por el número de documentos que se ejecutan normalmente en un momento dado.

Aumento del tamaño máximo del montón JVM = (tamaño de documentos en línea) x (número medio de documentos procesados).

**Calcular el tamaño máximo del montón de JVM**

En este ejemplo, la pila máxima de JVM actual se establece en 512 MB y el tamaño máximo en línea es de 64 KB. El servidor debe configurarse para el escenario en el que se ejecutan 10 trabajos simultáneamente y cada trabajo tiene 9 archivos de entrada y 1 archivo de resultado (un total de 10 archivos por trabajo y 100 archivos procesados simultáneamente). Todos los archivos tienen un tamaño inferior a 512 KB.

Para almacenar todos los archivos en línea, establezca el tamaño máximo en línea de al menos 512 KB.

El aumento requerido en el tamaño máximo del montón JVM se calcula mediante la siguiente ecuación:

(512 KB) x (100) = 51200 KB o 50 MB

El tamaño máximo del montón JVM debe aumentarse en 50 MB para un total de 562 MB.

**Consideración de la fragmentación del montón**

La configuración del tamaño de los documentos en línea en valores grandes aumenta el riesgo de que se produzca un error OutOfMemoryError en los sistemas que son propensos a la fragmentación del montón. Para almacenar un documento en línea, la memoria de pila JVM debe tener suficiente espacio contiguo. Algunos sistemas operativos, JVM y algoritmos de recolección de elementos no utilizados son propensos a la fragmentación del montón. La fragmentación reduce la cantidad de espacio de montón contiguo y puede generar un OutOfMemoryError incluso cuando existe suficiente espacio libre total.

Por ejemplo, las operaciones anteriores en el servidor de aplicaciones dejaron el montón JVM en un estado fragmentado y el recolector de elementos no utilizados no puede compactar el montón lo suficiente para recuperar grandes bloques de espacio libre. Se puede producir un OutOfMemoryError aunque el tamaño máximo del montón JVM se haya ajustado para aumentar el tamaño máximo en línea.

Para tener en cuenta la fragmentación del montón, el tamaño del documento en línea no debe ser superior al 0,1 % del tamaño total del montón. Por ejemplo, un tamaño máximo de pila JVM de 512 MB puede admitir un tamaño máximo en línea de 512 MB x 0,001 = 0,512 MB o 512 KB.

## Mejoras en el servidor de aplicaciones WebSphere {#websphere-application-server-enhancements}

Esta sección describe la configuración específica de un entorno de servidor de aplicaciones WebSphere.

### Aumento de la memoria máxima asignada a la JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Si está ejecutando Configuration Manager o está intentando generar código de implementación de JavaBeans (EJB) Enterprise mediante la utilidad de línea de comandos *ejbdeploy* y se produce un error OutOfMemory, aumente la cantidad de memoria asignada a JVM.

1. Edite la secuencia de comandos ejbdeploy en el directorio *[appserver root]*/DeployTool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux y UNIX) `ejbdeploy.sh`

1. Busque el parámetro `-Xmx256M` y cámbielo a un valor más alto, como `-Xmx1024M`.
1. Guarde el archivo.
1. Ejecute el comando `ejbdeploy` o vuelva a implementar con Configuration Manager.

## Mejora del rendimiento de Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Este contenido describe la configuración específica de un entorno del sistema operativo Microsoft Windows Server 2003.

El uso de la agrupación de conexiones en la conexión de búsqueda puede reducir el número de puertos necesarios hasta en un 50%. Esto se debe a que la conexión siempre utiliza las mismas credenciales para un dominio determinado y el contexto y los objetos relacionados se cierran explícitamente.

### Configure Windows Server para el agrupamiento de conexiones {#configure-your-windows-server-for-connection-pooling}

1. Haga clic en Inicio > Ejecutar para inicio del editor del Registro y, en el cuadro Abrir, escriba `regedit` y haga clic en Aceptar.
1. Vaya a la clave del Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. En el panel derecho del editor del Registro, busque el nombre del valor TcpTimedWaitDelay. Si el nombre no aparece, seleccione Editar > Nuevo > Valor DWORD en la barra de menús para agregar el nombre.
1. En el cuadro Nombre, escriba `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Si no ve un cursor parpadeante y `New Value #` dentro del cuadro, haga clic con el botón derecho en el panel derecho, seleccione Cambiar nombre y, en el cuadro Nombre, escriba `TcpTimedWaitDelay`*.*

1. Repita el paso 4 para los nombres de valor MaxUserPort, MaxHashTableSize y MaxFreeTcbs.
1. Haga clic con el doble en el panel derecho para establecer el valor TcpTimedWaitDelay. En Base, seleccione Decimal y, en el cuadro Valor, escriba `30`.
1. Haga clic con el doble en el panel derecho para establecer el valor de MaxUserPort. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65534`.
1. Haga clic con el doble dentro del panel derecho para establecer el valor de MaxHashTableSize. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65536`.
1. Haga clic con el doble en el panel derecho para establecer el valor de MaxFreeTcbs. En Base, seleccione Decimal y, en el cuadro Valor, escriba `16000`.

>[!NOTE]
>
>Se pueden producir problemas graves si modifica incorrectamente el Registro mediante el Editor del Registro o mediante otro método. Estos problemas pueden requerir la reinstalación del sistema operativo. Modifique el registro por su propia cuenta y riesgo.

