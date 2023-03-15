---
title: Directrices de rendimiento
seo-title: Performance Guidelines
description: AEM Este artículo proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de la implementación de la.
seo-description: This article provides general guidelines on how to optimize the performance of your AEM deployment.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2976'
ht-degree: 7%

---

# Directrices de rendimiento{#performance-guidelines}

AEM Esta página proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de la implementación de la. AEM Si es nuevo en el sector de la, consulte las páginas siguientes antes de empezar a leer las directrices de rendimiento:

* [AEM Conceptos básicos de](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM Información general sobre el almacenamiento en el](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)

AEM A continuación se ilustran las opciones de implementación disponibles para los usuarios (desplácese para ver todas las opciones):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Producto</strong></p> </td>
   <td><p><strong>Topología</strong></p> </td>
   <td><p><strong>Sistema operativo</strong></p> </td>
   <td><p><strong>Servidor de aplicaciones</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Seguridad</strong></p> </td>
   <td><p><strong>Microkernel</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Indexación</strong></p> </td>
   <td><p><strong>Servidor web</strong></p> </td>
   <td><p><strong>Explorador</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Sin AH</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>Segmento</p> </td>
   <td><p>Propiedad</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Destino</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>Archivo</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Análisis</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Red Hat</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>Autor-Descarga</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>Móvil</p> </td>
   <td><p>Author-Cluster</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Audiencia</p> </td>
  </tr>
  <tr>
   <td><p>En varios sitios</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Assets</p> </td>
  </tr>
  <tr>
   <td><p>Comercio</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>SO APPLE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Activación</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Móvil</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Doc Security</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Administración de procesos</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Aplicación de escritorio de  </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Las directrices de rendimiento se aplican principalmente a AEM Sites.

## Cuándo utilizar las directrices de rendimiento {#when-to-use-the-performance-guidelines}

Debe utilizar las directrices de rendimiento en las siguientes situaciones:

* **Primera implementación**: Cuando se planea implementar AEM Sites o Assets por primera vez, es importante comprender las opciones disponibles al configurar el micronúcleo, el almacén de nodos y el almacén de datos (en comparación con la configuración predeterminada). Por ejemplo, cambiar la configuración predeterminada del almacén de datos para TarMK a almacén de datos de archivo.
* **Actualización a una nueva versión**: Al actualizar a una nueva versión, es importante comprender las diferencias de rendimiento en comparación con el entorno en ejecución. AEM AEM Por ejemplo, si actualiza de la versión 6.1 a la versión 6.2, o de la versión 6.0 CRX2 a la versión 6.2 de OAK, la actualización se realizará de la versión 6.1 a la versión 6.2.
* **El tiempo de respuesta es lento**: Cuando la arquitectura de Nodestore seleccionada no cumple con sus requisitos, es importante comprender las diferencias de rendimiento en comparación con otras opciones de topología. Por ejemplo, implementar TarMK en lugar de MongoMK, o usar un almacén de datos de archivo en lugar de un almacén de datos de Amazon S3 o Microsoft Azure.
* **Adición de más autores**: Cuando la topología TarMK recomendada no cumple los requisitos de rendimiento y el nodo Autor ha alcanzado la capacidad máxima disponible, es importante comprender las diferencias de rendimiento en comparación con el uso de MongoMK con tres o más nodos Autor. Por ejemplo, implementar MongoMK en lugar de TarMK.
* **Añadir más contenido**: cuando la arquitectura de almacén de datos recomendada no cumple con sus requisitos, es importante comprender las diferencias de rendimiento en comparación con otras opciones de almacén de datos. Ejemplo: uso del Almacén de datos de Amazon S3 o Microsoft Azure en lugar de un Almacén de datos de archivo.

## Introducción {#introduction}

AEM En este capítulo se ofrece una descripción general de la arquitectura de la y sus componentes más importantes. También proporciona directrices de desarrollo y describe los escenarios de prueba utilizados en las pruebas de referencia de TarMK y MongoMK.

### AEM La plataforma de {#the-aem-platform}

AEM La plataforma de consta de los siguientes componentes:

![chlimage_1](assets/chlimage_1a.png)

