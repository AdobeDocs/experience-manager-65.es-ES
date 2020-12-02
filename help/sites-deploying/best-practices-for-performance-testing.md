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
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 0%

---


# Prácticas recomendadas para pruebas de rendimiento{#best-practices-for-performance-testing}

## Introducción {#introduction}

Las pruebas de rendimiento son una parte importante de cualquier implementación AEM. En función de los requisitos del cliente, se pueden realizar pruebas de rendimiento en las instancias de publicación, de autor o ambas.

En esta documentación se esbozarán las estrategias y metodologías generales para realizar pruebas de rendimiento, así como algunos de los instrumentos que el Adobe pone a disposición para ayudar en el proceso. Por último, analizaremos algunas de las herramientas disponibles en la AEM 6 para ayudar a ajustar el rendimiento, tanto desde una perspectiva de análisis de código como de configuración del sistema.

### Simulación de realidad {#simulating-reality}

Lo que es más importante al realizar pruebas de rendimiento es asegurarse de imitar un entorno de producción lo más cerca posible. Si bien esto a menudo puede ser difícil, es imperativo garantizar la precisión de estas pruebas. Al trabajar en el diseño de pruebas de rendimiento, es importante tener en cuenta los siguientes puntos:

* Contenido similar a la producción

Muchas mediciones de rendimiento en AEM, como el tiempo de respuesta de consulta, pueden verse afectadas por el tamaño del contenido en el sistema. Es importante asegurarse de que el entorno de ensayo tenga la copia más cercana posible de los datos de producción.

* Código de producción

La versión AEM y las revisiones implementadas en la producción deben ser las mismas en el entorno de prueba. También es importante probar la versión del código que se implementa en la producción.

* Configuración de red y hardware similar a la producción

Las pruebas no tendrán sentido sin un entorno que se asemeje al de la producción lo más cerca posible. Idealmente, las especificaciones de hardware, las interfaces de red, los equilibradores de carga y la CDN deben ser idénticas a la producción en el entorno de prueba.

* Carga de producción

Muchos problemas de rendimiento no se ven hasta que el sistema está bajo una carga pesada. Las pruebas de buen rendimiento deben simular la carga en la que estarán los sistemas de producción en su punto máximo.

### Configuración de objetivos {#setting-goals}

Antes de comenzar con las pruebas de rendimiento, es necesario establecer requisitos no funcionales para especificar los tiempos de carga y respuesta. Si va a realizar la migración desde un sistema existente, asegúrese de que el tiempo de respuesta es similar a los valores de producción actuales. Para la carga, es mejor tomar la carga máxima actual y doble. Esto garantizará que el sitio web pueda seguir funcionando bien a medida que crezca.

### Herramientas {#tools}

Existen muchas herramientas de prueba de rendimiento disponibles en el mercado. Cuando se ejecuta una herramienta de generación de carga, es importante asegurarse de que los equipos que realizan las pruebas tengan un ancho de banda de red suficiente. En caso contrario, una vez que la máquina de ensayo alcance los límites de su conexión, no se generará ninguna carga adicional en el entorno objeto de ensayo.

#### Herramientas de prueba {#testing-tools}

* La herramienta **Día duro** de Adobe se puede utilizar para generar carga en instancias de AEM y recopilar datos de rendimiento. El equipo de ingeniería de AEM de Adobe utiliza la herramienta para realizar pruebas de carga del propio producto AEM. Las secuencias de comandos ejecutadas en el Día difícil se configuran mediante archivos de propiedad y archivos XML de JMX. Para obtener más información, consulte la [documentación del Día duro](/help/sites-developing/tough-day.md).

