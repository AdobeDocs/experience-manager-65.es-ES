---
title: ¿Cómo configurar y solucionar problemas de un AEM Forms en un clúster de servidores JEE?
description: Obtenga información sobre cómo configurar y solucionar problemas de una AEM Forms en un clúster de servidores JEE
source-git-commit: 8502e0227819372db4120d3995fba51c7401d944
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# Configuración y solución de problemas de un AEM Forms en un clúster de servidores JEE {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## Conocimientos previos {#prerequisites}

Familiaridad con AEM Forms en JEE, JBoss, WebSphere y servidores de aplicaciones web, Red Hat Linux, SUSE Linux, Microsoft Windows, IBM AIX o Sun Solaris, Oracle, servidores de bases de datos IBM DB2 o SQL Server y entornos web.

## Nivel de usuario {#user-level}

Avanzado 

Un AEM Forms en JEE Cluster es una topología diseñada para permitir que AEM Forms en JEE sea resistente al fallo de un nodo de clúster y para escalar la capacidad del sistema más allá de las capacidades de un solo nodo. Un clúster combina varios nodos en un único sistema lógico que comparte datos y permite que las transacciones abarquen varios nodos en su ejecución. Un clúster es la manera más general de escalar AEM Forms en JEE, en el sentido de que cualquier combinación de servicios que gestionen cualquier combinación de cargas de trabajo puede ser soportada. Un clúster de AEM Forms en JEE no es necesariamente el mejor para todos los tipos de implementaciones, y en particular, una arquitectura de equilibrio de carga de servidor no agrupada puede ser apropiada en muchos casos.

El propósito de este documento es discutir los requisitos de configuración específicos y las áreas de problemas potenciales que puede encontrar con un clúster de AEM Forms en JEE.

## ¿Qué hay en un clúster? {#what-is-in-cluster}

Los nodos de clúster de AEM Forms en JEE se comunican entre ellos y comparten información para permitir que el clúster en su conjunto tenga una única configuración coherente y un solo estado de aplicación. El intercambio de información dentro del clúster se realiza de varias formas diferentes simultáneamente que se utilizan en diferentes contextos. Los métodos básicos de intercambio de información se ilustran en la figura siguiente:

![Clúster del servidor de aplicaciones](assets/application-server-cluster.jpg)

### Clúster del servidor de aplicaciones {#application-server-cluster}

Un clúster de AEM Forms en JEE se basa en las capacidades de agrupación en clúster del servidor de aplicaciones subyacente. Los clústeres de servidores de aplicaciones permiten administrar la configuración del clúster en su conjunto y proporcionan servicios de clúster de bajo nivel, como Java Naming and Directory Interface (JNDI), que permiten que los componentes de software se encuentren entre sí dentro del clúster. La sofisticación de los servicios de clúster y las dependencias técnicas subyacentes que tiene el servidor de aplicaciones dependen del servidor de aplicaciones. WebSphere y WebLogic tienen funcionalidades sofisticadas de administración para clústeres, mientras que JBoss tiene un enfoque muy básico.

### Caché de GemFire {#gemfire-cache}

La caché de GemFire es un mecanismo de caché distribuido implementado en cada nodo de clúster. Los nodos se encuentran entre sí y crean una única caché lógica que se mantiene coherente entre los nodos. Los nodos que se encuentran entre sí se unen para mantener una sola caché nocional que se muestra como una nube en la Figura 1. A diferencia de GDS y la base de datos, la caché es una entidad puramente nocional. El contenido en caché real se almacena en la memoria y en el directorio `LC_TEMP` de cada uno de los nodos del clúster.

### Base de datos {#database}

Todos los nodos del clúster comparten la base de datos AEM Forms on JEE (a la que se accede a través de las fuentes de datos JDBC IDP_DS, EDC_DS y otros). La mayoría de los datos persistentes relacionados con el estado de AEM Forms en JEE, como qué transacciones están en curso, los datos de usuario asociados con transacciones en curso, los datos sobre cómo se ha establecido la configuración del sistema, etc., se encuentran en esta base de datos.

