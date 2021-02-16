---
title: Arquitectura y topologías de implementación para AEM Forms
seo-title: Arquitectura y topologías de implementación para AEM Forms
description: Detalles de la arquitectura para AEM Forms y topologías recomendadas para clientes nuevos y existentes de AEM y clientes que actualizan desde LiveCycle ES4 a AEM Forms.
seo-description: Detalles de la arquitectura para AEM Forms y topologías recomendadas para clientes nuevos y existentes de AEM y clientes que actualizan desde LiveCycle ES4 a AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 0%

---


# Arquitectura y topologías de implementación para AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Arquitectura {#architecture}

AEM Forms es una aplicación implementada en AEM como paquete AEM. El paquete se conoce como paquete de complementos de AEM Forms. El paquete de complementos de AEM Forms contiene ambos servicios (proveedores de API), que se implementan en el contenedor OSGi de AEM, y servlets o JSP (que proporcionan funcionalidad de API front-end y REST) administrados por el marco de trabajo de AEM Sling. En el diagrama siguiente se muestra esta configuración:

![arquitectura](assets/architecture.png)

La arquitectura para AEM Forms incluye los siguientes componentes:

* **Servicios principales de AEM:servicios** básicos que AEM proporciona a una aplicación implementada. Estos servicios incluyen un repositorio de contenido compatible con JCR, un contenedor de servicio OSGI, un motor de flujos de trabajo, un almacén de confianza, un almacén de claves, etc. Estos servicios están disponibles para la aplicación AEM Forms, pero no los proporcionan los paquetes de AEM Forms. Estos servicios son una parte integral de la pila de AEM general y varios componentes de AEM Forms utilizan estos servicios.
* **Servicios de Forms:** Proporcione funciones relacionadas con los formularios, como crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos y descodificar formularios codificados con barras. Estos servicios están disponibles públicamente para el consumo mediante código personalizado que se ha implementado en AEM.
* **Capa web:** JSP o servlets, creados con servicios comunes y de formularios, que proporcionan las siguientes funcionalidades:

   * **Factoría** de creación: Una interfaz de usuario de administración de formularios y creación de formularios para la creación y administración de formularios.
   * **Facturación de formulario y envío anticipado**: Interfaz de usuario final para que la utilicen los usuarios finales del AEM Forms (por ejemplo, los ciudadanos que acceden a un sitio web del gobierno). Esto proporciona representaciones de formularios (formulario para mostrar en un explorador Web) y funcionalidades de envío.
   * **API** de REST: Los JSP y los servlets exportan un subconjunto de servicios de formularios para el consumo remoto por parte de clientes basados en HTTP, como el SDK móvil de formularios.

**AEM Forms en OSGi:** Un AEM Forms en el entorno OSGi es AEM Author o AEM Publish estándar con el paquete AEM Forms implementado en él. Puede ejecutar AEM Forms en OSGi en una configuración [de un solo servidor, de entorno y agrupada](/help/sites-deploying/recommended-deploys.md). La configuración de clúster solo está disponible para instancias de AEM Author.

**AEM Forms en JEE:** AEM Forms en JEE es un servidor AEM Forms que se ejecuta en la pila JEE. Cuenta con AEM Author con paquetes de complementos de AEM Forms y funciones adicionales de AEM Forms JEE que se han implementado de forma conjunta en una única pila de JEE que se ejecuta en un servidor de aplicaciones. Puede ejecutar AEM Forms en JEE en configuraciones de un solo servidor y agrupadas. AEM Forms en JEE solo es necesario para ejecutar seguridad de documento, administración de procesos y para clientes de LiveCycle que actualicen a AEM Forms. Estos son algunos escenarios adicionales para usar AEM Forms en JEE:

* **Compatibilidad con el espacio de trabajo HTML (para clientes que utilizan el espacio de trabajo HTML):** AEM Forms en JEE activa el inicio de sesión único con instancias de procesamiento, sirve determinados recursos procesados en instancias de procesamiento y gestiona el envío de formularios procesados en el espacio de trabajo HTML.
* **Procesamiento** avanzado de datos de comunicaciones interactivas/formularios: AEM Forms en JEE se puede utilizar para procesar datos de comunicación interactivos/formularios adicionales (y guardar los resultados en un almacén de datos adecuado) en casos de uso complejos donde se requieren capacidades avanzadas de administración de procesos.

AEM Forms en JEE también incluye los siguientes servicios de soporte para los componentes de AEM:

* **Administración integrada de usuarios:** permite que los usuarios de AEM Forms en JEE se reconozcan como formularios AEM en los usuarios de OSGi y ayuda a habilitar SSO para los usuarios de OSGi y JEE. Esto es necesario para situaciones en las que se requiere el inicio de sesión único entre AEM formularios en OSGi y AEM Forms en JEE (por ejemplo, espacio de trabajo HTML).
* **Alojamiento de recursos:** AEM Forms en JEE puede servir recursos (por ejemplo, formularios HTML5) procesados en AEM Forms en OSGi.

