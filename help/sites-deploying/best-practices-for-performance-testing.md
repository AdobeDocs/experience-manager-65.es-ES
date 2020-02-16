---
title: Prácticas recomendadas para pruebas de rendimiento
seo-title: Prácticas recomendadas para pruebas de rendimiento
description: Este artículo describe las estrategias y metodologías generales utilizadas para las pruebas de rendimiento, así como algunas de las herramientas disponibles para ayudar en el proceso.
seo-description: Este artículo describe las estrategias y metodologías generales utilizadas para las pruebas de rendimiento, así como algunas de las herramientas disponibles para ayudar en el proceso.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prácticas recomendadas para pruebas de rendimiento{#best-practices-for-performance-testing}

## Introducción {#introduction}

Las pruebas de rendimiento son una parte importante de cualquier implementación de AEM. En función de los requisitos del cliente, se pueden realizar pruebas de rendimiento en las instancias de publicación, de autor o ambas.

Esta documentación describe las estrategias y metodologías generales para realizar pruebas de rendimiento, así como algunas de las herramientas que Adobe pone a disposición para ayudar en el proceso. Por último, analizaremos algunas de las herramientas disponibles en AEM 6 para facilitar el ajuste del rendimiento, tanto desde la perspectiva del análisis de código como de la configuración del sistema.

### Simular realidad {#simulating-reality}

Lo que es más importante al realizar pruebas de rendimiento es asegurarse de imitar un entorno de producción lo más cerca posible. Si bien esto a menudo puede ser difícil, es imperativo garantizar la precisión de estas pruebas. Al trabajar en el diseño de pruebas de rendimiento, es importante tener en cuenta los siguientes puntos:

* Contenido similar a la producción

Muchas mediciones de rendimiento en AEM, como el tiempo de respuesta a consultas, pueden verse afectadas por el tamaño del contenido del sistema. Es importante asegurarse de que el entorno de prueba tenga la copia más cercana posible de los datos de producción.

* Código de producción

La versión de AEM y las revisiones implementadas en la producción deben ser las mismas en el entorno de prueba. También es importante probar la versión del código que se implementa en la producción.

* Configuración de red y hardware similar a la producción

Las pruebas carecerán de sentido sin un entorno que se asemeje al de la producción lo más cerca posible. Idealmente, las especificaciones de hardware, las interfaces de red, los equilibradores de carga y la CDN deben ser idénticas a la producción en el entorno de prueba.

* Carga de producción

Muchos problemas de rendimiento no se ven hasta que el sistema está bajo una carga pesada. Las pruebas de buen rendimiento deben simular la carga en la que estarán los sistemas de producción en su punto máximo.

### Configuración de objetivos {#setting-goals}

Antes de comenzar con las pruebas de rendimiento, es necesario establecer requisitos no funcionales para especificar los tiempos de carga y respuesta. Si va a realizar la migración desde un sistema existente, asegúrese de que el tiempo de respuesta es similar a los valores de producción actuales. Para la carga, es mejor tomar la carga máxima actual y duplicarla. Esto garantizará que el sitio web pueda seguir funcionando bien a medida que crezca.

### Herramientas {#tools}

Existen muchas herramientas de prueba de rendimiento disponibles en el mercado. Cuando se ejecuta una herramienta de generación de carga, es importante asegurarse de que los equipos que realizan las pruebas tengan un ancho de banda de red suficiente. En caso contrario, una vez que la máquina de ensayo alcance los límites de su conexión, no se generará ninguna carga adicional en el entorno objeto de ensayo.

#### Herramientas de prueba {#testing-tools}

* La herramienta **Días** difíciles de Adobe se puede utilizar para generar carga en instancias de AEM y recopilar datos de rendimiento. El equipo de ingeniería de AEM de Adobe utiliza la herramienta para realizar pruebas de carga del propio producto AEM. Las secuencias de comandos ejecutadas en el Día difícil se configuran mediante archivos de propiedad y archivos XML de JMX. Para obtener más información, consulte la documentación [del Día](/help/sites-developing/tough-day.md)duro.

* AEM proporciona herramientas integradas para ver rápidamente consultas, solicitudes y mensajes de error problemáticos. Para obtener más información, consulte la sección Herramientas [de](/help/sites-administering/operations-dashboard.md#diagnosis-tools) diagnóstico de la documentación del panel de operaciones.
* Apache proporciona un producto llamado **JMeter** que puede utilizarse para pruebas de rendimiento y carga, así como para el comportamiento funcional. Es software de código abierto y libre de usar, pero tiene un conjunto de funciones más pequeño que los productos empresariales y una curva de aprendizaje más pronunciada. JMeter se puede encontrar en el sitio web de Apache en [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** es un producto de prueba de carga de nivel empresarial. Hay disponible una versión de evaluación gratuita. Encontrará más información en [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* También se pueden utilizar herramientas de prueba de carga basadas en la nube como [Neustar](https://www.neustar.biz/services/web-performance/load-testing) .
* Cuando se trata de probar sitios web móviles o adaptables, se debe utilizar un conjunto de herramientas independiente. Funcionan limitando el ancho de banda de la red, simulando conexiones móviles más lentas como 3G o EDGE. Entre las herramientas más utilizadas se encuentran:

   * **[Acondicionador](https://nshipster.com/network-link-conditioner/)**de vínculos de red: proporciona una interfaz de usuario fácil de usar y funciona a un nivel bastante bajo en la pila de redes. Incluye versiones para OS X e iOS;[](https://nshipster.com/network-link-conditioner/)
   * [**Charles **](https://www.charlesproxy.com/)- una aplicación proxy de depuración web que, además de otros usos, proporciona una limitación de red. Las versiones se proporcionan para Windows, OS X y Linux.[](https://www.charlesproxy.com/)

#### Herramientas de optimización {#optimization-tools}

**Monitoreo**

La documentación sobre el rendimiento [de](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) supervisión es un buen recurso para herramientas y métodos que se pueden utilizar para diagnosticar problemas y señalar áreas de ajuste.

**Modo de desarrollador en la IU táctil**

Una de las nuevas funciones de la IU táctil de AEM 6 es el modo de desarrollador. Del mismo modo que los autores pueden cambiar entre los modos de edición y vista previa, los desarrolladores pueden cambiar al modo de desarrollador en la interfaz de usuario del autor para ver el tiempo de procesamiento de cada uno de los componentes de la página y ver los rastros de pila de cualquier error. Para obtener más información sobre el modo de desarrollador, consulte esta presentación [de](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)CQ Gems.

**Uso de rlog.jar para leer los registros de solicitud**

Para realizar un análisis más completo de los registros de solicitudes en un sistema AEM, `rlog.jar` puede buscar y ordenar los `request.log` archivos que genera AEM. Este archivo .jar se incluye con una instalación de AEM en la `/crx-quickstart/opt/helpers` carpeta. Para obtener más información sobre la herramienta de registro y el registro de solicitudes en general, consulte la documentación [de Monitoreo y Mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md) .

**La herramienta Explicar consulta**

La herramienta [](/help/sites-administering/operations-dashboard.md#explain-query) Explicar consulta de ACS AEM Tools se puede utilizar para ver los índices que se utilizan al ejecutar una consulta. Esto puede resultar muy útil al optimizar las consultas de ejecución lenta.

**Herramientas de PageSpeed**

Las herramientas de PageSpeed de Google ofrecen análisis del sitio para cumplir con las optimizaciones en cuanto al rendimiento de la página, así como un complemento que se puede instalar junto con el despachante en una instancia de Apache para obtener optimizaciones adicionales. Para obtener más información, consulte el [sitio Web](https://developers.google.com/speed/pagespeed/)Herramientas de PageSpeed.

## Entorno de creación {#author-environment}

### Realización de pruebas {#performing-tests}

Para realizar pruebas de rendimiento en el entorno de creación, es necesario simular la experiencia de los autores de producción. Esto significa que las instalaciones de creación deben contener todos los componentes, los paquetes OSGi, la personalización de la interfaz de usuario, los índices personalizados y cualquier otra adición que se haya realizado para las instancias de creación de producción.

Existen muchos marcos de automatización diseñados para las pruebas de carga y rendimiento. Las secuencias de comandos personalizadas se pueden grabar en estas herramientas y reproducirse para simular un número máximo de autores que realizan simultáneamente actividades de creación y activación de contenido similares. Se recomienda utilizar la herramienta Día duro para simular actividades como cargar miles de recursos o activar un gran número de páginas.

Para los tipos de entornos que tienen requisitos de carga de recursos pesada o creación de páginas, es imperativo utilizar herramientas como el Día duro para garantizar que el entorno funcione de manera eficiente bajo la carga máxima. [WebDAV](/help/sites-administering/webdav-access.md) es una herramienta que no requiere secuencias de comandos y que también puede utilizarse para cargar grandes cantidades de recursos.

#### Pasos específicos de MongoDB {#mongodb-specific-steps}

En sistemas con back-ends de MongoDB, AEM proporciona varios MBeans de [JMX](/help/sites-administering/jmx-console.md) que deben monitorearse al realizar pruebas de carga o rendimiento:

* MBean de estadísticas **de caché** consolidada. Se puede acceder directamente a ella si se dirige a:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para la caché denominada **Document-Diff**, la tasa de visitas debería haber finalizado `.90`. Si la tasa de visitas cae por debajo del 90%, es probable que tenga que modificar la `DocumentNodeStoreService` configuración. La asistencia técnica del producto de Adobe puede recomendar una configuración óptima para su entorno.

* El **Oak Repository Statistics** Mbean. Se puede acceder directamente a ella si se dirige a:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La sección **ObservationQueueMaxLength** mostrará el número de eventos en la cola de observación de Oak durante las últimas horas, minutos, segundos y semanas. Busque el mayor número de eventos en la sección &quot;por hora&quot;. Este número debe compararse con la `oak.observation.queue-length` configuración que se encuentra en el componente **SlingRepositoryManager** de la consola [OSGi](/help/sites-deploying/web-console.md). Si el número más alto que se muestra para la cola de observación supera la `queue-length` configuración, póngase en contacto con el servicio de asistencia técnica de Adobe para obtener ayuda con la elevación de la configuración. La configuración predeterminada es 1.000, pero la mayoría de las implementaciones generalmente necesitan aumentarla a 20.000 o 50.000.

## Entorno de publicación {#publish-environment}

### Realización de pruebas {#performing-tests-1}

La parte más importante de una implementación que debe someterse a pruebas de carga es el usuario final que se enfrenta al entorno de publicación o de envío.

Se pueden utilizar herramientas de prueba automatizadas de terceros para probar el rendimiento del sitio web. Estas herramientas le permitirán registrar los pasos que los usuarios seguirán en el sitio y ejecutar muchas de estas sesiones al mismo tiempo para simular la carga típica de un sitio web de producción.

La mayoría de los sitios web de producción dispone de optimizaciones, como el almacenamiento en caché del despachante y una red de entrega de contenido. Al realizar pruebas, debe asegurarse de que estas optimizaciones también están disponibles para el entorno de prueba. Además de supervisar los tiempos de respuesta de los usuarios finales, también es necesario supervisar las métricas del sistema en los servidores de publicación y los despachantes para garantizar que el sistema no se vea limitado por los recursos de hardware.

En un sistema que no requiere un alto nivel de personalización, el despachante debe almacenar en caché la mayoría de las solicitudes. Como resultado, la carga en la instancia de publicación debe permanecer relativamente plana. Si se requiere un alto nivel de personalización, se recomienda utilizar tecnologías como iFrames o solicitudes AJAX para el contenido personalizado, de modo que se permita el mayor número posible de descargas de despachantes.

Para pruebas básicas, Apache Bench puede utilizarse para medir tiempos de respuesta del servidor web y ayudar a crear cargas para medir cosas como fugas de memoria. Para obtener más información, consulte el ejemplo en la documentación [de](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)supervisión.

## Resolución de problemas de rendimiento {#troubleshooting-performance-issues}

Después de ejecutar pruebas de rendimiento en la instancia de autor, cualquier problema deberá investigarse, diagnosticarse y resolverse. Puede utilizar varias herramientas y técnicas al realizar análisis y solucionar problemas:

* Puede inspeccionar el registro [Rendimiento de la](/help/sites-administering/operations-dashboard.md#request-performance) solicitud en el panel de operaciones. Esta herramienta se puede utilizar para identificar solicitudes de página lentas
* Analizar consultas de ejecución lenta con la herramienta Rendimiento de [consultas](/help/sites-administering/operations-dashboard.md#query-performance)

* Busque errores o advertencias en la lista de errores. For more information, see [Logging](/help/sites-deploying/configure-logging.md)
* Monitoree los recursos de hardware del sistema, como la utilización de la memoria y la CPU, la E/S en disco o la E/S en red. Estos recursos suelen ser las causas de los cuellos de botella en el rendimiento
* Optimice la arquitectura de las páginas y la manera en que se dirigen para minimizar el uso de parámetros de URL y permitir el mayor almacenamiento en caché posible
* Siga la documentación de consejos [de optimización](/help/sites-deploying/configuring-performance.md) de [rendimiento y optimización de](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) rendimiento

* Si hay problemas con la edición de determinadas páginas o componentes en instancias de autor, utilice el modo de desarrollador de TouchUI para inspeccionar la página en cuestión. Esto proporcionará un desglose de cada área de contenido de la página, así como el tiempo de carga
* Minimice todos los JS y CSS del sitio. Para obtener más información sobre cómo hacer esto, consulte esta [entrada](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)del blog.
* Elimine CSS y JS incrustados de los componentes. Deben incluirse y minimizarse con las bibliotecas del lado del cliente para minimizar el número de solicitudes necesarias para procesar la página
* Utilice las herramientas del navegador, como la ficha Red de Chrome, para inspeccionar las solicitudes del servidor y ver cuáles tardan más.

Una vez identificadas las áreas problemáticas, se puede inspeccionar el código de la aplicación para obtener optimizaciones de rendimiento. Cualquier función de AEM predeterminada que no funcione correctamente se puede abordar con la asistencia técnica de Adobe.
