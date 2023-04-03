---
title: Prácticas recomendadas para pruebas de rendimiento
description: Obtenga información sobre las estrategias y metodologías generales utilizadas para las pruebas de rendimiento y algunas de las herramientas disponibles para ayudar al proceso.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# Prácticas recomendadas para pruebas de rendimiento{#best-practices-for-performance-testing}

## Introducción {#introduction}

Las pruebas de rendimiento son una parte importante de cualquier implementación AEM. Según los requisitos del cliente, se pueden realizar pruebas de rendimiento en las instancias de publicación, de autor o ambas.

Esta documentación describe estrategias y metodologías generales para realizar pruebas de rendimiento y algunas de las herramientas disponibles por Adobe para ayudar al proceso. Por último, lea un análisis de las herramientas disponibles en el AEM 6 para ayudarle a ajustar el rendimiento, tanto desde el análisis del código como desde la perspectiva de la configuración del sistema.

### Simulación de realidad {#simulating-reality}

Al realizar pruebas de rendimiento, asegúrese de imitar un entorno de producción lo más cerca posible. Si bien esa tarea puede resultar difícil, es imperativo garantizar la exactitud de esas pruebas. Al trabajar en el diseño de pruebas de rendimiento, es importante tener en cuenta los siguientes puntos:

* Contenido similar a la producción

Muchas mediciones de rendimiento en AEM, como el tiempo de respuesta de la consulta, pueden verse afectadas por el tamaño del contenido en el sistema. Es importante asegurarse de que el entorno de prueba tenga la copia de los datos de producción lo más cercana posible.

* Código de producción

La versión de AEM y las revisiones implementadas en la producción deben ser las mismas en el entorno de prueba. También es importante probar la versión del código que se implementa en la producción.

* Configuración de red y hardware similar a la producción

Las pruebas carecen de sentido sin un entorno que se asemeje lo más posible a la de producción. Lo ideal es que las especificaciones de hardware, las interfaces de red, los equilibradores de carga y la CDN sean idénticas a la producción en el entorno de prueba.

* Carga de producción

Muchos problemas de rendimiento no se ven hasta que el sistema está bajo una carga pesada. Las pruebas de buen rendimiento deben simular la carga en la que se encuentran los sistemas de producción en su punto máximo.

### Configuración de objetivos {#setting-goals}

Antes de comenzar con las pruebas de rendimiento, es necesario establecer requisitos no funcionales para especificar los tiempos de carga y respuesta. Si va a migrar desde un sistema existente, asegúrese de que los tiempos de respuesta sean similares a los valores de producción actuales. Para la carga, es mejor tomar la carga máxima actual y duplicarla. Al hacerlo, se garantiza que el sitio web pueda seguir funcionando bien a medida que crezca.

### Herramientas {#tools}

Hay muchas herramientas de prueba de rendimiento disponibles en el mercado. Al ejecutar una herramienta de generación de carga, es importante asegurarse de que los equipos que realizan las pruebas tengan suficiente ancho de banda de red. De lo contrario, una vez que la máquina de prueba alcanza los límites de su conexión, no se genera carga adicional en el entorno que se está probando.

#### Herramientas de prueba {#testing-tools}

* Adobe **Día duro** se puede utilizar para generar carga en instancias AEM y recopilar datos de rendimiento. El equipo AEM ingeniería de Adobe utiliza realmente la herramienta para realizar pruebas de carga del propio producto de AEM. Las secuencias de comandos ejecutadas en el día difícil se configuran mediante archivos de propiedad y archivos XML JMX. Para obtener más información, consulte la [Documentación del Día duro](/help/sites-developing/tough-day.md).

