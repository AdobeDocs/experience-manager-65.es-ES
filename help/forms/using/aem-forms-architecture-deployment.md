---
title: Arquitectura y topologías de implementación para AEM Forms
description: Detalles de arquitectura para AEM Forms y topologías recomendadas para clientes nuevos y existentes de AEM que actualicen de LiveCycle ES4 a AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 96%

---

# Arquitectura y topologías de implementación para AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html) |
| AEM 6.5 | Este artículo |

## Arquitectura {#architecture}

AEM Forms es una aplicación implementada en AEM como paquete de AEM. El paquete se conoce como paquete de complementos de AEM Forms. El paquete de complementos de AEM Forms contiene ambos servicios (proveedores de API), que se implementan en el contenedor OSGi de AEM y servlets o JSP (que proporcionan la funcionalidad de API de front-end y REST) administrados por el marco de trabajo de AEM Sling. El siguiente diagrama muestra esta configuración:

![arquitectura](assets/architecture.png)

La arquitectura para AEM Forms incluye los siguientes componentes:

* **Servicios principales de AEM:** servicios básicos que proporciona AEM a una aplicación implementada. Estos servicios incluyen un repositorio de contenido compatible con JCR, un contenedor de servicio OSGI, un motor de flujo de trabajo, un repositorio de confianza, un repositorio de claves, etc. Estos servicios están disponibles para la aplicación de AEM Forms, pero los paquetes de AEM Forms no los proporcionan. Estos servicios forman parte integral de la pila de AEM general y varios componentes de AEM Forms utilizan estos servicios.
* **Servicios de Forms:** proporcionan funciones relacionadas con los formularios, como crear, combinar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos y descodificar formularios de barras codificados. Estos servicios están disponibles públicamente para el consumo mediante el código personalizado que se ha implementado en AEM.
* **Capa web:** JSP o servlets, creados sobre servicios comunes y de formularios, que proporcionan las siguientes funcionalidades:

   * **Crear front-end**: una interfaz de usuario de creación y administración de formularios para crear y administrar formularios.
   * **Front-end Procesar y enviar formularios**: interfaz de usuario final para que la utilicen los usuarios finales de AEM Forms (por ejemplo, los ciudadanos que acceden a un sitio web del Gobierno). Proporciona funciones de representación de formularios (formulario de visualización en un explorador web) y envío.
   * **API de REST**: los JSP y los servlets exportan un subconjunto de servicios de formularios para el que lo consuman de manera remota clientes basados en HTTP, como el SDK móvil de formularios.

**AEM Forms en OSGi:** AEM Forms en un entorno OSGi es AEM Author estándar o AEM Publish con el paquete de AEM Forms implementado en él. Puede ejecutar AEM Forms en OSGi en un [entorno de servidor único, configuración de granjas y de clústeres](/help/sites-deploying/recommended-deploys.md). La configuración de clúster solo está disponible para instancias de autor de AEM.

**AEM Forms en JEE:** AEM Forms en JEE es un servidor de AEM Forms que se ejecuta en la pila JEE. Tiene AEM Author con paquetes de complementos de AEM Forms y capacidades adicionales de AEM Forms JEE implementadas en una única pila JEE que se ejecuta en un servidor de aplicaciones. Puede ejecutar AEM Forms en JEE en configuraciones de un solo servidor y agrupados. AEM Forms en JEE solo es necesario para ejecutar la seguridad de documentos, la administración de procesos y para clientes de LiveCycle que actualizan a AEM Forms. Estos son algunos escenarios adicionales para usar AEM Forms en JEE:

* **Compatibilidad con el espacio de trabajo HTML (para clientes que utilizan el espacio de trabajo HTML):** AEM Forms en JEE habilita el inicio de sesión único con instancias de procesamiento, sirve para ciertos recursos procesados en instancias de procesamiento y administra el envío de formularios procesados en el espacio de trabajo HTML.
* **Procesamiento de datos de formulario/comunicaciones interactivas adicionales avanzados**: AEM Forms en JEE se puede utilizar para procesar formularios o datos de comunicaciones interactivas adicionales (y guardar los resultados en un repositorio de datos adecuado) en casos de uso complejos en los que se requieren capacidades avanzadas de administración de procesos.

AEM Forms en JEE también incluye los siguientes servicios de compatibilidad con los componentes de AEM:

* **Administración de usuarios integrada:** permite que los usuarios de AEM Forms en JEE se reconozcan como AEM Forms en los usuarios de OSGi y ayuda a habilitar SSO para los usuarios de OSGi y JEE. Esto es necesario en los casos en los que se requiera el inicio de sesión único entre formularios de AEM en OSGi y AEM Forms en JEE (por ejemplo, en el espacio de trabajo HTML).
* **Alojamiento de recursos:** AEM Forms en JEE puede servir recursos (por ejemplo, formularios HTML5) procesados en AEM Forms en OSGi.

