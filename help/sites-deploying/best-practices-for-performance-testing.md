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
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Prácticas recomendadas para pruebas de rendimiento{#best-practices-for-performance-testing}

## Introducción {#introduction}

Las pruebas de rendimiento son una parte importante de cualquier implementación AEM. Según los requisitos del cliente, se pueden realizar pruebas de rendimiento en las instancias de publicación, de autor o ambas.

En esta documentación se esbozarán las estrategias y metodologías generales para realizar pruebas de rendimiento, así como algunas de las herramientas que el Adobe pone a disposición para ayudar en el proceso. Finalmente, analizaremos algunas de las herramientas disponibles en el AEM 6 para ayudar con el ajuste del rendimiento, tanto desde el análisis del código como desde la perspectiva de la configuración del sistema.

### Simulación de realidad {#simulating-reality}

Lo más importante al realizar pruebas de rendimiento es asegurarse de imitar un entorno de producción lo más fielmente posible. Aunque esto puede resultar difícil, es imperativo garantizar la exactitud de estas pruebas. Al trabajar en el diseño de pruebas de rendimiento, es importante tener en cuenta los siguientes puntos:

* Contenido similar a la producción

Muchas mediciones de rendimiento en AEM, como el tiempo de respuesta de la consulta, pueden verse afectadas por el tamaño del contenido en el sistema. Es importante asegurarse de que el entorno de prueba tenga la copia de los datos de producción lo más cercana posible.

* Código de producción

La versión de AEM y las revisiones implementadas en la producción deben ser las mismas en el entorno de prueba. También es importante probar la versión del código que se implementa en la producción.

* Configuración de red y hardware similar a la producción

Las pruebas carecerán de sentido sin un entorno que se asemeje lo más posible a la producción. Lo ideal es que las especificaciones de hardware, las interfaces de red, los equilibradores de carga y la CDN sean idénticas a la producción en el entorno de prueba.

* Carga de producción

Muchos problemas de rendimiento no se ven hasta que el sistema está bajo una carga pesada. Las pruebas de buen rendimiento deben simular la carga en la que se encuentran los sistemas de producción en su punto máximo.

### Configuración de objetivos {#setting-goals}

Antes de comenzar con las pruebas de rendimiento, es necesario establecer requisitos no funcionales para especificar los tiempos de carga y respuesta. Si va a migrar desde un sistema existente, asegúrese de que el tiempo de respuesta sea similar a los valores de producción actuales. Para la carga, es mejor tomar la carga máxima actual y duplicarla. Esto garantizará que el sitio web pueda seguir funcionando bien a medida que crezca.

### Herramientas {#tools}

Hay muchas herramientas de prueba de rendimiento disponibles en el mercado. Al ejecutar una herramienta de generación de carga, es importante asegurarse de que los equipos que realizan las pruebas tengan suficiente ancho de banda de red. De lo contrario, una vez que la máquina de prueba alcance los límites de su conexión, no se generará carga adicional en el entorno que se esté probando.

#### Herramientas de prueba {#testing-tools}

* La herramienta **Tough Day** de Adobe se puede utilizar para generar carga en instancias AEM y recopilar datos de rendimiento. El equipo de ingeniería de AEM de Adobe realmente utiliza la herramienta para realizar pruebas de carga del propio producto de AEM. Las secuencias de comandos ejecutadas en el día difícil se configuran mediante archivos de propiedad y archivos XML JMX. Para obtener más información, consulte la [Documentación del día difícil](/help/sites-developing/tough-day.md).

* AEM proporciona herramientas listas para usar para ver rápidamente consultas problemáticas, solicitudes y mensajes de error. Para obtener más información, consulte la sección [Herramientas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentación del Tablero de operaciones.
* Apache proporciona un producto llamado **JMeter** que puede utilizarse para pruebas de rendimiento y carga, así como para comportamientos funcionales. Es software de código abierto y libre de usar, pero tiene un conjunto de funciones más pequeño que los productos empresariales y una curva de aprendizaje más pronunciada. Puede encontrar JMeter en el sitio web de Apache en [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load** Runneres es un producto de prueba de carga de grado empresarial. Hay disponible una versión de evaluación gratuita. Encontrará más información en [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* También se pueden utilizar herramientas de prueba de carga basadas en la nube como [Neustar](https://www.neustar.biz/services/web-performance/load-testing).
* A la hora de probar sitios web móviles o adaptables, es necesario utilizar un conjunto de herramientas independientes. Funcionan limitando el ancho de banda de la red, simulando conexiones móviles más lentas como 3G o EDGE. Entre las herramientas más utilizadas están:

   * **[Condicionador de vínculos de red](https://nshipster.com/network-link-conditioner/)** : proporciona una interfaz de usuario fácil de usar y funciona a un nivel bastante bajo en la pila de redes. Incluye versiones para OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) : una aplicación proxy de depuración web que, además de varios otros usos, proporciona regulación de red. Se proporcionan versiones para Windows, OS X y Linux.

#### Herramientas de optimización {#optimization-tools}

**Monitoreo**

La documentación de [Monitorización del rendimiento](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) es un buen recurso para herramientas y métodos que se pueden usar para diagnosticar problemas y señalar áreas para el ajuste.

**Modo de desarrollador en la IU táctil**

Una de las nuevas funciones de la IU táctil de AEM 6 es el Modo de desarrollador. Del mismo modo que los autores pueden cambiar entre los modos de edición y vista previa, los desarrolladores pueden cambiar al modo de desarrollador en la interfaz de usuario de autor para ver el tiempo de procesamiento de cada uno de los componentes de la página y ver los rastros de pila de cualquier error. Para obtener más información sobre el modo de desarrollador, consulte esta [presentación de Gems de CQ](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Uso de rlog.jar para leer los registros de solicitud**

Para un análisis más completo de los registros de solicitud en un sistema AEM, se puede utilizar `rlog.jar` para buscar y ordenar los archivos `request.log` que AEM genera. Este archivo jar se incluye con una instalación AEM en la carpeta `/crx-quickstart/opt/helpers`. Para obtener más información sobre la herramienta de registro y el registro de solicitudes en general, consulte la documentación [Monitoring and Maintain](/help/sites-deploying/monitoring-and-maintaining.md) .

**La herramienta Explicar consulta**

La [Explain Query tool](/help/sites-administering/operations-dashboard.md#explain-query) en ACS AEM Tools se puede utilizar para ver los índices que se utilizan al ejecutar una consulta. Esto puede resultar muy útil al optimizar las consultas de ejecución lenta.

**Herramientas PageSpeed**

Las herramientas PageSpeed de Google ofrecen análisis del sitio para el cumplimiento de las prácticas recomendadas en el rendimiento de la página, así como un complemento que se puede instalar junto con Dispatcher en una instancia de Apache para realizar optimizaciones adicionales. Para obtener más información, consulte el [Sitio Web de herramientas PageSpeed](https://developers.google.com/speed/pagespeed/).

## Entorno de creación {#author-environment}

### Realización de pruebas {#performing-tests}

Para realizar pruebas de rendimiento en el entorno de creación, es necesario simular la experiencia de los autores de producción. Esto significa que las instalaciones de creación deben contener todos los componentes, paquetes OSGi, personalización de la interfaz de usuario, índices personalizados y cualquier otra adición que haya implementado para las instancias de creación de producción.

Hay muchos marcos de automatización disponibles que están diseñados para pruebas de carga y rendimiento. Los scripts personalizados se pueden registrar en estas herramientas y reproducirse para simular un número máximo de autores que realizan simultáneamente actividades similares de creación y activación de contenido. Se recomienda utilizar la herramienta Día difícil para simular actividades como cargar miles de recursos o activar un gran número de páginas.

Para los tipos de entornos que tienen requisitos de carga de recursos pesada o creación de páginas, es imperativo utilizar herramientas como el Día duro para garantizar que el entorno funcione de forma eficiente bajo carga máxima. [](/help/sites-administering/webdav-access.md) WebDAVes una herramienta que no requiere secuencias de comandos y que también puede utilizarse para cargar grandes cantidades de recursos.

#### Pasos específicos de MongoDB {#mongodb-specific-steps}

En sistemas con backends MongoDB, AEM proporciona varios [JMX](/help/sites-administering/jmx-console.md) MBeans que deben monitorizarse al realizar pruebas de carga o rendimiento:

* Las **Estadísticas de caché consolidada** MBean. Se puede acceder directamente desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para la caché denominada **Document-Diff**, la tasa de visitas debe ser superior a `.90`. Si la tasa de visitas cae por debajo del 90%, es probable que tenga que modificar la configuración de `DocumentNodeStoreService`. La compatibilidad con el producto de Adobe puede recomendar una configuración óptima para su entorno.

* El **Oak Repository Statistics** Mbean. Se puede acceder directamente desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La sección **ObservationQueueMaxLength** mostrará la cantidad de eventos en la cola de observación de Oak durante las últimas horas, minutos, segundos y semanas. Busque el mayor número de eventos en la sección &quot;por hora&quot;. Este número debe compararse con la configuración `oak.observation.queue-length` que se encuentra en el componente **SlingRepositoryManager** de la consola [OSGi](/help/sites-deploying/web-console.md). Si el número más alto mostrado para la cola de observación supera la configuración `queue-length`, póngase en contacto con el servicio de asistencia al Adobe para obtener ayuda para aumentar la configuración. El valor predeterminado es 1000, pero la mayoría de las implementaciones suelen necesitar elevarlo a 20 000 o 50 000.

## Entorno de publicación {#publish-environment}

### Realización de pruebas {#performing-tests-1}

La parte más importante de una implementación que debe someterse a pruebas de carga es el usuario final que se enfrenta al entorno de publicación o Dispatcher.

Se pueden utilizar herramientas de prueba automatizadas de terceros para probar el rendimiento del sitio web. Estas herramientas permiten registrar los pasos que los usuarios van a seguir en el sitio y ejecutar muchas de estas sesiones al mismo tiempo para simular la carga típica de un sitio web de producción.

La mayoría de los sitios web de producción cuentan con optimizaciones, como el almacenamiento en caché de Dispatcher y una red de entrega de contenido. Al realizar pruebas, debe asegurarse de que estas optimizaciones también estén disponibles para el entorno de prueba. Además de supervisar los tiempos de respuesta de los usuarios finales, también debe supervisar las métricas del sistema en los servidores de publicación y distribuidores para asegurarse de que el sistema no se vea limitado por los recursos de hardware.

En un sistema que no requiere un alto nivel de personalización, Dispatcher debe almacenar en caché la mayoría de las solicitudes. Como resultado, la carga en la instancia de publicación debe permanecer relativamente plana. Si se requiere un alto nivel de personalización, se recomienda utilizar tecnologías como iFrames o solicitudes de AJAX para el contenido personalizado para permitir el almacenamiento en caché de Dispatcher lo más posible.

Para pruebas básicas, Apache Bench se puede utilizar para medir tiempos de respuesta del servidor web y ayudar a crear carga para medir cosas como fugas de memoria. Para obtener más información, consulte el ejemplo en [Monitoring documentation](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Resolución de problemas de rendimiento {#troubleshooting-performance-issues}

Después de ejecutar pruebas de rendimiento en la instancia de autor, cualquier problema deberá investigarse, diagnosticarse y solucionarse. Puede utilizar varias herramientas y técnicas al realizar análisis y solucionar problemas:

* Puede inspeccionar el [registro de rendimiento de la solicitud](/help/sites-administering/operations-dashboard.md#request-performance) en el panel de operaciones. Esta herramienta se puede utilizar para identificar solicitudes de página lentas
* Analizar consultas lentas en ejecución con la [herramienta Rendimiento de consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Observe el error lof para ver errores o advertencias. Para obtener más información, consulte [Inicio de sesión](/help/sites-deploying/configure-logging.md)
* Supervise los recursos de hardware del sistema, como la utilización de la memoria y la CPU, la E/S de disco o la E/S de red. Estos recursos suelen ser la causa de cuellos de botella en el rendimiento
* Optimice la arquitectura de las páginas y cómo se dirigen para minimizar el uso de parámetros de URL y permitir el máximo almacenamiento en caché posible
* Siga la documentación de [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md) y [Consejos de ajuste del rendimiento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

* Si hay problemas para editar determinadas páginas o componentes en instancias de autor, utilice el modo de desarrollador de TouchUI para inspeccionar la página en cuestión. Esto proporciona un desglose de cada área de contenido en la página, así como su tiempo de carga
* Minimice todos los JS y CSS del sitio. Para obtener más información sobre cómo hacerlo, consulte esta [publicación de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine CSS y JS incrustados de los componentes. Deben incluirse y minimizarse con las bibliotecas del lado del cliente para minimizar el número de solicitudes necesarias para procesar la página
* Utilice herramientas del navegador como la pestaña Red de Chrome para inspeccionar las solicitudes del servidor y ver cuáles tardan más.

Una vez identificadas las áreas problemáticas, el código de la aplicación puede inspeccionarse para optimizar el rendimiento. Cualquier función predeterminada AEM características que no funcionan correctamente puede solucionarse con la compatibilidad con Adobe.
