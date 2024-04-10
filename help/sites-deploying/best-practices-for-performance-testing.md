---
title: Prácticas recomendadas para las pruebas de rendimiento
description: Conozca las estrategias generales y las metodologías utilizadas para las pruebas de rendimiento, así como algunas de las herramientas disponibles para ayudar en el proceso.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 0%

---

# Prácticas recomendadas para las pruebas de rendimiento{#best-practices-for-performance-testing}

## Introducción {#introduction}

AEM Las pruebas de rendimiento son una parte importante de cualquier implementación de la. Según los requisitos del cliente, las pruebas de rendimiento se pueden realizar en las instancias de publicación, las instancias de autor o ambas.

En esta documentación se describen las estrategias y metodologías generales para realizar pruebas de rendimiento y algunas de las herramientas que el Adobe pone a disposición para ayudar en el proceso. AEM Por último, lea un análisis de las herramientas disponibles en la versión 6 de para ayudar a ajustar el rendimiento, tanto desde el punto de vista del análisis del código como de la configuración del sistema.

### Simulación de la realidad {#simulating-reality}

Al realizar pruebas de rendimiento, asegúrese de imitar un entorno de producción lo más cerca posible. Si bien una tarea de este tipo a menudo puede ser difícil, es imperativo garantizar la precisión de estas pruebas. Al diseñar pruebas de rendimiento, es importante tener en cuenta los siguientes puntos:

* Contenido similar a la producción

AEM Muchas mediciones de rendimiento en los recursos, como el tiempo de respuesta a la consulta, pueden verse afectadas por el tamaño del contenido en el sistema. Es importante asegurarse de que el entorno de prueba tenga lo más cerca posible de una copia de los datos de producción.

* Código de producción

AEM La versión de la aplicación y las revisiones implementadas en la producción deben ser las mismas en el entorno de prueba. También es importante probar la versión del código que se implementa en la producción.

* Hardware y configuración de red similares a la producción

Las pruebas carecen de sentido sin un entorno que se asemeje al de producción lo más fielmente posible. Lo ideal es que las especificaciones de hardware, las interfaces de red, los equilibradores de carga y la red de distribución de contenido (CDN) sean idénticas a las de producción del entorno de prueba.

* Carga de producción

Muchos problemas de rendimiento no se ven hasta que el sistema está bajo una carga pesada. Las buenas pruebas de rendimiento deben simular la carga a la que se encuentran los sistemas de producción en su punto máximo.

### Estableciendo metas {#setting-goals}

Antes de comenzar las pruebas de rendimiento, es necesario establecer requisitos no funcionales para especificar los tiempos de carga y respuesta. Si está migrando desde un sistema existente, asegúrese de que los tiempos de respuesta sean similares a los valores de producción actuales. Para la carga, es mejor tomar la carga máxima actual y duplicarla. Al hacerlo, se asegura de que el sitio web pueda seguir funcionando bien a medida que crezca.

### Herramientas {#tools}

Hay muchas herramientas de prueba de rendimiento disponibles comercialmente en el mercado. Al ejecutar una herramienta de generación de carga, es importante asegurarse de que los equipos que realizan las pruebas tengan suficiente ancho de banda de red. De lo contrario, una vez que la máquina de prueba alcanza los límites de su conexión, no se genera ninguna carga adicional en el entorno en cuestión.

#### Herramientas de prueba {#testing-tools}

* Adobe **Día difícil** AEM se puede utilizar para generar carga en instancias de y recopilar datos de rendimiento. El equipo de ingeniería de Adobe AEM AEM utiliza la herramienta para probar la carga del producto en sí mismo, lo que lo convierte en una herramienta de prueba de la misma. Los scripts ejecutados en Día difícil se configuran mediante archivos de propiedad y archivos XML JMX. Para obtener más información, consulte la [Documentación de Día difícil](/help/sites-developing/tough-day.md).

