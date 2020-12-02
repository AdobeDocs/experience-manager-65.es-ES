---
title: Directrices de rendimiento
seo-title: Directrices de rendimiento
description: Este artículo proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de AEM.
seo-description: Este artículo proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de AEM.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
translation-type: tm+mt
source-git-commit: a678716e2c0520891e4228bc49b075f070ea45b7
workflow-type: tm+mt
source-wordcount: '2993'
ht-degree: 5%

---


# Pautas de rendimiento{#performance-guidelines}

Esta página proporciona directrices generales sobre cómo optimizar el rendimiento de la implementación de AEM. Si es nuevo en AEM, vaya a las páginas siguientes antes de que inicio de leer las directrices de rendimiento:

* [Conceptos básicos de AEM](/help/sites-deploying/deploy.md#basic-concepts)
* [Visión general del Almacenamiento en AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)

A continuación se muestran las opciones de implementación disponibles para AEM (desplácese hasta la vista de todas las opciones):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Producto</strong></p> </td>
   <td><p><strong>Topología</strong></p> </td>
   <td><p><strong>Sistema operativo</strong></p> </td>
   <td><p><strong>Servidor de aplicaciones</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Seguridad</strong></p> </td>
   <td><p><strong>Micro Kernel</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Indexación</strong></p> </td>
   <td><p><strong>Servidor web</strong></p> </td>
   <td><p><strong>Explorador</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>No es de alta disponibilidad</p> </td>
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
   <td><p>Descarga de autor</p> </td>
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
   <td><p>Audience</p> </td>
  </tr>
  <tr>
   <td><p>Varios sitios</p> </td>
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
   <td><p>Recursos</p> </td>
  </tr>
  <tr>
   <td><p>Comercio</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
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
   <td><p>LiveFile</p> </td>
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
   <td><p>Pantallas</p> </td>
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
   <td><p>Seguridad del documento</p> </td>
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
   <td><p>Process Mgt</p> </td>
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
   <td><p>aplicación de escritorio</p> </td>
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

## Cuándo utilizar las pautas de rendimiento {#when-to-use-the-performance-guidelines}

Debe utilizar las directrices de rendimiento en las siguientes situaciones:

* **Primera implementación**: Cuando planee implementar AEM Sites o Assets por primera vez, es importante comprender las opciones disponibles al configurar el micronúcleo, la tienda de nodos y el almacén de datos (en comparación con la configuración predeterminada). Por ejemplo, cambiar la configuración predeterminada del almacén de datos para TarMK al almacén de datos de archivos.
* **Actualización a una nueva versión**: Al actualizar a una nueva versión, es importante comprender las diferencias de rendimiento en comparación con el entorno en ejecución. Por ejemplo, la actualización de AEM 6.1 a 6.2, o de AEM 6.0 CRX2 a 6.2 OAK.
* **El tiempo de respuesta es lento**: Cuando la arquitectura seleccionada de Nodestore no cumple con sus requisitos, es importante comprender las diferencias de rendimiento en comparación con otras opciones de topología. Por ejemplo, implementar TarMK en lugar de MongoMK o usar un almacén de datos de archivos en lugar de un almacén de datos de Amazon S3 o Microsoft Azure.
* **Añadir más autores**: Cuando la topología TarMK recomendada no cumple los requisitos de rendimiento y el cambio de tamaño del nodo Autor ha alcanzado la capacidad máxima disponible, es importante comprender las diferencias de rendimiento en comparación con el uso de MongoMK con tres o más nodos Autor. Por ejemplo, implementar MongoMK en lugar de TarMK.
* **Añadir más contenido**: Cuando la arquitectura del almacén de datos recomendada no cumple sus requisitos, es importante comprender las diferencias de rendimiento en comparación con otras opciones del almacén de datos. Ejemplo: uso del almacén de datos de Amazon S3 o Microsoft Azure en lugar de un almacén de datos de archivos.

## Introducción {#introduction}

Este capítulo ofrece una visión general de la arquitectura de AEM y sus componentes más importantes. También proporciona directrices de desarrollo y describe los escenarios de prueba utilizados en las pruebas de referencia TarMK y MongoMK.

### La Plataforma AEM {#the-aem-platform}

La plataforma AEM consta de los siguientes componentes:

![chlimage_1](assets/chlimage_1a.png)

Para obtener más información sobre la plataforma AEM, consulte [Qué es AEM](/help/sites-deploying/deploy.md#what-is-aem).

### La Arquitectura AEM {#the-aem-architecture}

Hay tres elementos básicos importantes para una implementación AEM. La **Instancia de autor** que utilizan los autores, editores y aprobadores de contenido para crear y revisar contenido. Cuando se aprueba el contenido, se publica en un segundo tipo de instancia denominado **Instancia de publicación** desde donde los usuarios finales acceden a él. El tercer bloque de creación es el **Dispatcher**, que es un módulo que gestiona el almacenamiento en caché y el filtrado de direcciones URL y que se instala en el servidor web. Para obtener información adicional sobre la arquitectura de AEM, consulte [Escenarios de implementación típicos](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernels {#micro-kernels}

Los micro kernels actúan como administradores de persistencia en AEM. Existen tres tipos de micronúcleos utilizados con AEM: TarMK, MongoDB y Base de datos relacional (bajo soporte restringido). Elegir uno que se adapte a sus necesidades depende de la finalidad de la instancia y del tipo de implementación que se esté planteando. Para obtener información adicional sobre Micro Kernels, consulte la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

En AEM, los datos binarios se pueden almacenar independientemente de los nodos de contenido. La ubicación en la que se almacenan los datos binarios se denomina **Almacén de datos**, mientras que la ubicación de los nodos y las propiedades de contenido se denomina **Almacén de nodos**.

>[!NOTE]
>
>Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes para las instancias de AEM Author y Publish.

>[!CAUTION]
>
>El micronúcleo de la base de datos relacional está bajo soporte restringido. Póngase en contacto con [Adobe Customer Care](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) antes de utilizar este tipo de micronúcleo.

![climage_1-3](assets/chlimage_1-3a.png)

### Almacén de datos {#data-store}

Cuando se trata de un gran número de binarios, se recomienda utilizar un almacén de datos externo en lugar de los almacenes de nodos predeterminados para maximizar el rendimiento. Por ejemplo, si su proyecto requiere un gran número de recursos multimedia, almacenarlos en el archivo o en el almacén de datos de Azure/S3 hará que el acceso a ellos sea más rápido que almacenarlos directamente en una base de datos Mongo.

Para obtener más información sobre las opciones de configuración disponibles, consulte [Configuración de los almacenes de datos y nodos](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe recomienda elegir la opción de implementar AEM en los servicios web de Azure o Amazon (AWS) mediante los servicios gestionados de Adobe, donde los clientes se beneficiarán de un equipo que tenga la experiencia y las habilidades de implementar y operar AEM en estos entornos informáticos en la nube. Consulte nuestra [documentación adicional sobre los servicios administrados de Adobe](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>Para obtener recomendaciones sobre cómo implementar AEM en Azure o AWS, fuera de los servicios gestionados de Adobe, le recomendamos encarecidamente que trabaje directamente con el proveedor de nube o con uno de nuestros socios que admita la implementación de AEM en el entorno de nube de su elección. El proveedor o socio de nube seleccionado es responsable de las especificaciones de tamaño, el diseño y la implementación de la arquitectura que admitirán para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.
>
>Para obtener más información, consulte también la página [requisitos técnicos](/help/sites-deploying/technical-requirements.md#supported-platforms).

### Búsqueda {#search-features}

En esta sección se enumeran los proveedores de índices personalizados que se utilizan con AEM. Para obtener más información sobre la indexación, consulte [Consultas de roble e indización](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Para la mayoría de las implementaciones, Adobe recomienda el uso del índice de Lucene. Debe utilizar Solr únicamente para la escalabilidad en implementaciones especializadas y complejas.

![climage_1-4](assets/chlimage_1-4a.png)

### Directrices de desarrollo {#development-guidelines}

Debe desarrollarse para AEM objetivo de **performance y escalabilidad**. A continuación se presentan varias prácticas recomendadas que puede seguir:

**DO**

* Aplicar separación de presentación, lógica y contenido
* Usar las API de AEM existentes (por ejemplo: Sling) y herramientas (por ejemplo: Replicación)
* Desarrollar en el contexto del contenido real
* Desarrollar para lograr una máxima capacidad de caché
* Minimizar el número de guardas (por ejemplo: mediante flujos de trabajo transitorios)
* Asegúrese de que todos los puntos finales HTTP son RESTful
* Restringir el alcance de la observación JCR
* Tenga en cuenta el subproceso asincrónico

**NO**

* No utilice las API de JCR directamente, si puede
* No cambie /libs, sino que utilice superposiciones
* No usar consultas siempre que sea posible
* No utilice Sling Bindings para obtener los servicios OSGi en el código Java, sino más bien utilice:

   * @Referencia en un componente DS
   * @Inyectar en un modelo Sling
   * sling.getService() en una clase Sightly Use
   * sling.getService() en un JSP
   * a ServiceTracker
   * acceso directo al registro de servicios OSGi

Para obtener más información sobre el desarrollo de AEM, lea [Desarrollar: conceptos básicos](/help/sites-developing/the-basics.md). Para obtener más información sobre las mejores prácticas, consulte [Optimizaciones para el desarrollo](/help/sites-developing/best-practices.md).

### Comparar escenarios {#benchmark-scenarios}

>[!NOTE]
>
>Todas las pruebas de referencia mostradas en esta página se han realizado en un laboratorio.

Los escenarios de prueba detallados a continuación se utilizan para las secciones de referencia de los capítulos TarMK, MongoMk y TarMK vs MongoMk. Para ver qué escenario se utilizó para una prueba de referencia en particular, lea el campo Escenario de la tabla [Especificaciones técnicas](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark).

**Escenario de un solo producto**

AEM Assets:

* Interacciones del usuario: Recursos de exploración / Recursos de búsqueda / Descargar recurso / Leer metadatos de recursos / Actualizar metadatos de recursos / Cargar recursos / Ejecutar flujo de trabajo de carga de recursos
* Modo de ejecución: usuarios simultáneos, interacción única por usuario

**Escenario de mezcla de productos**

AEM Sites + Assets:

* Interacciones del usuario del sitio: Leer página de artículos / Leer página / Crear párrafo / Editar párrafo / Crear página de contenido / Activar página de contenido / Búsqueda de autor
* Interacciones del usuario de recursos: Recursos de exploración / Recursos de búsqueda / Descargar recurso / Leer metadatos de recursos / Actualizar metadatos de recursos / Cargar recursos / Ejecutar flujo de trabajo de carga de recursos
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

**Caso de uso vertical**

Medios:

* Leer página de artículos (27,4%), página de lectura (10,9%), crear sesión (2,6%), activar página de contenido (1,7%), crear página de contenido (0,4%), crear párrafo (4,3%), editar párrafo (0,9%), componente de imagen (0,9%), recursos de exploración (20%), leer metadatos de recursos (8,5%), descargar recursos (4,2%), Recurso de búsqueda (0,2%), Actualizar metadatos de recursos (2,4%), Cargar recursos (1,2%), Examinar proyectos (4,9%), Leer proyectos (6,6%), Recurso de Añado de proyectos (1,2%), Sitio de Añado de proyectos (1,2%), Crear proyectos (0,1%), Búsqueda de autores (0,4%)
* Modo de ejecución: usuarios simultáneos, interacciones mixtas por usuario

## TarMK {#tarmk}

Este capítulo proporciona directrices generales de rendimiento para TarMK que especifican los requisitos mínimos de arquitectura y la configuración de configuración. También se proporcionan pruebas de referencia para una mayor aclaración.

Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de AEM Author como para las de Publish.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento de carro](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Directrices de arquitectura mínima de TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>Las directrices de arquitectura mínimas que se presentan a continuación son para entornos de producción y sitios de alto tráfico. Son **no** las [especificaciones mínimas](/help/sites-deploying/technical-requirements.md#prerequisites) necesarias para ejecutar AEM.

Para lograr un buen rendimiento al utilizar TarMK, debe realizar el inicio desde la siguiente arquitectura:

* Una instancia de Autor
* Dos instancias de publicación
* Dos despachantes

A continuación se ilustran las directrices de arquitectura para AEM sitios y AEM Assets.

>[!NOTE]
>
>Si se comparte el almacén de datos del archivo, la replicación sin binario debe activarse **en**.

**Directrices de arquitectura de etiquetas para AEM Sites**

![climage_1-5](assets/chlimage_1-5a.png)

**Directrices de arquitectura de etiquetas para AEM Assets**

![climage_1-6](assets/chlimage_1-6a.png)

### Directrices de configuración de TarMK {#tarmk-settings-guideline}

Para un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, [consulte esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Value</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajo de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitoria de granito</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> </td>
   <td>Añada estos parámetros JVM en la secuencia de comandos de inicio de AEM para evitar que consultas expansivas sobrecarguen los sistemas.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Activado</p> <p>Activado</p> <p>Activado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo del montón</p> </td>
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
   <td>Este flujo de trabajo administra XMP escritura en el binario original y establece la fecha de la última modificación en JCR.</td>
  </tr>
 </tbody>
</table>

### Prueba comparativa del rendimiento de TarMK {#tarmk-performance-benchmark}

#### Especificaciones técnicas {#technical-specifications}

Las pruebas de referencia se realizaron con arreglo a las siguientes especificaciones:

|  | **Nodo de autor** |
|---|---|
| Servidor | Hardware de metal desnudo (HP) |
| Sistema operativo | RedHat Linux |
| CPU/núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40GHz, 8 núcleos |
| RAM | 32 GB |
| Disco | Magnético |
| Java | Oracle JRE versión 8 |
| JVM Heap | 16 GB |
| Producto | AEM 6.2 |
| Nodestore | TarMK |
| Almacén de datos | Archivo DS |
| Escenario | Producto único: Recursos / 30 subprocesos simultáneos |

#### Resultados del indicador de rendimiento {#performance-benchmark-results}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como base de referencia y no son los números de rendimiento reales.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

La razón principal para elegir el servidor de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usando MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor se debe en general al hecho de que la CPU y la capacidad de memoria de un único servidor, que admite todas las actividades de creación concurrentes, ya no son sostenibles.

Para obtener más información sobre TarMK, consulte [Escenarios de implementación](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) y [Almacenamiento de mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Directrices de arquitectura mínima de MongoMK {#mongomk-minimum-architecture-guidelines}

Para lograr un buen rendimiento al utilizar MongoMK, debe realizar el inicio de la siguiente arquitectura:

* Tres instancias de creación
* Dos instancias de publicación
* Tres instancias de MongoDB
* Dos despachantes

>[!NOTE]
>
>En entornos de producción, MongoDB siempre se utilizará como conjunto de réplicas con un primario y dos secundarios. Las lecturas y las escrituras van a la primaria y las lecturas pueden ir a la secundaria. Si el almacenamiento no está disponible, uno de los secundarios se puede reemplazar por un árbitro, pero los conjuntos de réplicas de MongoDB siempre deben estar compuestos por un número impar de instancias.

>[!NOTE]
>
>Si se comparte el almacén de datos del archivo, la replicación sin binario debe activarse **en**.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Directrices de configuración de MongoMK {#mongomk-settings-guidelines}

Para un buen rendimiento, debe seguir las directrices de configuración que se presentan a continuación. Para obtener instrucciones sobre cómo cambiar la configuración, [consulte esta página](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Configuración</strong></td>
   <td><strong>Parámetro</strong></td>
   <td><strong>Valor (predeterminado)</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Colas de trabajo de Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU. </td>
   <td>De forma predeterminada, el número de subprocesos simultáneos por cola de trabajos es igual al número de núcleos de CPU.</td>
  </tr>
  <tr>
   <td>Cola de flujo de trabajo transitoria de granito</td>
   <td><code>Max Parallel</code></td>
   <td>Establezca el valor en la mitad del número de núcleos de CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parámetros de JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100 000</p> <p>250000</p> <p>Verdadero</p> <p>60000</p> </td>
   <td>Añada estos parámetros JVM en la secuencia de comandos de inicio de AEM para evitar que consultas expansivas sobrecarguen los sistemas.</td>
  </tr>
  <tr>
   <td>Configuración del índice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Activado</p> <p>Activado</p> <p>Activado</p> </td>
   <td>Para obtener más información sobre los parámetros disponibles, consulte <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">esta página</a>.</td>
  </tr>
  <tr>
   <td>Almacén de datos = Almacén de datos S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferior</p> <p>2-10% del tamaño máximo del montón</p> </td>
   <td>Consulte también <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configuraciones del almacén de datos</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 3)</p> <p>4 (4)</p> <p>./cache,size=2048,binario=0,-compacto,-compress</p> </td>
   <td><p>El tamaño predeterminado de la caché se establece en 256 MB.</p> <p>Tiene impacto en el tiempo que lleva realizar la invalidación de caché.</p> </td>
  </tr>
  <tr>
   <td>observación de robles</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>min &amp; max = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Prueba comparativa de rendimiento de MongoMK {#mongomk-performance-benchmark}

### Especificaciones técnicas {#technical-specifications-1}

Las pruebas de referencia se realizaron con arreglo a las siguientes especificaciones:

|  | **Nodo de creación** | **Nodo MongoDB** |
|---|---|---|
| Servidor | Hardware de metal desnudo (HP) | Hardware de metal desnudo (HP) |
| Sistema operativo | RedHat Linux | RedHat Linux |
| CPU/núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40GHz, 8 núcleos | CPU Intel(R) Xeon(R) E5-2407 @2,40GHz, 8 núcleos |
| RAM | 32 GB | 32 GB |
| Disco | Magnético: >1.000 IOPS | Magnético: >1.000 IOPS |
| Java | Oracle JRE versión 8 | N/D |
| JVM Heap | 16 GB | N/D |
| Producto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/D |
| Almacén de datos | Archivo DS | N/D |
| Escenario | Producto único: Recursos / 30 subprocesos simultáneos | Producto único: Recursos / 30 subprocesos simultáneos |

### Resultados del indicador de rendimiento {#performance-benchmark-results-1}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como base de referencia y no son los números de rendimiento reales.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

La regla básica que debe tenerse en cuenta al elegir entre los dos es que TarMK está diseñado para el rendimiento, mientras que MongoMK se utiliza para la escalabilidad. Adobe recomienda que TarMK sea la tecnología de persistencia predeterminada que utilizan los clientes en todos los escenarios de implementación, tanto para las instancias de AEM Author como para las de Publish.

La razón principal para elegir el servidor de persistencia MongoMK sobre TarMK es escalar las instancias horizontalmente. Esto significa tener dos o más instancias de autor activas ejecutándose en todo momento y usando MongoDB como sistema de almacenamiento de persistencia. La necesidad de ejecutar más de una instancia de autor suele deberse a que la CPU y la capacidad de memoria de un único servidor, que admite todas las actividades de creación concurrentes, ya no son sostenibles.

Para obtener más información sobre TarMK vs MongoMK, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Directrices TarMK vs MongoMk {#tarmk-vs-mongomk-guidelines}

**Beneficios de TarMK**

* Diseñado específicamente para aplicaciones gestoras de contenido
* Los archivos son siempre coherentes y se pueden realizar copias de seguridad con cualquier herramienta de backup basada en archivos
* Proporciona un mecanismo de conmutación por error: consulte [Cold Standby](/help/sites-deploying/tarmk-cold-standby.md) para obtener más información
* Proporciona alto rendimiento y almacenamiento de datos confiable con un overhead operacional mínimo
* Menor TCO (costo total de propiedad)

**Criterios para elegir MongoMK**

* Número de usuarios con nombre conectados en un día: en miles o más
* Número de usuarios simultáneos: en cientos o más
* Volumen de ingestas de recursos por día: en cientos de miles o más
* Volumen de las ediciones de página por día: en cientos de miles o más
* Volumen de búsquedas por día: en decenas de miles o más

### Prueba comparativa de TarMK frente a MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Los números que se presentan a continuación se han normalizado a 1 como base de referencia y no son números de rendimiento reales.

### Escenario 1 Especificaciones técnicas {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo OAK de creación</strong></td>
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
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40GHz, 8 núcleos</td>
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40GHz, 8 núcleos</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
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
   <td>JVM Heap16 GB</td>
   <td>16 GB</td>
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
   <td>Archivo DS </td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> Producto único: Recursos / 30 subprocesos simultáneos por ejecución</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resultados del indicador de rendimiento del escenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Escenario 2 Especificaciones técnicas {#scenario-technical-specifications-1}

>[!NOTE]
>
>Para habilitar el mismo número de autores con MongoDB que con un sistema TarMK, necesita un clúster con dos nodos AEM. Un clúster MongoDB de cuatro nodos puede gestionar 1,8 veces el número de autores que una instancia TarMK. Un clúster MongoDB de ocho nodos puede gestionar 2,3 veces el número de autores que una instancia TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo TarMK de creación</strong></td>
   <td><strong>Nodo MongoMK de creación</strong></td>
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
   <td>60 GB</td>
   <td>60 GB</td>
   <td>60 GB</td>
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
   <td>JVM Heap16 GB</td>
   <td>30 GB</td>
   <td>30 GB</td>
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
   <td>Archivo DS </td>
   <td><br /> Archivo DS</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Escenario</td>
   <td><p><br /> <br /> Caso de uso vertical: Medios / 2000 subprocesos simultáneos</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Resultados del indicador de rendimiento del escenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Directrices de escalabilidad de arquitectura para AEM Sites y recursos {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Resumen de las directrices de rendimiento {#summary-of-performance-guidelines}

Las directrices presentadas en esta página se pueden resumir de la siguiente manera:

* **TarMK con File** Datastorees la arquitectura recomendada para la mayoría de los clientes:

   * Topología mínima: una instancia de autor, dos instancias de publicación, dos despachantes
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **MongoMK con File** Datastorees la arquitectura recomendada para la escalabilidad horizontal del nivel Autor:

   * Topología mínima: tres instancias de creación, tres instancias de MongoDB, dos instancias de publicación, dos despachantes
   * Replicación sin binarios activada si se comparte el almacén de datos de archivos

* **** No debe almacenarse en el disco local, no en un almacenamiento conectado a la red (NAS)
* Al utilizar **Amazon S3**:

   * El almacén de datos de Amazon S3 se comparte entre el nivel Autor y Publicación
   * La replicación sin binario debe estar activada
   * La colección de elementos no utilizados del almacén de datos requiere una primera ejecución en todos los nodos Autor y Publicar y, a continuación, una segunda ejecución en Autor

* **El índice personalizado debe crearse además del** índice predeterminado basado en las búsquedas más comunes

   * Los índices de Lucene deben usarse para los índices personalizados

* **La personalización del flujo de trabajo puede mejorar sustancialmente el rendimiento**, por ejemplo, eliminando el paso del vídeo en el flujo de trabajo &quot;Actualizar recurso&quot;, desactivando los oyentes que no se utilizan, etc.

Para obtener más información, lea también la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).
