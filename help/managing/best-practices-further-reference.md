---
title: 'Lista de comprobación: más referencia'
seo-title: 'Lista de comprobación: más referencia'
description: Obtenga más información sobre los detalles que explican y/o aumentan los documentos y principios cubiertos por la lista de comprobación de la gestión de proyectos - prácticas recomendadas.
seo-description: Obtenga más información sobre los detalles que explican y/o aumentan los documentos y principios cubiertos por la lista de comprobación de la gestión de proyectos - prácticas recomendadas.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
translation-type: tm+mt
source-git-commit: 37ec3d8ce779ba392e6a92c828efb5fad749abec

---


# Lista de comprobación: más referencia{#the-checklist-further-reference}

Esta página proporciona más detalles para detallar y/o ampliar los documentos y principios cubiertos por la lista de verificación de [Gestión de Proyectos - Optimizaciones](/help/managing/best-practices.md).

## AEM - ¿Qué va a usar? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>Las listas que figuran en esta subsección no son exhaustivas, sino que están destinadas a ser una introducción.

### Funciones de AEM {#features-within-aem}

Al implementar AEM (especialmente por primera vez), tendrá que revisar las [capacidades y los flujos de trabajo de AEM](https://www.adobe.com/marketing/experience-manager.html) para asegurarse de qué áreas desea o necesita.

Considere las funciones de AEM que va a utilizar y el impacto en su diseño; por ejemplo:

* [Comercio](/help/sites-administering/ecommerce.md)
* [Pantallas](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Recursos](/help/assets/assets.md)
* [Etiquetas](/help/sites-administering/tags.md)
* [Administración y traducción de varios sitios](/help/sites-administering/msm-and-translation.md)
* [Formularios](/help/forms/home.md)
* [Comunidades](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

Además, compruebe las [Notas](/help/release-notes/release-notes.md)de la versión, en las distintas versiones de AEM, para ver cuándo se agregaron nuevas funciones.

### Integraciones {#integrations}

AEM se puede integrar con otros productos de Adobe y/o servicios de terceros. Esto puede aumentar la potencia y la funcionalidad a su disposición.

Consulte Integración [de](/help/sites-administering/integration.md) soluciones para obtener información completa.

## ¿Migrar o actualizar? {#migrate-or-upgrade}

Una consideración importante es si desea:

* Actualice la instalación existente en su lugar.
* Migrar el contenido del sistema actual a una nueva instalación.

Al pasar de una versión anterior a la versión actual, hay dos opciones:

* Utilice el Administrador [de](/help/sites-administering/package-manager.md) paquetes para exportar todo el contenido y el código de la aplicación del sistema antiguo al nuevo.
* [Actualice](/help/sites-deploying/upgrade.md) el sistema antiguo en su lugar. Esta es la opción recomendada en la mayoría de los casos.

## Reglas básicas de tierra {#basic-ground-rules}

Al igual que con cualquier proyecto, es fundamental establecer normas básicas lo antes posible. Entre estas características se incluyen:

>[!NOTE]
>
>Estos puntos son genéricos, la lista [de comprobación de](/help/managing/best-practices.md) optimizaciones trata aspectos específicos relacionados con AEM.

* **Funciones**

   Estos deben estar claramente definidos y ser conocidos por todos los participantes en el proyecto. Además, es aconsejable destacar:

   * Responsables de tomar decisiones
   * Puntos de contacto

* **Responsabilidades**

   * Para cada función, una definición clara de las responsabilidades relacionadas con el proyecto ayuda a evitar confusiones.

* **Participación**

   Al hacer participar a las partes interesadas lo antes posible, puede alentarlas a que se conviertan en *partes interesadas* en el proyecto, aumentando así su compromiso con su éxito.

   * Por parte del cliente, esto incluye a los autores, que tendrán que trabajar con el sistema día a día.
   * Dentro de su propio equipo de proyectos, esto también incluirá a las personas responsables de la garantía de calidad. Cuanto más comprendan los requisitos del cliente, mejor podrán planificar las pruebas.

* **Rutas de comunicación**

   * Aunque no se deben formalizar excesivamente, las definiciones específicas deben garantizar que las personas clave estén siempre informadas y, por lo tanto, se mantengan actualizadas. Debe prestarse especial atención a la comunicación con partes externas.

* **Procesos**

   Los procesos que se definirán dependerán del proyecto individual. Intenta de nuevo mantener estas opciones sencillas, teniendo en cuenta:

   * Definir procesos (y vías de comunicación) para interactuar con terceros; por ejemplo, agencias de diseño y proveedores de software de terceros, entre otros.
   * A menudo, el cliente tendrá sus propios procedimientos y herramientas de administración de proyectos e informes.

* **Herramientas de seguimiento**

   Hay muchas herramientas disponibles para rastrear información sobre errores, tareas y otros aspectos del proyecto; consulte [Visión general de las herramientas](#overview-of-potential-tools) potenciales para obtener más detalles.

   * El punto clave a tener en cuenta aquí es mantener sólo una copia de la información y compartir la información (y por lo tanto, el acceso a la herramienta que se está utilizando). Esto facilitará el mantenimiento y ayudará a evitar discrepancias.

* **Ámbito**

   Definir claramente qué es lo que debe cubrir el proyecto a varios niveles:

   * las versiones individuales (si se utiliza un proceso de lanzamiento iterativo, independientemente de si se entregan a los clientes o al equipo de prueba interno).
   * el proyecto de AEM.
   * todo el proyecto; incluyendo cualquier software de terceros, su impacto en las pruebas, problemas de organización y muchos otros.
   * Para algunos aspectos también puede ser útil indicar lo que *no* está dentro del ámbito del proyecto. Esto puede ayudar a evitar confusiones y suposiciones incorrectas, aunque debería limitarse a cuestiones esenciales.

* **Informes**

   Defina claramente qué información informará, en qué forma, con qué frecuencia y a quién.

* **Terminología**

   * Defina las abreviaturas y/o la terminología específica del cliente que se utilizarán.

* **Suposiciones**

   * Defina las suposiciones que se estén realizando.

Esta información puede definirse en un Manual del proyecto; el uso de una Wiki también puede ayudar a asegurar que los cambios en curso se manejen eficientemente. En todos los casos en que se definen, los factores clave son los siguientes:

* La información se define y se mantiene
* La información se comunica claramente a todas las personas interesadas. Aunque la práctica estándar de la administración de proyectos no se puede repetir con suficiente frecuencia que una definición clara de la función y una buena comunicación pueden hacer o romper un proyecto.
* Sólo se mantiene una versión de cualquier información que se esté rastreando; por ejemplo: seguimiento de errores, seguimiento de problemas, etc.

## Indicadores de rendimiento clave y métricas de objetivo {#key-performance-indicators-and-target-metrics}

Las organizaciones utilizan indicadores de rendimiento clave (KPI) para evaluar su éxito al alcanzar los objetivos. Estos indicadores son valores mensurables que pueden utilizarse para demostrar la eficacia con que se cumplen los objetivos específicos.

Estos indicadores pueden ser:

* Negocios:

   * Se utiliza para medir objetivos comerciales clave.
   * Es importante elegir KPI adecuados para su negocio o escenario con definiciones claras de cuáles son, cómo se medirán, cómo se utilizarán y quién los usará.

* Actuación:

   * Defina cómo medir el rendimiento del sistema.
   * Algunos ejemplos incluyen el tiempo de carga de la página, el tiempo de respuesta del servidor y el rendimiento de la consulta de la base de datos.

Algunos indicadores, pero no todos, se pueden basar en las métricas de objetivo que identifique y defina.

### Métricas de Target {#target-metrics}

Las métricas se utilizan para definir mediciones cuantitativas de la calidad de su sitio web; son básicamente una definición de los objetivos de rendimiento que desea alcanzar y se pueden utilizar para definir [los KPI (Indicadores de rendimiento clave)](#key-performance-indicators-and-target-metrics).

Se pueden definir muchas métricas, pero a menudo las que defina cubren sus objetivos de rendimiento y concurrencia. En particular, factores que pueden ser difíciles de cuantificar y que a menudo son propensos a la evaluación *emocional* :

* &quot;nuestro sitio web es *demasiado lento* hoy&quot; - ¿cuándo califica *lentamente* ?

* &quot;todo *se detiene* cuando mi colega inicia sesión&quot; - ¿cuántos usuarios simultáneos pueden admitir el sistema?
* &quot;cuando busco, el sistema *se detiene* &quot; - ¿qué tipo de solicitudes de búsqueda están afectando al sistema?
* &quot;se tarda *años* en descargar el archivo&quot; - ¿Cuáles son los tiempos de descarga aceptables (bajo condiciones de red normales)?

Las métricas de Target se definen al inicio de un proyecto para:

* indique las dimensiones esperadas del sitio web que va a ofrecer
* indique la calidad mínima que desea alcanzar
* definir cómo se medirán realmente estos factores
* se utilizará como base para los indicadores de rendimiento [clave](#key-performance-indicators-and-target-metrics)

Como siempre se debe tener cuidado al definir las métricas objetivo:

* si se fijan demasiado altos, pueden ser completamente inalcanzables
* si se configuran fluctuaciones demasiado bajas, puede que no se resalten
* garantizar que se puedan medir repetida y sistemáticamente
* proporcionar un equilibrio entre los diferentes factores que se miden
* determinadas métricas se relacionarán con un entorno de prueba, pero algunas deberían reflejar los escenarios de la vida real, ya que deben ser medibles y reproducibles en el sitio web de producción
* priorizar las métricas según su importancia para el sitio Web
* limitar las métricas a un conjunto que se pueda monitorear de forma realista

Durante el desarrollo del proyecto pueden actualizarse y sintonizarse según corresponda. Una vez que el proyecto se haya implementado correctamente, se pueden utilizar para ayudarle a controlar la instalación y supervisar/mantener los niveles de servicio necesarios para el funcionamiento continuo.

Cuando se utilizan correctamente, estas métricas pueden proporcionar una herramienta útil; cuando se utilizan irresponsablemente, pueden ser una distracción que desperdicia tiempo. Como siempre, se necesita entender lo que se mide, cómo se mide y por qué.

>[!NOTE]
>
>En esta sección se tratarán los principios básicos y las cuestiones que deben examinarse. Cada instalación es diferente, por lo que los valores reales que se medirán diferirán.

### Todo depende del diseño del proyecto {#everything-rests-on-your-project-design}

Todas las métricas que se medirán se verán afectadas, de alguna manera, por el diseño del proyecto. Por el contrario, muchos problemas se resolverán mejor con los cambios de diseño.

Por lo tanto, debe definir las métricas de objetivo *antes* de decidir el diseño. Esto le permite optimizar el diseño en función de estos factores. Una vez que el proyecto se haya desarrollado, será difícil realizar cambios en los principios básicos de diseño.

Cuando cree la estructura del sitio web, siga la estructura recomendada para los sitios web de AEM. Asegúrese de comprender los siguientes problemas y/o principios:

* Cómo estructurar el contenido del sitio web.
* Cómo funcionan las plantillas y los componentes.
* Funcionamiento del almacenamiento en caché.
* Impacto del contenido personalizado.
* Cómo funciona la función de búsqueda.
* Cómo puede utilizar CSS y tecnologías relacionadas para crear código HTML compacto y no redundante.

Si cree que el diseño no sigue las directrices o no está seguro de algunas de las implicaciones, aclare estos problemas antes de iniciar la fase de programación o de rellenar el contenido.

### Infraestructura {#infrastructure}

Para definir o evaluar la infraestructura, ayudará a definir valores objetivo como:

* visitantes/día; tanto promedio como máximo
* visitas individuales/día; tanto promedio como máximo
* número de páginas web disponibles
* volumen de contenido web

Según su situación y la importancia estratégica del sitio web, esto le ayudará a evaluar y elegir su infraestructura:

* número de servidores
* número de instancias de AEM (creación y publicación)

### Actuación {#performance}

Existen varios factores de rendimiento que se pueden evaluar:

* tiempos de respuesta para páginas individuales, teniendo en cuenta:

   * tiempos de respuesta en un entorno de creación
   * tiempos de respuesta en el entorno de publicación

* tiempos de respuesta para solicitudes de búsqueda

Esta sección se puede leer junto con la optimización [del rendimiento](/help/sites-deploying/configuring-performance.md) , que amplía los detalles técnicos para medir el rendimiento.

#### Tiempos de respuesta para páginas individuales {#response-times-for-individual-pages}

Un problema clave es el tiempo que tarda el sitio web en responder a las solicitudes de los visitantes.

Aunque este valor variará para cada solicitud, se puede definir un valor de objetivo promedio. Una vez que se ha demostrado que este valor es alcanzable y sostenible, puede utilizarse para monitorear el rendimiento del sitio web e indicar el desarrollo de posibles problemas

Diferentes objetivos en entornos de autor y publicación

Los tiempos de respuesta que perseguirá serán diferentes en los entornos de autor y publicación, lo que refleja la audiencia de destino:

* **Entorno de creación**

   Este entorno lo utilizan los autores que introducen y actualizan contenido, por lo que debe:

   * atiende a un pequeño número de usuarios que generan un gran número de solicitudes al actualizar páginas de contenido y los elementos individuales de esas páginas
   * sea lo más rápido posible para maximizar su productividad y lograr que el contenido llegue a su sitio Web

* **Entorno de publicación**

   Este entorno contiene contenido que pone a disposición de los usuarios:

   * la velocidad sigue siendo vital, pero a menudo es más lenta que un entorno de creación
   * a menudo se aplican mecanismos adicionales de mejora del rendimiento:

      * el contenido se almacena en la caché
      * se aplica el equilibrio de carga

#### Configuración de los tiempos de respuesta objetivo {#setting-target-response-times}

Entonces, ¿cómo puede decidir los tiempos de respuesta alcanzables (promedio)? A menudo se trata de una cuestión de experiencia:

* experiencias pasadas en su sitio web
* experiencia con AEM
* reconocimiento de páginas complejas que tienen tiempos de respuesta superiores a la media (si es posible, deben optimizarse individualmente)

Sin embargo, en circunstancias controladas pueden aplicarse las siguientes directrices:

* El 70 % de las solicitudes de páginas deben responder en menos de 100 ms.
* El 25% de las solicitudes de páginas deben responder en menos de 100 ms-300 ms.
* El 4% de las solicitudes de páginas deben responder en menos de 300 ms-500 ms.
* El 1% de las solicitudes de páginas deben responder en menos de 500 ms-1000 ms.
* Ninguna página debe responder más lentamente que un segundo.

Los números anteriores asumen las siguientes condiciones:

* medidas en la publicación (sin entorno de creación y/o sobrecarga de CFC)
* medida en el servidor (sin sobrecarga de red)
* no almacenado en caché (sin caché de salida AEM, sin caché de Dispatcher)
* solo para elementos complejos con muchas dependencias (HTML, JS, PDF, ...)
* no hay otra carga en el sistema

Existen varios mecanismos que puede utilizar para supervisar los tiempos de respuesta:

* **Supervisión de los tiempos de respuesta con el archivo request.log de AEM**

   Un buen punto de partida para el análisis de rendimiento es el registro de solicitudes. Entre otra información, puede utilizarla para ver los tiempos de respuesta de solicitudes individuales. Consulte Optimización [del rendimiento](/help/sites-deploying/configuring-performance.md) para obtener más información.

* **Supervisión de los tiempos de respuesta con comentarios HTML**

   Los comentarios HTML se pueden utilizar para incluir información sobre el tiempo de respuesta en el origen de cada página:

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Solicitudes de búsqueda {#search-requests}

Las solicitudes de búsqueda pueden tener un impacto significativo en el sitio web, en términos de:

* Tiempo de respuesta de la búsqueda real

   * Una función de búsqueda rápida es un objetivo de calidad para el sitio Web

* Impacto en el rendimiento general

   * Como una función de búsqueda debe analizar (potencialmente grandes) secciones del contenido, o un índice extraído especialmente, esto puede afectar al rendimiento de todo el sistema si no se optimiza

El establecimiento de objetivos para las solicitudes de búsqueda también depende de la experiencia:

* experiencia de AEM
* una evaluación de la frecuencia con la que se utilizará la búsqueda en comparación con otros objetivos
* su administrador de persistencia
* su índice de búsqueda
* la complejidad de la función de búsqueda; una función de búsqueda básica que sólo permite la entrada de un término de búsqueda será más rápida que una búsqueda avanzada que permite al usuario crear afirmaciones de búsqueda complejas mediante Y/O/NO.

Estos deben planificarse e integrarse desde el comienzo mismo del proyecto. Entre los mecanismos disponibles para la vigilancia figuran los siguientes:

* **Supervisión de los tiempos de respuesta de búsqueda con el archivo request.log de AEM**

   Nuevamente, request.log puede utilizarse para monitorear los tiempos de respuesta de las solicitudes de búsqueda; consulte Optimización [del rendimiento](/help/sites-deploying/configuring-performance.md) para obtener más información.

* **Mecanismos programados para medir los tiempos de respuesta de búsqueda**

   Para personalizar la información que recopila sobre las solicitudes de búsqueda y su rendimiento, se recomienda incluir la recopilación de información en el código fuente del proyecto; consulte Optimización [del rendimiento](/help/sites-deploying/configuring-performance.md) para obtener más información.

### Concurrencia {#concurrency}

El sitio web estará disponible para varios usuarios/visitantes, tanto en los entornos de autor como de publicación. Los números suelen ser más de los que se usaban al realizar pruebas, pero también fluctúan y son difíciles de predecir. El sitio web deberá estar diseñado para un número promedio de usuarios/visitantes simultáneos sin que se observe un impacto negativo en el rendimiento. De nuevo, el `request.log` puede utilizarse para realizar pruebas de concurrencia; consulte Optimización [del rendimiento](/help/sites-deploying/configuring-performance.md) para obtener más información.

Los objetivos para el número de usuarios simultáneos dependen del tipo de entorno:

* **Entorno de creación**

   * Generalmente se puede estimar con precisión el número de usuarios simultáneos. Usted sabrá cuántos autores tiene en total, aunque (probablemente) no todos estarán activos al mismo tiempo.

* **Entorno de publicación**

   * Esto es más difícil de predecir, por lo que debe seleccionar un valor objetivo. De nuevo, esto debería basarse en la experiencia de su sitio web actual junto con expectativas realistas de su nuevo sitio web.
   * Los eventos especiales (por ejemplo, cuando publica contenido nuevo y muy popular) pueden superar las expectativas, o incluso las capacidades (como a veces se informa en la prensa cuando se ponen a la venta entradas para ciertos eventos).

### Capacidad y volumen {#capacity-and-volume}

Antes de analizar las métricas relacionadas, una definición rápida de los términos:

* **Volumen**

   * Cantidad de salida que procesa y entrega el sistema.

* **Capacidad**

   * Capacidad del sistema para entregar el volumen.
   * En cada paso, la capacidad y el volumen se miden de manera diferente, como se muestra en la tabla siguiente. Para obtener el mejor rendimiento, asegúrese de que la capacidad coincide con el volumen en cada paso y de que tanto la capacidad como el volumen se comparten en todos los pasos. Por ejemplo, puede calcular la navegación en el equipo cliente o colocarla en la caché, en lugar de calcularla en el servidor para cada solicitud.

* **Capacidad y volumen**

   | Qué / Dónde | Capacidad | Volumen |
   |---|---|---|
   | Cliente | Potencia computacional del equipo del usuario. | Complejidad del diseño de página. |
   | Red | Ancho de banda de la red. | Tamaño de la página (código, imágenes, etc.). |
   | Caché de despachante | Memoria del servidor del servidor Web (memoria principal y disco duro). | Servidor web (memoria principal y disco duro). Número y tamaño de las páginas en caché. |
   | Caché de salida | Memoria del servidor de AEM (memoria principal y unidad de disco duro). | Número y tamaño de las páginas en la caché de salida, número de dependencias por página. La caché del despachante disminuye este volumen. |
   | Servidor web | Potencia computacional del servidor Web. | Cantidad de solicitudes. El almacenamiento en caché reduce este volumen. |
   | Plantilla | Potencia computacional del servidor Web. | Complejidad de las plantillas. |
   | Repositorio | Rendimiento del repositorio. | Número de páginas cargadas desde el repositorio. |

### Otras métricas {#other-metrics}

Las secciones anteriores detallan las principales métricas que se van a definir.

Según sus requisitos específicos, puede resultar útil definir métricas adicionales, ya sea de forma aislada o teniendo en cuenta las clasificaciones anteriores.

Sin embargo, es preferible tener un pequeño conjunto de métricas principales precisas que funcionen de manera fácil y confiable, en lugar de intentar medir y definir cada aspecto del sitio web. Por su propia naturaleza, su sitio web empezará a cambiar y a evolucionar tan pronto como se entregue a sus usuarios.

## Seguridad {#security}

La seguridad es crucial y un desafío cada vez mayor. Se ***debe*** considerar y planificar desde las primeras etapas del proyecto.

La lista de comprobación [de seguridad](/help/sites-administering/security-checklist.md) detalla los pasos que debe seguir para garantizar que la instalación de AEM sea segura cuando se implemente. Otros aspectos relacionados con la seguridad se tratan en [Seguridad (al desarrollarse)](/help/sites-developing/security.md) y Administración y seguridad [del usuario](/help/sites-administering/security.md).

## Tareas paralelas e iterativas {#parallel-and-iterative-tasks}

>[!NOTE]
>
>Lo siguiente:
>
>* Ofrece información general sobre la *primera* implementación de un proyecto de AEM.
>* Está concebido como una visión general abstracta; consulte la lista [de comprobación de](/help/managing/best-practices.md) proyectos para fases/hitos/tareas específicas.
>* Cualquier escalón de tiempo es teórico.
>



Para una nueva implementación de un proyecto AEM estándar, deberá considerar tareas como:

* Entrega desde el proceso de ventas.
* Implementación de la aplicación para clientes (**Desarrollo**).
* Instalación y configuración de la infraestructura (y procesos relacionados) en el sitio del cliente (**Infraestructura**).
* Creación (o migración) del contenido (**Contenido**).
* Entrega a operaciones (**Mantenimiento/Soporte**).
* Versiones de seguimiento.

![chlimage_1-2](assets/chlimage_1-2.png)

Se recomienda utilizar un enfoque iterativo en todos los aspectos:

![climage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Divida el lanzamiento del proyecto en **lanzamiento(s)** suave(s) (disponibilidad reducida, varias iteraciones) y lanzamiento **duro** (disponibilidad completa - Activo) para permitir el ajuste, la optimización y la formación del usuario en condiciones realistas en el entorno de producción.

>[!NOTE]
>
>Consulte la lista [de comprobación de](/help/managing/best-practices.md) proyectos para ver ejemplos de tareas que debe realizar (o evaluar) durante el ciclo de vida del proyecto.

Algunos puntos a tener en cuenta para cada categoría son:

* **Desarrollo**

   * Defina primero la arquitectura base.
   * Utilice varias iteraciones (sprints) para el desarrollo:

      * La primera velocidad equivale al primer ciclo completo de desarrollo.
      * La primera impresión resulta en la primera implementación en el entorno de prueba.
      * Cada sprint tiene un resultado ejecutable.
      * Cada sprint recibe una firma del cliente (prueba estructurada mínima con comentarios).
   * Planee la posibilidad de actualizar la versión de AEM disponible durante el proyecto.
   * Planifique pruebas y optimización durante las copias.
   * Planee las fases de estabilización y optimización.
   * Cree un registro de los elementos que se planearán para futuras versiones.
   * Planee la participación y entrega de socios.


* **Infraestructura**

   * Defina primero la arquitectura base:

      * Defina los requisitos de rendimiento.
      * Defina los objetivos de rendimiento (es decir, defina claramente las expectativas).
      * Definir la arquitectura de hardware e infraestructura; incluido el tamaño.
      * Defina la implementación.
   * Utilizar varias iteraciones; para el primer sprint y la configuración inicial prepare:

      * Entorno de desarrollo.
      * Proceso de desarrollo.
      * Entorno de prueba.
      * Proceso de implementación (incluida la administración de la configuración).
   * Planifique varias pruebas de carga.
   * Planifique pruebas y optimización durante las copias.
   * Planee una fase de estabilización y optimización.
   * Implemente en el entorno de producción lo antes posible (permita que el equipo de operaciones configure el sistema para obtener experiencia).
   * Utilice los usuarios con nombre y las funciones definidas lo antes posible.
   * Planee la formación (por ejemplo, formación de administrador).
   * Planifique la transferencia a las operaciones.



* **Contenido**

   * La arquitectura básica:
      * Controla la jerarquía de contenido.
      * Ayuda a definir el concepto de contenido.
      * Define el uso y el diseño de los MSM.
      * Define funciones, grupos, flujos de trabajo y permisos.
   * Considere la utilidad de crear páginas sin conexión.
   * Planee la creación temprana de las primeras páginas y el contenido (para su uso en pruebas y comentarios).
   * Planee la migración del contenido existente.
   * Planee la &quot;migración en sprint&quot; después de la refactorización.
   * Planee la &quot;descarga de contenido&quot; (mapa del sitio para contenido de lanzamiento).

## Calcular el tiempo y el esfuerzo {#estimating-time-and-effort}

En función de la lista de tareas resultante, puede realizar estimaciones iniciales de tiempo y esfuerzo para definiciones de tareas (de alto nivel). Esto debe incluir una indicación de quién (cliente o socio) hará qué y cuándo.

En la lista siguiente se muestran las aproximaciones estándar y las interrelaciones de esfuerzo que se requieren y, por lo tanto, los costos:

>[!CAUTION]
>
>Estas cifras sólo pueden utilizarse para las estimaciones iniciales. Un desarrollador experimentado de AEM debe realizar un análisis detallado.

| Fase | Esfuerzo |
|---|---|
| Desarrollo | Una estimación aproximada de 2 a 4 horas para cada nodo de componente cubrirá todos los requisitos de desarrollo. |
| Prueba de desarrollador | 15% del desarrollo |
| Seguimiento | 10% del desarrollo |
| Documentación | 15% del desarrollo |
| Documentación de JavaDoc | 10% del desarrollo |
| Corrección de errores | 15% del desarrollo |
| Administración de proyectos | 20% de los costos de los proyectos para la gestión y gestión de proyectos en curso |

La planificación detallada puede relacionar los recursos disponibles o necesarios con los plazos y los costos.

## Arquitectura de referencia {#reference-architecture}

La arquitectura de referencia se proporciona para proporcionar una solución de plantilla para la arquitectura AEM. La arquitectura de referencia aborda los problemas que se suelen encontrar en los sistemas empresariales, como la escala, la fiabilidad y la seguridad.

Se deben definir las siguientes métricas del sitio:

| Clasificación | Definición |
|---|---|
| Número de sitios de Internet |  |
| Número de sitios de intranet |  |
| Número de bases de código (por ejemplo, si Internet e intranet difieren) |  |
| Número de páginas individuales |  |
| Número de visitas al sitio / día |  |
| Número de vistas de página / día |  |
| Volumen (en GB) de transferencia de datos / día |  |
| Número de usuarios simultáneos (grupo de usuarios cerrado) |  |
| Número de visitantes simultáneos (publicación) |  |
| Número de autores simultáneos |  |
| Número de autores registrados |  |
| Número de activaciones de página / día laborable |  |
| Número de activaciones de página durante la implementación |  |

## Visión General de las Herramientas Potenciales {#overview-of-potential-tools}

Se proporciona la siguiente lista para informarle de las herramientas que se pueden utilizar. Está pensada como una introducción, no como una extensa lista de recomendaciones, y ciertamente no debería disuadirle de utilizar otras herramientas que prefiera.

<table>
 <tbody>
  <tr>
   <td><strong>Producto</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>La propia AEM proporciona una serie de mecanismos que le ayudan a supervisar, probar, investigar y depurar su aplicación; incluyendo:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modo de desarrollador</a></li>
     <li>La Consola <a href="/help/sites-developing/hobbes.md">de pruebas</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Tablero de operaciones</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Perspectiva de contenido</a></li>
     <li>El árbol <a href="/help/sites-authoring/author-environment-tools.md#content-tree">de contenido</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selenio</td>
   <td><a href="https://docs.seleniumhq.org/">Selenium</a> es una herramienta de prueba Open Source. Las pruebas se ejecutan directamente en el explorador, emulando el funcionamiento de los usuarios.</td>
  </tr>
  <tr>
   <td>Microsoft Project</td>
   <td>Una herramienta de gestión de proyectos de uso común.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> es una herramienta de código abierto para rastrear y administrar los detalles de sus errores de software. Los flujos de trabajo se pueden imponer a los detalles del error según sea necesario.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> es un software de control de revisión.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse es un IDE de código abierto, compuesto por varios proyectos. Se centran en la creación de una plataforma de desarrollo abierta compuesta de marcos, herramientas y tiempos de ejecución ampliables para la creación, implementación y administración de software durante todo el ciclo de vida.</p> <p>Consulte <a href="/help/sites-developing/howto-projects-eclipse.md">Cómo desarrollar proyectos de AEM con Eclipse</a> para obtener más información.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Un IDE profesional (y, por lo tanto, responsable de los costes de licencia) que ofrece una amplia gama de características. </p> <p>Consulte <a href="/help/sites-developing/ht-intellij.md">Cómo desarrollar proyectos de AEM con IntelliJ IDEA</a> para obtener más información.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> es una herramienta de gestión y comprensión de proyectos de software que puede administrar el proceso de construcción de un proyecto (software y documentación).</td>
  </tr>
 </tbody>
</table>

## Lectura adicional {#further-reading}

Además, las siguientes secciones son de particular interés:

* [Introducción](/help/sites-deploying/deploy.md#getting-started)
* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Monitoreo y mantenimiento de la instancia](/help/sites-deploying/monitoring-and-maintaining.md)

### Prácticas recomendadas {#best-practices}

Adobe ofrece otras optimizaciones para todas las fases y audiencias:

* [Implementación](/help/sites-deploying/best-practices.md)
* [Creación](/help/sites-authoring/best-practices.md)
* [Administración](/help/sites-administering/administer-best-practices.md)
* [Desarrollo de](/help/sites-developing/best-practices.md)
* [Administración de proyectos](/help/managing/best-practices.md)