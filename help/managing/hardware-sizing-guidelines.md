---
title: 'Pautas para configurar el tamaño del hardware '
seo-title: 'Pautas para configurar el tamaño del hardware '
description: Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto de AEM.
seo-description: Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto de AEM.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Pautas para configurar el tamaño del hardware{#hardware-sizing-guidelines} 

Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto de AEM. Las estimaciones de tamaño dependen de la arquitectura del proyecto, la complejidad de la solución, el tráfico previsto y los requisitos del proyecto. Esta guía le ayuda a determinar las necesidades de hardware para una solución específica o a encontrar una estimación superior e inferior de los requisitos de hardware.

Los factores básicos a tener en cuenta son (en este orden):

* **Velocidad de red**

   * Latencia de red
   * Ancho de banda disponible

* **Velocidad computacional**

   * Eficacia de almacenamiento en caché
   * Tráfico previsto
   * Complejidad de plantillas, aplicaciones y componentes
   * Autores simultáneos
   * Complejidad de la operación de creación (edición de contenido simple, implementación de MSM, etc.)

* **Rendimiento de E/S**

   * Rendimiento y eficiencia del almacenamiento de archivos o bases de datos

* **Disco duro**

   * al menos dos o tres veces más grande que el tamaño del repositorio

* **Memoria**

   * Tamaño del sitio web (número de objetos de contenido, páginas y usuarios)
   * Número de usuarios/sesiones que están activos al mismo tiempo

## Arquitectura {#architecture}

Una configuración típica de AEM consiste en un autor y un entorno de publicación. Estos entornos tienen diferentes requisitos con respecto al tamaño de hardware subyacente y la configuración del sistema. Las consideraciones detalladas para ambos entornos se describen en las secciones Entorno [de](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) creación y Entorno [de](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) publicación.

En una configuración de proyecto típica, tiene varios entornos en los que realizar la etapa de proyecto:

* **Entorno** de desarrollo Desarrollar nuevas características o realizar cambios significativos. Lo mejor es trabajar con un entorno de desarrollo por desarrollador (generalmente instalaciones locales en sus sistemas personales).

* **Entorno** de prueba de creación Para comprobar los cambios. El número de entornos de prueba puede variar en función de los requisitos del proyecto (por ejemplo, por separado para control de calidad, pruebas de integración o pruebas de aceptación del usuario).

* **Entorno** de prueba de publicación principalmente para probar casos de uso de colaboración social o la interacción entre el autor y varias instancias de publicación.

* **Entorno** de producción de creaciónPara que los autores editen contenido.

* **Entorno** de producción de publicaciónPara ofrecer contenido publicado.

Además, los entornos pueden variar, desde un sistema de un solo servidor que ejecuta AEM y un servidor de aplicaciones, hasta un conjunto de instancias agrupadas de varios servidores y varias CPU de gran escala. Le recomendamos que utilice un equipo independiente para cada sistema de producción y que no ejecute otras aplicaciones en estos equipos.

## Consideraciones genéricas sobre el tamaño del hardware {#generic-hardware-sizing-considerations}

En las secciones que figuran a continuación se proporciona orientación sobre cómo calcular los requisitos de hardware, teniendo en cuenta diversas consideraciones. Para sistemas grandes, le sugerimos que realice un sencillo conjunto de pruebas de referencia internas en una configuración de referencia.

La optimización del rendimiento es una tarea fundamental que debe realizarse antes de poder realizar cualquier referencia para un proyecto específico. Asegúrese de aplicar los consejos proporcionados en la documentación [de Optimización de](/help/sites-deploying/configuring-performance.md) rendimiento antes de realizar pruebas de referencia y utilizar sus resultados para cualquier cálculo de tamaño de hardware.

Los requisitos de tamaño de hardware para casos de uso avanzados deben basarse en una evaluación detallada del rendimiento del proyecto. Las características de los casos de uso avanzado que requieren recursos de hardware excepcionales incluyen combinaciones de:

* carga útil y rendimiento de alto contenido
* uso extensivo de código personalizado, flujos de trabajo personalizados o bibliotecas de software de terceros
* integración con sistemas externos no admitidos

### Espacio en disco/Disco duro {#disk-space-hard-drive}

El espacio en disco necesario depende en gran medida del volumen y el tipo de la aplicación web. Los cálculos deben tener en cuenta:

* la cantidad y el tamaño de las páginas, los recursos y otras entidades almacenadas en el repositorio, como flujos de trabajo, perfiles, etc.
* la frecuencia estimada de los cambios de contenido y, por tanto, la creación de versiones de contenido
* volumen de las representaciones de recursos DAM que se generarán
* el crecimiento global del contenido a lo largo del tiempo

El espacio en disco se monitorea continuamente durante la limpieza de revisión en línea y sin conexión. Si el espacio disponible en disco cae por debajo de un valor crítico, el proceso se cancelará. El valor crítico es el 25% del espacio de disco actual del repositorio y no se puede configurar. Se recomienda ajustar el tamaño del disco al menos dos o tres veces más grande que el tamaño del repositorio, incluido el crecimiento estimado.

Considere una configuración de arreglos redundantes de discos independientes (RAID, por ejemplo, RAID 10) para la redundancia de datos.

>[!NOTE]
>
>El directorio temporal de una instancia de producción debe tener al menos 6 GB de espacio disponible.

#### Virtualización {#virtualization}

AEM funciona bien en entornos virtualizados, pero puede haber factores como CPU o E/S que no se pueden equiparar directamente con hardware físico. Una recomendación es elegir una velocidad de E/S más alta (en general) ya que esto es un factor crítico en la mayoría de los casos. La evaluación comparativa de su entorno es necesaria para comprender con precisión qué recursos se necesitarán.

#### Paralelización de instancias de AEM {#parallelization-of-aem-instances}

**Error de seguridad**

Se implementa un sitio web seguro contra fallos en al menos dos sistemas independientes. Si un sistema se desglosa, otro sistema puede tomar el control y así compensar la falla del sistema.

**Capacidad de ampliación de los recursos del sistema**

Aunque todos los sistemas están en funcionamiento, hay un mayor rendimiento computacional disponible. Que el rendimiento adicional no es necesariamente lineal con el número de nodos de clúster, ya que la relación depende en gran medida del entorno técnico; consulte la documentación [del](/help/sites-deploying/recommended-deploys.md) clúster para obtener más información.

La estimación de cuántos nodos de clúster son necesarios se basa en los requisitos básicos y casos de uso específicos del proyecto web en particular:

* Desde el punto de vista de la seguridad frente a fallos, es necesario determinar, para todos los entornos, la gravedad del fallo y el tiempo de compensación del fallo en función del tiempo que tarde en recuperarse un nodo de clúster.
* Para el aspecto de la escalabilidad, el número de operaciones de escritura es básicamente el factor más importante; consulte [Autores que trabajan en paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para el entorno de creación y Colaboración [](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) social para el entorno de publicación. Se puede establecer el equilibrio de carga para operaciones que accedan al sistema únicamente para procesar operaciones de lectura; consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para obtener más información.

## Crear cálculos específicos del entorno {#author-environment-specific-calculations}

Con fines de referencia, Adobe ha desarrollado algunas pruebas de referencia para instancias de creación independientes.

* **Prueba comparativa 1** Calcule el rendimiento máximo de un perfil de carga donde los usuarios realizan un simple ejercicio de creación de página sobre una carga base de 300 páginas existentes de naturaleza similar. Los pasos necesarios eran iniciar sesión en el sitio, crear una página con un SWF y una imagen o texto, agregar una nube de etiquetas y, a continuación, activar la página.

   * **Resultado** El rendimiento máximo para un ejercicio de creación de página simple como el anterior (considerado como una transacción) se encontró en 1730 transacciones/hora.

* **Prueba comparativa 2** Calcule el rendimiento máximo cuando el perfil de carga tiene una combinación de creación de página nueva (10%), modificación de una página existente (80%) y creación y posterior modificación de una página en sucesión (10%). La complejidad de las páginas sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza agregando una imagen y modificando el contenido del texto. De nuevo, el ejercicio se realizó sobre una carga base de 300 páginas de la misma complejidad definida en la prueba de referencia 1.

   * **Resultado** El rendimiento máximo para este escenario de operación de mezcla fue de 3252 transacciones por hora.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que se incluya una proporción fija de cada tipo de transacción en la carga de trabajo.

Las dos pruebas anteriores destacan claramente que el rendimiento varía según el tipo de operación. Utilice las actividades de su entorno como base para ajustar el tamaño del sistema. Obtendrá un mejor rendimiento con acciones menos intensivas como la modificación (que también es más común).

### Almacenamiento en caché {#caching}

En el entorno de creación, la eficacia de almacenamiento en caché suele ser mucho menor, ya que los cambios en el sitio web son más frecuentes y el contenido es muy interactivo y personalizado. Con el despachante, puede almacenar en caché bibliotecas de AEM, JavaScript, archivos CSS e imágenes de diseño. Esto acelera algunos aspectos del proceso de creación. Si configura el servidor web para que establezca además encabezados para el almacenamiento en caché del navegador en estos recursos, se reducirá el número de solicitudes HTTP y se mejorará la capacidad de respuesta del sistema según la experiencia de los autores.

### Autores que trabajan en paralelo {#authors-working-in-parallel}

En el entorno de creación, el número de autores que trabajan en paralelo y la carga que sus interacciones agregan al sistema son los principales factores limitantes. Por lo tanto, le recomendamos que escale su sistema en función del rendimiento compartido de los datos.

En estos casos, Adobe ejecutó pruebas de referencia en un clúster de instancias de autor de dos nodos compartido sin nada.

* **Prueba de referencia 1a** Con un clúster activo-activo-no compartido de 2 instancias de creación, calcule el rendimiento máximo con un perfil de carga en el que los usuarios realizan un simple ejercicio de creación de página sobre una carga base de 300 páginas existentes, todo de naturaleza similar.

   * **Resultado** El rendimiento máximo para un ejercicio de creación de página simple, como por ejemplo, anterior (considerado como una transacción), se encuentra en transacciones de 2016/hora. Se trata de un aumento de aproximadamente un 16 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

* **Prueba de referencia 2b** Con un clúster activo-activo-no compartido-nada de 2 instancias de autor, calcule el rendimiento máximo cuando el perfil de carga tenga una combinación de creación de página nueva (10%), modificación de páginas existentes (80%) y creación y modificación de una página en sucesión (10%). La complejidad de la página sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza agregando una imagen y modificando el contenido del texto. Nuevamente, el ejercicio se realizó sobre una carga base de 300 páginas de complejidad, tal como se define en la prueba de referencia 1.

   * **Resultado** El rendimiento máximo para este escenario de operación mixta fue de 6288 transacciones/hora. Se trata de un aumento de aproximadamente el 93 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que se incluya una proporción fija de cada tipo de transacción en la carga de trabajo.

Las dos pruebas anteriores resaltan claramente que AEM se escala bien para los autores que realizan operaciones básicas de edición con AEM. En general, AEM es más eficaz para escalar las operaciones de lectura.

En un sitio web típico, la mayoría de la creación se realiza durante la fase del proyecto. Después de que el sitio web se ponga en marcha, el número de autores que trabajan en paralelo suele reducirse a una media inferior (modo operativo).

Puede calcular el número de equipos (o CPU) necesarios para el entorno de creación de la siguiente manera:

`n = numberOfParallelAuthors / 30`

Esta fórmula puede servir como guía general para escalar CPU cuando los autores realizan operaciones básicas con AEM. Supone que el sistema y la aplicación están optimizados. Sin embargo, la fórmula no tendrá el valor true para características avanzadas como MSM o Recursos (consulte las secciones siguientes).

Consulte también los comentarios adicionales sobre [Paralelización](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) y Optimización [del rendimiento](/help/sites-deploying/configuring-performance.md).

### Recomendaciones de hardware {#hardware-recommendations}

Normalmente puede utilizar el mismo hardware para su entorno de creación que se recomienda para su entorno de publicación. Normalmente, el tráfico de sitios web es mucho menor en los sistemas de creación, pero la eficiencia de la caché también es menor. Sin embargo, el factor fundamental aquí es el número de autores que trabajan en paralelo, junto con el tipo de acciones que se están realizando en el sistema. En general, la agrupación en clústeres AEM (del entorno de creación) es más eficaz para escalar las operaciones de lectura; en otras palabras, un clúster de AEM se escala bien con los autores que realizan operaciones de edición básicas.

Las pruebas de referencia de Adobe se realizaron utilizando el sistema operativo RedHat 5.5, que se ejecuta en una plataforma de hardware Hewlett-Packard ProLiant DL380 G5 con la siguiente configuración:

* Dos CPU Intel Xeon X5450 de cuatro núcleos a 3,00 GHz
* 8 GB de RAM
* Gigabit Ethernet Broadcom NetXtreme II BCM5708
* Controladora RAID HP Smart Array, caché de 256 MB
* Dos discos SAS de 146 GB a 10.000 RPM configurados como un conjunto de bandas RAID 0
* SPEC CINT2006 La puntuación de referencia de tasa es 110

Las instancias de AEM se ejecutaban con un tamaño mínimo de pila de 256M, un tamaño máximo de pila de 1024M.

## Publicar cálculos específicos del entorno {#publish-environment-specific-calculations}

### Eficacia del almacenamiento en caché y tráfico {#caching-efficiency-and-traffic}

La eficacia de la caché es crucial para la velocidad del sitio web. La siguiente tabla muestra cuántas páginas por segundo puede gestionar un sistema AEM optimizado mediante un proxy inverso, como el despachante:

| Proporción de caché | Páginas/s (pico) | Millones de páginas por día (promedio) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Renuncia de responsabilidad: Los números se basan en una configuración de hardware predeterminada y pueden variar según el hardware específico utilizado.

La proporción de caché es el porcentaje de páginas que el distribuidor puede devolver sin tener que acceder a AEM. El 100 % indica que el distribuidor responde a todas las solicitudes; el 0 % significa que AEM calcula cada página.

### Complejidad de plantillas y aplicaciones {#complexity-of-templates-and-applications}

Si utiliza plantillas complejas, AEM necesitará más tiempo para procesar una página. Esto no afecta a las páginas tomadas de la caché, pero el tamaño de la página sigue siendo relevante cuando se considera el tiempo de respuesta general. El procesamiento de una página compleja puede tardar diez veces más que el procesamiento de una página simple.

### Fórmula {#formula}

Con la fórmula siguiente, puede calcular una estimación de la complejidad general de su solución de AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

En función de la complejidad, puede determinar el número de servidores (o núcleos de CPU) que necesita para el entorno de publicación de la siguiente manera:

`n = (traffic * complexity / 1000 ) * activations`

Las variables de la ecuación son las siguientes:

<table>
 <tbody>
  <tr>
   <td>tráfico</td>
   <td>El tráfico máximo esperado por segundo. Puede estimar esto como el número de visitas diarias a la página, dividido por 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilice 1 para una aplicación sencilla, 2 para una aplicación compleja o un valor intermedio:</p>
    <ul>
     <li>1: sitio completamente anónimo y orientado al contenido</li>
     <li>1.1: sitio completamente anónimo y orientado al contenido con personalización de cliente/destino</li>
     <li>1.5: un sitio orientado al contenido con secciones anónimas e iniciadas, personalización de cliente/Target</li>
     <li>1.7: para un sitio orientado al contenido con secciones anónimas e iniciadas, personalización de cliente/Target y contenido generado por el usuario</li>
     <li>2: donde todo el sitio requiere iniciar sesión, con un uso extensivo del contenido generado por el usuario y una variedad de técnicas de personalización</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>El porcentaje de páginas que salen de la caché del despachante. Utilice 1 si todas las páginas provienen de la caché o 0 si AEM calcula cada página.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilice un valor entre 1 y 10 para indicar la complejidad de las plantillas. Los números más altos indican plantillas más complejas, utilizando el valor 1 para sitios con un promedio de 10 componentes por página, el valor 5 para un promedio de página de 40 componentes y 10 para un promedio de más de 100 componentes.</td>
  </tr>
  <tr>
   <td>activations</td>
   <td>Número de activaciones promedio (replicación de páginas y recursos de tamaño medio del autor al nivel de publicación) por hora dividido por x, donde x es el número de activaciones realizadas en un sistema sin efectos secundarios de rendimiento para otras tareas procesadas por el sistema. También puede predefinir un valor inicial pesimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Si tiene un sitio web más complejo, también necesita servidores web más potentes para que AEM pueda responder a una solicitud en un momento aceptable.

* Complejidad por debajo de 4:
・ 1024 MB de RAM JVM* ・ CPU de bajo a mediano rendimiento

* Complejidad entre 4 y 8:
・ 2048 MB de RAM JVM* ・ CPU de medio a alto rendimiento

* Complejidad superior a 8:
・ 4096 MB de RAM JVM* ・ CPU de alto y alto rendimiento

>[!NOTE]
>
>* Reserva suficiente RAM para tu sistema operativo además de la memoria necesaria para tu JVM.

## Cálculos adicionales específicos de casos de uso {#additional-use-case-specific-calculations}

Además del cálculo para una aplicación Web predeterminada, es posible que deba considerar factores específicos para los siguientes casos de uso. Los valores calculados se añadirán al cálculo predeterminado.

### Consideraciones específicas de los recursos {#assets-specific-considerations}

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de pila y configure el flujo de trabajo de recursos de actualización de DAM para utilizar el paquete [de](/help/assets/camera-raw.md) Camera Raw para la ingestión de imágenes sin procesar.

>[!NOTE]
Un mayor rendimiento de las imágenes significa que los recursos informáticos deben ser capaces de mantener el ritmo de la E/S del sistema y viceversa. Por ejemplo, si los flujos de trabajo se inician mediante la importación de imágenes, la carga de muchas imágenes a través de WebDAV podría causar un retraso en los flujos de trabajo.
El uso de discos separados para TarPM, almacén de datos e índice de búsqueda puede ayudar a optimizar el comportamiento de E/S del sistema (sin embargo, generalmente tiene sentido mantener el índice de búsqueda localmente).

>[!NOTE]
Consulte también la Guía [de rendimiento de](/help/sites-deploying/assets-performance-sizing.md)recursos.

### Administrador de multisitio {#multi-site-manager}

El consumo de recursos al usar AEM MSM en un entorno de creación depende en gran medida de los casos de uso específicos. Los factores básicos son:

* Número de Live Copies
* Periodicidad de los lanzamientos
* Tamaño del árbol de contenido que se va a desplegar
* Funcionalidad conectada de las acciones de implementación

La prueba del caso de uso planificado con un fragmento de contenido representativo puede ayudarle a comprender mejor el consumo de recursos. Si extrapola los resultados con el rendimiento planificado, puede evaluar los recursos adicionales necesarios para el MSM de AEM.

Tenga en cuenta también que los autores que trabajen en paralelo percibirán efectos secundarios de rendimiento si los casos de uso de MSM de AEM consumen más recursos de los previstos.

### Consideraciones sobre el tamaño de Comunidades de AEM {#aem-communities-sizing-considerations}

Los sitios de AEM que incluyen funciones de comunidades de AEM (sitios de la comunidad) experimentan un alto nivel de interacción de los visitantes del sitio (miembros) en el entorno de publicación.

Las consideraciones de tamaño de un sitio de comunidad dependen de la interacción esperada de los miembros de la comunidad y de si el rendimiento óptimo del contenido de la página es de mayor importancia.

Los miembros del contenido generado por el usuario (UGC) enviados se almacenan por separado del contenido de la página. Aunque la plataforma AEM utiliza un almacén de nodos que replica el contenido del sitio de creación para publicación, AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para el almacén UGC, es necesario elegir un proveedor de recursos de almacenamiento (SRP), que influye en la implementación elegida.
Consulte

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md)
* [Topologías recomendadas para las comunidades](/help/communities/topologies.md)