* AEM proporciona herramientas listas para usar para ver rápidamente consultas problemáticas, solicitudes y mensajes de error. Para obtener más información, consulte la [Herramientas de diagnóstico](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentación del Tablero de operaciones.
* Apache proporciona un producto llamado **JMeter** que se puede utilizar para pruebas de rendimiento y carga, y comportamiento funcional. Es software de código abierto y libre de usar, pero tiene un conjunto de funciones más pequeño que los productos empresariales y una curva de aprendizaje más pronunciada. Puede encontrar JMeter en el sitio web de Apache en [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Cargar ejecución** es un producto de prueba de carga de nivel empresarial. Hay disponible una versión de evaluación gratuita. Encontrará más información en [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* Herramientas de prueba de carga de sitios web como [Neustar](https://neustarsecurityservices.com/web-performance-management) también se puede utilizar.
* Al probar sitios web móviles o adaptables, se debe utilizar un conjunto de herramientas independiente. Funcionan limitando el ancho de banda de la red, simulando conexiones móviles más lentas como 3G o EDGE. Entre las herramientas más utilizadas están las siguientes:

   * **[Condicionador de vínculo de red](https://nshipster.com/network-link-conditioner/)** : proporciona una interfaz de usuario fácil de usar y funciona a un nivel bastante bajo en la pila de redes. Incluye versiones para OS X y iOS;
   * [**Charles**](https://www.charlesproxy.com/) : una aplicación proxy de depuración web que, además de otros usos, proporciona restricciones de red. Se proporcionan versiones para Windows, OS X y Linux®.

#### Herramientas de optimización {#optimization-tools}

**Monitoreo**

La variable [Monitorización del rendimiento](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) La documentación es un buen recurso para herramientas y métodos que se pueden utilizar para diagnosticar problemas y señalar áreas para el ajuste.

**Modo de desarrollador en la IU táctil**

Una de las nuevas funciones de la IU táctil de AEM 6 es el Modo de desarrollador. Del mismo modo que los autores pueden cambiar entre los modos de edición y vista previa, los desarrolladores pueden cambiar al modo de desarrollador en la interfaz de usuario del autor. Al hacerlo, puede ver el tiempo de procesamiento de cada uno de los componentes de la página y ver los seguimientos de pila de cualquier error. Para obtener más información sobre el modo de desarrollador, consulte esta [Presentación de CQ Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**Uso de rlog.jar para leer los registros de solicitud**

Para un análisis más completo de los registros de solicitudes en un sistema AEM, `rlog.jar` se puede usar para buscar y ordenar `request.log` archivos que AEM genera. Este archivo jar se incluye con una instalación AEM en la variable `/crx-quickstart/opt/helpers` carpeta. Para obtener más información sobre la herramienta de registro y el inicio de sesión de solicitud en general, consulte la [Supervisión y mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md) documentación.

**La herramienta Explicar consulta**

La variable [Explicar la herramienta Consulta](/help/sites-administering/operations-dashboard.md#explain-query) en ACS AEM Tools se puede utilizar para ver los índices que se utilizan al ejecutar una consulta. Esta herramienta es útil para optimizar las consultas de ejecución lenta.

**Herramientas PageSpeed**

Las herramientas PageSpeed de Google ofrecen análisis de sitios para el cumplimiento de las prácticas recomendadas en el rendimiento de la página y un complemento que se puede instalar junto a Dispatcher en una instancia de Apache para realizar optimizaciones adicionales.
Consulte la [Sitio Web de las herramientas de PageSpeed](https://developers.google.com/speed).

## Entorno de creación {#author-environment}

### Realización de pruebas {#performing-tests}

Para realizar pruebas de rendimiento en el entorno de creación, es necesario simular la experiencia de los autores de producción. Es decir, las instalaciones de creación deben contener todos los componentes, paquetes OSGi, personalización de la interfaz de usuario, índices personalizados y cualquier otra adición que haya implementado para las instancias de creación de producción.

Hay muchos marcos de automatización disponibles que están diseñados para pruebas de carga y rendimiento. Los scripts personalizados se pueden registrar en estas herramientas y reproducirse para simular un número máximo de autores que realizan simultáneamente actividades similares de creación y activación de contenido. Se recomienda utilizar la herramienta Día difícil para simular actividades como cargar miles de recursos o activar un gran número de páginas.

Para los tipos de entornos que tienen requisitos de carga pesada de recursos o creación de páginas, es imperativo utilizar herramientas como el Día duro. De este modo, se garantiza que el entorno funcione de forma eficiente bajo carga máxima. [WebDAV](/help/sites-administering/webdav-access.md) es una herramienta que no requiere secuencias de comandos y que también puede utilizarse para cargar grandes cantidades de recursos.

#### Pasos específicos de MongoDB {#mongodb-specific-steps}

En sistemas con backends MongoDB, AEM proporciona varios [JMX](/help/sites-administering/jmx-console.md) MBas que deben monitorizarse al realizar pruebas de carga o rendimiento:

* La variable **Estadísticas de caché consolidada** MBean. Se puede acceder directamente desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Para la caché denominada **Document-Diff**, la tasa de visitas debería haber terminado `.90`. Si la tasa de visitas es inferior al 90 %, es probable que tenga que editar su `DocumentNodeStoreService` configuración. La compatibilidad con el producto de Adobe puede recomendar una configuración óptima para su entorno.

* La variable **Estadísticas del repositorio Oak** Mbean. Se puede acceder directamente desde:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La variable **ObservationQueueMaxLength** muestra el número de eventos en la cola de observación de Oak durante las últimas horas, minutos, segundos y semanas. Busque el mayor número de eventos en la sección &quot;por hora&quot;. Compare este número con el `oak.observation.queue-length` configuración. Si el número más alto mostrado para la cola de observación supera el `queue-length` configuración:

1. Cree un archivo llamado: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` que contiene el parámetro `oak.observation.queue‐length=50000`
1. Colóquela en la carpeta /crx-quickstart/install.

>[!NOTE]
>Consulte [AEM 6.x | Consejos de ajuste del rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en)

La configuración predeterminada es 10 000, pero la mayoría de las implementaciones deben aumentarla a 20 000 o 50 000.

## Entorno de publicación {#publish-environment}

### Realización de pruebas {#performing-tests-1}

La parte más importante de una implementación que debe someterse a pruebas de carga es el usuario final que se enfrenta al entorno de publicación o Dispatcher.

Se pueden utilizar herramientas de prueba automatizadas de terceros para probar el rendimiento del sitio web. Estas herramientas permiten registrar los pasos que siguen los usuarios en el sitio y ejecutar muchas de estas sesiones al mismo tiempo para simular la carga típica de un sitio web de producción.

La mayoría de los sitios web de producción cuentan con optimizaciones, como el almacenamiento en caché de Dispatcher y una red de entrega de contenido. Al realizar pruebas, asegúrese de que estas optimizaciones también estén disponibles para el entorno de prueba. Además de supervisar los tiempos de respuesta de los usuarios finales, supervise las métricas del sistema en los servidores de publicación y distribuidores para asegurarse de que el sistema no se vea limitado por los recursos de hardware.

En un sistema que no requiere un alto nivel de personalización, Dispatcher debe almacenar en caché la mayoría de las solicitudes. Como resultado, la carga en la instancia de publicación debe permanecer relativamente plana. Si se requiere un alto nivel de personalización, se recomienda utilizar tecnologías como iFrames o solicitudes de AJAX para el contenido personalizado para permitir el almacenamiento en caché de Dispatcher lo más posible.

Para pruebas básicas, Apache Bench se puede utilizar para medir tiempos de respuesta del servidor web y ayudar a crear carga para medir cosas como fugas de memoria. Consulte el ejemplo en la [Documentación de monitorización](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Resolución de problemas de rendimiento {#troubleshooting-performance-issues}

Después de ejecutar pruebas de rendimiento en la instancia de autor, cualquier problema debe investigarse, diagnosticarse y solucionarse. Puede utilizar varias herramientas y técnicas al realizar análisis y solucionar problemas:

* Puede inspeccionar el [Registro de rendimiento de la solicitud](/help/sites-administering/operations-dashboard.md#request-performance) en el panel de operaciones. Esta herramienta se puede utilizar para identificar solicitudes de página lentas
* Analice las consultas de ejecución lenta con el [Herramienta Rendimiento de consulta](/help/sites-administering/operations-dashboard.md#query-performance)

* Observe el registro de errores en busca de errores o advertencias. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).
* Supervise los recursos de hardware del sistema, como la utilización de la memoria y la CPU, la E/S de disco o la E/S de red. Estos recursos suelen ser la causa de cuellos de botella en el rendimiento.
* Optimice la arquitectura de las páginas y cómo se dirigen para minimizar el uso de parámetros de URL y permitir el almacenamiento en caché en la medida de lo posible.
* Siga las [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md) y [Consejos de ajuste del rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en) documentación.

* Si hay problemas para editar determinadas páginas o componentes en instancias de autor, utilice el modo de desarrollador de TouchUI para inspeccionar la página en cuestión. Al hacerlo, se proporciona un desglose de cada área de contenido de la página y su tiempo de carga.
* Minimice todos los JS y CSS del sitio. Consulte esta [publicación de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimine CSS y JS incrustados de los componentes. Deben incluirse y minimizarse con las bibliotecas del lado del cliente para minimizar el número de solicitudes necesarias para procesar la página.
* Para inspeccionar las solicitudes del servidor y ver cuáles tardan más, utilice herramientas de navegador como la pestaña Red de Chrome.

Una vez identificadas las áreas problemáticas, el código de la aplicación puede inspeccionarse para optimizar el rendimiento. Cualquier función predeterminada AEM características que no funcionan correctamente puede solucionarse con la compatibilidad con Adobe.