### Almacenamiento global de documentos {#global-document-storage}

Global Document Storage (GDS) es un área de almacenamiento basada en file system que utiliza Document Manager (clase IDPDocument) en AEM Forms en JEE. El GDS almacena archivos de corta duración y de larga duración que deben ser accesibles para todos los nodos del clúster.

### Otros elementos {#other-items}

Además de estos recursos compartidos principales, hay otros elementos que tienen un comportamiento de clúster específico, como Quartz. Quartz es un subsistema de programador utilizado por AEM Forms en JEE, y utiliza tablas de base de datos para mantener sus conocimientos sobre lo que se ha programado y qué actividades programadas se están ejecutando. Quartz debe configurarse de forma diferente para instalaciones de un solo nodo y clústeres, y toma su ejemplo de otros AEM Forms en la configuración de JEE.

## Problemas comunes de configuración {#common-configuration}

Una de las cosas más frustrantes sobre el mantenimiento o la solución de problemas de un AEM Forms en un clúster JEE es que no hay un lugar único para confirmar positivamente que el clúster esté en buen estado. Para confirmar que todo está bien en el clúster, se requiere cierta investigación y análisis, y hay varios modos de fallo para el funcionamiento del clúster, dependiendo de lo que esté mal con la configuración del clúster. La figura siguiente ilustra un clúster mal configurado en el que varios de los recursos compartidos no se comparten correctamente.

![Clúster mal configurado](assets/bad-configuration-cluster.png)

Una cosa interesante e importante que hay que tener en cuenta es que debe estar familiarizado con la forma en que funciona la agrupación en clústeres y con los tipos de cosas que se deben buscar y verificar en un clúster, incluso si no tiene intención de ejecutar AEM Forms en JEE en un clúster. Esto se debe a que algunas partes de AEM Forms en JEE pueden tomar indicaciones sobre cómo operar en un clúster incorrectamente y asumir el comportamiento del clúster que no espera.

Entonces, ¿qué hay de malo en la configuración de uso compartido de la Figura anterior? Las secciones siguientes describen los problemas:

### (1) Configuración del clúster de GemFire {#gemfire-cluster-configuration}

Varias cosas pueden salir mal con la caché de Gemfire. Dos escenarios típicos son:

* Los nodos que deberían poder encontrarse entre sí no pueden hacerlo.

* Los nodos que no se supone que se deben agrupar se encuentran entre sí y comparten una caché cuando no deben hacerlo.

Si tiene nodos que desea agrupar, es esencial que se encuentren entre sí en la red. De forma predeterminada, lo hacen mediante mensajes UDP de multidifusión. Cada nodo envía mensajes de difusión anunciando que está presente, y cualquier nodo que reciba un mensaje de este tipo comienza a hablar con los demás nodos que encuentra. Este tipo de método de autodescubrimiento es muy común, y muchos tipos de software y dispositivos lo hacen.

Un problema común con la detección automática es que los mensajes de multidifusión pueden ser filtrados por la red como parte de la política de red o debido a las reglas del firewall de software, o simplemente no pueden enrutar a través de la red que existe entre nodos. Debido a la dificultad general de hacer que el autodescubrimiento UDP funcione en redes complejas, es una práctica habitual que las implementaciones de producción utilicen un método de descubrimiento alternativo: localizadores TCP. Se puede encontrar una discusión general de los localizadores TCP en las referencias.

**¿Cómo sé si estoy usando localizadores o UDP?**

Las siguientes propiedades de JVM controlan el método que utiliza la caché de GemFire para encontrar otros nodos.

Configuración de multidifusión:

* `adobe.cache.multicast-port`: Puerto de multidifusión utilizado para comunicarse con otros miembros del sistema distribuido. Si se establece en cero, la multidifusión se desactiva tanto para la detección de miembros como para la distribución.

* `gemfire.mcast-address` (opcional): Anula la dirección IP predeterminada utilizada por Gemfire.

Configuración del localizador TCP:

* `adobe.cache.cluster-locators`: La dirección IP/nombre de host del localizador TCP y el puerto del localizador TCP para todos los localizadores utilizados por los miembros del sistema para comunicarse con localizadores en ejecución.

La lista debe incluir todos los localizadores actualmente en uso y debe configurarse de manera coherente para cada miembro del sistema de clústeres.

Si la lista de localizadores TCP está vacía, no se utilizan localizadores y se utiliza el método de multidifusión en su lugar.

**¿Cómo puedo comprobar si mi localizador TCP se está ejecutando?**

Primero, si los localizadores TCP están en uso, debe tener los localizadores TCP listados en la siguiente propiedad JVM en todos los nodos del clúster:

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

No es necesario ejecutar los localizadores en AEM Forms en los nodos del clúster JEE; se pueden ejecutar en otros sistemas separados del clúster, si lo desea. Más de un sistema puede ejecutar localizadores, y por lo general se considera una práctica recomendada que los localizadores se ejecuten en dos ubicaciones frente a la posibilidad de que una sola falla de los localizadores pueda causar un problema con el reinicio del clúster. En cada uno de los sistemas que ejecutan localizadores, debe poder verificar que se están ejecutando utilizando los siguientes comandos en esos equipos:

`netstat -an | grep 22345`

La respuesta esperada debería ser esta:

`tcp 0 0 *.22345 *.* LISTEN`

Otro comando de verificación es este:

`ps -ef | grep gemfire`

La respuesta esperada debería tener un aspecto similar al siguiente:

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**¿Cómo veo qué nodos GemFire piensa que están en el clúster?**

GemFire produce información de registro que puede utilizarse para diagnosticar qué miembros del clúster han sido encontrados y adoptados por la caché de GemFire. Esto se puede usar para verificar que se encuentran todos los miembros del clúster correctos y que no se está produciendo ninguna detección de nodos del clúster adicional o incorrecta. El archivo de registro de GemFire se encuentra en el directorio temporal configurado de AEM Forms en JEE:

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

La cadena numérica después de `adobeZZ_` es única para el nodo de servidor y, por lo tanto, debe buscar el contenido real del directorio temporal. Los dos caracteres después de `adobe` dependen del tipo de servidor de la aplicación: `wl`, `jb` o `ws`.

Los siguientes registros de muestra muestran lo que sucede cuando se encuentra un clúster de dos nodos.

En el primer nodo, AP-HP8:

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

En el otro nodo, AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**¿Y si GemFire está encontrando nodos que no deberían?**

Cada clúster distinto que comparte una red corporativa debe utilizar un conjunto separado de localizadores TCP, si se utilizan localizadores TCP, o un número de puerto UDP independiente si se utiliza la configuración UDP de multidifusión. Dado que el autodescubrimiento UDP es la configuración predeterminada para AEM Forms en JEE, y el mismo puerto predeterminado, 33456, puede estar en uso por múltiples clústeres, es posible que los clústeres que no deberían estar intentando comunicarse puedan estar haciéndolo de forma inesperada; por ejemplo, los clústeres de producción y control de calidad deben permanecer separados, pero pueden conectarse entre sí a través de multidifusión UDP.

La situación más común en la que puede descubrir puertos duplicados en una red en la que GemFire está agrupando incorrectamente es durante el arranque de un clúster. Lo que puede encontrar es que el proceso de arranque falla sin causa clara. Normalmente, se ven errores como este:

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

En este caso, el bootstrapper está trabajando con GemFire para acceder a las tablas requeridas, y hay una incoherencia entre las tablas a las que se accede a través de JDBC y la información de la tabla almacenada en caché devuelta por GemFire, que proviene de un clúster diferente con una base de datos subyacente diferente.

Aunque un puerto duplicado a menudo se hará evidente durante el arranque, es posible que esta situación se muestre más tarde, cuando se reinicie un clúster después de estar inactivo cuando se produjo el arranque del otro clúster, o cuando la configuración de la red se cambie para que los clústeres que estaban previamente aislados, con fines de multidifusión, sean visibles entre sí.