* AEM proporciona herramientas listas para usar para ver rápidamente consultas, solicitudes y mensajes de error problemáticos. Para obtener más información, consulte la [Herramientas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentación del tablero de operaciones.
* Apache proporciona un producto llamado **JMeter** que se puede utilizar para pruebas de rendimiento y carga, y comportamiento funcional. Es software de código abierto y libre de usar, pero tiene un conjunto de características más pequeño que los productos empresariales y una curva de aprendizaje más pronunciada. JMeter se encuentra en el sitio web de Apache en [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Cargar ejecutor** es un producto de prueba de carga de nivel empresarial. Hay disponible una versión de evaluación gratuita. Encontrará más información en [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* Herramientas de prueba de carga del sitio web como [Vercara](https://vercara.com/website-performance-management) también se puede utilizar.
* Al probar sitios web móviles o adaptables, se debe utilizar un conjunto independiente de herramientas. Funcionan limitando el ancho de banda de la red, simulando conexiones móviles más lentas como 3G o EDGE. Entre las herramientas más utilizadas se encuentran las siguientes:

   * **[Acondicionador de enlace de red](https://nshipster.com/network-link-conditioner/)** : proporciona una interfaz de usuario fácil de usar y funciona a un nivel bastante bajo en la pila de red. Incluye versiones para OS X y iOS;
   * [**Charles**](https://www.charlesproxy.com/) : una aplicación proxy de depuración web que, además de otros usos, proporciona limitación de red. Se proporcionan versiones para Windows, OS X y Linux®.

#### Herramientas de optimización {#optimization-tools}

**Monitorización**

El [Monitorización del rendimiento](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) La documentación de es un buen recurso para herramientas y métodos que se pueden utilizar para diagnosticar problemas y localizar áreas para ajustar.

**Modo de desarrollador en IU táctil**

AEM Una de las nuevas funciones de la IU táctil de la 6 es el modo de desarrollador. Del mismo modo que los autores pueden cambiar entre los modos de edición y vista previa, los desarrolladores pueden cambiar al modo de desarrollador en la interfaz de usuario del autor. Al hacerlo, puede ver el tiempo de procesamiento de cada uno de los componentes de la página y los seguimientos de pila de los errores. Para obtener más información sobre el modo de desarrollador, consulte [Presentación de CQ Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html).

**Uso del archivo log.jar para leer los registros de solicitudes**

AEM Para obtener un análisis más completo de los registros de solicitudes de un sistema de, `rlog.jar` se puede utilizar para buscar y ordenar los `request.log` AEM archivos que genera el. AEM Este archivo .jar se incluye con una instalación de en `/crx-quickstart/opt/helpers` carpeta. Para obtener más información sobre la herramienta de registro y el registro de solicitudes en general, consulte la [Supervisión y mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md) documentación.

**La herramienta de consulta Explicar**

El [Herramienta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query) AEM en ACS se pueden utilizar herramientas para ver los índices que se utilizan al ejecutar una consulta. Esta herramienta es útil cuando se optimizan consultas de ejecución lenta.

**Herramientas de velocidad de página**

Las herramientas PageSpeed de Google ofrecen análisis de sitio para la adherencia a las prácticas recomendadas para el rendimiento de la página y un complemento que se puede instalar junto con Dispatcher en una instancia de Apache para optimizaciones adicionales.
Consulte la [Sitio web de herramientas de PageSpeed](https://developers.google.com/speed).

## Entorno de creación {#author-environment}

### Realización de pruebas {#performing-tests}

Para realizar pruebas de rendimiento en el entorno de creación, es necesario simular la experiencia de los autores de producción. Es decir, las instalaciones de creación deben contener todos los componentes, paquetes OSGi, personalización de la interfaz de usuario, índices personalizados y cualquier otra adición que tenga para las instancias de creación de producción.

Hay muchos marcos de automatización disponibles que están diseñados para pruebas de carga y rendimiento. Las secuencias de comandos personalizadas se pueden registrar en estas herramientas y luego reproducirse para simular un número máximo de autores que realizan actividades similares de creación y activación de contenido simultáneamente. Se recomienda utilizar la herramienta Día difícil para simular actividades como cargar miles de recursos o activar una gran cantidad de páginas.

Para los tipos de entornos que tienen requisitos de carga pesada de recursos o creación de páginas, es imperativo utilizar herramientas como Día difícil. Al hacerlo, se garantiza que el entorno funcione de forma eficiente con carga máxima. [WebDAV](/help/sites-administering/webdav-access.md) es una herramienta que no requiere scripts y que también se puede utilizar para cargar grandes cantidades de recursos.

#### Pasos específicos de MongoDB {#mongodb-specific-steps}

AEM En sistemas con back-ends MongoDB, proporciona varias opciones de configuración, entre las que se incluyen: [JMX](/help/sites-administering/jmx-console.md) MBeans que deben supervisarse al realizar pruebas de carga o rendimiento:

* El **Estadísticas de caché consolidadas** MBean. Se puede acceder directamente a ella desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para la caché denominada **Document-Diff**, la tasa de visitas debe haber terminado `.90`. Si la tasa de visitas cae por debajo del 90 %, es probable que deba editar su `DocumentNodeStoreService` configuración. El soporte del producto de Adobe puede recomendar configuraciones óptimas para su entorno.

* El **Estadísticas del repositorio de Oak** Mbean. Se puede acceder directamente a ella desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

El **ObservationQueueMaxLength** Esta sección muestra el número de eventos en la cola de observación de Oak durante las últimas horas, minutos, segundos y semanas. Busque el mayor número de eventos en la sección &quot;por hora&quot;. Compare este número con el `oak.observation.queue-length` configuración. Si el número más alto mostrado para la cola de observación supera el `queue-length` configuración:

1. Cree un archivo con el nombre: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` que contiene el parámetro `oak.observation.queue‐length=50000`
1. Colóquelo en la carpeta /crx-quickstart/install.

>[!NOTE]
>Consulte [AEM.x | Consejos de ajuste de rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=es)

La configuración predeterminada es 10 000, pero la mayoría de las implementaciones deben aumentarla a 20 000 o 50 000.

## Entorno de publicación {#publish-environment}

### Realización de pruebas {#performing-tests-1}

La parte más importante de una implementación que debe estar sujeta a pruebas de carga es el usuario final que se enfrenta al entorno de publicación o Dispatcher.

Se pueden utilizar herramientas de prueba automatizadas de terceros para probar el rendimiento del sitio web. Estas herramientas permiten registrar los pasos que siguen los usuarios en el sitio y ejecutar muchas de estas sesiones al mismo tiempo para simular la carga típica de un sitio web de producción.

La mayoría de los sitios web de producción tienen optimizaciones, como el almacenamiento en caché de Dispatcher y una red de entrega de contenido. Al realizar pruebas, asegúrese de que estas optimizaciones también estén disponibles para el entorno de prueba. Además de supervisar los tiempos de respuesta de los usuarios finales, supervise las métricas del sistema en los servidores de publicación y los distribuidores para garantizar que el sistema no se vea limitado por los recursos de hardware.

En un sistema que no requiera un nivel alto de personalización, Dispatcher debe almacenar en caché la mayoría de las solicitudes. Como resultado, la carga en la instancia de publicación debe permanecer relativamente plana. AJAX Si se requiere un alto nivel de personalización, se recomienda utilizar tecnologías como iFrames o solicitudes de para el contenido personalizado para permitir el mayor almacenamiento en caché posible de Dispatcher.

Para pruebas básicas, Apache Bench se puede utilizar para medir los tiempos de respuesta de los servidores web y ayudar a crear carga para medir cosas como pérdidas de memoria. Consulte el ejemplo en la [Monitorización de documentación](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Solución de problemas de rendimiento {#troubleshooting-performance-issues}

Después de ejecutar pruebas de rendimiento en la instancia de autor, cualquier problema debe investigarse, diagnosticarse y solucionarse. Puede utilizar varias herramientas y técnicas al realizar análisis y abordar problemas:

* Puede inspeccionar el [Registro de rendimiento de solicitudes](/help/sites-administering/operations-dashboard.md#request-performance) en el tablero de operaciones. Esta herramienta se puede utilizar para identificar solicitudes de página lentas.
* Analizar consultas de ejecución lenta con [Herramienta de rendimiento de consultas](/help/sites-administering/operations-dashboard.md#query-performance)

* Observe el registro de errores para ver si hay errores o advertencias. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).
* Supervise los recursos de hardware del sistema, como la utilización de memoria y CPU, E/S de disco o E/S de red. Estos recursos suelen ser la causa de cuellos de botella en el rendimiento.
* Optimizar la arquitectura de las páginas y cómo se dirigen para minimizar el uso de parámetros de URL y permitir el mayor almacenamiento en caché posible.
* Siga las [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md) y [Consejos de rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=es) documentación.

* Si hay problemas con la edición de determinadas páginas o componentes en instancias de autor, utilice el modo de desarrollador de TouchUI para inspeccionar la página en cuestión. Al hacerlo, se proporciona un desglose de cada área de contenido de la página y de su tiempo de carga.
* Minimice todos los JS y CSS del sitio. Ver esto [publicación de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine CSS y JS incrustados de los componentes. Deben incluirse y minificarse con las bibliotecas del lado del cliente para minimizar el número de solicitudes necesarias para procesar la página.
* Para inspeccionar las solicitudes del servidor y ver cuáles tardan más, utilice herramientas del explorador como la pestaña Red de Chrome.

Una vez identificadas las áreas problemáticas, se puede inspeccionar el código de la aplicación para ver si hay optimizaciones del rendimiento. AEM Cualquier característica de la versión predeterminada que no funcione correctamente se puede solucionar con la compatibilidad con Adobes.
