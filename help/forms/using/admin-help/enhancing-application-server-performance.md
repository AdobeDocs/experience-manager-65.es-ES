---
title: Mejora del rendimiento del servidor de aplicaciones
seo-title: Enhancing application server performance
description: Este documento describe la configuración opcional que puede configurar para mejorar el rendimiento del servidor de aplicaciones de formularios AEM.
seo-description: This document describes optional settings that you can configure to improve the performance of your AEM forms application server.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# Mejora del rendimiento del servidor de aplicaciones{#enhancing-application-server-performance}

Este contenido describe la configuración opcional que puede configurar para mejorar el rendimiento del servidor de aplicaciones de formularios AEM.

## Configuración de fuentes de datos del servidor de aplicaciones {#configuring-application-server-data-sources}

AEM formularios utiliza el repositorio de AEM formularios como su origen de datos. El repositorio de AEM forms almacena recursos de aplicaciones y, en tiempo de ejecución, los servicios pueden recuperar recursos del repositorio como parte de la finalización de un proceso empresarial automatizado.

El acceso al origen de datos puede ser significativo, dependiendo del número de módulos de formularios AEM que esté ejecutando y del número de usuarios simultáneos que accedan a la aplicación. El acceso a la fuente de datos se puede optimizar mediante la agrupación de conexiones. *Agrupación de conexiones* es una técnica que se utiliza para evitar la sobrecarga de realizar nuevas conexiones de base de datos cada vez que una aplicación u objeto de servidor requiere acceso a la base de datos. La agrupación de conexiones se utiliza generalmente en aplicaciones basadas en web y de empresa y normalmente la gestiona un servidor de aplicaciones, pero no se limita a ellas.

Es importante configurar correctamente los parámetros del grupo de conexiones para que nunca se queden sin conexiones, lo que puede provocar que el rendimiento de la aplicación se deteriore.

Para configurar correctamente la configuración del grupo de conexiones, es importante que el administrador del servidor de aplicaciones supervise el grupo de conexiones durante las horas punta del día. La supervisión garantiza que haya suficientes conexiones disponibles para aplicaciones y usuarios en todo momento. La mayoría de los servidores de aplicaciones incluyen herramientas de monitorización.

Puede monitorizar varias estadísticas para cada instancia de fuente de datos JDBC en su dominio utilizando la consola de administración del servidor de WebLogic. Consulte la documentación de WebLogic para obtener más información.

Cuando el administrador del servidor de aplicaciones determina la configuración correcta del grupo de conexiones, esa persona debe comunicar esta información al administrador de la base de datos. El administrador de la base de datos necesita esta información porque el número de conexiones de la base de datos es igual al número de conexiones del grupo de conexiones del origen de datos. A continuación, complete los pasos para configurar la configuración del grupo de conexiones para su servidor de aplicaciones y el tipo de fuente de datos como se describe a continuación.

### Configuración del grupo de conexiones para WebLogic para Oracle y MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. En Estructura del dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en IDP_DS.
1. En la siguiente pantalla, haga clic en la ficha Configuración > Agrupamiento de conexiones e introduzca un valor en los cuadros siguientes:

   * Capacidad inicial
   * Capacidad máxima
   * Aumento de capacidad
   * Tamaño de caché de instrucciones

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configuración del grupo de conexiones para WebLogic para SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. En Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura del dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en EDC_DS.
1. En la siguiente pantalla, haga clic en la ficha Configuración > Agrupamiento de conexiones e introduzca un valor en los cuadros siguientes:

   * Capacidad inicial
   * Capacidad máxima
   * Aumento de capacidad
   * Tamaño de caché de instrucciones

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configuración del grupo de conexiones para WebSphere para DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores de JDBC. En el panel derecho, haga clic en la fuente de datos que ha creado, ya sea Proveedor de controladores JDBC universal DB2 o LiveCycle - db2 - IDP_DS.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Conexiones máximas y en el cuadro Conexiones mínimas.
1. Haga clic en Aceptar o en Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.

### Configuración del grupo de conexiones para WebSphere para Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores de JDBC. En el panel derecho, haga clic en el origen de datos Controlador JDBC de Oracle que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Conexiones máximas y en el cuadro Conexiones mínimas.
1. Haga clic en Aceptar o en Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.

### Configurar la configuración del grupo de conexiones para WebSphere para SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC y, en el panel derecho, haga clic en la fuente de datos del controlador JDBC definido por el usuario que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Conexiones máximas y en el cuadro Conexiones mínimas :
1. Haga clic en Aceptar o en Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.