La interfaz de usuario de creación de AEM Forms no admite la creación de Documentos de registro (DOR), PDF forms y HTML5 Forms. Estos recursos están diseñados con la aplicación Forms Designer independiente y se cargan individualmente en AEM Forms Manager. Como alternativa, para AEM Forms en JEE, los formularios pueden diseñarse como recursos de aplicaciones (en AEM Forms Workbench) e implementarse en AEM Forms en el servidor JEE.

Tanto AEM Forms en OSGi como AEM Forms en JEE tienen funciones de flujo de trabajo. Puede crear e implementar rápidamente flujos de trabajo básicos para varias tareas en los formularios AEM en OSGi, sin tener que instalar la capacidad de administración de procesos completa de AEM Forms en JEE. Existen algunas diferencias en las [características del flujo de trabajo centrado en el formulario en AEM Forms sobre OSGi y la capacidad de administración de procesos de AEM Forms en JEE](capabilities-osgi-jee-workflows.md). El desarrollo y la administración de flujos de trabajo centrados en formularios en AEM Forms en OSGi utiliza las funciones conocidas de Flujo de trabajo de AEM y Bandeja de entrada de AEM.

## Terminologías {#terminologies}

En la siguiente imagen se muestran varias configuraciones de servidor de AEM Form y sus componentes que se utilizan en una implementación típica de AEM Forms:

![aem_forms_-_recommendations_topología](assets/aem_forms_-_recommendedtopology.png)

**Autor:** Una instancia de autor es un servidor de AEM Forms que se ejecuta en el modo de ejecución estándar de Autor. Puede ser AEM Forms en JEE o AEM Forms en el entorno OSGi. Está destinado a usuarios internos, formularios y diseñadores de comunicaciones interactivos, así como a desarrolladores. Activa las siguientes funcionalidades:

* **Creación y gestión de formularios y comunicaciones interactivas:** Los diseñadores y desarrolladores pueden crear y editar formularios adaptables y comunicaciones interactivas, cargar otros tipos de formularios creados externamente, por ejemplo, formularios creados en Adobe Forms Designer, y administrar estos recursos mediante la consola de Forms Manager.
* **Publicación de formularios y comunicaciones interactivas:** los recursos alojados en una instancia de autor se pueden publicar en una instancia de publicación para realizar operaciones en tiempo de ejecución. La publicación de recursos utiliza las funciones de replicación de AEM. Adobe recomienda que se configure un agente de replicación en todas las instancias de creación para insertar manualmente los formularios publicados en las instancias de procesamiento, y que otro agente de replicación se configure en las instancias de procesamiento con el déclencheur *Al recibir* habilitado para replicar automáticamente los formularios recibidos en instancias de publicación.

**Publicar:** una instancia de publicación es un servidor de AEM Forms que se ejecuta en el modo de ejecución estándar de Publish. Las instancias de publicación están destinadas a usuarios finales de aplicaciones basadas en formularios, por ejemplo, usuarios que acceden a un sitio web público y envían formularios. Activa las siguientes funcionalidades:

* Representación y envío de Forms para usuarios finales.
* Transportación de datos de formulario enviados sin procesar a instancias de procesamiento para su posterior procesamiento y almacenamiento en el sistema final de registro. La implementación predeterminada que se proporciona en AEM Forms lo logra mediante las capacidades de replicación inversa de AEM. También hay una implementación alternativa disponible para insertar directamente los datos del formulario en servidores de procesamiento en lugar de guardarlos localmente primero (este último es un requisito previo para que se active la replicación inversa). Los clientes que tienen problemas con el almacenamiento de datos potencialmente confidenciales en instancias de publicación pueden participar en esta [implementación alternativa](/help/forms/using/configuring-draft-submission-storage.md), ya que las instancias de procesamiento suelen estar en una zona más segura.
* Representación y envío de comunicaciones y cartas interactivas: Una comunicación y una carta interactivas se procesan en las instancias de publicación y los datos correspondientes se envían a las instancias de procesamiento para su almacenamiento y posterior procesamiento. Los datos se pueden guardar localmente en una instancia de publicación y replicar de forma inversa en una instancia de procesamiento (opción predeterminada) posteriormente, o bien insertarse directamente en una instancia de procesamiento sin guardar en la instancia de publicación. Esta última implementación es útil para los clientes conscientes de la seguridad.