AEM Para obtener más información sobre la plataforma de la, consulte [AEM ¿Qué es la?](/help/sites-deploying/deploy.md#what-is-aem).

### AEM La arquitectura de la {#the-aem-architecture}

AEM Existen tres componentes básicos importantes para una implementación de la. El **Instancia de autor** que utilizan los autores, editores y aprobadores de contenido para crear y revisar contenido. Cuando se aprueba el contenido, se publica en un segundo tipo de instancia denominado **Instancia de publicación** desde donde los usuarios finales acceden a él. El tercer componente es el **Dispatcher** que es un módulo que administra el almacenamiento en caché y el filtrado de URL y que está instalado en el servidor web. AEM Para obtener más información sobre la arquitectura de la, consulte [Escenarios de implementación habituales](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernels {#micro-kernels}

AEM Los Micro Kernels actúan como administradores de persistencia en la. AEM Existen tres tipos de Micro Kernels utilizados con el sistema: TarMK, MongoDB y Base de datos relacional (con soporte restringido). Elegir uno que se adapte a sus necesidades depende de la finalidad de la instancia y del tipo de implementación que se esté planteando. Para obtener más información sobre Micro Kernels, consulte la [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) página.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

AEM En, los datos binarios se pueden almacenar de forma independiente de los nodos de contenido. La ubicación donde se almacenan los datos binarios se denomina **Almacén de datos**, mientras que la ubicación de los nodos de contenido y las propiedades se denomina **Almacenamiento de nodos**.

>[!NOTE]
>
>Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes tanto para las instancias de autor de AEM como para las de publicación.

>[!CAUTION]
>
>El micronúcleo de la base de datos relacional tiene compatibilidad restringida. Contacto [Adobe del Servicio de atención al cliente](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) antes de usar este tipo de Micro Kernel.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Almacén de datos {#data-store}

Cuando se trata de un gran número de binarios, se recomienda utilizar un almacén de datos externo en lugar de los almacenes de nodos predeterminados para maximizar el rendimiento. Por ejemplo, si el proyecto requiere un gran número de recursos multimedia, almacenarlos en el almacén de datos de File o Azure/S3 hará que acceder a ellos sea más rápido que almacenarlos directamente en un MongoDB.

Para obtener más información sobre las opciones de configuración disponibles, consulte [Configuración de almacenes de datos y nodos](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe AEM recomienda elegir la opción de implementar en Azure o Amazon Web Service (AWS AEM) mediante Adobe Managed Services, donde los clientes se beneficiarán de un equipo que tenga la experiencia y las habilidades de implementar y operar en estos entornos de computación en la nube (Cloud Computing), y que tenga la experiencia y las habilidades necesarias para implementar y operar en estos entornos de computación en la nube (Cloud Compute). Consulte nuestro [Documentación adicional sobre Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>AEM Para obtener recomendaciones sobre cómo implementar en Azure o AWS AEM, fuera de Adobe Managed Services, le recomendamos encarecidamente que trabaje directamente con el proveedor de la nube o con uno de nuestros socios que admitan la implementación de los entornos de nube que elija. Es posible que tenga que trabajar en el entorno de nube que más le guste. El proveedor o socio de nube seleccionado es responsable de las especificaciones de tamaño, diseño e implementación de la arquitectura que admitirá para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.
>
>Para obtener más información, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md#supported-platforms) página.

### Búsqueda {#search-features}

AEM En esta sección se enumeran los proveedores de índices personalizados utilizados con las listas de proveedores de índices de. Para obtener más información sobre la indexación, consulte [Consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Para la mayoría de las implementaciones, Adobe recomienda utilizar el índice Lucene. Sólo debe utilizar Solr para la escalabilidad en implementaciones especializadas y complejas.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Directrices de desarrollo {#development-guidelines}

AEM Usted debe desarrollar para la orientación de la para **rendimiento y escalabilidad**. A continuación se presentan una serie de prácticas recomendadas que puede seguir:

**HACER**

* Aplicar la separación de presentación, lógica y contenido
* AEM Utilice las API existentes de la (por ejemplo, Sling) y las herramientas (por ejemplo, Replication)
* Desarrollar en el contexto de contenido real
* Desarrollar para lograr una caché óptima
* Minimizar el número de guardados (por ejemplo, mediante flujos de trabajo transitorios)
* Asegúrese de que todos los puntos finales HTTP sean RESTful
* Restringir el ámbito de la observación JCR
* Tenga en cuenta el subproceso asincrónico

**NO LO HAGAS**

* No utilice directamente las API de JCR, si es posible
* No cambie /libs, sino que utilice superposiciones
* No utilice consultas siempre que sea posible
* No utilice enlaces de Sling para obtener servicios OSGi en código Java, sino que utilice:

   * @Reference en un componente DS
   * @Inject en un modelo Sling
   * sling.getService() en una clase de uso de Sightly
   * sling.getService() en un JSP
   * un ServiceTracker
   * acceso directo al registro de servicios OSGi

AEM Para obtener más información sobre el desarrollo de la, lea [Desarrollo: Conceptos básicos](/help/sites-developing/the-basics.md). Para conocer las prácticas recomendadas adicionales, consulte [Prácticas recomendadas de desarrollo](/help/sites-developing/best-practices.md).

### Escenarios de referencia {#benchmark-scenarios}

>[!NOTE]
>
>Todas las pruebas de referencia mostradas en esta página se han realizado en un entorno de laboratorio.

Los escenarios de prueba detallados a continuación se utilizan para las secciones de referencia de los capítulos TarMK, MongoMk y TarMK vs MongoMk. Para ver qué escenario se ha utilizado para una prueba de referencia determinada, lea el campo Escenario del [Especificaciones técnicas](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) tabla.

**Escenario de un solo producto**

AEM Assets:

* Interacciones del usuario: Examinar recursos/Buscar recursos/Descargar recurso/Leer metadatos del recurso/Actualizar metadatos del recurso/Cargar recurso/Ejecutar flujo de trabajo de cargar recurso
* Modo de ejecución: usuarios simultáneos, una sola interacción por usuario

**Escenario de mezcla de productos**

AEM Sites + Recursos:

* Interacciones de usuario de Sites: Leer página de artículo/Leer página/Crear párrafo/Editar párrafo/Crear página de contenido/Activar página de contenido/Búsqueda de autor
* Interacciones de usuario de Assets: Examinar recursos/buscar recursos/descargar recursos/leer metadatos de recursos/actualizar metadatos de recursos/cargar recursos/ejecutar flujo de trabajo de cargar recursos
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

**Caso de uso vertical**

Medios:

* Leer página de artículo (27,4 %), Leer página (10,9 %), Crear sesión (2,6 %), Activar página de contenido (1,7 %), Crear página de contenido (0,4 %), Crear párrafo (4,3 %), Editar párrafo (0,9 %), Componente de imagen (0,9 %), Examinar recursos (20 %), Leer metadatos de recursos (8,5 %), Descargar recurso (4,2 %), Buscar recurso (0,2 %), Actualizar metadatos de recursos (2,4 %), Cargar recursos (1,2,2 %), Examinar proyecto (4 %) 0,9%), Leer proyecto (6,6%), Proyecto Agregar recurso (1,2%), Proyecto Agregar sitio (1,2%), Crear proyecto (0,1%), Búsqueda de autor (0,4%)
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

## TarMK {#tarmk}

Este capítulo proporciona directrices generales de rendimiento para TarMK que especifican los requisitos mínimos de arquitectura y la configuración. También se proporcionan pruebas de referencia para una mayor aclaración.

Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de autor de AEM como para las de publicación.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento de tar](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Directrices de arquitectura mínima de TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>Las directrices de arquitectura mínimas que se presentan a continuación son para entornos de producción y sitios de alto tráfico. Estos son **no** el [especificaciones mínimas](/help/sites-deploying/technical-requirements.md#prerequisites) AEM necesario para ejecutar la.

Para establecer un buen rendimiento al usar TarMK, debe comenzar desde la siguiente arquitectura:

* Una instancia de autor
* Dos instancias de publicación
* Dos Dispatcher

AEM A continuación se ilustran las directrices de arquitectura para sitios de y AEM Assets.

>[!NOTE]
>
>La replicación sin binarios debe activarse **ACTIVADO** si se comparte el almacén de datos de archivos.

**Directrices de arquitectura TAR para AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Directrices de arquitectura TAR para AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Directrices de configuración de TarMK {#tarmk-settings-guideline}

Para obtener un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, [ver esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajos de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitorio de Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> </td>
   <td>AEM Añada estos parámetros JVM en el script de inicio de la para evitar que las consultas expansivas se sobrecarguen en los sistemas.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Habilitado</p> <p>Habilitado</p> <p>Habilitado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo de la pila</p> </td>
   <td>Consulte también <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configuraciones del almacén de datos</a>.</td>
  </tr>
  <tr>
   <td>Flujo de trabajo de recursos de actualización DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>comprobado</td>
   <td>Este flujo de trabajo administra la actualización de recursos.</td>
  </tr>
  <tr>
   <td>Reescritura de metadatos DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>comprobado</td>
   <td>XMP Este flujo de trabajo gestiona la reescritura de la al binario original y define la fecha de la última modificación en JCR.</td>
  </tr>
 </tbody>
</table>

### Referencia de rendimiento de TarMK {#tarmk-performance-benchmark}

#### Especificaciones técnicas {#technical-specifications}

Los ensayos de referencia se realizaron con arreglo a las siguientes especificaciones:

|  | **Nodo de autor** |
|---|---|
| Servidor | Hardware de metal desnudo (HP) |
| Sistema operativo | RedHat Linux |
| CPU/núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 núcleos |
| RAM | 32GB |
| Disco | Magnético |
| Java | Oracle JRE versión 8 |
| Montón de JVM | 16GB |
| Producto | AEM 6.2 |
| Nodestore | TarMK |
| Almacén de datos | DS de archivo |
| Escenario | Un solo producto: recursos / 30 hilos simultáneos |

#### Resultados de referencia de rendimiento {#performance-benchmark-results}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son los números de rendimiento real.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

La razón principal para elegir el backend de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usar MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe generalmente al hecho de que la capacidad de CPU y memoria de un solo servidor, que admite todas las actividades de creación simultáneas, ya no es sostenible.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento de Mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Directrices de arquitectura mínima de MongoMK {#mongomk-minimum-architecture-guidelines}

Para establecer un buen rendimiento al utilizar MongoMK, debe comenzar desde la siguiente arquitectura:

* Tres instancias de autor
* Dos instancias de publicación
* Tres instancias de MongoDB
* Dos Dispatcher

>[!NOTE]
>
>En entornos de producción, MongoDB siempre se utilizará como un conjunto de réplicas con un principal y dos secundarios. Las lecturas y escrituras van a la primaria y las lecturas pueden ir a la secundaria. Si el almacenamiento no está disponible, uno de los secundarios se puede reemplazar por un árbitro, pero los conjuntos de réplicas de MongoDB siempre deben estar compuestos por un número impar de instancias.

>[!NOTE]
>
>La replicación sin binarios debe activarse **ACTIVADO** si se comparte el almacén de datos de archivos.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Directrices de configuración de MongoMK {#mongomk-settings-guidelines}

Para obtener un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, [ver esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Valor (predeterminado)</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajos de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitorio de Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> <p>60000</p> </td>
   <td>AEM Añada estos parámetros JVM en el script de inicio de la para evitar que las consultas expansivas se sobrecarguen en los sistemas.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Habilitado</p> <p>Habilitado</p> <p>Habilitado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo de la pila</p> </td>
   <td>Consulte también <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configuraciones del almacén de datos</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>El tamaño predeterminado de la caché se establece en 256 MB.</p> <p>Afecta al tiempo que se tarda en invalidar la caché.</p> </td>
  </tr>
  <tr>
   <td>oak-observación</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>mín. y máx. = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Análisis de rendimiento de MongoMK {#mongomk-performance-benchmark}

### Especificaciones técnicas {#technical-specifications-1}

Los ensayos de referencia se realizaron con arreglo a las siguientes especificaciones:

|  | **Nodo Autor** | **Nodo MongoDB** |
|---|---|---|
| Servidor | Hardware de metal desnudo (HP) | Hardware de metal desnudo (HP) |
| Sistema operativo | RedHat Linux | RedHat Linux |
| CPU/núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 núcleos |
| RAM | 32GB | 32GB |
| Disco | Magnético: >1.000 IOPS | Magnético: >1.000 IOPS |
| Java | Oracle JRE versión 8 | N/D |
| Montón de JVM | 16GB | N/D |
| Producto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/D |
| Almacén de datos | DS de archivo | N/D |
| Escenario | Un solo producto: recursos / 30 hilos simultáneos | Un solo producto: recursos / 30 hilos simultáneos |

### Resultados de referencia de rendimiento {#performance-benchmark-results-1}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son los números de rendimiento real.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

La regla básica que debe tenerse en cuenta al elegir entre los dos es que TarMK está diseñado para el rendimiento, mientras que MongoMK se utiliza para la escalabilidad. Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de autor de AEM como para las de publicación.

La razón principal para elegir el backend de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usar MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor suele deberse al hecho de que la capacidad de CPU y memoria de un solo servidor, que admite todas las actividades de creación simultáneas, ya no es sostenible.

Para obtener más información sobre TarMK frente a MongoMK, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Directrices TarMK vs MongoMk {#tarmk-vs-mongomk-guidelines}

**Ventajas de TarMK**

* Creado específicamente para aplicaciones de gestión de contenido
* Los archivos siempre son coherentes y se pueden realizar copias de seguridad utilizando cualquier herramienta de copia de seguridad basada en archivos
* Proporciona un mecanismo de conmutación por error: consulte [Espera en frío](/help/sites-deploying/tarmk-cold-standby.md) para obtener más información
* Proporciona un alto rendimiento y un almacenamiento de datos fiable con una sobrecarga operativa mínima
* Menor coste total de propiedad (TCO)

**Criterios para elegir MongoMK**

* Número de usuarios con nombre conectados en un día: en miles o más
* Número de usuarios simultáneos: en cientos o más
* Volumen de ingestas de recursos por día: en cientos de miles o más
* Volumen de ediciones de página al día: en cientos de miles o más
* Volumen de búsquedas por día: en decenas de miles o más

### Puntos de referencia de TarMK vs MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como línea de base y no son números de rendimiento real.

### Especificaciones técnicas del escenario 1 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo OAK de autor</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>Hardware de metal desnudo (HP)</td>
   <td>Hardware de metal desnudo (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/núcleos</td>
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 núcleos</td>
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 núcleos</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32GB</td>
   <td>32GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>Magnético: &gt;1.000 IOPS</td>
   <td>Magnético: &gt;1.000 IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE versión 8</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Montón de JVM16 GB</td>
   <td>16GB</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Producto </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK o MongoMK</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Almacén de datos</td>
   <td>DS de archivo </td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> Un solo producto: Recursos / 30 hilos simultáneos por ejecución</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resultados de referencia de rendimiento del escenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Especificaciones técnicas del escenario 2 {#scenario-technical-specifications-1}

>[!NOTE]
>
>AEM Para habilitar el mismo número de autores con MongoDB que con un sistema TarMK, necesita un clúster con dos nodos de. Un clúster MongoDB de cuatro nodos puede administrar 1,8 veces el número de autores que una instancia de TarMK. Un clúster de MongoDB de ocho nodos puede administrar 2,3 veces el número de autores que una instancia de TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo TarMK de autor</strong></td>
   <td><strong>Nodo MongoMK de autor</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
  </tr>
  <tr>
   <td>Servidor</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>CPU/núcleos</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60GB</td>
   <td>60GB</td>
   <td>60GB</td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>SSD: 10.000 IOPS</td>
   <td>SSD: 10.000 IOPS</td>
   <td>SSD: 10.000 IOPS</td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE versión 8</td>
   <td><br /> Oracle JRE versión 8</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Montón de JVM16 GB</td>
   <td>30GB</td>
   <td>30GB</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Producto </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Almacén de datos</td>
   <td>DS de archivo </td>
   <td><br /> DS de archivo</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> <br /> Caso de uso vertical: Media / 2000 subprocesos simultáneos</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Resultados de referencia de rendimiento del escenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Directrices de escalabilidad de arquitectura para AEM Sites y Assets {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Resumen de las directrices de rendimiento  {#summary-of-performance-guidelines}

Las directrices presentadas en esta página se pueden resumir de la siguiente manera:

* **TarMK con almacén de datos de archivos** es la arquitectura recomendada para la mayoría de los clientes de:

   * Topología mínima: una instancia de autor, dos instancias de publicación, dos instancias de Dispatcher
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **MongoMK con almacén de datos de archivos** es la arquitectura recomendada para la escalabilidad horizontal del nivel de Author:

   * Topología mínima: tres instancias de autor, tres instancias de MongoDB, dos instancias de publicación, dos instancias de Dispatcher
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **Nodestore** debe almacenarse en el disco local, no en un almacenamiento conectado a la red (NAS)
* Al utilizar **Amazon S3**:

   * El almacén de datos de Amazon S3 se comparte entre los niveles Author y Publish
   * La replicación sin binarios debe estar activada
   * La recolección de elementos no utilizados del almacén de datos requiere una primera ejecución en todos los nodos de autor y publicación y, a continuación, una segunda ejecución en autor

* **Se debe crear un índice personalizado además del índice predeterminado** según las búsquedas más comunes

   * Los índices de Lucene deben utilizarse para los índices personalizados

* **La personalización del flujo de trabajo puede mejorar sustancialmente el rendimiento**, por ejemplo, eliminando el paso de vídeo en el flujo de trabajo &quot;Actualizar recurso&quot;, desactivando los oyentes que no se utilizan, etc.

Para obtener más información, lea la [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) página.
