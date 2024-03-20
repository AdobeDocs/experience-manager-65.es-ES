---
title: Directrices de tamaño de hardware
description: AEM Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto de.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
solution: Experience Manager, Experience Manager 6.5
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '2833'
ht-degree: 0%

---

# Directrices de tamaño de hardware{#hardware-sizing-guidelines}

AEM Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto de. Las estimaciones de tamaño dependen de la arquitectura del proyecto, la complejidad de la solución, el tráfico esperado y los requisitos del proyecto. Esta guía le ayuda a determinar las necesidades de hardware para una solución específica, o a encontrar una estimación superior e inferior para los requisitos de hardware.

Los factores básicos a considerar son (en este orden):

* **Velocidad de red**

   * Latencia de red
   * Ancho de banda disponible

* **Velocidad de cómputo**

   * Eficiencia del almacenamiento en caché
   * Tráfico esperado
   * Complejidad de plantillas, aplicaciones y componentes
   * Autores simultáneos
   * Complejidad de la operación de creación (edición de contenido simple, despliegue de MSM, etc.)

* **Rendimiento de E/S**

   * Rendimiento y eficacia del almacenamiento de archivos o bases de datos

* **Disco duro**

   * al menos dos o tres veces más grande que el tamaño del repositorio

* **Memoria**

   * Tamaño del sitio web (número de objeto de contenido, páginas y usuarios)
   * Número de usuarios/sesiones activos al mismo tiempo

## Arquitectura {#architecture}

AEM Una configuración típica de la consiste en un autor y un entorno de publicación. Estos entornos tienen diferentes requisitos con respecto al tamaño del hardware subyacente y a la configuración del sistema. Las consideraciones detalladas para ambos entornos se describen en la sección [entorno de creación](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) y [entorno de publicación](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) secciones.

En una configuración de proyecto típica, tiene varios entornos en los que almacenar en zona intermedia las fases del proyecto:

* **Entorno de desarrollo**
Para desarrollar nuevas funciones o realizar cambios significativos. La práctica recomendada es trabajar con un entorno de desarrollo por desarrollador (instalaciones locales en sus sistemas personales).

* **Entorno de prueba del autor**
Para comprobar los cambios. El número de entornos de prueba puede variar según los requisitos del proyecto (por ejemplo, pruebas de control de calidad independientes, pruebas de integración o pruebas de aceptación de usuarios).

* **Entorno de prueba de publicación**
Principalmente para probar casos de uso de colaboración social o la interacción entre el autor y varias instancias de publicación.

* **Entorno de producción del autor**
Para que los autores editen el contenido.

* **Entorno de producción de publicación**
Para servir contenido publicado.

AEM Además, los entornos pueden variar, desde un sistema de un solo servidor que ejecuta el servidor de aplicaciones y un servidor de aplicaciones, hasta un conjunto de gran escala de instancias agrupadas de varios servidores y varias CPU. El Adobe recomienda que utilice un equipo independiente para cada sistema de producción y que no ejecute otras aplicaciones en estos equipos.

## Consideraciones genéricas de tamaño de hardware {#generic-hardware-sizing-considerations}

Las secciones siguientes proporcionan instrucciones sobre cómo calcular los requisitos de hardware, teniendo en cuenta diversas consideraciones. En el caso de los sistemas grandes, Adobe sugiere que realice un conjunto sencillo de pruebas de referencia internas en una configuración de referencia.

La optimización del rendimiento es una tarea fundamental que debe realizarse antes de poder realizar cualquier evaluación comparativa para un proyecto específico. Asegúrese de aplicar los consejos proporcionados en la [Documentación de optimización del rendimiento](/help/sites-deploying/configuring-performance.md) antes de realizar cualquier prueba de evaluación comparativa y utilizar sus resultados para cualquier cálculo de tamaño de hardware.

Los requisitos de tamaño de hardware para casos de uso avanzados deben basarse en una evaluación detallada del rendimiento del proyecto. Las características de los casos de uso avanzados que requieren recursos de hardware excepcionales incluyen combinaciones de:

* alto rendimiento/carga útil de contenido
* amplio uso de código personalizado, flujos de trabajo personalizados o bibliotecas de software de terceros
* integración con sistemas externos no compatibles

