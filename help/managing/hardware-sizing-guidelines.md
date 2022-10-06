---
title: Pautas para configurar el tamaño del hardware
seo-title: Hardware Sizing Guidelines
description: Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto AEM.
seo-description: These sizing guidelines offer an approximation of the hardware resources required to deploy an AEM project.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2816'
ht-degree: 0%

---

# Pautas para configurar el tamaño del hardware {#hardware-sizing-guidelines}

Estas directrices de tamaño ofrecen una aproximación de los recursos de hardware necesarios para implementar un proyecto AEM. Las estimaciones de tamaño dependen de la arquitectura del proyecto, la complejidad de la solución, el tráfico esperado y los requisitos del proyecto. Esta guía le ayuda a determinar las necesidades de hardware para una solución específica, o a encontrar una estimación superior e inferior de los requisitos de hardware.

Los factores básicos a tener en cuenta son (en este orden):

* **Velocidad de red**

   * Latencia de red
   * Ancho de banda disponible

* **Velocidad de cómputo**

   * Eficiencia de almacenamiento en caché
   * Tráfico esperado
   * Complejidad de las plantillas, aplicaciones y componentes
   * Autores simultáneos
   * Complejidad de la operación de creación (edición simple de contenido, implementación de MSM, etc.)

* **Rendimiento de E/S**

   * Rendimiento y eficiencia del almacenamiento de archivos o bases de datos

* **Disco duro**

   * al menos dos o tres veces más grande que el tamaño del repositorio

* **Memoria**

   * Tamaño del sitio web (número de objetos de contenido, páginas y usuarios)
   * Número de usuarios/sesiones que están activas al mismo tiempo

## Arquitectura {#architecture}

Una configuración de AEM típica consta de un autor y un entorno de publicación. Estos entornos tienen diferentes requisitos con respecto al tamaño de hardware subyacente y la configuración del sistema. Las consideraciones detalladas para ambos entornos se describen en la sección [entorno de creación](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) y [entorno de publicación](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) secciones.

En una configuración de proyecto típica, tiene varios entornos en los que realizar la etapa de proyecto:

* **Entorno de desarrollo**
Para desarrollar nuevas funciones o realizar cambios significativos. Una práctica recomendada es trabajar con un entorno de desarrollo por desarrollador (normalmente instalaciones locales en sus sistemas personales).

* **Entorno de prueba de creación**
Para verificar los cambios. El número de entornos de prueba puede variar en función de los requisitos del proyecto (por ejemplo, por separado para el control de calidad, las pruebas de integración o las pruebas de aceptación del usuario).

* **Publicar entorno de prueba**
Principalmente para probar casos de uso de colaboración social o la interacción entre el autor y varias instancias de publicación.

* **Entorno de producción de creación**
Para que los autores editen el contenido.

* **Publicar entorno de producción**
Para mostrar contenido publicado.

Además, los entornos pueden variar, desde un sistema de un solo servidor que ejecute AEM y un servidor de aplicaciones, hasta un conjunto de instancias agrupadas de múltiples servidores y varias CPU a gran escala. Le recomendamos que utilice un equipo independiente para cada sistema de producción y que no ejecute otras aplicaciones en estos equipos.

## Consideraciones genéricas sobre el tamaño del hardware {#generic-hardware-sizing-considerations}

Las secciones siguientes proporcionan instrucciones sobre cómo calcular los requisitos de hardware, teniendo en cuenta diversas consideraciones. Para los sistemas grandes, le sugerimos que realice un sencillo conjunto de pruebas de referencia internas en una configuración de referencia.

La optimización del rendimiento es una tarea fundamental que debe realizarse antes de poder realizar cualquier prueba comparativa para un proyecto específico. Asegúrese de aplicar los consejos proporcionados en la [Documentación sobre la optimización del rendimiento](/help/sites-deploying/configuring-performance.md) antes de realizar pruebas de referencia y utilizar sus resultados para cualquier cálculo de tamaño de hardware.

Los requisitos de tamaño de hardware para casos de uso avanzados deben basarse en una evaluación detallada del rendimiento del proyecto. Las características de los casos de uso avanzado que requieren recursos de hardware excepcionales incluyen combinaciones de:

* carga útil/rendimiento de alto contenido
* uso extensivo de código personalizado, flujos de trabajo personalizados o bibliotecas de software de terceros
* integración con sistemas externos no compatibles

### Espacio en disco/Disco duro {#disk-space-hard-drive}

El espacio en disco necesario depende en gran medida del volumen y el tipo de la aplicación web. Los cálculos deben tener en cuenta:

* la cantidad y el tamaño de las páginas, los recursos y otras entidades almacenadas en el repositorio, como flujos de trabajo, perfiles, etc.
* la frecuencia estimada de cambios de contenido y, por lo tanto, la creación de versiones de contenido
* el volumen de las representaciones de recursos DAM que se generarán
* el crecimiento general del contenido a lo largo del tiempo

El espacio en disco se monitorea continuamente durante la limpieza de revisión en línea y sin conexión. Si el espacio en disco disponible cae por debajo de un valor crítico, el proceso se cancelará. El valor crítico es el 25% de la huella de disco actual del repositorio y no es configurable. Se recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio, incluido el crecimiento estimado.

Considere una configuración de matrices redundantes de discos independientes (RAID, por ejemplo, RAID10) para la redundancia de datos.

>[!NOTE]
>
>El directorio temporal de una instancia de producción debe tener al menos 6 GB de espacio disponible.

#### Virtualización {#virtualization}

AEM funciona bien en entornos virtualizados, pero puede haber factores como CPU o E/S que no se pueden equiparar directamente al hardware físico. Una recomendación es elegir una velocidad de E/S más alta (en general) ya que esto es un factor crítico en la mayoría de los casos. La evaluación comparativa del entorno es necesaria para comprender con precisión qué recursos se necesitarán.

#### Paralelización de instancias de AEM {#parallelization-of-aem-instances}

**Fallo de seguridad**

Se implementa un sitio web seguro contra fallos en al menos dos sistemas separados. Si un sistema se rompe, otro puede tomar el control y compensar así el fallo del sistema.

**Escalabilidad de los recursos del sistema**

Mientras todos los sistemas están en ejecución, hay disponible un mayor rendimiento informático. Que el rendimiento adicional no es necesariamente lineal con el número de nodos del clúster, ya que la relación depende en gran medida del entorno técnico; consulte la [Documentación del clúster](/help/sites-deploying/recommended-deploys.md) para obtener más información.

La estimación de cuántos nodos de clúster son necesarios se basa en los requisitos básicos y en casos de uso específicos del proyecto web en particular:

* Desde la perspectiva de la seguridad ante fallos, es necesario determinar, para todos los entornos, la importancia de la falla y el tiempo de compensación de la falla en función del tiempo que tarda un nodo de cluster en recuperarse.
* Para el aspecto de la escalabilidad, el número de operaciones de escritura es básicamente el factor más importante; see [Autores que trabajan en paralelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) para el entorno de creación y [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) para el entorno de publicación. Se puede establecer el equilibrio de carga para las operaciones que acceden al sistema únicamente para procesar las operaciones de lectura; see [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para obtener más información.

## Crear cálculos específicos de entorno {#author-environment-specific-calculations}

A efectos de evaluación comparativa, Adobe ha desarrollado algunas pruebas de referencia para instancias de autor independientes.

* **Prueba de referencia 1**
Calcule el rendimiento máximo de un perfil de carga donde los usuarios realizan un simple ejercicio de creación de página sobre una carga base de 300 páginas existentes de naturaleza similar. Los pasos necesarios eran iniciar sesión en el sitio, crear una página con un SWF e imagen/texto, agregar una nube de etiquetas y, a continuación, activar la página.

   * **Resultado**
El rendimiento máximo para un ejercicio de creación de página simple como el anterior (considerado como una transacción) se encontró en 1730 transacciones/hora.

* **Prueba de referencia 2**
Calcule el rendimiento máximo cuando el perfil de carga tenga una combinación de creación de página nueva (10 %), modificación de una página existente (80 %) y creación y posterior modificación de una página sucesiva (10 %). La complejidad de las páginas sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza añadiendo una imagen y modificando el contenido del texto. De nuevo, el ejercicio se realizó sobre una carga base de 300 páginas de la misma complejidad que la definida en la prueba de referencia 1.

   * **Resultado**
El rendimiento máximo para un escenario de operación mixta de este tipo se encontró en 3252 transacciones por hora.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que una proporción fija de cada tipo de transacción se incluya en la carga de trabajo.

Las dos pruebas anteriores resaltan claramente que el rendimiento varía según el tipo de operación. Utilice las actividades del entorno como base para dimensionar el sistema. Obtendrá un mejor rendimiento con acciones menos intensivas, como la modificación (que también es más común).

### Almacenamiento en caché {#caching}

En el entorno de creación, la eficacia del almacenamiento en caché suele ser mucho menor, ya que los cambios en el sitio web son más frecuentes y también el contenido es altamente interactivo y personalizado. Con Dispatcher, puede almacenar en caché AEM bibliotecas, JavaScript, archivos CSS e imágenes de diseño. Esto acelera algunos aspectos del proceso de creación. Si configura el servidor web para que establezca encabezados adicionales para el almacenamiento en caché del explorador en estos recursos, se reducirá el número de solicitudes HTTP y, por lo tanto, se mejorará la capacidad de respuesta del sistema según la experiencia de los autores.

### Autores que trabajan en paralelo {#authors-working-in-parallel}

En el entorno de creación, el número de autores que trabajan en paralelo y la carga que sus interacciones añaden al sistema son los principales factores limitantes. Por lo tanto, le recomendamos que escale su sistema en función del rendimiento compartido de los datos.

Para estos escenarios, Adobe ejecutó pruebas de referencia en un clúster de dos nodos shared-nada de instancias de autor.

* **Prueba de referencia 1a**
Con un clúster activo-activo de shared-nada de 2 instancias de autor, calcule el rendimiento máximo con un perfil de carga donde los usuarios realizan un simple ejercicio de creación de página sobre una carga base de 300 páginas existentes, todo de naturaleza similar.

   * **Resultado**
El rendimiento máximo para un ejercicio de creación de página simple, como el anterior, (considerado como una transacción) se encuentra en transacciones de 2016/hora. Esto supone un aumento de aproximadamente el 16 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

* **Prueba de referencia 2b**
Con un clúster activo-activo de contenido compartido de nada de 2 instancias de autor, calcule el rendimiento máximo cuando el perfil de carga tenga una combinación de creación de página nueva (10 %), modificación de páginas existentes (80 %) y creación y modificación de una página sucesiva (10 %). La complejidad de la página sigue siendo la misma que en el perfil de la prueba de referencia 1. La modificación básica de la página se realiza añadiendo una imagen y modificando el contenido del texto. De nuevo, el ejercicio se realizó sobre una carga base de 300 páginas de complejidad igual a la definida en la prueba de referencia 1.

   * **Resultado**
El rendimiento máximo para un escenario de operación mixta de este tipo se encontró en 6288 transacciones/hora. Esto supone un aumento de aproximadamente el 93 % en comparación con una instancia de autor independiente para la misma prueba de referencia.

>[!NOTE]
>
>La tasa de rendimiento no distingue entre tipos de transacciones dentro de un perfil de carga. El método utilizado para medir el rendimiento garantiza que una proporción fija de cada tipo de transacción se incluya en la carga de trabajo.

Las dos pruebas anteriores resaltan claramente que AEM escala bien para los autores que realizan operaciones de edición básicas con AEM. En general, AEM es más eficaz en escalar las operaciones de lectura.

En un sitio web típico, la mayoría de la creación se produce durante la fase del proyecto. Una vez que el sitio web se pone en marcha, el número de autores que trabajan en paralelo normalmente se hunde en un promedio menor (modo operativo).

Puede calcular el número de equipos (o CPUs) necesarios para el entorno de creación de la siguiente manera:

`n = numberOfParallelAuthors / 30`

Esta fórmula puede servir como guía general para escalar CPUs cuando los autores realizan operaciones básicas con AEM. Se supone que el sistema y la aplicación están optimizados. Sin embargo, la fórmula no tendrá el valor &quot;True&quot; para funciones avanzadas como MSM o Assets (consulte las secciones siguientes).

Consulte también los comentarios adicionales sobre [Paralelización](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) y [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md).

### Hardware Recommendations {#hardware-recommendations}

Normalmente, puede utilizar el mismo hardware para su entorno de creación que se recomienda para su entorno de publicación. Normalmente, el tráfico de sitios web es mucho menor en los sistemas de creación, pero la eficacia de la caché también es menor. Sin embargo, el factor fundamental aquí es el número de autores que trabajan en paralelo, junto con el tipo de acciones que se están realizando en el sistema. En general, el agrupamiento de AEM (del entorno de creación) es más eficaz para escalar las operaciones de lectura; en otras palabras, un clúster AEM escala bien con los autores que realizan operaciones de edición básicas.

Las pruebas de referencia en Adobe se realizaron utilizando el sistema operativo RedHat 5.5, que se ejecuta en una plataforma de hardware Hewlett-Packard ProLiant DL380 G5 con la siguiente configuración:

* Dos CPUs Intel Xeon X5450 de cuatro núcleos a 3,00 GHz
* 8 GB de RAM
* Broadcom NetXtreme II BCM5708 Gigabit Ethernet
* Controlador RAID HP Smart Array, caché de 256 MB
* Dos discos SAS de 146 GB a 10.000 RPM configurados como un conjunto de bandas RAID 0
* SPEC CINT2006 La puntuación de referencia de tasa es 110

AEM instancias se ejecutaban con un tamaño mínimo de pila de 256M, un tamaño máximo de pila de 1024M.

## Publicar cálculos específicos de entornos {#publish-environment-specific-calculations}

### Eficiencia de almacenamiento en caché y tráfico {#caching-efficiency-and-traffic}

La eficacia de la caché es crucial para la velocidad del sitio web. La siguiente tabla muestra cuántas páginas por segundo puede gestionar un sistema de AEM optimizado mediante un proxy inverso, como Dispatcher:

| Relación de caché | Páginas/s (pico) | Millones de páginas por día (media) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99 % | 910 | 32 |
| 95 % | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Renuncia de responsabilidad: Los números se basan en una configuración de hardware predeterminada y pueden variar según el hardware específico utilizado.

La proporción de caché es el porcentaje de páginas que el despachante puede devolver sin tener que acceder a AEM. El 100 % indica que Dispatcher responde a todas las solicitudes, 0 % significa que AEM calcula cada página.

### Complejidad de las plantillas y las aplicaciones {#complexity-of-templates-and-applications}

Si utiliza plantillas complejas, AEM necesitará más tiempo para procesar una página. Las páginas tomadas de la caché no se ven afectadas por esto, pero el tamaño de la página sigue siendo relevante cuando se considera el tiempo de respuesta general. La representación de una página compleja puede tardar diez veces más que la representación de una página simple.

### Fórmula {#formula}

Con la fórmula siguiente, puede calcular una estimación de la complejidad general de su solución AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

En función de la complejidad, puede determinar el número de servidores (o núcleos de CPU) que necesita para el entorno de publicación de la siguiente manera:

`n = (traffic * complexity / 1000 ) * activations`

Las variables de la ecuación son las siguientes:

<table>
 <tbody>
  <tr>
   <td>tráfico</td>
   <td>El tráfico máximo esperado por segundo. Puede estimar esto como el número de visitas al día de la página, dividido por 35 000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilice 1 para una aplicación simple, 2 para una aplicación compleja o un valor intermedio:</p>
    <ul>
     <li>1: un sitio web totalmente anónimo y orientado al contenido</li>
     <li>1.1: un sitio totalmente anónimo y orientado al contenido con personalización del lado del cliente/Target</li>
     <li>1.5: un sitio orientado al contenido con secciones anónimas y con sesión iniciada, personalización del lado del cliente/Target</li>
     <li>1.7: para un sitio orientado al contenido con secciones anónimas y con sesión iniciada, personalización del lado del cliente/Target y contenido generado por el usuario</li>
     <li>2 - donde todo el sitio requiere iniciar sesión, con un uso extenso del contenido generado por el usuario y una variedad de técnicas de personalización</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>El porcentaje de páginas que salen de la caché de Dispatcher. Utilice 1 si todas las páginas provienen de la caché, o 0 si todas las páginas están calculadas por AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilice un valor entre 1 y 10 para indicar la complejidad de las plantillas. Los números más altos indican plantillas más complejas, utilizando el valor 1 para sitios con un promedio de 10 componentes por página, el valor 5 para un promedio de página de 40 componentes y 10 para un promedio de más de 100 componentes.</td>
  </tr>
  <tr>
   <td>activaciones</td>
   <td>Número de activaciones promedio (replicación de páginas y recursos de tamaño medio desde el autor hasta el nivel de publicación) por hora dividido entre x, donde x es el número de activaciones realizadas en un sistema sin efectos secundarios de rendimiento para otras tareas procesadas por el sistema. También puede predefinir un valor inicial pesimista como x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Si tiene un sitio web más complejo, también necesita servidores web más potentes para que AEM responder a una solicitud en un tiempo aceptable.

* Complejidad por debajo de 4: ・ 1024 MB de RAM JVM&#42;
・ CPU de bajo a mediano rendimiento

* Complejidad entre 4 y 8: ・ 2048 MB de RAM JVM&#42;
・ CPU de mediano a alto rendimiento

* Complejidad superior a 8: ・ 4096 MB de RAM JVM&#42;
・ CPU de alto a alto rendimiento

>[!NOTE]
>
>&#42; Reserve suficiente RAM para su sistema operativo además de la memoria necesaria para su JVM.

## Cálculos específicos adicionales de casos de uso {#additional-use-case-specific-calculations}

Además del cálculo de una aplicación web predeterminada, es posible que deba tener en cuenta factores específicos para los siguientes casos de uso. Los valores calculados se añaden al cálculo predeterminado.

### Consideraciones específicas de los recursos {#assets-specific-considerations}

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de memoria y configure la variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo para usar la variable [paquete Camera Raw](/help/assets/camera-raw.md) para la ingesta de imágenes sin procesar.

>[!NOTE]
>
>Un mayor rendimiento de las imágenes significa que los recursos informáticos deben ser capaces de mantenerse al ritmo de las E/S del sistema y viceversa. Por ejemplo, si la importación de imágenes inicia los flujos de trabajo, la carga de muchas imágenes a través de WebDAV podría provocar un atraso en los flujos de trabajo.
>
>El uso de discos separados para TarPM, almacén de datos e índice de búsqueda puede ayudar a optimizar el comportamiento de E/S del sistema (sin embargo, normalmente tiene sentido mantener el índice de búsqueda localmente).

>[!NOTE]
>
>Consulte también la [Guía de rendimiento de recursos](/help/sites-deploying/assets-performance-sizing.md).

### Administrador de varios sitios {#multi-site-manager}

El consumo de recursos al utilizar AEM MSM en un entorno de creación depende en gran medida de los casos de uso específicos. Los factores básicos son:

* Número de Live Copies
* Periodicidad de los lanzamientos
* Tamaño del árbol de contenido que desea desplegar
* Funcionalidad conectada de las acciones de despliegue

La prueba del caso de uso planificado con un extracto de contenido representativo puede ayudarle a comprender mejor el consumo de recursos. Si extrapola los resultados con el rendimiento planificado, puede evaluar los recursos adicionales necesarios para el MSM AEM.

Tenga en cuenta también que los autores que trabajan en paralelo percibirán efectos secundarios de rendimiento si AEM casos de uso de MSM consumen más recursos de los previstos.

### Consideraciones sobre el tamaño de AEM Communities {#aem-communities-sizing-considerations}

AEM sitios que incluyen funciones de AEM Communities (sitios de la comunidad) experimentan un alto nivel de interacción de los visitantes del sitio (miembros) en el entorno de publicación.

Las consideraciones sobre el tamaño de un sitio de la comunidad dependen de la interacción esperada de los miembros de la comunidad y de si el rendimiento óptimo del contenido de la página es de mayor importancia.

Los miembros de contenido generado por el usuario (UGC) enviados se almacenan por separado del contenido de la página. Aunque la plataforma de AEM utiliza un almacén de nodos que replica el contenido del sitio de autor a publicación, AEM Communities utiliza un único almacén común para UGC que nunca se replica.

Para el almacén UGC, es necesario elegir un proveedor de recursos de almacenamiento (SRP), que influye en la implementación elegida.
Consulte

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md)
* [Topologías recomendadas para comunidades](/help/communities/topologies.md)