## Optimización de documentos en línea e impacto en la memoria de JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Si suele procesar documentos de un tamaño relativamente pequeño, puede mejorar el rendimiento asociado con la velocidad de transferencia de documentos y el espacio de almacenamiento. Para ello, implemente las siguientes configuraciones de producto de AEM forms:

* Aumente el tamaño máximo en línea del documento predeterminado para AEM formularios, de modo que sea mayor que el tamaño de la mayoría de los documentos.
* Para procesar archivos más grandes, especifique los directorios de almacenamiento que se encuentran en un sistema de disco de alta velocidad o un disco RAM.

El tamaño máximo en línea y los directorios de almacenamiento (el directorio de archivos temporales de formularios AEM y el directorio GDS) se configuran en la consola de administración.

### Tamaño de documento y tamaño de línea máximo {#document-size-and-maximum-inline-size}

Cuando un documento enviado para su procesamiento por formularios AEM es menor o igual que el tamaño en línea máximo del documento predeterminado, el documento se almacena en línea en el servidor y el documento se serializa como un objeto Documento de Adobe. Almacenar documentos en línea puede tener importantes ventajas en el rendimiento. Sin embargo, si utiliza el flujo de trabajo de formularios, el contenido también puede almacenarse en la base de datos para realizar un seguimiento. Por lo tanto, el aumento del tamaño máximo en línea puede afectar al tamaño de la base de datos.

Un documento que es mayor que el tamaño en línea máximo se almacena en el sistema de archivos local. El objeto Documento de Adobe que se transfiere desde y hacia el servidor es sólo un puntero a ese archivo.

Cuando el contenido del documento está en línea (es decir, es inferior al tamaño en línea máximo), el contenido se almacena en la base de datos como parte de la carga útil de serialización del documento. Por lo tanto, el aumento del tamaño máximo en línea puede afectar al tamaño de la base de datos.

**Cambiar el tamaño de línea máximo**

1. En la consola de administración, haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. Introduzca un valor en el cuadro Tamaño de línea máximo del documento predeterminado y haga clic en Aceptar.

   >[!NOTE]
   >
   >El valor de la propiedad Tamaño en línea máximo del documento debe ser idéntico para AEM Forms en el entorno JEE y AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE. Estos pasos actualizaron el valor solo para AEM Forms en el entorno JEE y no para AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE.

1. Reinicie el servidor de aplicaciones con la siguiente propiedad del sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La propiedad del sistema mencionada anteriormente anula el valor de la propiedad Tamaño en línea máximo del documento establecida para AEM Forms en el entorno JEE y AEM Forms en el paquete OSGi incluye AEM Forms en el entorno JEE.

>[!NOTE]
>
>El tamaño en línea máximo predeterminado es de 65536 bytes.

### Tamaño máximo de pila de JVM {#jvm-maximum-heap-size}

Un aumento en el tamaño máximo en línea requiere más memoria para almacenar los documentos serializados. Por lo tanto, generalmente también requiere un aumento en el tamaño máximo de pila de JVM.

Un sistema muy cargado que está procesando muchos documentos puede saturar rápidamente la memoria de pila de JVM. Para evitar un error OutOfMemoryError, aumente el tamaño máximo de pila de JVM en una cantidad correspondiente al tamaño de los documentos en línea multiplicado por el número de documentos que normalmente se ejecutan en un momento determinado.

Aumento del tamaño máximo de pila de JVM = (tamaño de documentos en línea) x (número promedio de documentos procesados).

**Cálculo del tamaño máximo de pila de JVM**

En este ejemplo, la pila máxima actual de JVM se establece en 512 MB y el tamaño máximo en línea es de 64 KB. El servidor debe configurarse para el escenario en el que se ejecutan 10 trabajos simultáneamente, y cada trabajo tiene 9 archivos de entrada y 1 archivo de resultado (un total de 10 archivos por trabajo y 100 archivos procesados simultáneamente). Todos los archivos tienen un tamaño inferior a 512 kB.

Para almacenar todos los archivos en línea, establezca el tamaño máximo en línea en al menos 512 KB.

El aumento requerido en el tamaño máximo de pila de JVM se calcula mediante la siguiente ecuación:

(512 KB) x (100) = 51200 KB o 50 MB

El tamaño máximo de pila de JVM debe aumentarse en 50 MB para un total de 562 MB.