### Espacio en disco/ Disco duro {#disk-space-hard-drive}

El espacio en disco necesario depende en gran medida del volumen y del tipo de la aplicación web. Los cálculos deben tener en cuenta lo siguiente:

* la cantidad y el tamaño de las páginas, los recursos y otras entidades almacenadas en el repositorio, como flujos de trabajo, perfiles, etc.
* la frecuencia estimada de los cambios de contenido y, por lo tanto, la creación de versiones de contenido
* el volumen de representaciones de recursos DAM que se generarán
* el crecimiento general del contenido con el tiempo

El espacio en disco se supervisa continuamente durante la Limpieza de revisiones en línea y sin conexión. Si el espacio disponible en disco cae por debajo de un valor crítico, el proceso se cancela. El valor crítico es el 25 % del espacio en disco actual del repositorio y no se puede configurar. Adobe recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio, incluido el crecimiento estimado.

Considere una configuración de matrices redundantes de discos independientes (RAID, por ejemplo, RAID10) para la redundancia de datos.

>[!NOTE]
>
>El directorio temporal de una instancia de producción debe tener al menos 6 GB de espacio disponible.

#### Virtualización {#virtualization}

AEM El funcionamiento es correcto en entornos virtualizados, pero puede haber factores como la CPU o la E/S que no se pueden equiparar directamente con el hardware físico. Una recomendación es elegir una velocidad de E/S más alta (en general), ya que este es un factor crítico, por lo general. La evaluación comparativa de su entorno es necesaria para comprender con precisión qué recursos se requieren.

#### AEM Paralelización de instancias de {#parallelization-of-aem-instances}

**Seguridad contra fallos**

Un sitio web a prueba de fallos se implementa en al menos dos sistemas independientes. Si un sistema se avería, otro sistema puede asumir el control y así compensar el fallo del sistema.

**Adaptación de recursos del sistema**

Mientras todos los sistemas están en funcionamiento, se dispone de un mayor rendimiento informático. Ese rendimiento adicional no es necesariamente lineal con el número de nodos de clúster, ya que la relación depende en gran medida del entorno técnico. Consulte [Documentación de clúster](/help/sites-deploying/recommended-deploys.md) para obtener más información.

La estimación de cuántos nodos de clúster son necesarios se basa en los requisitos básicos y casos de uso específicos del proyecto web en particular:

* Desde la perspectiva de la seguridad contra fallos, es necesario determinar, para todos los entornos, el grado de importancia del fallo y el tiempo de compensación del fallo en función del tiempo que tarda un nodo de clúster en recuperarse.
* Para el aspecto de la escalabilidad, el número de operaciones de escritura es básicamente el factor más importante; consulte [Autores que trabajan en paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para el entorno de creación y [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) para el entorno de publicación. El equilibrio de carga se puede establecer para operaciones que acceden al sistema únicamente para procesar operaciones de lectura; consulte [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para obtener más información.

## Crear cálculos específicos del entorno {#author-environment-specific-calculations}

Para fines de evaluación comparativa, Adobe ha desarrollado algunas pruebas de referencia para instancias de autor independientes.

* **Prueba de referencia 1**
Calcule el rendimiento máximo de un perfil de carga en el que los usuarios realizan un ejercicio simple de creación de páginas sobre una carga base de 300 páginas existentes de naturaleza similar. Los pasos involucrados fueron iniciar sesión en el sitio, crear una página con un SWF e imagen/texto, añadir una nube de etiquetas y luego activar la página.

   * **Resultado**
El rendimiento máximo para un ejercicio simple de creación de página como el anterior (considerado como una transacción) se encuentra en 1730 transacciones/hora.

* **Prueba de referencia 2**
Calcule el rendimiento máximo cuando el perfil de carga tenga una combinación de creación de página nueva (10 %), modificación de una página existente (80 %) y creación y luego modificación de una página en sucesión (10 %). La complejidad de las páginas sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza añadiendo una imagen y modificando el contenido del texto. Una vez más, el ejercicio se realizó sobre una carga base de 300 páginas de la misma complejidad definida en la prueba de referencia 1.

   * **Resultado**
El rendimiento máximo para este escenario de operación mixta se encontró en 3252 transacciones por hora.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que se incluya una proporción fija de cada tipo de transacción en la carga de trabajo.

Las dos pruebas anteriores resaltan claramente que el rendimiento varía según el tipo de operación. Utilice las actividades de su entorno como base para cambiar el tamaño del sistema. Se obtiene un mejor rendimiento con acciones menos intensivas como modificar (que también es más común).

### Almacenamiento en caché {#caching}

En el entorno de creación, la eficacia del almacenamiento en caché suele ser mucho menor, ya que los cambios en el sitio web son más frecuentes y el contenido es muy interactivo y personalizado. AEM Con Dispatcher, puede almacenar en caché bibliotecas de, JavaScript, archivos CSS e imágenes de diseño. Esto acelera algunos aspectos del proceso de creación. La configuración del servidor web para que también establezca encabezados para el almacenamiento en caché del explorador en estos recursos, reduce el número de solicitudes HTTP y, por lo tanto, mejora la capacidad de respuesta del sistema según la experimentan los autores.

### Autores que trabajan en paralelo {#authors-working-in-parallel}

En el entorno de creación, el número de autores que trabajan en paralelo y la carga que sus interacciones añaden al sistema son los principales factores limitantes. Por lo tanto, Adobe recomienda escalar el sistema en función del rendimiento compartido de los datos.

Para estos escenarios, Adobe ejecutó pruebas de referencia en un clúster de dos nodos que no compartían nada de instancias de autor.

* **Ensayo de referencia 1a**
Con un clúster activo-activo de no compartir nada de 2 instancias de autor, calcule el rendimiento máximo con un perfil de carga en el que los usuarios realizan un ejercicio simple de creación de páginas sobre una carga base de 300 páginas existentes, todas de naturaleza similar.

   * **Resultado**
El rendimiento máximo para un ejercicio simple de creación de páginas, como el anterior (considerado como una transacción) se encuentra en 2016 transacciones/hora. Esto supone un aumento de aproximadamente el 16 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

* **Ensayo de referencia 2b**
Con un clúster activo-activo de no compartir nada de 2 instancias de autor, calcule el rendimiento máximo cuando el perfil de carga tenga una combinación de creación de páginas nuevas (10 %), modificación de una página existente (80 %) y creación y modificación de una página en sucesión (10 %). La complejidad de la página sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza añadiendo una imagen y modificando el contenido del texto. Una vez más, el ejercicio se realizó sobre una carga base de 300 páginas de complejidad igual a la definida en la prueba de referencia 1.

   * **Resultado**
El rendimiento máximo para este escenario de operación mixta se encontró en 6288 transacciones/hora. Esto supone un aumento de aproximadamente el 93 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que se incluya una proporción fija de cada tipo de transacción en la carga de trabajo.

AEM AEM Las dos pruebas anteriores resaltan claramente que las escalas de los autores que realizan operaciones básicas de edición con el lenguaje de la son buenas. AEM En general, el método de lectura es más eficaz para escalar las operaciones de lectura.

En un sitio web típico, la mayoría de los trabajos de creación se realizan durante la fase del proyecto. Después de que el sitio web se pone en marcha, el número de autores que trabajan en paralelo generalmente se hunde a un promedio más bajo (modo operativo).

Puede calcular el número de equipos (o CPU) necesarios para el entorno de creación de la siguiente manera:

`n = numberOfParallelAuthors / 30`

AEM Esta fórmula puede servir como guía general para escalar las CPU cuando los autores realizan operaciones básicas con el método de la. Supone que el sistema y la aplicación están optimizados. Sin embargo, la fórmula no será verdadera para funciones avanzadas como MSM o Assets (consulte las secciones siguientes).

Consulte también [Paralelización](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) y [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md).

### Hardware Recommendations {#hardware-recommendations}

Normalmente, puede utilizar el mismo hardware para el entorno de creación que se recomienda para el entorno de publicación. Normalmente, el tráfico del sitio web es menor en los sistemas de creación, pero la eficacia de la caché también es menor. Sin embargo, el factor fundamental aquí es el número de autores que trabajan en paralelo, junto con el tipo de acciones que se realizan al sistema. AEM AEM En general, la agrupación en clúster (del entorno de creación) es más eficaz para escalar las operaciones de lectura; en otras palabras, un clúster de creación en clúster se adapta mejor a los autores que realizan operaciones básicas de edición.

Las pruebas de referencia en el Adobe se realizaron utilizando el sistema operativo Red Hat® 5.5, que se ejecuta en una plataforma de hardware Hewlett-Packard ProLiant DL380 G5 con la siguiente configuración:

* Dos CPU Intel Xeon® X5450 de núcleo cuádruple a 3 GHz
* 8 GB de RAM
* Gigabit Ethernet Broadcom NetXtreme II BCM5708
* Controladora RAID HP Smart Array, caché de 256 MB
* Dos discos SAS de 146 GB a 10.000 rpm configurados como un conjunto de bandas RAID0
* SPEC CINT2006 La puntuación de la referencia de tarifa es de 110

AEM Las instancias de se ejecutaban con un tamaño de pila mínimo de 256 M, un tamaño de pila máximo de 1024 M.

## Publicar cálculos específicos del entorno {#publish-environment-specific-calculations}

### Eficiencia del almacenamiento en caché y tráfico {#caching-efficiency-and-traffic}

La eficacia de la caché es crucial para la velocidad del sitio web. AEM La siguiente tabla muestra cuántas páginas por segundo puede gestionar un sistema de optimizado mediante un proxy inverso, como Dispatcher:

| Proporción de caché | Páginas/s (pico) | Millones de páginas/día (promedio) |
|---|---|---|
| 100 % | 1000-2000 | 35-70 |
| 99 % | 910 | 32 |
| 95 % | 690 | 25 |
| 90 % | 520 | 18 |
| 60 % | 220 | 8 |
| 0 % | 100 | 3,5 |

>[!CAUTION]
>
>Descargo de responsabilidad: los números se basan en una configuración de hardware predeterminada y pueden variar según el hardware específico utilizado.

AEM La proporción de caché es el porcentaje de páginas que Dispatcher puede devolver sin tener que acceder a la caché de la aplicación de la manera de acceder a la página de la página de la aplicación AEM 100 % indica que Dispatcher responde a todas las solicitudes; 0 % significa que calcula todas las páginas, mientras que el valor de 0 % se calcula de manera que se calculan todas las páginas.

### Complejidad de las plantillas y aplicaciones {#complexity-of-templates-and-applications}

AEM Si utiliza plantillas complejas, necesita más tiempo para procesar una página. Las páginas tomadas de la caché de no se ven afectadas por esto, pero el tamaño de la página sigue siendo relevante teniendo en cuenta el tiempo de respuesta general. Procesar una página compleja puede tardar fácilmente diez veces más que procesar una página simple.

### Fórmula {#formula}

AEM Mediante la fórmula siguiente, puede calcular una estimación de la complejidad general de la solución de la solución de la que se ha obtenido la solución de la manera siguiente:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

En función de la complejidad, puede determinar el número de servidores (o núcleos de CPU) que necesita para el entorno de publicación de la siguiente manera:

`n = (traffic * complexity / 1000 ) * activations`

Las variables de la ecuación son las siguientes:

<table>
 <tbody>
  <tr>
   <td>tráfico</td>
   <td>El tráfico máximo esperado por segundo. Puede estimarlo como el número de visitas a la página por día, dividido entre 35 000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilice 1 para una aplicación simple, 2 para una aplicación compleja o un valor intermedio:</p>
    <ul>
     <li>1 - un sitio totalmente anónimo y orientado al contenido</li>
     <li>1.1: un sitio totalmente anónimo y orientado al contenido con personalización de cliente/destinatario</li>
     <li>1.5: un sitio orientado al contenido con secciones anónimas e iniciadas, personalización del lado del cliente/destinatario</li>
     <li>1.7: para un sitio orientado al contenido con secciones anónimas e iniciadas, personalización del lado del cliente/destinatario y contenido generado por el usuario</li>
     <li>2 - donde todo el sitio requiere inicio de sesión, con un amplio uso del contenido generado por el usuario y varias técnicas de personalización</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>El porcentaje de páginas que salen de la caché de Dispatcher. AEM Utilice 1 si todas las páginas proceden de la caché, o 0 si todas las páginas están calculadas por el método de la.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilice un valor entre 1 y 10 para indicar la complejidad de las plantillas. Los números más altos indican plantillas más complejas, utilizando el valor 1 para sitios con un promedio de 10 componentes por página, el valor 5 para un promedio de página de 40 componentes y 10 para un promedio de más de 100 componentes.</td>
  </tr>
  <tr>
   <td>activaciones</td>
   <td>Número de activaciones promedio (replicación de páginas y recursos de tamaño promedio desde el nivel de creación al de publicación) por hora dividido por x, donde x es el número de activaciones realizadas en un sistema sin efectos secundarios de rendimiento a otras tareas procesadas por el sistema. También puede predefinir un valor inicial pesimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

AEM Si tiene un sitio web más complejo, también necesita servidores web más potentes para que pueda responder a una solicitud en un tiempo aceptable.

* Complejidad inferior a 4:
   * 1024 MB de RAM JVM&#42;
   * CPU de bajo a medio rendimiento

* Complejidad de 4 a 8:
   * RAM JVM DE 2048 MB&#42;
   * CPU de rendimiento medio a alto

* Complejidad superior a 8:
   * 4096 MB de RAM JVM&#42;
   * CPU de alto a alto rendimiento

>[!NOTE]
>
>&#42; Reserve suficiente RAM para su sistema operativo además de la memoria necesaria para su JVM.

## Cálculos adicionales específicos de casos de uso {#additional-use-case-specific-calculations}

Además del cálculo para una aplicación web predeterminada, tenga en cuenta factores específicos para los siguientes casos de uso. Los valores calculados se añaden al cálculo predeterminado.

### Consideraciones específicas de los recursos {#assets-specific-considerations}

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de pila y configure el [!UICONTROL Recurso de actualización DAM] flujo de trabajo para utilizar [paquete Camera Raw](/help/assets/camera-raw.md) para la ingesta de imágenes sin procesar.

>[!NOTE]
>
Un mayor rendimiento de las imágenes significa que los recursos informáticos deben poder seguir el ritmo de E/S del sistema y a la inversa. Por ejemplo, si la importación de imágenes inicia flujos de trabajo, la carga de muchas imágenes a través de WebDAV podría provocar un registro de flujos de trabajo pendientes.
>
El uso de discos independientes para TarPM, almacén de datos e índice de búsqueda puede ayudar a optimizar el comportamiento de E/S del sistema (sin embargo, normalmente tiene sentido mantener el índice de búsqueda localmente).

>[!NOTE]
>
Consulte también la [Guía de rendimiento de Assets](/help/sites-deploying/assets-performance-sizing.md).

### Administrador de varios sitios {#multi-site-manager}

AEM El consumo de recursos al utilizar MSM en un entorno de creación depende en gran medida de los casos de uso específicos. Los factores básicos son:

* Número de Live-Copies
* Periodicidad de los despliegues
* Tamaño del árbol de contenido a desplegar
* Funcionalidad conectada de las acciones de despliegue

La prueba del caso de uso planificado con un extracto representativo del contenido puede ayudarle a comprender mejor el consumo de recursos. AEM Si extrapola los resultados con el rendimiento planificado, puede evaluar los recursos adicionales necesarios para el MSMs.

Además, tenga en cuenta los autores que trabajan en paralelo. AEM Percibirán efectos secundarios sobre el rendimiento si los casos de uso de MSM consumen más recursos de los planeados.

### Consideraciones de tamaño de AEM Communities {#aem-communities-sizing-considerations}

AEM Los sitios de que incluyen funciones de AEM Communities (sitios de la comunidad) experimentan un alto nivel de interacción por parte de los visitantes del sitio (miembros) en el entorno de publicación.

Las consideraciones de tamaño para un sitio de comunidad dependen de la interacción anticipada por los miembros de la comunidad y de si el rendimiento óptimo del contenido de la página es de mayor importancia.

El contenido generado por el usuario (UGC) de los miembros enviados se almacena por separado del contenido de la página. AEM Aunque la plataforma de la utiliza un almacén de nodos que replica el contenido del sitio desde el autor hasta la publicación, AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para el almacén de UGC, es necesario elegir un proveedor de recursos de almacenamiento (SRP), que influya en la implementación elegida.
Consulte

* [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md)
* [Topologías recomendadas para comunidades](/help/communities/topologies.md)