**Procesamiento:** una instancia de AEM Forms que se ejecuta en modo de ejecución de Autor sin usuarios asignados al grupo de administrador de formularios. Puede implementar AEM Forms en JEE o AEM Forms en OSGi como una instancia de procesamiento. Los usuarios no están asignados para garantizar que las actividades de creación y administración de formularios no se realicen en la instancia de procesamiento y solo se produzcan en la instancia de autor. Una instancia de procesamiento activa las siguientes funcionalidades:

* **Procesamiento de datos de formulario sin procesar procedentes de una instancia de Publish:** Esto se logra principalmente en una instancia de Procesamiento a través de flujos de trabajo de AEM que déclencheur cuando llegan los datos. Los flujos de trabajo pueden utilizar el paso del Modelo de datos de formulario que se proporciona de forma predeterminada para archivar los datos o el documento en un almacén de datos adecuado.
* **Almacenamiento seguro de los datos** del formulario: El procesamiento proporciona un repositorio detrás del servidor de seguridad para los datos de formulario sin procesar que están aislados de los usuarios. Ni los diseñadores de formularios de la instancia Autor ni los usuarios finales de la instancia Publicar pueden acceder a este repositorio.

   >[!NOTE]
   >
   > Adobe recomienda utilizar un almacén de datos de terceros para guardar los datos procesados finales en lugar de utilizar AEM repositorio.

* **Almacenamiento y postprocesamiento de los datos de correspondencia procedentes de una instancia de Publish:** AEM los flujos de trabajo realizan el postprocesamiento opcional de las definiciones de letras correspondientes. Estos flujos de trabajo pueden guardar los datos procesados finales en un almacén de datos externo adecuado.

* **Alojamiento** de HTML Workspace: Una instancia de procesamiento aloja el front-end para el espacio de trabajo HTML. El espacio de trabajo HTML proporciona la interfaz de usuario para la asignación de grupos/tareas asociada para los procesos de revisión y aprobación.

Una instancia de procesamiento está configurada para ejecutarse en el modo de ejecución Autor porque:

* Permite la replicación inversa de datos de formularios sin procesar desde una instancia de Publish. El controlador de almacenamiento de datos predeterminado requiere la función de replicación inversa.
* Se recomienda ejecutar AEM Flujos de trabajo, que son los principales medios para procesar datos de formularios sin procesar que llegan desde una instancia de Publish, en un sistema de estilo de autor.

## Topologías físicas de muestra para AEM Forms en JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Las topologías de AEM Forms en JEE que se recomiendan a continuación son principalmente para clientes que se actualizan desde LiveCycle o una versión anterior de AEM Forms en JEE. Adobe recomienda utilizar AEM Forms en OSGi para instalaciones nuevas. Una nueva instalación de AEM Forms en JEE solo se recomienda para utilizar las funciones de seguridad de Documento y administración de procesos.

### Topología para usar servicios de documento o capacidades de seguridad de documento {#topology-for-using-document-services-or-document-security-capabilities}

Los clientes de AEM Forms que planeen usar únicamente servicios de documento o capacidades de seguridad de documento pueden tener una topología similar a la que se muestra a continuación. Esta topología recomienda utilizar una sola instancia de AEM Forms. También puede crear un clúster o conjunto de servidores de AEM Forms, si es necesario. Esta topología se recomienda cuando la mayoría de los usuarios accede mediante programación a las capacidades del servidor de AEM Forms y la intervención a través de la interfaz de usuario es mínima. La topología es útil en operaciones de procesamiento por lotes de servicios de documento. Por ejemplo, con el servicio de salida se crean cientos de documentos PDF no editables diariamente.

Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un único servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funciones específicas en un entorno de producción. Por ejemplo, para un entorno que utilice el servicio de generación de archivos PDF para convertir miles de páginas al día y agregar firmas digitales para limitar el acceso a documentos, configure servidores AEM Forms independientes para el servicio de generación de archivos PDF y las funciones de firma digital. Ayuda a proporcionar un rendimiento óptimo y a escalar los servidores de forma independiente.

![basic-features](assets/basic-features.png)

### Topología para usar la administración de procesos de AEM Forms {#topology-for-using-aem-forms-process-management}

Los clientes de AEM Forms que planeen utilizar las funciones de administración de procesos de AEM Forms, por ejemplo, HTML Workspace puede tener una topología similar a la que se muestra a continuación. El AEM Forms en el servidor JEE puede estar en un único servidor o configuración de clúster.

Si está realizando la actualización desde LiveCycle ES4, esta topología refleja de cerca lo que ya tiene en LiveCycle, excepto por la adición de AEM Author integrado en AEM Forms en JEE. Además, no hay cambios en los requisitos de clustering para los clientes que realizan una actualización. Si estaba utilizando AEM Forms en un entorno agrupado, puede continuar con lo mismo en AEM 6.5 Forms. Para una nueva instalación de AEM Forms de JEE para utilizar HTML Workspace, es necesario ejecutar AEM instancia de creación integrada en el entorno JEE.