**Consideración de la fragmentación de montículos**

Establecer el tamaño de los documentos en línea en valores grandes aumenta el riesgo de un error OutOfMemoryError en sistemas que son propensos a una fragmentación en montículos. Para almacenar un documento en línea, la memoria de pila de JVM debe tener suficiente espacio contiguo. Algunos sistemas operativos, JVM y algoritmos de recolección de basura son propensos a la fragmentación de montones. La fragmentación reduce la cantidad de espacio en pilas contiguo y puede provocar un error OutOfMemoryError incluso cuando existe suficiente espacio libre total.

Por ejemplo, las operaciones anteriores en el servidor de aplicaciones dejaron la pila de JVM en un estado fragmentado, y el recolector de basura no puede compactar la pila lo suficiente para recuperar grandes bloques de espacio libre. Se puede producir un OutOfMemoryError aunque el tamaño máximo de pila de JVM se haya ajustado para un aumento en el tamaño máximo en línea.

Para tener en cuenta la fragmentación de montículos, el tamaño del documento en línea no debe ser superior al 0,1 % del tamaño total de montículos. Por ejemplo, un tamaño máximo de pila de JVM de 512 MB puede admitir un tamaño máximo en línea de 512 MB x 0,001 = 0,512 MB o 512 KB.

## Mejoras en el servidor de aplicaciones WebSphere {#websphere-application-server-enhancements}

En esta sección se describe la configuración específica de un entorno WebSphere Application Server.

### Aumento de la memoria máxima asignada a la JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Si está ejecutando Configuration Manager o está intentando generar código de implementación de Enterprise JavaBeans (EJB) utilizando la utilidad de línea de comandos *ejbdeploy* y se produce un error OutOfMemory, aumenta la cantidad de memoria asignada a JVM.

1. Edite la secuencia de comandos ejbdeploy en la sección *[raíz de appserver]*/deploy tool/itp/ directorio:

   * (Windows) `ejbdeploy.bat`
   * (Linux y UNIX) `ejbdeploy.sh`

1. Busque la `-Xmx256M` y cambie a un valor superior, como `-Xmx1024M`.
1. Guarde el archivo.
1. Ejecute el `ejbdeploy` o volver a implementar mediante Configuration Manager.

## Mejora del rendimiento de Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Este contenido describe la configuración específica de un entorno de sistema operativo Microsoft Windows Server 2003.

El uso de la agrupación de conexiones en la conexión de búsqueda puede reducir el número de puertos necesarios hasta en un 50%. Esto se debe a que esa conexión siempre utiliza las mismas credenciales para un dominio determinado y el contexto y los objetos relacionados se cierran explícitamente.

### Configurar Windows Server para el agrupamiento de conexiones {#configure-your-windows-server-for-connection-pooling}

1. Haga clic en Inicio > Ejecutar para iniciar el editor del Registro y, en el cuadro Abrir, escriba `regedit` y haga clic en Aceptar.
1. Vaya a la clave del Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. En el panel derecho del editor del Registro, busque el nombre del valor TcpTimedWaitDelay . Si no aparece el nombre, seleccione Editar > Nuevo > Valor DWORD en la barra de menús para agregar el nombre.
1. En el cuadro Nombre, escriba `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Si no ve un cursor parpadeante y `New Value #` dentro del cuadro, haga clic con el botón derecho en el panel derecho, seleccione Cambiar nombre y, en el cuadro Nombre, escriba `TcpTimedWaitDelay`*.*

1. Repita el paso 4 para los nombres de valor MaxUserPort, MaxHashTableSize y MaxFreeTcbs.
1. Haga doble clic dentro del panel derecho para establecer el valor TcpTimedWaitDelay . En Base, seleccione Decimal y, en el cuadro Valor, escriba `30`.
1. Haga doble clic dentro del panel derecho para establecer el valor MaxUserPort. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65534`.
1. Haga doble clic dentro del panel derecho para establecer el valor MaxHashTableSize. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65536`.
1. Haga doble clic dentro del panel derecho para establecer el valor MaxFreeTcbs. En Base, seleccione Decimal y, en el cuadro Valor, escriba `16000`.

>[!NOTE]
>
>Pueden producirse problemas graves si modifica el registro incorrectamente utilizando el Editor del Registro o utilizando otro método. Estos problemas pueden requerir la reinstalación del sistema operativo. Modifique el registro por su cuenta y riesgo.
