---
title: Optimización del rendimiento
seo-title: Optimización del rendimiento
description: Aprenda a configurar ciertos aspectos de la AEM para optimizar el rendimiento.
seo-description: Aprenda a configurar ciertos aspectos de la AEM para optimizar el rendimiento.
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '6722'
ht-degree: 2%

---


# Optimización del rendimiento{#performance-optimization}

>[!NOTE]
>
>Para obtener instrucciones generales sobre el rendimiento, lea la página [Pautas de rendimiento](/help/sites-deploying/performance-guidelines.md).
>
>Para obtener más información acerca de la solución de problemas y la corrección de problemas de rendimiento, consulte también el [árbol de rendimiento](/help/sites-deploying/performance-tree.md).
>
>Además, puede revisar un artículo de Knowledge Base en [Consejos de ajuste de rendimiento.](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

Un problema clave es el tiempo que tarda el sitio web en responder a las solicitudes de visitante. Aunque este valor variará para cada solicitud, se puede definir un valor de destinatario promedio. Una vez que se ha demostrado que este valor es alcanzable y sostenible, puede utilizarse para monitorear el rendimiento del sitio web e indicar el desarrollo de posibles problemas.

Los tiempos de respuesta que va a buscar serán diferentes en los entornos de creación y publicación, lo que refleja las diferentes características de la audiencia de destinatario:

## Entorno de creación {#author-environment}

Este entorno lo utilizan los autores que introducen y actualizan contenido. Debe atender a un pequeño número de usuarios, cada uno de los cuales genera un gran número de solicitudes de rendimiento al actualizar las páginas de contenido y los elementos individuales de esas páginas.

## Entorno de publicación {#publish-environment}

Este entorno contiene contenido que puede poner a disposición de los usuarios. En este caso, el número de solicitudes es incluso bueno y la velocidad es igualmente vital, pero dado que la naturaleza de las solicitudes es menos dinámica, se pueden aplicar mecanismos adicionales de mejora del rendimiento; como almacenar en caché el contenido o el equilibrio de carga.

>[!NOTE]
>
>* Después de configurar la optimización del rendimiento, siga los procedimientos de [Día duro](/help/sites-developing/tough-day.md) para probar el entorno bajo una carga pesada.
>* Consulte también [Consejos de ajuste del rendimiento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

>



## Metodología de optimización del rendimiento {#performance-optimization-methodology}

Una metodología de optimización del rendimiento para proyectos de CQ se puede resumir en cinco reglas muy sencillas que se pueden seguir para evitar problemas de rendimiento del inicio:

1. [Planificación para la optimización](#planning-for-optimization)
1. [Simular realidad](#simulate-reality)
1. [Establecer objetivos sólidos](#establish-solid-goals)
1. [Permanecer relevante](#stay-relevant)
1. [Ciclos de iteración ágiles](#agile-iteration-cycles)

Estas reglas, en gran medida, se aplican a los proyectos Web en general y son pertinentes para los directores de proyectos y administradores de sistemas a fin de garantizar que sus proyectos no se enfrenten a problemas de rendimiento cuando llegue el momento de su lanzamiento.

### Planificación para la optimización {#planning-for-optimization}

![climage_1-3](assets/chlimage_1-3.jpeg)

Alrededor del 10% del esfuerzo del proyecto debe planificarse para la fase de optimización del rendimiento. Por supuesto, los requisitos reales de optimización del rendimiento dependerán del nivel de complejidad de un proyecto y de la experiencia del equipo de desarrollo. Si bien el proyecto puede (en última instancia) no requerir todo el tiempo asignado, es recomendable planificar siempre la optimización del rendimiento en la región sugerida.

Siempre que sea posible, un proyecto debe lanzarse en forma suave a una audiencia limitada para reunir experiencia en la vida real y realizar más optimizaciones, sin la presión adicional que sigue a un anuncio completo.

Una vez que esté &quot;activo&quot;, la optimización del rendimiento no finaliza. Este es el momento en el que experimenta la carga &quot;real&quot; en su sistema. Es importante planificar ajustes adicionales después del lanzamiento.

Dado que la carga del sistema cambia y que los perfiles de rendimiento del sistema cambian con el tiempo, se debe programar una &quot;optimización&quot; o &quot;comprobación de estado&quot; del rendimiento a intervalos de 6 a 12 meses.

### Simular realidad {#simulate-reality}

![climage_1-4](assets/chlimage_1-4.jpeg)

Si se activa con un sitio web y se descubre después del lanzamiento que se ha encontrado con problemas de rendimiento, solo hay una razón para ello: Las pruebas de carga y rendimiento no simulan la realidad lo suficientemente de cerca.

Simular la realidad es difícil y el esfuerzo que usted querrá razonablemente invertir para ser &quot;real&quot; depende de la naturaleza de su proyecto. &quot;Real&quot; significa no sólo &quot;código real&quot; y &quot;tráfico real&quot;, sino también &quot;contenido real&quot;, especialmente con respecto al tamaño y la estructura del contenido. Tenga en cuenta que las plantillas pueden comportarse de manera completamente diferente según el tamaño y la estructura del repositorio.

### Establecer objetivos sólidos {#establish-solid-goals}

![climage_1-5](assets/chlimage_1-5.jpeg)

No hay que subestimar la importancia de establecer adecuadamente los objetivos de rendimiento. A menudo, una vez que las personas se centran en objetivos de rendimiento específicos, es muy difícil cambiar estos objetivos posteriormente, incluso si se basan en suposiciones irresponsables.

Establecer objetivos de rendimiento sólidos y buenos es una de las áreas más complicadas. A menudo es mejor recopilar registros de la vida real y puntos de referencia de un sitio web comparable (por ejemplo, el predecesor del nuevo sitio web).

### Permanecer relevante {#stay-relevant}

![climage_1-6](assets/chlimage_1-6.jpeg)

Es importante optimizar un cuello de botella a la vez. Si intenta hacer cosas en paralelo sin validar el impacto de una optimización, perderá el seguimiento de qué medida de optimización realmente ayudó.

### Ciclos de iteración ágiles {#agile-iteration-cycles}

![climage_1-7](assets/chlimage_1-7.jpeg)

El ajuste del rendimiento es un proceso iterativo que implica, mide, análisis, optimización y validación hasta que se alcance el objetivo. Para tener debidamente en cuenta este aspecto, implemente un proceso de validación ágil en la fase de optimización en lugar de un proceso de prueba de peso más intenso después de cada iteración.

Esto significa en gran medida que el desarrollador que implementa la optimización debe tener una manera rápida de saber si la optimización ya ha alcanzado el objetivo. Esta información es valiosa, ya que cuando se alcanza el objetivo, la optimización finaliza.

## Pautas de rendimiento básicas {#basic-performance-guidelines}

En general, mantenga las solicitudes HTML sin almacenar en caché a menos de 100 ms. Más concretamente, puede servir de guía lo siguiente:

* El 70% de las solicitudes de páginas deben responderse en menos de 100 ms.
* El 25% de las solicitudes de páginas debe obtener una respuesta en un plazo de 100 ms a 300 ms.
* El 4% de las solicitudes de páginas debe obtener una respuesta en un plazo de 300 ms a 500 ms.
* El 1% de las solicitudes de páginas debe obtener una respuesta en un plazo de 500 ms a 1000 ms.
* Ninguna página debe responder más lentamente que un segundo.

Los números anteriores asumen las siguientes condiciones:

* medido en la publicación (sin gastos generales relacionados con un entorno de creación)
* medida en el servidor (sin sobrecarga de red)
* no almacenado en caché (sin caché de salida CQ, sin caché de Dispatcher)
* solo para elementos complejos con muchas dependencias (HTML, JS, PDF, ...)
* no hay otra carga en el sistema

Hay una serie de problemas que con frecuencia contribuyen a los problemas de rendimiento. Estos giran principalmente en torno a:

* ineficiencia en la caché del despachante
* el uso de consultas en las plantillas de visualización normales.

El ajuste de nivel de JVM y SO no suele dar lugar a grandes saltos en el rendimiento y, por lo tanto, debe realizarse al final del ciclo de optimización.

La forma en que se estructura un repositorio de contenido también puede afectar al rendimiento. Para un mejor rendimiento, el número de nodos secundarios conectados a nodos individuales en un repositorio de contenido no debe superar los 1000 (como regla general).

Sus mejores amigos durante un ejercicio de optimización de rendimiento habitual son:

* el `request.log`
* temporización basada en componentes
* por último, pero no menos importante, un generador de perfiles de Java.

### Rendimiento al cargar y editar recursos digitales {#performance-when-loading-and-editing-digital-assets}

Debido al gran volumen de datos que implica cargar y editar recursos digitales, el rendimiento puede convertirse en un problema.

Dos cosas afectan al rendimiento aquí:

* CPU: varios núcleos permiten un trabajo más fluido al transcodificar
* Disco duro: los discos RAID paralelos logran lo mismo

Para mejorar el rendimiento, puede considerar lo siguiente:

* ¿Cuántos recursos se van a cargar al día? Una buena estimación puede basarse en:

![chlimage_1-77](assets/chlimage_1-77.png)

* Plazo en el que se harán las modificaciones (normalmente la duración de la jornada laboral, más para las operaciones internacionales).
* El tamaño medio de las imágenes cargadas (y el tamaño de las representaciones generadas por imagen) en megabytes.
* Determinar la velocidad de datos promedio:

![chlimage_1-78](assets/chlimage_1-78.png)

* El 80% de todas las ediciones se realizarán en el 20% del tiempo, por lo que en el tiempo pico tendrá 4 veces la tasa de datos promedio. Este es su objetivo de rendimiento.

## Monitoreo del performance {#performance-monitoring}

El rendimiento (o la falta de él) es una de las primeras cosas que los usuarios notan, por lo que, al igual que con cualquier aplicación con una interfaz de usuario, el rendimiento es de importancia clave. Para optimizar el rendimiento de la instalación de CQ, debe supervisar los distintos atributos de la instancia y su comportamiento.

Para obtener información sobre cómo realizar la supervisión del rendimiento, consulte [Rendimiento de monitoreo](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

Los problemas que causan problemas de rendimiento suelen ser difíciles de rastrear, incluso cuando sus efectos son fáciles de ver.

Un punto de partida básico es un buen conocimiento de su sistema cuando funciona de la manera normal. A menos que sepa cómo se &quot;ve&quot; y &quot;se comporta&quot; su entorno cuando se desempeña correctamente, puede resultar difícil localizar el problema cuando se deteriora el rendimiento. Esto significa que debe dedicar algún tiempo a investigar el sistema cuando se está ejecutando sin problemas y asegurarse de que la recopilación de información de rendimiento es una tarea constante. Esto le proporcionará una base para la comparación en caso de que el rendimiento sufra.

El diagrama siguiente ilustra la ruta que puede tomar una solicitud de contenido de CQ y, por lo tanto, el número de diferentes elementos que pueden afectar al rendimiento.

![chlimage_1-79](assets/chlimage_1-79.png)

El rendimiento también es un equilibrio entre volumen y capacidad:

**** VolumenCantidad de resultados que procesa y entrega el sistema.

**** CapacidadLa capacidad del sistema para entregar el volumen.

Esto se puede ilustrar en varias ubicaciones de la cadena web.

![chlimage_1-80](assets/chlimage_1-80.png)

Existen varias áreas funcionales que a menudo son responsables de impactar en el rendimiento:

* Almacenamiento en caché
* Código de aplicación (proyecto)
* Funcionalidad de búsqueda

### Reglas básicas sobre rendimiento {#basic-rules-regarding-performance}

Algunas reglas deben tenerse en cuenta al optimizar el rendimiento:

* El ajuste del rendimiento *debe* formar parte de cada proyecto.
* No optimice al principio del ciclo de desarrollo.
* El rendimiento es tan bueno como el vínculo más débil.
* Siempre piense en la capacidad frente al volumen.
* Optimice primero las cosas importantes.
* Nunca optimice sin *objetivos* realistas.

>[!NOTE]
>
>Tenga en cuenta que el mecanismo que utilice para medir el rendimiento a menudo afectará exactamente lo que intenta medir. Siempre debe intentar tener en cuenta estas discrepancias y eliminar el mayor efecto posible; en particular, los complementos de navegador deben desactivarse siempre que sea posible.

## Configuración para el rendimiento {#configuring-for-performance}

Determinados aspectos de CQ (y/o el CRX subyacente) se pueden configurar para optimizar el rendimiento. Las siguientes son posibilidades y sugerencias, debe asegurarse de si utiliza o no la funcionalidad en cuestión antes de realizar cambios.

>[!NOTE]
>
>Para obtener más información, consulte el [artículo de KB](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

### Indexación de búsqueda {#search-indexing}

A partir de AEM 6.0, Adobe Experience Manager utiliza una arquitectura de repositorio basada en Oak.

Puede encontrar la información de indexación actualizada aquí:

* [Prácticas recomendadas para Consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Consultas e indexación](/help/sites-deploying/queries-and-indexing.md)

### Procesamiento simultáneo de flujo de trabajo {#concurrent-workflow-processing}

Limite el número de procesos de flujo de trabajo que se ejecutan simultáneamente para mejorar el rendimiento. De forma predeterminada, el motor de flujos de trabajo procesa tantos flujos de trabajo en paralelo como hay procesadores disponibles para la VM de Java. Cuando los pasos del flujo de trabajo requieren grandes cantidades de recursos de procesamiento (RAM o CPU), la ejecución de varios de estos flujos de trabajo en paralelo puede generar grandes demandas en los recursos disponibles del servidor.

Por ejemplo, cuando se cargan imágenes (o recursos DAM en general), los flujos de trabajo importan automáticamente las imágenes a DAM. Las imágenes suelen ser de alta resolución y pueden consumir fácilmente cientos de MB de pila para su procesamiento. La administración de estas imágenes en paralelo coloca una carga alta en el subsistema de memoria y en el recolector de elementos no utilizados.

El motor de flujos de trabajo utiliza colas de trabajos de Apache Sling para gestionar y programar el procesamiento de elementos de trabajo. Los siguientes servicios de cola de trabajos se han creado de forma predeterminada desde la fábrica del servicio de configuración de cola de trabajos de Apache Sling para procesar los trabajos de flujo de trabajo:

* Cola de flujo de trabajo de granito: La mayoría de los pasos del flujo de trabajo, como los que procesan recursos DAM, utilizan el servicio de cola de flujo de trabajo de Granite.
* Cola de trabajos de proceso externo de Granite Workflow: Este servicio se utiliza para pasos especiales del flujo de trabajo externo que se utilizan normalmente para comunicarse con un sistema externo y realizar encuestas para obtener resultados. Por ejemplo, el paso Proceso de Extracción de medios de InDesign se implementa como un proceso externo. El motor de flujos de trabajo utiliza la cola externa para procesar la encuesta. (Consulte [com.day.cq.workflow.exec.WorkflowExternalProcess](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html)).

Configure estos servicios para limitar el número máximo de procesos de flujo de trabajo que se ejecutan simultáneamente.

**Nota:** La configuración de estas colas de trabajos afecta a todos los flujos de trabajo a menos que haya creado una cola de trabajos para un modelo de flujo de trabajo específico (consulte  [Configuración de la cola para un ](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) modelo de flujo de trabajo específico más abajo).

**Configuración en el repositorio**

Si está configurando los servicios [mediante un nodo sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository), debe encontrar el PID de los servicios existentes, por ejemplo: org.apache.sling.evento.job.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. Puede descubrir el PID mediante la consola web.

Debe configurar la propiedad denominada queue.maxparalelo.

**Configuración en la consola web**

Para configurar estos servicios [mediante la Consola Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), localice los elementos de configuración existentes debajo de la fábrica del servicio de configuración de cola de trabajos Apache Sling.

Debe configurar la propiedad denominada Número máximo de trabajos paralelos.

### Configurar la cola para un flujo de trabajo específico {#configure-the-queue-for-a-specific-workflow}

Cree una cola de trabajos para un modelo de flujo de trabajo específico para que pueda configurar la gestión de trabajos para ese modelo de flujo de trabajo. De este modo, las configuraciones afectan al procesamiento de un flujo de trabajo específico, mientras que la configuración de la cola de flujo de trabajo de Granite predeterminada controla el procesamiento de otros flujos de trabajo.

Cuando se ejecutan los modelos de flujo de trabajo, crean trabajos de Sling para un tema específico. De forma predeterminada, el tema coincide con los temas configurados para la cola general de flujo de trabajo de granito o la cola de trabajos de proceso externo de granito de flujo de trabajo:

* com/adobe/granite/workflow/job&amp;ast;
* com/adobe/granite/workflow/external/job&amp;ast;

Los temas de trabajo reales que generan los modelos de flujo de trabajo incluyen el sufijo específico del modelo. Por ejemplo, el modelo de flujo de trabajo [!UICONTROL Recurso de actualización de DAM] genera trabajos con el siguiente tema:

com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model

Por lo tanto, puede crear una cola de trabajos para el tema que coincida con los temas del trabajo del modelo de flujo de trabajo. La configuración de las propiedades relacionadas con el rendimiento de la cola afecta únicamente al modelo de flujo de trabajo que genera los trabajos que coinciden con el tema de la cola.

El siguiente procedimiento crea una cola de trabajos para un flujo de trabajo, utilizando como ejemplo el flujo de trabajo [!UICONTROL Recurso de actualización de DAM].

1. Ejecute el modelo de flujo de trabajo para el que desea crear la cola de trabajos, de modo que se generen estadísticas de temas. Por ejemplo, agregue una imagen a Assets para ejecutar el flujo de trabajo [!UICONTROL Recurso de actualización de DAM].
1. Abra la consola Trabajos de Sling. ([http://localhost:4502/system/console/slingevent](http://localhost:4502/system/console/slingevent))
1. Descubra los temas relacionados con el flujo de trabajo en la consola. Para DAM Update Asset, se encuentran los siguientes temas:

   * com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model

1. Cree una cola de trabajos para cada uno de estos temas. Para crear una cola de trabajos, cree una configuración de fábrica para el servicio de fábrica Apache Sling Job Queue.

   Las configuraciones de fábrica son similares a la cola Granite Workflow que se describe en [Procesamiento simultáneo de flujo de trabajo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing), excepto que la propiedad Topics coincide con el tema de los trabajos de flujo de trabajo.

### Servicio de sincronización de recursos DAM CQ5 {#cq-dam-asset-synchronization-service}

El `AssetSynchronizationService` se utiliza para sincronizar recursos de repositorios montados (incluidos LiveLink, Documentum, entre otros). De forma predeterminada, esto hace una comprobación periódica cada 300 segundos (5 minutos), por lo que si no utiliza repositorios montados, puede deshabilitar este servicio.

Esto se realiza [configurando el servicio OSGi](/help/sites-deploying/configuring-osgi.md) **Servicio de sincronización de recursos CQ DAM** para establecer el **período de sincronización** ( `scheduler.period`) en (un mínimo de) 1 año (definido en segundos).

### Varias instancias de DAM {#multiple-dam-instances}

La implementación de varias instancias de DAM puede ayudar al rendimiento cuando, por ejemplo:

* tiene una carga elevada debido a la carga regular de un gran número de recursos para el entorno de creación; aquí se puede dedicar una instancia de DAM independiente a la prestación de servicios al autor.
* tiene varios equipos en ubicaciones mundiales (por ejemplo, EE.UU., Europa, Asia).

Otras consideraciones son:

* separar &quot;trabajo en curso&quot; en el autor de &quot;final&quot; en la publicación
* separar los usuarios internos de los usuarios/visitantes externos en la publicación (por ejemplo, agentes, representantes de prensa, clientes, estudiantes, etc.).

## Prácticas recomendadas para garantizar la calidad {#best-practices-for-quality-assurance}

El rendimiento es muy importante para el entorno de publicación. Por lo tanto, debe planificar y analizar cuidadosamente las pruebas de rendimiento que realizará para el entorno de publicación durante la implementación del proyecto.

Esta sección tiene como objetivo proporcionar una visión general estandarizada de los problemas relacionados con la definición de un concepto de prueba específicamente para pruebas de rendimiento en el entorno *publish*. Esto es de interés primordial para los ingenieros de control de calidad, los directores de proyectos y los administradores de sistemas.

Lo siguiente abarca un enfoque estandarizado de las pruebas de rendimiento para una aplicación CQ en el entorno *Publish*. Esto incluye las cinco fases siguientes:

* [Verificación del conocimiento](#verification-of-knowledge)
* [Definición del ámbito de aplicación](#scope-definition)
* [Metodologías de prueba](#test-methodologies)
* [Definición de objetivos de rendimiento](#defining-the-performance-goals)
* [Optimización](#optimization)

El control es un proceso adicional y abarcador, necesario pero no limitado a las pruebas.

### Verificación del conocimiento {#verification-of-knowledge}

Un primer paso es el documento de la información básica que necesita conocer antes de poder realizar pruebas de inicio:

* la arquitectura de su entorno de prueba
* un mapa de la aplicación en el que se detallan los elementos internos que deberán someterse a pruebas (tanto aisladas como combinadas)

#### Arquitectura de prueba {#test-architecture}

Debe realizar un documento claro de la arquitectura del entorno de prueba que se utiliza para las pruebas de rendimiento.

Necesitará una reproducción del entorno de publicación de producción planificado, junto con Dispatcher y Load Balancer.

#### Mapa de aplicaciones {#application-map}

Para obtener una descripción general clara, puede crear un mapa de toda la aplicación (puede que lo tenga de las pruebas en el entorno de creación).

Una representación de diagrama de los elementos internos de la aplicación puede proporcionar una visión general de los requisitos de ensayo; con la codificación de color también puede servir de base para el sistema de informes.

### Definición de ámbito {#scope-definition}

Una aplicación generalmente tiene una selección de casos de uso. Algunos serán muy importantes, otros menos.

Para centrar el ámbito de las pruebas de rendimiento en la publicación, se recomienda definir los siguientes parámetros:

* casos de uso comercial más importantes
* casos de uso técnico más críticos

El número de casos de uso depende de usted, pero debe limitarse a un número fácilmente manejable (por ejemplo, entre 5 y 10).

Una vez seleccionados los casos de uso clave, los indicadores de rendimiento clave (KPI) y las herramientas utilizadas para medirlos se pueden definir para cada caso. Algunos ejemplos de KPI comunes son:

* Tiempo de respuesta de extremo a extremo
* Tiempo de respuesta del servlet
* Tiempo de respuesta para un solo componente
* Tiempo de respuesta para los servicios
* Número de subprocesos inactivos en el grupo de subprocesos
* Número de conexiones gratuitas
* Recursos del sistema como CPU y acceso a E/S

### Metodologías de prueba {#test-methodologies}

Este concepto tiene 4 escenarios utilizados para definir y probar los objetivos de rendimiento:

* Pruebas de un solo componente
* Pruebas de componentes combinadas
* *Viendo* el escenario
* Situaciones de error

Basado en los siguientes principios.

**Puntos de interrupción de componentes**

* Cada componente tiene un punto de interrupción específico cuando se relaciona con el rendimiento. Esto significa que un componente puede mostrar un buen rendimiento hasta que se llegue a un punto específico, tras lo cual el rendimiento se degradará rápidamente.
* Para obtener una descripción general completa de la aplicación, primero debe comprobar los componentes para determinar cuándo se alcanza el punto de interrupción de cada uno.
* Para encontrar el punto de interrupción, puede realizar una prueba de carga en la que, durante un período de tiempo, aumente el número de usuarios para crear una carga cada vez mayor. Al supervisar esta carga y la respuesta de los componentes, se encontrará con un comportamiento de rendimiento específico cuando se alcance el punto de interrupción del componente. El punto se puede calificar por el número de transacciones simultáneas por segundo, junto con el número de usuarios simultáneos (si el componente es sensible a este KPI).
* A continuación, esta información puede servir de referencia para las mejoras, indicar la eficacia de las medidas que se utilizan y ayudar a definir los escenarios de las pruebas.

**Transacciones**

* El término transacción se utiliza para representar la solicitud de una página web completa, incluida la propia página y todas las llamadas posteriores; es decir, la solicitud de página, cualquier llamada de AJAX, imágenes y otros objetos.**Solicitud de desglose**
* Para analizar completamente cada solicitud, puede representar cada elemento de la pila de llamadas y luego calcular el tiempo de procesamiento promedio de cada uno.

### Definición de Objetivos de Performance {#defining-the-performance-goals}

Una vez definido el ámbito y los KPI relacionados, se pueden establecer los objetivos de rendimiento específicos. Esto implica diseñar escenarios de prueba, junto con valores de destinatario.

Tendrá que probar el rendimiento en condiciones de media y pico. Además, necesitará pruebas de escenario de Going Live para asegurarse de que puede satisfacer el mayor interés en su sitio web cuando esté disponible por primera vez.

Cualquier experiencia o estadística que haya recopilado de un sitio web existente también puede ser útil para determinar objetivos futuros; por ejemplo, el tráfico principal del sitio web activo.

#### Pruebas de un solo componente {#single-component-tests}

Será necesario probar los componentes críticos, tanto en las condiciones medias como en las de mayor actividad.

En ambos casos, puede definir el número esperado de transacciones por segundo cuando un número predefinido de usuarios utiliza el sistema.

| Componente | Tipo de prueba | #Usuarios | Tx/s (esperado) | Tx/s (probado) | Descripción |
|---|---|---|---|---|---|
| Página principal de usuario único | Promedio | 1 | 1 |  |  |
|  | Pico | 1 | 3 |  |  |
| Página principal 100 usuarios | Promedio | 100 | 1 |  |  |
|  | Pico | 100 | 1 |  |

#### Pruebas de componentes combinadas {#combined-component-tests}

Al probar los componentes en combinación, se refleja mejor el comportamiento de las aplicaciones. De nuevo, deben probarse las condiciones medias y pico.

| Escenario | Componente | #Usuarios | Tx/s (esperado) | Tx/s (probado) | Descripción |
|---|---|---|---|---|---|
| Media mixta | Página principal | 10 | 1 |  |  |
|  | Búsqueda   | 10 | 1 |  |  |
|  | Noticias | 10 | 2 |  |  |
|  | Sucesos | 10 | 1 |  |  |
|  | Activaciones | 10 | 3 |  | Simulación del comportamiento del autor. |
| Pico mixto | Página principal | 100 | 5 |  |  |
|  | Búsqueda   | 50 | 5 |  |  |
|  | Noticias | 100 | 10 |  |  |
|  | Sucesos | 100 | 10 |  |  |
|  | Activaciones | 20 | 20 |  | Simulación del comportamiento del autor. |

#### Pruebas en directo {#going-live-tests}

Durante los primeros días después de que su sitio web esté disponible, puede esperar un mayor nivel de interés. Probablemente esto será incluso bueno con respecto a los valores máximos que ha estado probando. Se recomienda encarecidamente probar los escenarios de Going Live para asegurarse de que el sistema pueda ocuparse de esta situación.

| Escenario | Tipo de prueba | #Usuarios | Tx/s (esperado) | Tx/s (probado) | Descripción |
|---|---|---|---|---|---|
| Llegar al pico en directo | Página principal | 200 | 20 |  |  |
|  | Búsqueda   | 100 | 10 |  |  |
|  | Noticias | 200 | 20 |  |  |
|  | Sucesos | 200 | 20 |  |  |
|  | Activaciones | 20 | 20 |  | Simulación del comportamiento del autor. |

#### Pruebas del escenario de error {#error-scenario-tests}

Los escenarios de error también deben probarse para garantizar que el sistema reaccione correcta y adecuadamente. No sólo en la forma en que se gestiona el error, sino también en el impacto que puede tener en el rendimiento. Por ejemplo:

* qué sucede cuando el usuario intenta introducir un término de búsqueda no válido en el cuadro de búsqueda
* qué sucede cuando el término de búsqueda es tan general que devuelve un número excesivo de resultados

Al diseñar estas pruebas, hay que recordar que no todos los escenarios se producirán de manera regular. Sin embargo, su impacto en todo el sistema es importante.

| Escenario de error | Tipo de error | #Usuarios | Tx/s (esperado) | Tx/s (probado) | Descripción |
|---|---|---|---|---|---|
| Sobrecarga del componente de búsqueda | Buscar en comodín global (asterisco) | 10 | 1 |  | Sólo &amp;ast;&amp;ast;&amp;ast;;;; ast;; se buscan. |
|  | Palabra de detención | 20 | 2 |  | Buscando una palabra de parada. |
|  | Cadena vacía | 10 | 1 |  | Buscando una cadena vacía. |
|  | Caracteres especiales | 10 | 1 |  | Buscando caracteres especiales. |

#### Pruebas de resistencia {#endurance-tests}

Algunos problemas sólo se encontrarán después de que el sistema haya estado funcionando durante un período de tiempo continuo; sea eso horas o incluso días. Se utiliza una prueba de resistencia para probar una carga media constante durante un período de tiempo requerido. Se puede analizar cualquier degradación del rendimiento.

| Escenario | Tipo de prueba | #Usuarios | Tx/s (esperado) | Tx/s (probado) | Descripción |
|---|---|---|---|---|---|
| Ensayo de resistencia (72 horas) | Página principal | 10 | 1 |  |  |
|  | Búsqueda   | 10 | 1 |  |  |
|  | Noticias | 20 | 2 |  |  |
|  | Sucesos | 10 | 1 |  |  |
|  | Activaciones | 1 | 1 |  | Simulación del comportamiento del autor. |

### Optimización {#optimization}

En las etapas posteriores de la implementación necesitará optimizar la aplicación para cumplir/maximizar los objetivos de rendimiento.

Todas las optimizaciones realizadas deberán probarse para garantizar que:

* no afecta a la funcionalidad
* se verificó con las pruebas de carga antes de liberarse

Hay una selección de herramientas disponibles para ayudarle con la generación de carga, la supervisión del rendimiento y/o la análisis de resultados:

* [JMeter](https://jakarta.apache.org/jmeter/)
* [Cargar ejecutor](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)
* [](https://www.determyne.com/) DetermyneInsideApps
* [InfraRED](https://www.infraredsoftware.com/)
* [Perfil interactivo de Java](https://jiprof.sourceforge.net/)
* Muchas más...

Después de la optimización, tendrá que volver a realizar pruebas para confirmar el impacto.

### Informes {#reporting}

Se necesitarán sistemas de informes continuos para mantener a todos informados de la situación; como se mencionó anteriormente con la codificación de color, el mapa de arquitectura puede utilizarse para esto.

Una vez completadas todas las pruebas, debe informar sobre:

* cualquier error crítico encontrado
* cuestiones no críticas que seguirán siendo objeto de investigación
* cualquier suposición realizada durante las pruebas
* cualquier recomendación que surja de la prueba

## Optimización del rendimiento al utilizar Dispatcher {#optimizing-performance-when-using-the-dispatcher}

El [despachante](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) es la herramienta de almacenamiento en caché o equilibrio de carga del Adobe. Al utilizar Dispatcher, debe considerar la posibilidad de optimizar el rendimiento de la caché del sitio web.

>[!NOTE]
>
>Las versiones de Dispatcher son independientes de AEM, pero la documentación de Dispatcher está incrustada en la documentación de AEM. Utilice siempre la documentación de Dispatcher incrustada en la documentación para la versión más reciente de AEM.
>
>Es posible que se le haya redirigido a esta página si ha seguido un vínculo a la documentación de Dispatcher insertado en la documentación de una versión anterior de AEM.

Dispatcher oferta una serie de mecanismos integrados que puede utilizar para optimizar el rendimiento si el sitio web los aprovecha. Esta sección le explica cómo diseñar su sitio Web para maximizar los beneficios del almacenamiento en caché.

>[!NOTE]
>
>Puede ayudarle a recordar que Dispatcher almacena la caché en un servidor web estándar. Esto significa que:
>
>* puede almacenar en caché todo lo que pueda almacenar como página y solicitar mediante una dirección URL
>* no puede almacenar otras cosas, como cookies, datos de sesión y datos de formulario.

>
>
En general, muchas estrategias de almacenamiento en caché implican seleccionar buenas direcciones URL y no depender de estos datos adicionales.
>
>Con Dispatcher versión 4.1.11 también puede almacenar en caché los encabezados de respuesta; consulte [Almacenamiento en caché de encabezados de respuesta HTTP](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache).


### Cálculo de la proporción de caché de despachante {#calculating-the-dispatcher-cache-ratio}

La fórmula de relación de caché calcula el porcentaje de solicitudes que gestiona la memoria caché con respecto al número total de solicitudes que llegan al sistema. Para calcular la proporción de caché necesita lo siguiente:

* Número total de solicitudes. Esta información está disponible en Apache `access.log`. Para obtener más información, consulte la [documentación oficial de Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* El número de solicitudes que se han servido a la instancia de Publish. Esta información está disponible en el `request.log` de la instancia. Para obtener más información, consulte [Interpretación de request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) y [Búsqueda de los archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

La fórmula para calcular la proporción de caché es:

* (El número total de solicitudes **menos** el número de solicitudes en Publicar) **dividido** por el número total de solicitudes.

Por ejemplo, si el número total de solicitudes es 129491 y el número de solicitudes servidas por la instancia de publicación es 58959, la proporción de caché es: **(129491 - 58959)/129491= 54,5%**.

Si no tiene un par de uno a uno de publicador/despachante, deberá agregar solicitudes de todos los despachantes y editores juntos para obtener una medición precisa. Consulte también [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Para obtener el mejor rendimiento, Adobe recomienda una proporción de caché del 90 % al 95 %.

#### Uso de Codificación de Página Coherente {#using-consistent-page-encoding}

Con Dispatcher versión 4.1.11 puede almacenar en caché los encabezados de respuesta. Si no está almacenando encabezados de respuesta en caché en Dispatcher, se pueden producir problemas si almacena información de codificación de página en el encabezado. En este caso, cuando Dispatcher envía una página desde la caché, se utiliza la codificación predeterminada del servidor web para la página. Existen dos formas de evitar este problema:

* Si solo utiliza una codificación, asegúrese de que la codificación utilizada en el servidor web sea la misma que la codificación predeterminada del sitio web AEM.
* Utilice una etiqueta `<META>` en la sección HTML `head` para establecer la codificación, como en el ejemplo siguiente:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Evitar parámetros de URL {#avoid-url-parameters}

Si es posible, evite los parámetros de URL para las páginas que desee almacenar en caché. Por ejemplo, si tiene una galería de imágenes, la siguiente URL nunca se almacena en caché (a menos que Dispatcher [esté configurado en consecuencia](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

Sin embargo, puede colocar estos parámetros en la dirección URL de la página, como se indica a continuación:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>Esta URL llama a la misma página y a la misma plantilla que Gallery.html. En la definición de plantilla, puede especificar qué secuencia de comandos procesa la página o puede utilizar la misma secuencia de comandos para todas las páginas.

#### Personalizar por dirección URL {#customize-by-url}

Si permite que los usuarios cambien el tamaño de fuente (o cualquier otra personalización del diseño), asegúrese de que las diferentes personalizaciones se reflejan en la dirección URL.

Por ejemplo, las cookies no se almacenan en caché, por lo que si almacena el tamaño de fuente en una cookie (o mecanismo similar), el tamaño de fuente no se conserva para la página en caché. Como resultado, Dispatcher devuelve documentos de cualquier tamaño de fuente al azar.

Si se incluye el tamaño de fuente en la URL como selector, se evita este problema:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>En la mayoría de los aspectos del diseño, también es posible utilizar hojas de estilo y/o secuencias de comandos del lado del cliente. Normalmente, funcionan muy bien con el almacenamiento en caché.
>
>Esto también es útil para una versión de impresión, donde puede utilizar una URL como: &quot;
>
>`www.myCompany.com/news/main.print.html`
>
>Al utilizar la secuencia de comandos de la definición de plantilla, puede especificar una secuencia de comandos independiente que procese las páginas de impresión.

#### Invalidación de archivos de imagen utilizados como títulos {#invalidating-image-files-used-as-titles}

Si procesa títulos de página u otro texto como imágenes, se recomienda almacenar los archivos para que se eliminen al actualizar el contenido de la página:

1. Coloque el archivo de imagen en la misma carpeta que la página.
1. Utilice el siguiente formato de nombre para el archivo de imagen:

   `<page file name>.<image file name>`

Por ejemplo, puede almacenar el título de la página myPage.html en el archivo myPage.title.gif. Este archivo se elimina automáticamente si se actualiza la página, por lo que cualquier cambio en el título de la página se refleja automáticamente en la caché.

>[!NOTE]
>
>El archivo de imagen no existe necesariamente físicamente en la instancia de AEM. Puede utilizar una secuencia de comandos que cree dinámicamente el archivo de imagen. A continuación, Dispatcher almacena el archivo en el servidor web.

#### Invalidación de archivos de imagen utilizados para la navegación {#invalidating-image-files-used-for-navigation}

Si utiliza imágenes para las entradas de navegación, el método es básicamente el mismo que con los títulos, un poco más complejo. Almacene todas las imágenes de navegación con las páginas de destinatario. Si utiliza dos imágenes para normal y activo, puede utilizar los siguientes scripts:

* Secuencia de comandos que muestra la página, como de costumbre.
* Una secuencia de comandos que procesa solicitudes &quot;.normal&quot; y devuelve la imagen normal.
* Una secuencia de comandos que procesa solicitudes &quot;.active&quot; y devuelve la imagen activada.

Es importante crear estas imágenes con el mismo nombre que la página para asegurarse de que una actualización de contenido elimina estas imágenes, así como la página.

En el caso de las páginas que no se modifican, las imágenes permanecen en la caché, aunque las páginas mismas suelen invalidarse automáticamente.

#### Personalización {#personalization}

El despachante no puede almacenar en caché datos personalizados, por lo que se recomienda limitar la personalización a donde sea necesaria. Para ilustrar por qué:

* Si utiliza una página de inicio personalizable libremente, esa página debe estar compuesta cada vez que un usuario la solicite.
* Si, por el contrario, oferta una selección de 10 páginas de inicio diferentes, puede almacenar en caché cada una de ellas, lo que mejora el rendimiento.

>[!NOTE]
>
>Si personaliza cada página (por ejemplo, colocando el nombre del usuario en la barra de título), no podrá almacenarla en caché, lo que puede causar un gran impacto en el rendimiento.
>
>Sin embargo, si tiene que hacer esto, puede:
>
>* utilice iFrames para dividir la página en una parte que sea la misma para todos los usuarios y una parte que sea la misma para todas las páginas del usuario. A continuación, puede almacenar en caché ambas partes.
>* utilice JavaScript del lado del cliente para mostrar información personalizada. Sin embargo, debe asegurarse de que la página se siga mostrando correctamente si un usuario desactiva JavaScript.

>



#### Conexiones adhesivas {#sticky-connections}

[Conexión fija ](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#the-benefits-of-load-balancing) Asegúrese de que los documentos de un usuario están compuestos en el mismo servidor. Si un usuario abandona esta carpeta y luego regresa a ella, la conexión se mantendrá. Defina una carpeta para albergar todos los documentos que requieran conexiones adhesivas para el sitio web. Trata de no tener otros documentos. Esto afecta al equilibrio de carga si utiliza páginas personalizadas y datos de sesión.

#### Tipos MIME {#mime-types}

Existen dos maneras en que un explorador puede determinar el tipo de archivo:

1. Por su extensión (p. ej. .html, .gif, .jpg, etc.)
1. Por el tipo MIME que el servidor envía con el archivo.

Para la mayoría de los archivos, el tipo MIME está implícito en la extensión del archivo. i.e.:

1. Por su extensión (p. ej. .html, .gif, .jpg, etc.)
1. Por el tipo MIME que el servidor envía con el archivo.

Si el nombre del archivo no tiene extensión, se muestra como texto sin formato.

Con Dispatcher versión 4.1.11 puede almacenar en caché los encabezados de respuesta. Si no almacena en caché los encabezados de respuesta en Dispatcher, tenga en cuenta que el tipo MIME forma parte del encabezado HTTP. Por lo tanto, si la aplicación AEM devuelve archivos que no tienen un final de archivo reconocido y dependen del tipo MIME en su lugar, estos archivos pueden mostrarse incorrectamente.

Para asegurarse de que los archivos se almacenan correctamente en la caché, siga estas directrices:

* Asegúrese de que los archivos siempre tengan la extensión adecuada.
* Evite las secuencias de comandos genéricas del servidor de archivos, que tienen direcciones URL como download.jsp?file=2214. Vuelva a escribir la secuencia de comandos para utilizar las direcciones URL que contengan la especificación del archivo; para el ejemplo anterior, sería download.2214.pdf.

## Rendimiento de backup {#backup-performance}

Esta sección presenta una serie de pruebas de referencia utilizadas para evaluar el performance de los backups de CQ y los efectos de la actividad de backup en el performance de las aplicaciones. La copia de seguridad de CQ presenta una carga significativa en el sistema mientras se ejecuta, y la medimos, así como los efectos de la configuración de demora de copia de seguridad que intenta modular estos efectos. El objetivo es la oferta de algunos datos de referencia sobre el rendimiento esperado de los backups en configuraciones realistas y cantidades de datos de producción, así como proporcionar una guía sobre cómo calcular los tiempos de backup para los sistemas planificados.

### Entorno de referencia {#reference-environment}

#### Sistema físico {#physical-system}

Los resultados obtenidos en el presente documento se obtuvieron a partir de puntos de referencia ejecutados en un entorno de referencia con la siguiente configuración. Esta configuración está diseñada para ser similar a un entorno de producción típico en un centro de datos:

* H-P ProLiant DL380 G6, 8 CPUs x 2,533 GHz
* Unidades SCSI serial de 300 GB a 10.000 RPM
* Controlador RAID de hardware; 8 unidades en una matriz RAID 0+5
* CPU de imagen VMware x 2 Intel Xeon E5540 a 2,53 GHz
* RedHat Linux 2.6.18-194.el5; Java 1.6.0_29
* Instancia de Single Author que ejecuta CQ 5.5 GM.

El subsistema de disco de este servidor es bastante rápido, representativo de una configuración RAID de alto rendimiento que podría utilizarse en un servidor de producción. El rendimiento del backup puede ser sensible al rendimiento del disco y los resultados de este entorno reflejan el rendimiento en una configuración RAID muy rápida. La imagen VMWare está configurada para tener un solo volumen de disco grande que reside físicamente en el almacenamiento de disco local, en el arreglo RAID.

La configuración de CQ coloca el repositorio y el almacén de datos en el mismo volumen lógico, junto con todo el sistema operativo y el software de CQ. El directorio destinatario para copias de seguridad también reside en este sistema de archivos lógico.

#### Volúmenes de datos {#data-volumes}

La siguiente tabla ilustra el tamaño de los volúmenes de datos que se utilizan en los análisis de rendimiento de backup. El contenido de la línea base inicial se instala primero y, a continuación, se añaden cantidades conocidas adicionales de datos para aumentar el tamaño del contenido del que se realiza una copia de seguridad. Las copias de seguridad se crearán en incrementos específicos para representar un gran aumento del contenido y lo que se puede producir en un día. La distribución del contenido (páginas, imágenes, etiquetas) se basará en términos generales en una composición de recursos de producción realista. Las páginas, imágenes y etiquetas estarán limitadas a un máximo de 800 páginas secundarias. Cada página incluirá los componentes de título, Flash, texto/imagen, vídeo, proyección de diapositivas, formulario, tabla, nube y carrusel. Las imágenes se cargarán desde un grupo de 400 archivos únicos de un tamaño de 37 kB a 594 kB.

<table>
 <tbody>
  <tr>
   <td><strong>Contenido</strong></td>
   <td><strong>Nodos</strong></td>
   <td><strong>Páginas</strong></td>
   <td><strong>Imágenes</strong></td>
   <td><strong>Etiquetas</strong></td>
  </tr>
  <tr>
   <td>Instalación básica</td>
   <td>69.610</td>
   <td>562</td>
   <td>256</td>
   <td>237</td>
  </tr>
  <tr>
   <td>Contenido pequeño para backup incremental</td>
   <td><br type="_moz" /> </td>
   <td>+100</td>
   <td>+2</td>
   <td>+2</td>
  </tr>
  <tr>
   <td>Gran contenido para copia de seguridad completa</td>
   <td><br type="_moz" /> </td>
   <td>+10.000</td>
   <td>+100</td>
   <td>+100</td>
  </tr>
 </tbody>
</table>

El parámetro de referencia de copia de seguridad se repite con los conjuntos de contenido adicionales agregados en cada repetición.

#### Comparar escenarios {#benchmark-scenarios}

Los análisis de rendimiento de backup cubren dos escenarios principales: realiza copias de seguridad cuando el sistema se encuentra bajo una carga de aplicación significativa y realiza copias de seguridad cuando el sistema está inactivo. Aunque la recomendación general es que las copias de seguridad se realicen cuando el sistema CQ esté tan inactivo como sea posible, existen situaciones en las que es necesario que la copia de seguridad se ejecute cuando el sistema está bajo carga.

**Las Copias de seguridad de** estado inactivo se realizan sin ninguna otra actividad en CQ.

**En** LoadBackups se realizan mientras el sistema tiene una carga inferior al 80 % de los procesos en línea. El retraso de la copia de seguridad varió para ver el impacto en la carga.

Los tiempos de copia de seguridad y el tamaño del backup resultante se obtienen de los registros del servidor de CQ. Normalmente, se recomienda que los backups se programen para tiempos de inactividad cuando CQ esté inactivo, como en mitad de la noche. Este escenario es representativo del enfoque recomendado.

La carga consistirá en creaciones/eliminaciones de página, recorridos y consultas, con la mayoría de la carga proveniente de las consultas y los recorridos de página. Añadir y eliminar demasiadas páginas aumenta continuamente el tamaño del espacio de trabajo e impide que las copias de seguridad se completen. La distribución de la carga que utilizará la secuencia de comandos es del 75 % de las conversiones de página, del 24 % de las consultas y del 1 % de las creaciones de página (nivel único sin subpáginas anidadas). Las transacciones medias máximas por segundo en un sistema inactivo se alcanzan con 4 subprocesos simultáneos, que es lo que se utilizará al probar las copias de seguridad en carga.

El impacto de la carga en el performance del backup se puede estimar por la diferencia entre el performance con y sin esta carga de la aplicación. El impacto del backup en el rendimiento de las aplicaciones se encuentra comparando el rendimiento del escenario en transacciones por hora con y sin un backup simultáneo en curso, y con backups que funcionan con diferentes configuraciones de &quot;retraso de backup&quot;.

**Configuración de retrasoPara varios de los escenarios también variamos la configuración de demora de copia de seguridad, utilizando valores de 10 ms (predeterminado), 1 ms y 0 ms, para explorar cómo esta configuración afectó el rendimiento de las copias de seguridad.** 

**Tipo de** copia de seguridadTodas las copias de seguridad eran copias de seguridad externas del repositorio realizadas en un directorio de copia de seguridad sin crear un archivo comprimido, excepto en un caso para la comparación en el que el comando tar se utilizó directamente. Dado que las copias de seguridad incrementales no se pueden crear en un archivo zip, o cuando la copia de seguridad completa previa es un archivo zip, el método de directorio de copia de seguridad es el más utilizado en situaciones de producción.

### Resumen de los resultados {#summary-of-results}

#### Tiempo de Backup y Resolución de Problemas {#backup-time-and-troughput}

El principal resultado de estos análisis de rendimiento es mostrar cómo varían los tiempos de backup en función del tipo de backup y la cantidad total de datos. El siguiente gráfico muestra el tiempo de copia de seguridad obtenido mediante la configuración de copia de seguridad predeterminada, en función del número total de páginas.

![chlimage_1-81](assets/chlimage_1-81.png)

Los tiempos de backup en una instancia inactiva son bastante coherentes, con un promedio de 0,608 MB/s independientemente de los backups completos o incrementales (ver gráfico a continuación). El tiempo de backup es simplemente una función de la cantidad de datos a los que se hace backup. El tiempo para completar una copia de seguridad completa aumenta claramente con el número total de páginas. El tiempo para completar una copia de seguridad incremental también aumenta con el número total de páginas, pero a una velocidad mucho menor. El tiempo que se tarda en completar el backup incremental es mucho menor debido a la cantidad relativamente pequeña de datos de los que se hace backup.

El tamaño de la copia de seguridad producida es el principal determinante del tiempo que se tarda en completar una copia de seguridad. El siguiente gráfico muestra el tiempo que se tarda en función del tamaño final de la copia de seguridad.

![chlimage_1-82](assets/chlimage_1-82.png)

Este gráfico ilustra que tanto los backups incrementales como los completos siguen un patrón de tamaño y tiempo simple que podemos medir como rendimiento. Los tiempos de backup en una instancia inactiva son bastante coherentes, con un promedio de 0,61 MB/s independientemente de los backups completos o incrementales en el entorno de referencia.

#### Retraso de copia de seguridad {#backup-delay}

El parámetro de demora de copia de seguridad se proporciona para limitar la medida en que los backups pueden interferir con las cargas de trabajo de producción. El parámetro especifica un tiempo de espera en milisegundos, que se intercala en la operación de copia de seguridad archivo por archivo. El efecto global depende en parte del tamaño de los archivos afectados. La medición del performance de backup en MB/seg ofrece una manera razonable de comparar los efectos del retraso en el backup.

* La ejecución simultánea de un backup con carga regular de aplicaciones tendrá un impacto negativo en el rendimiento de la carga regular.
* El impacto puede ser ligero —hasta un 5%— o muy significativo— causando hasta un 75% de caída en el rendimiento, y esto probablemente depende más de la aplicación que de cualquier otra cosa.
* El backup no es una carga pesada en la CPU, por lo que las cargas de trabajo de producción intensivas en CPU se verían menos afectadas por el backup que las que requieren mucho uso de E/S.

![chlimage_1-83](assets/chlimage_1-83.png)

Para comparar el rendimiento obtenido usando un backup del filesystem (usando &#39;tar&#39;) para hacer backup de los mismos archivos del repositorio. El rendimiento del tar es comparable, pero ligeramente superior al del backup con el retraso establecido en cero. La configuración de incluso un pequeño retraso reduce en gran medida el rendimiento de backup y el retraso predeterminado de 10 ms da como resultado un rendimiento mucho menor. En situaciones en las que las copias de seguridad pueden programarse cuando el uso general de la aplicación es muy bajo o la aplicación puede estar completamente inactiva, probablemente sea conveniente reducir el retraso por debajo del valor predeterminado para permitir que la copia de seguridad se realice más rápidamente.

El impacto real del rendimiento de las aplicaciones de un backup en curso depende de los detalles de la infraestructura y la aplicación. La elección del valor de retraso debe realizarse por análisis empírica de la aplicación, pero debe elegirse lo más pequeño posible, de modo que las copias de seguridad puedan completarse lo más rápido posible. Dado que sólo existe una correlación débil entre la elección del valor de retraso y el impacto en el rendimiento de la aplicación, la elección del retraso debería favorecer tiempos de backup generales más cortos, a fin de minimizar el impacto general de los backups. Un backup que tarda 8 horas en completarse, pero que afecta al rendimiento en -20%, probablemente tendrá un bueno impacto total que uno que tarde 2 horas en completarse pero afecta al rendimiento en -30%.

### Referencias {#references}

* [Administración: Backup y Restore](/help/sites-administering/backup-and-restore.md)
* [Administración: capacidad y volumen](/help/managing/best-practices-further-reference.md#capacity-and-volume)