La interfaz de usuario de creación de AEM Forms no es compatible con la creación de documentos de registro (DOR), formularios PDF y formularios HTML5. Estos recursos están diseñados con la aplicación independiente de Forms Designer y se cargan individualmente en AEM Forms Manager. Alternativamente, para AEM Forms en JEE, los formularios se pueden diseñar como recursos de aplicación (en AEM Forms Workbench) e implementarse en AEM Forms en el servidor JEE.

Tanto AEM Forms en OSGi como AEM Forms en JEE tienen funcionalidades de flujo de trabajo. Puede crear e implementar rápidamente flujos de trabajo básicos para diversas tareas en AEM Forms en OSGi, sin tener que instalar la capacidad completa de Administración de procesos de AEM Forms en JEE. Hay alguna diferencia en las características [del flujo de trabajo centrado en formularios en AEM Forms sobre OSGi y la capacidad de administración de procesos de AEM Forms en JEE](capabilities-osgi-jee-workflows.md). El desarrollo y la administración de flujos de trabajo centrados en formularios en AEM Forms en OSGi utilizan las capacidades conocidas Flujo de trabajo de AEM y Bandeja de entrada de AEM.

## Terminologías {#terminologies}

La siguiente imagen muestra varias configuraciones del servidor de AEM Forms y sus componentes que se utilizan en una implementación típica de AEM Forms:

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**Autor:** una instancia de autor es un servidor de AEM Forms que se ejecuta en el modo de ejecución estándar de Autor. Puede ser AEM Forms en JEE o AEM Forms en un entorno OSGi. Está dirigido a usuarios internos, diseñadores de formularios y de comunicaciones interactivas y desarrolladores. Habilita las siguientes funcionalidades:

* **Crear y administrar formularios y comunicaciones interactivas:** los diseñadores y desarrolladores pueden crear y editar formularios adaptables y comunicaciones interactivas, cargar otros tipos de formularios creados externamente, por ejemplo, formularios creados en Adobe Forms Designer y administrar estos recursos mediante la consola de Forms Manager.
* **Publicar formularios y comunicaciones interactivas:** los recursos alojados en una instancia de autor se pueden publicar en una instancia de publicación para realizar operaciones de tiempo de ejecución. AEM La publicación de recursos utiliza las funciones de replicación de la. Adobe recomienda que se configure un agente de replicación en todas las instancias de autor para insertar manualmente los formularios publicados en las instancias de procesamiento y que se configure otro agente de replicación en las instancias de procesamiento con el activador *Recepción* habilitado para replicar automáticamente los formularios recibidos en las instancias de publicación.

**Publicación:** una instancia de publicación es un servidor de AEM Forms que se ejecuta en el modo de ejecución de publicación estándar. Las instancias de publicación están destinadas a los usuarios finales de aplicaciones basadas en formularios como, por ejemplo, los usuarios que acceden a un sitio web público y envían formularios. Habilita las siguientes funcionalidades:

* Procesar y enviar formularios para usuarios finales.
* Transportar datos de formulario enviados sin procesar a instancias de procesamiento para su procesamiento y almacenamiento posteriores en el sistema final de registro. La implementación predeterminada que se proporciona en AEM Forms logra esto al utilizar las capacidades de replicación inversa de AEM. También hay una implementación alternativa disponible para insertar directamente los datos del formulario en servidores de procesamiento en lugar de guardarlos localmente primero (siendo este último un requisito previo para que se active la replicación inversa). Los clientes que tengan dudas sobre el almacenamiento de datos confidenciales en instancias de publicación pueden participar en esto [implementación alternativa](/help/forms/using/configuring-draft-submission-storage.md), ya que las instancias de procesamiento normalmente se encuentran en una zona más segura.
* Presentar y enviar comunicaciones y cartas interactivas: se procesa una comunicación interactiva y una carta en las instancias de publicación y los datos correspondientes se envían a instancias de procesamiento para su almacenamiento y posprocesamiento. Los datos se pueden guardar localmente en una instancia de publicación y replicarse de forma inversa en una instancia de procesamiento (opción predeterminada) posteriormente, o insertarse directamente en la instancia de procesamiento sin guardar en la instancia de publicación. Esta última implementación es útil para los clientes conscientes de la seguridad.

**Procesamiento:** instancia de AEM Forms que se ejecuta en el modo de ejecución de Autor sin usuarios asignados al grupo de administrador de formularios. Puede implementar AEM Forms en JEE o en OSGi como instancia de procesamiento. Los usuarios no están asignados para garantizar que las actividades de creación y administración de formularios no se realicen en la instancia de procesamiento y solo se produzcan en la instancia de autor. Una instancia de procesamiento habilita las siguientes funcionalidades:

* **Procesar los datos de formulario sin procesar procedentes de una instancia de publicación:** esto se logra principalmente en una instancia de procesamiento a través de flujos de trabajo de AEM que se activan cuando llegan los datos. Los flujos de trabajo pueden utilizar el paso Modelo de datos de formulario que se proporciona de forma predeterminada para archivar los datos o el documento en un almacén de datos adecuado.
* **Almacenamiento seguro de datos de formulario**: el procesamiento proporciona un repositorio detrás del firewall para los datos de formulario sin procesar que están aislados de los usuarios. Ni los diseñadores de formularios de la instancia de autor ni los usuarios finales de la instancia de publicación pueden acceder a este repositorio.

  >[!NOTE]
  >
  >El Adobe AEM recomienda utilizar un repositorio de datos de terceros para guardar los datos procesados finales en lugar de utilizar el repositorio de datos de la aplicación de la versión de.

* **Almacenar y posprocesar los datos de correspondencia que llegan desde una instancia de publicación:** los flujos de trabajo de AEM realizan el posprocesamiento opcional de las definiciones de cartas correspondientes. Estos flujos de trabajo pueden guardar los datos procesados finales en un repositorio de datos externo adecuado.

* **Alojamiento en el espacio de trabajo HTML**: una instancia de procesamiento aloja el front-end para el espacio de trabajo HTML. El espacio de trabajo HTML proporciona la interfaz de usuario para la asignación de tareas/grupos asociados para los procesos de revisión y aprobación.

Una instancia de procesamiento está configurada para ejecutarse en el modo de ejecución de Autor debido a lo siguiente:

* Permite la replicación inversa de los datos de formulario sin procesar de una instancia de publicación. El controlador de almacenamiento de datos predeterminado requiere la característica de replicación inversa.
* Los flujos de trabajo de AEM, que son el principal medio de procesar los datos de formulario sin procesar que llegan desde una instancia de publicación, se recomiendan para ejecutarse en un sistema de estilo Autor.

## Topologías físicas de muestra para AEM Forms en JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Las topologías de AEM Forms en JEE recomendadas a continuación están destinadas principalmente a clientes que actualizan desde LiveCycle o una versión anterior de AEM Forms en JEE. Adobe recomienda utilizar AEM Forms en OSGi para instalaciones nuevas. Una nueva instalación de AEM Forms en JEE solo se recomienda para utilizar las capacidades de seguridad de documentos y administración de procesos.

### Topología para utilizar los servicios de documentos o funciones de seguridad de documentos {#topology-for-using-document-services-or-document-security-capabilities}

Los clientes de AEM Forms que planeen utilizar únicamente servicios de documentos o capacidades de seguridad de documentos pueden tener una topología similar a la que se muestra a continuación. Esta topología recomienda utilizar una sola instancia de AEM Forms. También puede crear un clúster o una granja de servidores de AEM Forms, si es necesario. Esta topología se recomienda cuando la mayoría de los usuarios acceden mediante programación a las capacidades del servidor de AEM Forms y la intervención a través de la interfaz de usuario es mínima. La topología es útil en las operaciones de procesamiento por lotes de los servicios de documentos. Por ejemplo, utilizar el servicio de salida para crear cientos de documentos PDF no editables diariamente.

Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, para un entorno que utiliza el servicio Generador de PDF para convertir miles de páginas al día y agregar firmas digitales para limitar el acceso a los documentos, configure servidores AEM Forms independientes para el servicio Generador de PDF y las funciones de firma digital. Esto permite proporcionar un rendimiento óptimo y escalar los servidores de forma independiente entre sí.

![basic-features](assets/basic-features.png)

### Topología para usar la administración de procesos de AEM Forms {#topology-for-using-aem-forms-process-management}

Los clientes de AEM Forms que planean utilizar las funciones de administración de procesos de AEM Forms, por ejemplo, el espacio de trabajo HTML, pueden tener una topología similar a la que se muestra a continuación. El servidor de AEM Forms en JEE puede estar configurado en un solo servidor o en clúster.

Si actualiza desde LiveCycle ES4, esta topología se corresponde estrechamente con lo que ya tiene en LiveCycle, excepto por la adición de AEM Author integrado a AEM Forms en JEE. Además, no hay cambios en los requisitos de agrupación en clúster para los clientes que realizan una actualización. Si utilizaba AEM Forms en un entorno en clúster, puede continuar con el mismo en AEM 6.5 Forms. Para una nueva instalación de AEM Forms de JEE para utilizar el espacio de trabajo HTML, la ejecución de la instancia de autor de AEM integrada en el entorno JEE es un requisito adicional.