* AEM proporciona herramientas listas para usar para ver rápidamente consultas, solicitudes y mensajes de error problemáticos. Para obtener más información, consulte la sección [Herramientas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentación de Panel de operaciones.
* Apache proporciona un producto llamado **JMeter** que puede utilizarse para pruebas de rendimiento y carga, así como para comportamiento funcional. Es software de código abierto y libre de usar, pero tiene un conjunto de funciones más pequeño que los productos empresariales y una curva de aprendizaje más pronunciada. JMeter se encuentra en el sitio web de Apache en [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load** Runneres es un producto de prueba de carga de nivel empresarial. Hay disponible una versión de evaluación gratuita. Encontrará más información en [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* También se pueden utilizar herramientas de prueba de carga basadas en la nube como [Neustar](https://www.neustar.biz/services/web-performance/load-testing).
* Cuando se trata de probar sitios web móviles o adaptables, se debe utilizar un conjunto de herramientas independiente. Funcionan limitando el ancho de banda de la red, simulando conexiones móviles más lentas como 3G o EDGE. Entre las herramientas más utilizadas se encuentran:

   * **[Acondicionador](https://nshipster.com/network-link-conditioner/)**  de vínculos de red: proporciona una interfaz de usuario fácil de usar y funciona a un nivel bastante bajo en la pila de redes. Incluye versiones para OS X e iOS; [](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/) : una aplicación proxy de depuración web que, además de otros usos, proporciona una limitación de red. Las versiones se proporcionan para Windows, OS X y Linux. [](https://www.charlesproxy.com/)

#### Herramientas de optimización {#optimization-tools}

**Monitoreo**

La documentación de [Performance de monitoreo](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) es un buen recurso para herramientas y métodos que se pueden utilizar para diagnosticar problemas y señalar áreas para el ajuste.

**Modo de desarrollador en la IU táctil**

Una de las nuevas funciones de la IU táctil de AEM 6 es el modo de desarrollador. Al igual que los autores pueden cambiar entre los modos de edición y previsualización, los desarrolladores pueden cambiar al modo de desarrollador en la interfaz de usuario del autor para ver el tiempo de procesamiento de cada uno de los componentes de la página y ver los rastros de pila de cualquier error. Para obtener más información sobre el modo de desarrollador, consulte esta [presentación de CQ Gems](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Uso de rlog.jar para leer los registros de solicitud**

Para obtener una análisis más completa de los registros de solicitudes en un sistema AEM, `rlog.jar` puede utilizarse para buscar y ordenar los archivos `request.log` que AEM genera. Este archivo jar se incluye con una instalación AEM en la carpeta `/crx-quickstart/opt/helpers`. Para obtener más información sobre la herramienta de registro y el registro de solicitudes en general, consulte la documentación [Monitoreo y mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md).

**La herramienta Explicar Consulta**

La [herramienta Explicar Consulta](/help/sites-administering/operations-dashboard.md#explain-query) en ACS AEM Tools se puede utilizar para vista de los índices que se utilizan al ejecutar una consulta. Esto puede resultar muy útil al optimizar consultas de ejecución lenta.

**Herramientas de PageSpeed**

Análisis del sitio de oferta de las herramientas de Google PageSpeed para la adherencia a las optimizaciones para el rendimiento de la página, así como un complemento que se puede instalar junto con el despachante en una instancia de Apache para optimizaciones adicionales. Para obtener más información, consulte el [sitio Web de las herramientas de PageSpeed](https://developers.google.com/speed/pagespeed/).

## Entorno de creación {#author-environment}

### Realización de pruebas {#performing-tests}

Para realizar pruebas de rendimiento en el entorno del autor, es necesario simular la experiencia de los autores de producción. Esto significa que las instalaciones de creación deben contener todos los componentes, los paquetes OSGi, la personalización de la interfaz de usuario, los índices personalizados y cualquier otra adición que se haya realizado para las instancias de creación de producción.

Existen muchos marcos de automatización diseñados para las pruebas de carga y rendimiento. Las secuencias de comandos personalizadas se pueden grabar en estas herramientas y reproducirse para simular un número máximo de autores que realizan simultáneamente actividades de activación y creación de contenido similares. Se recomienda utilizar la herramienta Día duro para simular actividades como cargar miles de recursos o activar un gran número de páginas.

Para los tipos de entornos que requieren una carga de recursos pesada o la creación de páginas, es imperativo utilizar herramientas como el Día duro para garantizar que el entorno funcione de manera eficiente bajo la carga máxima. [](/help/sites-administering/webdav-access.md) WebDAVes una herramienta que no requiere secuencias de comandos y que también puede utilizarse para cargar grandes cantidades de recursos.

#### Pasos específicos de MongoDB {#mongodb-specific-steps}

En sistemas con back-ends de MongoDB, AEM proporciona varios [MBeans de JMX](/help/sites-administering/jmx-console.md) que se deben monitorear al realizar pruebas de carga o rendimiento:

* Las **Estadísticas de caché consolidada** MBean. Se puede acceder directamente a ella si se dirige a:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para la memoria caché denominada **Documento-Diff**, la tasa de visitas debe ser superior a `.90`. Si la tasa de visitas cae por debajo del 90%, es probable que tenga que modificar la configuración `DocumentNodeStoreService`. La asistencia técnica del producto de Adobe puede recomendar una configuración óptima para su entorno.

* El **Oak Repository Statistics** grano. Se puede acceder directamente a ella si se dirige a:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La sección **ObservationQueueMaxLength** mostrará el número de eventos en la cola de observación de Oak durante las últimas horas, minutos, segundos y semanas. Busque el mayor número de eventos en la sección &quot;por hora&quot;. Este número debe compararse con la configuración `oak.observation.queue-length` que se encuentra en el componente **SlingRepositoryManager** de la consola [OSGi](/help/sites-deploying/web-console.md). Si el número más alto que se muestra para la cola de observación supera la configuración `queue-length`, póngase en contacto con el servicio de soporte técnico de Adobe para obtener ayuda para aumentar la configuración. La configuración predeterminada es 1.000, pero la mayoría de las implementaciones generalmente necesitan aumentarla a 20.000 o 50.000.

## Entorno de publicación {#publish-environment}

### Realización de pruebas {#performing-tests-1}

La parte más importante de una implementación que debe someterse a pruebas de carga es el usuario final que se enfrenta al entorno de publicación o envío.

Se pueden utilizar herramientas de prueba automatizadas de terceros para probar el rendimiento del sitio web. Estas herramientas le permitirán registrar los pasos que los usuarios seguirán en el sitio y ejecutar muchas de estas sesiones al mismo tiempo para simular la carga típica de un sitio web de producción.

La mayoría de los sitios web de producción dispone de optimizaciones, como el almacenamiento en caché del despachante y una red de envío de contenido. Al realizar pruebas, debe asegurarse de que estas optimizaciones también están disponibles para el entorno de prueba. Además de supervisar los tiempos de respuesta de los usuarios finales, también es necesario supervisar las métricas del sistema en los servidores de publicación y los despachantes para garantizar que el sistema no se vea limitado por los recursos de hardware.

En un sistema que no requiere un alto nivel de personalización, el despachante debe almacenar en caché la mayoría de las solicitudes. Como resultado, la carga en la instancia de publicación debe permanecer relativamente plana. Si se requiere un alto nivel de personalización, se recomienda utilizar tecnologías como iFrames o solicitudes de AJAX para el contenido personalizado, de modo que se permita el almacenamiento en caché del despachante lo más posible.

Para pruebas básicas, Apache Bench puede utilizarse para medir tiempos de respuesta del servidor web y ayudar a crear cargas para medir cosas como fugas de memoria. Para obtener más información, consulte el ejemplo en la [documentación de monitoreo](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Solución de problemas de rendimiento {#troubleshooting-performance-issues}

Después de ejecutar pruebas de rendimiento en la instancia de autor, cualquier problema deberá investigarse, diagnosticarse y resolverse. Puede utilizar varias herramientas y técnicas al realizar análisis y resolver problemas:

* Puede inspeccionar el [registro de rendimiento de solicitudes](/help/sites-administering/operations-dashboard.md#request-performance) en el Panel de operaciones. Esta herramienta se puede utilizar para identificar solicitudes de página lentas
* Analizar consultas de ejecución lenta con la [herramienta de rendimiento de Consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Busque errores o advertencias en la lista de errores. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md)
* Monitoree los recursos de hardware del sistema, como la utilización de la memoria y la CPU, la E/S en disco o la E/S en red. Estos recursos suelen ser las causas de los cuellos de botella en el rendimiento
* Optimice la arquitectura de las páginas y la manera en que se dirigen para minimizar el uso de parámetros de URL y permitir el mayor almacenamiento en caché posible
* Siga la documentación de [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md) y [Consejos de ajuste del rendimiento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

* Si hay problemas con la edición de determinadas páginas o componentes en instancias de autor, utilice el modo de desarrollador de TouchUI para inspeccionar la página en cuestión. Esto proporcionará un desglose de cada área de contenido de la página, así como el tiempo de carga
* Minimice todos los JS y CSS del sitio. Para obtener más información sobre cómo hacerlo, consulte esta [entrada de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine CSS y JS incrustados de los componentes. Deben incluirse y minimizarse con las bibliotecas del lado del cliente para minimizar el número de solicitudes necesarias para procesar la página
* Utilice las herramientas del navegador, como la ficha Red de Chrome, para inspeccionar las solicitudes del servidor y ver cuáles tardan más.

Una vez identificadas las áreas problemáticas, se puede inspeccionar el código de la aplicación para obtener optimizaciones de rendimiento. Cualquier función predeterminada AEM las funciones que no funcionan correctamente se puede abordar con la asistencia de Adobe.