El almacén de datos de formularios es un almacén de datos de terceros que se utiliza para almacenar los datos procesados finales de los formularios y las comunicaciones interactivas. Es un elemento opcional de la topología. También puede configurar una instancia de procesamiento y utilizar su repositorio como sistema final de registro, si es necesario.

![topología_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

La topología se recomienda a los clientes que planeen utilizar AEM Forms en el servidor JEE para las capacidades de administración de procesos (espacio de trabajo HTML) sin necesidad de utilizar las funciones de posprocesamiento, formularios adaptables, formularios HTML5 y comunicaciones interactivas.

### Topología para el uso de formularios adaptables, formularios HTML5, capacidades de comunicación interactiva {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Los clientes de AEM Forms que planeen utilizar las funciones de captura de datos de AEM Forms, por ejemplo, formularios adaptables, HTML5 Forms, PDF forms, pueden tener una topología similar a la que se muestra a continuación. Esta topología también se recomienda para utilizar las capacidades de comunicación interactiva de AEM Forms.

![topología-para-uso-formularios-osgi-module](assets/topology-for-using-forms-osgi-modules.png)

Puede realizar los siguientes cambios o personalizaciones en la topología sugerida anteriormente:

* El uso de HTML Workspace y la aplicación de AEM Forms requiere un autor AEM o una instancia de procesamiento. Puede utilizar la instancia de creación de AEM integrada en AEM Forms en el servidor JEE en lugar de configurar un servidor de creación de AEM externo adicional.
* Solo se requiere una instancia de AEM Author o Processing para flujos de trabajo centrados en Forms en OSGi, formularios adaptables, portal de formularios y comunicación interactiva.
* la interfaz de usuario del agente de comunicaciones interactivo generalmente se ejecuta dentro de la organización. Por lo tanto, puede mantener un servidor de publicación para la interfaz de usuario del agente dentro de la red privada.
* Los formularios AEM de la instancia de OSGi integrada en AEM Forms en el servidor JEE también pueden ejecutar flujos de trabajo centrados en Forms en OSGi y carpetas vigiladas.

## Topologías físicas de muestra para usar AEM Forms en OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topología para la captura de datos, comunicación interactiva, flujo de trabajo centrado en formularios en las capacidades de OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Los clientes de AEM Forms que planeen utilizar las funciones de captura de datos de AEM Forms, por ejemplo, formularios adaptables, HTML5 Forms, PDF forms, pueden tener una topología similar a la que se muestra a continuación. Esta topología también se recomienda para utilizar comunicaciones interactivas y Flujos de trabajo Forms-Centric en la funcionalidad OSGi, por ejemplo, para utilizar la Bandeja de entrada AEM y la Aplicación AEM Forms para flujos de trabajo de procesos empresariales.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topología para usar capacidades de carpetas vigiladas para procesamiento por lotes sin conexión {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Los clientes de AEM Forms que planeen utilizar Carpetas vigiladas para el procesamiento por lotes pueden tener una topología similar a la que se muestra a continuación. La topología muestra un entorno agrupado, pero usted decide utilizar una sola instancia o un conjunto de servidores AEM Forms en función de la carga. La fuente de datos de terceros es su propio sistema de registro. Actúa como fuente de entrada para carpetas vigiladas. La topología también muestra el resultado en forma de archivo impreso. También puede almacenar el contenido de salida en un sistema de archivos, enviarlo por correo electrónico y utilizar otros métodos personalizados para consumir resultados.

![offline-batch-processing-via-watch-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topología para utilizar las capacidades de servicios de documento para el procesamiento sin conexión basado en API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Los clientes de AEM Forms que planeen utilizar únicamente la funcionalidad de servicios de documento pueden tener una topología similar a la que se muestra a continuación. Esta topología recomienda utilizar un clúster de AEM Forms en servidores OSGi. Esta topología se recomienda cuando la mayoría de los usuarios acceden mediante programación (mediante API) al servidor de AEM Forms y la intervención a través de la interfaz de usuario es mínima. La topología es muy útil en varios casos de cliente de software. Por ejemplo, varios clientes que utilizan el servicio PDF Generator para crear documentos PDF a petición.

Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un único servidor, debe planificar la capacidad, balancear la carga y configurar servidores dedicados para funciones específicas en un entorno de producción. Por ejemplo, para un entorno que utilice el servicio de generación de archivos PDF para convertir miles de páginas al día y varios formularios adaptables para capturar datos, configure servidores AEM Forms independientes para el servicio de generación de archivos PDF y funciones de formularios adaptables. Ayuda a proporcionar un rendimiento óptimo y a escalar los servidores de forma independiente.

![offline-api-based-processing](assets/offline-api-based-processing.png)