El repositorio de datos de formulario es un repositorio de datos de terceros que se utiliza para almacenar datos procesados finales de formularios y comunicaciones interactivas. Es un elemento opcional de la topología. También puede configurar una instancia de procesamiento y utilizar su repositorio como el sistema final de registro, si fuera necesario.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

Se recomienda la topología a los clientes que planean utilizar AEM Forms en el servidor JEE para las funcionalidades de administración de procesos (espacio de trabajo HTML) sin utilizar ninguna funcionalidad de posprocesamiento, formularios adaptables, formularios HTML5 y comunicaciones interactivas.

### Topología para el uso de formularios adaptables, formularios HTML5, funciones de comunicaciones interactivas {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Los clientes de AEM Forms que planean utilizar las funciones de captura de datos de AEM Forms, por ejemplo, los formularios adaptables, formularios HTML5 o formularios PDF, pueden tener una topología similar a la que se muestra a continuación. Esta topología también se recomienda para usar capacidades de comunicaciones interactivas de AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Puede realizar los siguientes cambios o personalizaciones en la topología sugerida anteriormente:

* El uso del espacio de trabajo HTML y la aplicación de AEM Forms requiere una instancia de autor o de procesamiento de AEM. Puede utilizar la instancia de autor de AEM integrada en AEM Forms en el servidor JEE en lugar de configurar un servidor de autor de AEM externo adicional.
* Una instancia de autor o de procesamiento de AEM solo es necesaria para flujos de trabajo centrados en Forms en OSGi, formularios adaptables, portal de formularios y comunicaciones interactivas.
* La interfaz de usuario de Agente de comunicaciones interactivas se suele ejecutar dentro de la organización. Por lo tanto, puede mantener un servidor de publicación para la interfaz de usuario de Agente dentro de la red privada.
* AEM Forms en la instancia OSGi integrada en AEM Forms en el servidor JEE también pueden ejecutar flujos de trabajo centrados en Forms en OSGi y carpetas vigiladas.

## Ejemplo de topologías físicas para usar AEM Forms en OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topología para la captura de datos, comunicaciones interactivas, flujos de trabajo centrados en formularios sobre las capacidades de OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Los clientes de AEM Forms que planean utilizar las funciones de captura de datos de AEM Forms, por ejemplo, los formularios adaptables, formularios HTML5 o formularios PDF, pueden tener una topología similar a la que se muestra a continuación. Esta topología también se recomienda para utilizar comunicaciones interactivas y flujos de trabajo centrados en Forms en la capacidad OSGi, por ejemplo, para utilizar la bandeja de entrada de AEM y la aplicación de AEM Forms para flujos de trabajo de procesos empresariales.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topología para el uso de las funciones de carpeta vigilada para el procesamiento por lotes sin conexión {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Los clientes de AEM Forms que planean utilizar carpetas vigiladas para el procesamiento por lotes pueden tener una topología similar a la que se muestra a continuación. La topología muestra un entorno agrupado, pero decide utilizar una instancia única o una granja de servidores de AEM Forms en función de la carga. La fuente de datos de terceros es su propio sistema de registro. Actúa como fuente de entrada para carpetas vigiladas. La topología también muestra los resultados en forma de archivo impreso. También puede almacenar el contenido de salida en un sistema de archivos, enviarlo por correo electrónico y utilizar otros métodos personalizados para consumir resultados.

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topología para utilizar las funcionalidades de servicios de documentos para el procesamiento sin conexión basado en API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Los clientes de AEM Forms que planean utilizar únicamente la funcionalidad de servicios de documentos pueden tener una topología similar a la que se muestra a continuación. Esta topología recomienda utilizar un clúster de AEM Forms en servidores OSGi. Esta topología se recomienda cuando la mayoría de los usuarios acceden mediante programación (mediante API) al servidor de AEM Forms y la intervención a través de la interfaz de usuario es mínima. La topología es muy útil en varios casos de cliente de software. Por ejemplo, varios clientes que utilizan el servicio Generador de PDF para crear documentos PDF bajo demanda.

Aunque AEM Forms le permite configurar y ejecutar todas las funcionalidades desde un solo servidor, debe planificar la capacidad, equilibrar la carga y configurar servidores dedicados para funcionalidades específicas en un entorno de producción. Por ejemplo, en el caso de un entorno que utiliza el servicio PDF Generator para convertir miles de páginas al día y varios formularios adaptables para capturar datos, deberá configurar servidores de AEM Forms independientes para el servicio PDF Generator y las capacidades relacionadas con los formularios adaptables. Esto permite proporcionar un rendimiento óptimo y escalar los servidores de forma independiente entre sí.

![offline-api-based-processing](assets/offline-api-based-processing.png)