Para diagnosticar estas situaciones, es mejor observar los registros de GemFire y considerar cuidadosamente si solo se están encontrando los nodos esperados. Para corregir el problema, es necesario cambiar la variable

`adobe.cache.multicast-port`

a un valor diferente en uno de los clústeres o en ambos.

### 2) Uso compartido de GDS {#gds-sharing}

El uso compartido de GDS se configura fuera de AEM Forms en el propio JEE, en el nivel O/S, donde debe organizar que la misma estructura de directorio compartido esté disponible para todos los nodos del clúster. En sistemas de tipo Windows, esto generalmente se logra configurando un recurso compartido de archivos de un nodo a otro, o desde un sistema de archivos remoto como un dispositivo NAS a todos los nodos. En sistemas UNIX, el uso compartido de GDS suele realizarse mediante el uso compartido de archivos NFS, ya sea de un nodo a otro o desde un dispositivo NAS.

Un posible modo de error para el clúster es si este recurso compartido de archivos remoto deja de estar disponible o tiene problemas sutiles. Un montaje remoto puede fallar debido a problemas de red, configuraciones de seguridad o configuraciones incorrectas. Un reinicio del sistema puede causar cambios de configuración realizados días o semanas antes de que entren en vigor, y esto puede causar sorpresas.

**¿Qué sucedería si un recurso compartido NFS no se monta?**

En UNIX, la manera en que los montes NFS se asignan a la estructura de directorios puede permitir que un directorio GDS aparentemente utilizable esté disponible, incluso si el montaje falla. Tenga en cuenta lo siguiente:

* Servidor NAS: Carpeta compartida NFS /u01/iapply/livecycle_gds
* Nodo 1: un punto de montaje a la carpeta compartida (alojada en el servidor DB) ubicada aquí: /u01/iapply/livecycle_gds
* Nodo 2: un punto de montaje a la carpeta compartida (alojada en el servidor DB) ubicada aquí: /u01/iapply/livecycle_gds

* LCES especifica la ruta a GDS: /u01/iapply/livecycle_gds

Si el montaje en el nodo 1 falla, la estructura del directorio aún contendrá una ruta /u01/iapply/livecycle_gds al punto de montaje vacío, y el nodo aparecerá para ejecutarse correctamente. Sin embargo, dado que el contenido de GDS no se está compartiendo realmente con el otro nodo, el clúster no funcionará correctamente. Esto puede ocurrir y pasa, y el resultado es que el clúster falla de maneras misteriosas.

La práctica recomendada es organizar las cosas para que el punto de montaje Linux no se utilice como la raíz del GDS, sino como un directorio dentro del mismo que se utiliza como la raíz del GDS:

* Si tiene un servidor NFS, puede tener un directorio: /some/storage/lc_cluster_dev/LC_GDS
* Y en su nodo de clúster tiene un punto de montaje: /u01/iapply/shared
* Monte nfs_server: /some/storage/lc_cluster_dev/u01/iapply/shared
* Apunte su GDS a /u01/iapply/shared/LC_GDS

Ahora, si por alguna razón el montaje no se realiza correctamente, el punto de montaje desnudo no contiene un directorio LC_GDS y el clúster fallará de forma predecible, ya que no puede encontrar ningún GDS.

**¿Cómo puedo verificar que todos los nodos vean el mismo GDS y tengan permisos?**

La mejor manera de verificar el acceso y uso compartido de GDS es acceder a cada uno de los nodos como un usuario interactivo, ya sea a través de SSH o telnet a nodos UNIX, o a través del escritorio remoto a sistemas Windows. Debe poder navegar al directorio o sistema de archivos GDS configurado en cada nodo y crear archivos de prueba de todos los nodos visibles en todos los demás nodos.

Preste atención al ID de usuario con el que funciona AEM Forms en JEE. En las instalaciones llave en mano de Windows, esto es como administrador local. En UNIX, puede ser como un usuario de servicio específico configurado en el script de inicio o en la configuración del servidor de aplicaciones. Es importante que este ID de usuario pueda crear y manipular archivos GDS por igual en todos los nodos.

En sistemas UNIX, las configuraciones NFS suelen establecer de forma predeterminada la desconfianza hacia la propiedad raíz o los derechos de acceso raíz a archivos y objetos. Si está ejecutando el servidor de aplicaciones como usuario raíz, encuentra que necesita especificar opciones en el servidor NFS, el nodo que monta los archivos, o ambos para permitir el acceso y control bilateral de los archivos creados por un nodo y a los que se accede por otro.

### 3) Uso compartido de bases de datos {#database-sharing}

Para que un clúster funcione correctamente, es esencial que todos los miembros del clúster compartan la misma base de datos. El margen para equivocarse es más o menos:

* configurar accidentalmente IDP_DS, EDC_DS, AdobeDefaultSA_DS u otras fuentes de datos requeridas de forma diferente en nodos de clúster separados, de modo que los nodos apunten a bases de datos diferentes.
* configurar accidentalmente varios nodos separados para compartir una base de datos cuando no deberían.

Según el servidor de aplicaciones, puede ser natural que la conexión JDBC se defina en un ámbito de clúster, de modo que no sea posible establecer definiciones diferentes en nodos diferentes. En Jboss, sin embargo, es completamente posible configurar las cosas para que una fuente de datos, como IDP_DS, apunte a una base de datos en el nodo 1, pero apunte a algo más en el nodo 2.

El problema inverso es más común, es decir, una situación en la que varios AEM Forms independientes (o de clúster) en nodos JEE apuntan accidentalmente al mismo esquema cuando no están pensados para hacerlo. Esto ocurre con frecuencia cuando un DBA proporciona, sin saberlo, una sola AEM Forms sobre la información de conexión de la base de datos JEE a los equipos de configuración DEV y QA, y ninguno de ellos se da cuenta de que las instancias DEV y QA requieren bases de datos independientes.

## Clúster del servidor de aplicaciones {#application-server-cluster-1}

Para que AEM Forms tenga éxito en el clúster JEE, es esencial que el servidor de aplicaciones esté configurado y funcione correctamente como un clúster. En WebSphere y Weblogic, este es un proceso directo y bien documentado. En Jboss, la configuración del clúster es un poco más práctica, y asegurar que los nodos estén configurados para actuar como un clúster y de hecho encontrar y comunicarse entre sí puede ser un desafío. JBoss se basa internamente en JGroups, que usa multidifusión UDP para encontrar y coordinar con nodos del mismo nivel, y algunos de los problemas mencionados con GemFire pueden ocurrir, como nodos que no se encuentran entre sí cuando deberían, o que se encuentran entre sí cuando no deberían.

Referencias:

* [Servicios empresariales de alta disponibilidad a través de clústeres JBoss](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Oracle WebLogic Server: uso de clústeres](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### ¿Cómo puedo comprobar que JBoss se está agrupando correctamente? {#check-jboss-clustering}

Cuando se inicia JBoss, como se descubren los miembros del clúster, los mensajes a nivel INFO sobre el nodo que se une al clúster se registran en el archivo de registro/consola.

Si se especificó un nombre de clúster mediante la opción de línea de comandos -g al ejecutarse, verá mensajes similares a los siguientes:

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Programador de cuarzo {#quartz-scheduler}

En su mayor parte, AEM Forms sobre el uso por JEE del planificador interno de Quartz en un clúster está pensado para seguir automáticamente la configuración de clúster global de AEM Forms en JEE en general. Sin embargo, hay un error, #2794033, que hace que la configuración automática del clúster de Quartz falle si los localizadores TCP se están utilizando para Gemfire en lugar de para la detección automática de multidifusión. En este caso, Quartz se ejecutará incorrectamente en modo no agrupado. Esto creará interbloqueos y corrupción de datos en las tablas de Quartz. Los efectos adversos son peores en la versión 8.2.x que en la versión 9.0, ya que Quartz no se utiliza tanto, pero sigue ahí.

Las correcciones están disponibles de la siguiente manera para este problema: 8.2.1.2 QF2.143 y 9.0.0.2 QF2.44.

También existe una solución alternativa, que es establecer ambas propiedades:

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

Tenga en cuenta que una configuración utiliza un punto entre &quot;cluster&quot; y &quot;locators&quot; y la otra utiliza un guión. Esto es fácil de implementar y menos riesgoso que aplicar un parche de software, pero implica crear artificialmente una configuración adicional confusa y mal nombrada.

### ¿Cómo puedo comprobar que Quartz se está ejecutando como un solo nodo o clúster? {#check-quartz}

Para determinar cómo se ha configurado Quartz, debe ver los mensajes generados por el servicio AEM Forms en el programador de JEE durante el inicio. Estos mensajes se generan con la gravedad INFO y puede ser necesario ajustar el nivel de registro y reiniciar para obtener los mensajes. En la secuencia de inicio de AEM Forms on JEE, la inicialización de Quartz comienza con la siguiente línea:

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
Es importante localizar esta primera línea en los registros porque algunos servidores de aplicaciones también utilizan Quartz y sus instancias de Quartz no deben confundirse con la instancia que utiliza el servicio AEM Forms en el programador de JEE. Esto indica que el servicio Scheduler se está iniciando y las líneas que lo siguen le indicarán si se está iniciando o no correctamente en modo agrupado. Aparecen varios mensajes en esta secuencia, y es el último mensaje &quot;iniciado&quot; que revela cómo está configurado Quartz:

Aquí se da el nombre de la instancia de Quartz: `IDPSchedulerService_$_ap-hp8.ottperflab.corp.adobe.com1312883903975`. El nombre de la instancia de Quartz del programador siempre comenzará con la cadena `IDPSchedulerService_$_`. La cadena que se anexa al final de esto le indica si Quartz se está ejecutando o no en modo agrupado. El identificador único largo generado a partir del nombre de host del nodo y una cadena larga de dígitos, aquí `ap-hp8.ottperflab.corp.adobe.com1312883903975`, indica que está funcionando en un clúster. Si funciona como un solo nodo, el identificador será un número de dos dígitos, &quot;20&quot;:

INFO `[org.quartz.core.QuartzScheduler]` El planificador `IDPSchedulerService_$_20` se inició.
Esta comprobación debe realizarse en todos los nodos del clúster por separado, ya que el planificador de cada nodo determina de forma independiente si debe funcionar en modo de clúster.

### ¿Qué clase de problemas se producen si Quartz se está ejecutando en el modo incorrecto? {#quartz-running-in-wrong-mode}

Si Quartz está configurado para ejecutarse como un solo nodo, pero en realidad se está ejecutando en un clúster y compartiendo tablas de base de datos de Quartz con otros nodos, esto resultará en un funcionamiento poco fiable del servicio AEM Forms en el Programador JEE y normalmente irá acompañado de interbloqueos de base de datos. Este es un seguimiento de pila bastante típico que podría ver en esta situación:

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### ¿Cómo sincronizo los relojes del sistema en un clúster? {#ynchronize-system-clocks-cluster}

Para que un clúster funcione sin problemas, es esencial que los relojes de todos los nodos del clúster se sincronicen estrechamente. Esto no se puede hacer adecuadamente a mano y tiene que hacerlo algún tipo de servicio de sincronización de tiempo que se ejecuta muy regularmente. Los relojes de todos los nodos deben estar dentro de un segundo entre sí. La práctica recomendada exige que no sólo se sincronicen los nodos del clúster, sino también el equilibrador de carga, el servidor de bases de datos, el servidor GDS NAS y cualquier otro componente.

La sincronización horaria de Windows tiende a estar en el controlador de dominio. Los sistemas UNIX pueden sincronizarse utilizando NTP con un origen de tiempo diferente. Es mejor que todos los sistemas (tanto el AEM Forms en los nodos JEE como otros componentes del sistema) se sincronicen con el mismo origen, si es posible.

Es absolutamente insuficiente, incluso en los entornos de prueba más temporales, para configurar manualmente los relojes en los nodos. La configuración manual de los relojes no dará una sincronización lo suficientemente precisa, y los relojes de los dos nodos se desplazarán inevitablemente entre sí, incluso durante un período de un solo día. Un mecanismo de sincronización de tiempo activo es esencial para una operación fiable del clúster.

### Equilibrador de carga {#load-balancer}

Un requisito típico de un clúster que proporciona servicios interactivos del usuario es un equilibrador de carga HTTP que distribuirá solicitudes HTTP en todo el clúster. El uso correcto de un equilibrador de carga con un AEM Forms en un clúster JEE requiere la configuración de lo siguiente:

* durabilidad de la sesión

* Reglas de reescritura de URL

* comprobación de estado del nodo

### ¿Qué debo hacer con mi función de comprobación de estado del equilibrador de carga? {#load-balancer-health-check}

Algunos equilibradores de carga se pueden configurar para realizar una comprobación de estado periódica en los nodos que se están equilibrando de carga. Normalmente, se trata de una URL a una función de aplicación a la que el equilibrador de carga intentará acceder. Si la carga se realiza correctamente, se supone que el nodo está en buen estado y se mantiene en el conjunto de equilibrio de carga. Si la dirección URL no se carga, se supone que el nodo es defectuoso y se elimina del conjunto. Normalmente, la URL de comprobación de estado simplemente está conectada a la página de inicio de sesión de AEM Forms en la interfaz de administración de JEE. Esto no es una comprobación de estado ideal para un miembro del clúster y sería mejor implementar un proceso de corta duración y usar la URL de la API de REST como función de comprobación de estado.

## Ruta de acceso del archivo temporal y configuración de clúster similar {#temporary-file-path-cluster-settings}

Ciertas configuraciones de ruta de archivo en AEM Forms en JEE se establecen en todo el clúster y tienen la misma configuración efectiva en cada nodo, pero se interpretan de forma independiente en cada nodo para hacer referencia a archivos locales. Las claves que hay que tener en cuenta son la configuración de la ruta de fuente y la configuración temporal del directorio. Vaya a la pantalla Configuraciones principales de AdminUI (Inicio > Configuración > Sistema principal > Configuraciones principales)

Se debe comprobar la siguiente configuración:

1. Ubicación del directorio temporal
1. Ubicación del directorio de fuentes del servidor de Adobe
1. Ubicación del directorio de fuentes del cliente
1. Ubicación del directorio de fuentes del sistema
1. Ubicación del archivo de configuración de servicios de datos

El clúster solo tiene una configuración de ruta única para cada una de estas opciones de configuración. Por ejemplo, la ubicación del directorio temporal puede ser `/home/project/QA2/LC_TEMP`. En un clúster, es necesario que cada nodo tenga realmente esta ruta concreta accesible. Si un nodo tiene la ruta de archivo temporal esperada y otro nodo no, el nodo que no funcionará correctamente.

Aunque estos archivos y rutas pueden compartirse entre los nodos o ubicarse por separado, o en sistemas de archivos remotos, generalmente se recomienda que sean copias locales en el almacenamiento en disco del nodo local.

La ruta de acceso del Directorio temporal, en particular, no debe compartirse entre nodos. Se debe utilizar un procedimiento similar al descrito para verificar el GDS para verificar que el directorio temporal no se esté compartiendo: vaya a cada nodo, cree un archivo temporal en la ruta indicada por la configuración de la ruta y, a continuación, verifique que los demás nodos no compartan el archivo. La ruta de acceso temporal del directorio debe hacer referencia al almacenamiento de disco local en cada nodo, si es posible, y debe comprobarse.

Para cada configuración de ruta, asegúrese de que la ruta existe realmente y es accesible desde cada nodo del clúster, utilizando la identidad de uso efectiva bajo la cual se ejecuta AEM Forms en JEE. El contenido del directorio de fuentes debe ser legible. El directorio temporal debe permitir la lectura, escritura y control.
















