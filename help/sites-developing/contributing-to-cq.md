---
title: Contribución a AEM
seo-title: Contributing to AEM
description: AEM se desarrolla siguiendo metodologías probadas que comúnmente se practican en grandes proyectos de código abierto
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 1%

---

# Contribución a AEM{#contributing-to-aem}

## Metodología de desarrollo {#development-methodology}

AEM se desarrolla siguiendo metodologías probadas que se practican comúnmente en grandes proyectos de código abierto. Muchos elementos principales de AEM pila de tecnología se mantienen como proyectos activos de código abierto, como Sling y Jackrabbit, que fueron aportados a la Apache Software Foundation. Un aspecto importante de este espíritu que está presente en AEM es que se le anima a utilizar las listas de correo y los foros en línea disponibles para interactuar directamente con el equipo de desarrollo.

Si está contribuyendo a componentes de AEM, debe familiarizarse con AEM como lo haría al contribuir a un proyecto de código abierto y comunicarse con el equipo principal existente como lo haría cuando tuviera la intención de contribuir a dicho proyecto.

## Experiencia requerida {#required-experience}

El Protocolo de transferencia de hipertexto (HTTP) es fundamental para todo lo que hacemos. Por lo tanto, antes de contribuir a AEM, debe tener una comprensión profunda de HTTP, idealmente en la medida en que sea capaz de escribir su propia implementación Java de un servidor HTTP multiproceso con agrupación de subprocesos. También debe comprender el comportamiento de mantenimiento de HTTP/1.1 y tener un conocimiento profundo de las interacciones del lado del servidor/cliente con JavaScript, especialmente el estilo asincrónico de interacción representado por AJAX.

Dado que el dinamismo de la página y el contenido interactivo son clave para la experiencia de WM, es esencial que tenga una comprensión bastante profunda del Modelo de objetos de documento y su potencial de manipulación programática en respuesta a los eventos. Debería tener algún conocimiento, por ejemplo, de la manipulación DOM en tiempo real y del comportamiento de arrastrar y soltar en varios documentos del navegador (por ejemplo, utilizando iframes).

En el nivel más alto, debe tener una comprensión sólida de:

* el protocolo [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferiblemente [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Hojas de estilo en cascada
* Lenguaje de marcado extensible (XML)
* Patrones de diseño asincrónicos de JavaScript y XML (AJAX)
* Notación de objetos JavaScript (JSON)
* Modelo de objetos de documento
* Interacciones apátridas frente a apátridas
* [Identificadores de recursos uniformes](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies del explorador
* y otros conceptos modernos de desarrollo web

La pila de tecnología de Adobe Experience Manager se basa en el contenedor OSGI [Apache Felix](https://felix.apache.org/) con el marco web [Apache Sling](https://sling.apache.org/site/index.html) e incrusta un repositorio de contenido Java ([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)) basado en [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Debe familiarizarse con estos proyectos individuales, así como con cualquier otro componente de código abierto (por ejemplo, Apache Lucene) utilizado en el área en la que desee contribuir.

## Conocimiento tribal {#tribal-knowledge}

Ciertos conceptos y principios rectores están profundamente arraigados en la cultura del antiguo Día. Esta sección enumera algunos de los problemas &quot;profundamente incrustados en el ADN&quot; que debe tener en cuenta.

### Todo es contenido {#everything-is-content}

El contenido incluye no solo todos los datos que persiste la aplicación web. El código de programa, las bibliotecas, las secuencias de comandos, las plantillas, el HTML, CSS, las imágenes y los artefactos de todo tipo se mantienen en el repositorio de contenido y se importan/exportan en forma de paquetes mediante el Administrador de paquetes y Uso compartido de paquetes.

### El modelo de David {#david-s-model}

La forma en que el contenido debe ser modelado en un Repositorio de Contenido Java requiere una forma de pensar completamente diferente a la práctica habitual en el sector de software para modelado de datos en el mundo relacional. La lectura esencial para cualquier recién llegado a la gestión de contenido es el modelo de David: Una guía para el modelado de contenido](https://wiki.apache.org/jackrabbit/DavidsModel).[

### RESTful {#restfulness}

El enfoque del REST está profundamente arraigado en lo que hacemos. Esto significa, entre otras cosas, evitar interacciones con las declaraciones y tener en cuenta que las URI son direcciones definitivas para el contenido y los servicios.

REST (REpresentational State Transfer) se refiere al estilo arquitectónico del software en el que se basa la World Wide Web. Describe los elementos clave que hacen que la web funcione y, por lo tanto, proporciona un conjunto de principios sobre cómo se debe diseñar el software basado en la web. Al diseñar una API para utilizarla en la web, tiene sentido adherir a estas &quot;prácticas recomendadas&quot;.

Debido a que REST proporciona la filosofía guía detrás de mucho de lo que hacemos, usted debería considerar esencial conocer bien los principios del diseño RESTful. Un buen lugar para empezar es con la tesis de Roy Field](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).[

### Resolución de solicitudes de Sling {#sling-request-resolution}

Un aspecto clave para comprender AEM es cómo se relacionan las solicitudes entrantes con el contenido y el comportamiento de la aplicación, cómo se estructura el contenido en el repositorio de contenido y dónde AEM la lógica de la aplicación para gestionar la solicitud. Obtenga información sobre la descomposición de la URL de Apache [Sling](https://sling.apache.org/site/url-decomposition.html) y la forma en que aplica el estilo arquitectónico de REST y sus restricciones de sistema sin estado, almacenables en caché y en capas.

Los aspectos clave para comprender la resolución de solicitudes de Apache Sling son cómo las solicitudes se asignan principalmente a un recurso específico del repositorio de contenido, cómo las propiedades adicionales de la solicitud, junto con las propiedades de estos objetos de contenido, determinan qué código de aplicación se invocará para procesar el contenido y cómo el código en /apps anula el código en /libs.

### Guía de inicio rápido {#quickstart}

No es el paso tres: Para instalar y ejecutar, simplemente descarga y hace doble clic en el archivo JAR de inicio rápido. No hay paso tres. Cualquier funcionalidad opcional adicional debe requerir nada más que instalar el paquete apropiado desde Package Share.

Tamaño de inicio rápido pequeño: Mantenga el tamaño del archivo JAR de inicio rápido como mínimo. Utilice de forma inteligente y optimizada las bibliotecas, moviendo la funcionalidad opcional al uso compartido de paquetes.

Tiempo de inicio más rápido: Cuando realice un cambio que pueda afectar al tiempo de inicio, asegúrese de que sea más corto, no más largo.

### Lean y Media {#lean-and-mean}

Somos partidarios del código y los proyectos que son ligeros, pequeños, rápidos y elegantes. &quot;Suficiente&quot; no es suficiente.

Reutilización de código: Nuestra arquitectura de producto basada en OSGi y la filosofía de &quot;todo es contenido&quot; significa que tenemos oportunidades inusualmente buenas para reutilizar código y artefactos. Tratamos de aprovechar ese hecho siempre que sea posible para mantener las características en blanco y negro.

Acoplamiento suelto: Somos partidarios de interacciones unidas de manera flexible sobre dependencias ajustadas e &quot;intimidad no deseada&quot;. El acoplamiento flexible también permite una mayor reutilización del código.

### No rompas la demostración {#don-t-break-the-demo}

Familiarícese con los scripts de demostración y las funcionalidades de producto que se muestran con más frecuencia en las demostraciones. Comprenda que, como mínimo, nada que haga debe romper la función de &quot;script de demostración&quot;. El producto principal siempre debe estar listo para la demostración, incluso durante el desarrollo.

### Diseño para confiabilidad {#design-for-reliability}

Nos esforzamos por diseñar y codificar las funciones de manera que no se procese correctamente, de modo que (por ejemplo) un problema con un solo elemento DOM no cause que una página entera no se represente. En otras palabras: Hagan cosas que sean fatales, mortales. Hagan que todo lo demás sobreviva. Haga que el producto sea &quot;indulgente&quot;.

### La anormalidad es la nueva normalidad {#abnormal-is-the-new-normal}

No dependa de los enlaces de apagado, asegúrese de la limpieza al inicio. La terminación anormal es una terminación normal.

`shutdown == kill -9 == power outage`

### Prepárese para la agrupación en clústeres elásticos {#be-ready-for-elastic-clustering}

Siempre esté listo para la agrupación elástica, siempre suponga que hay agrupación en clúster. Como regla general, cumplir con todo lo que se encuentra en el repositorio de contenido significa que es compatible con clústeres integrados.

### Diseño para compatibilidad con versiones anteriores {#design-for-backward-compatibility}

Nada que haga debería romper el código antiguo de un cliente. Considere solo `/libs` para contener código de producto que se pueda actualizar durante una actualización. La sección `/apps` del repositorio es código de proyecto, y la sección `/etc` contiene configuraciones personalizadas que deben preservarse. Por lo general, no sobrescriba nada en `/apps`, `/content` y `/home`. Después de una actualización, el código del proyecto antiguo, las configuraciones y el contenido deben seguir funcionando como siempre antes de la actualización.

El diseño para la compatibilidad con versiones anteriores también garantiza que la experiencia de actualización coincida con la simplicidad de la instalación inicial. Basta con detener AEM, reemplazar el archivo JAR de inicio rápido e iniciar AEM de nuevo. Con una base de instalación de rápido crecimiento, la eficiencia de la actualización será una ventaja cada vez más significativa.

Aunque las API existentes se pueden y se deben marcar como obsoletas cuando una funcionalidad más reciente las reemplaza, todas las API que se hicieron públicas en una versión anterior de 5.x deben seguir funcionando, ya que es posible que se usen en código de aplicación personalizado. Estas API no deben eliminarse.

También debe tenerse en cuenta la compatibilidad con versiones anteriores en lo que respecta a la coherencia general de la estructura de contenido y la experiencia del usuario.

## Conceptos principales {#core-concepts}

**Instancia de autor** : normalmente, por motivos de seguridad, gobernanza y otros, un sitio de producción dividirá las instancias de AEM en instancias de autor y publicación. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre AEM instancias.

**Almacenamiento en caché, fritura y hornear** : Tradicionalmente, los conceptos de hornear y fritar son una importante distinción entre los diferentes sistemas de administración de contenido web. En la jerga de CMS, &quot;agrupamiento&quot; se refiere al concepto de comprometer datos en archivos estáticos en el momento de la publicación, mientras que &quot;fritación&quot; se refiere al concepto de procesamiento de datos para la presentación final en el momento de la solicitud (es decir, justo a tiempo).

**Clustering y equilibrio de carga** : para aumentar la disponibilidad y mejorar el rendimiento de un entorno de producción, es común combinar varias instancias de creación y/o publicación (en clústeres), ya sea poniéndolas a disposición de diferentes grupos de usuarios o equilibrándolas de carga tras una configuración de Dispatcher.

También es posible combinar varias instancias del repositorio de contenido para crear una solución JCR *de alta disponibilidad*, que luego se puede integrar con su solución AEM para maximizar la protección contra fallos de hardware y software. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obtener más información.

**Componente** : en AEM, un componente es un tipo de objeto, cuyas instancias generalmente se pueden crear arrastrándolas y soltándolas desde, por ejemplo, la barra de tareas. Por ejemplo, los componentes listos para usar que se incluyen con AEM incluyen los componentes Texto, Título, Nube de etiquetas, Carrusel, Imagen y Lista, todos disponibles en la barra de tareas durante la ejecución.

**Buscador de contenido** : en el modo de creación, el Buscador de contenido es un panel especial (marco) en el lado izquierdo de la página que, según la pestaña que seleccione en la parte superior, muestra listas de imágenes, documentos, recursos de Flash, páginas, párrafos o recursos de repositorio que puede arrastrar y soltar desde el Buscador de contenido en la página en la que está trabajando (a la derecha).

**Recursos digitales** : en AEM, los recursos digitales son (normalmente) imágenes y archivos multimedia enriquecidos. Para obtener más información, consulte Uso de recursos digitales en DAM.

**Dispatcher** : Dispatcher es una herramienta de almacenamiento en caché y de equilibrio de carga, además de proporcionar ciertas salvaguardias de seguridad.

**Widgets de ExtJS** : la mayoría de los elementos de la interfaz de usuario de AEM utilizan ExtJS, que es una biblioteca de widgets de terceros escrita en JavaScript. ExtJS cuenta con utilidades de interfaz de usuario personalizables de alto rendimiento y un modelo de componentes ampliable y bien diseñado.

**JCR, Repositorio de contenido Java** : la especificación del Repositorio de contenido Java (JSR-283) proporciona un modelo de datos abstracto y una interfaz de programación de aplicaciones para realizar un repositorio de datos NoSQL con capacidad de ampliación masiva que combina características de un sistema de archivos y una base de datos de objetos. Aunque no necesita comprender el JSR-283 con detalle, debe tomarse tiempo para familiarizarse con las capacidades básicas de JCR y el modelo de datos subyacente, ya que JCR es lo que hace posible la filosofía de AEM &quot;todo es contenido&quot;.

En esencia, JCR es un sistema de nodos y propiedades, en el que los nodos pueden heredar de otros nodos y todo el contenido se almacena como propiedad *values*. Tenga en cuenta que, además de la herencia ordinaria, JCR permite un concepto de nodos &quot;mixtos&quot;, que permite modelar la herencia múltiple.

JCR tiene varios tipos de nodos predefinidos y tipos de propiedades, pero en general el sistema de escritura es bastante flexible, y (de hecho) una de las ventajas de JCR es que permite almacenar/administrar contenido estructurado y no estructurado con la misma facilidad. Es decir, JCR puede admitir datos altamente estructurados, pero también puede admitir estructuras de datos dinámicas arbitrarias sin restricciones de esquema.

El JavaDoc para la API Java de JCR está [aquí](http://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de intentar leer el JavaDoc o la especificación JCR en sí, es posible que desee consultar [esta explicación de alto nivel](/help/sites-developing/the-basics.md#java-content-repository) de JCR implementada por Adobe Experience Services.

**Multi-Site Manager (MSM)** : La función MSM de AEM ayuda a los clientes a gestionar contenido multilingüe y multinacional, lo que les permite equilibrar la personalización centralizada con contenido localizado.

**OSGi** : OSGi es la tecnología de tiempo de ejecución basada en servicios que proporciona la base para el desarrollo de Java modularizado en AEM. Es un marco de trabajo que proporciona no solo un entorno de carga de clases y ejecución altamente dinámico (y seguro) para los recursos de código (conocidos como paquetes), sino también control total sobre la visibilidad y el ciclo de vida de los distintos servicios expuestos por paquetes. Un registro de servicios proporciona un modelo de cooperación para paquetes que tiene en cuenta la dinámica del ciclo vital (y los requisitos de versión). OSGi resuelve muchos de los problemas que los servidores de aplicaciones pretendían resolver, pero lo hace de una manera ligera y altamente dinámica, lo que permite, por ejemplo, implementar servicios en caliente (haciendo que el nuevo código esté disponible inmediatamente sin reiniciar el servidor).

**Parsys, sistema de párrafos** : el sistema de párrafos (parsys) es un componente compuesto que permite a los autores añadir componentes de distintos tipos a una página y contiene otros componentes de párrafos. Cada tipo de párrafo se representa como un componente. El propio sistema de párrafo también es un componente, que contiene los demás componentes del párrafo.

**Microkernel** : Cada espacio de trabajo en el repositorio puede configurarse por separado para almacenar sus datos a través de un micronúcleo específico (una clase que administra la lectura y escritura de los datos). Del mismo modo, el almacén de versiones de todo el repositorio también puede configurarse de forma independiente para utilizar un micronúcleo en particular. Hay varios microkernels disponibles, capaces de almacenar datos en diversos formatos de archivo o bases de datos relacionales. (Por ejemplo, hay gestores de persistencia para MongoDB, DB2 o Oracle) El micronúcleo predeterminado para AEM es TarMK (ver más abajo).

**Instancia de publicación** : por motivos de seguridad, control y otros, un sitio de producción suele dividir las instancias de AEM en instancias de autor y publicación. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre AEM instancias.

**Inicio rápido** : a diferencia de muchos otros programas, instala AEM utilizando un solo archivo JAR autoextraíble de &quot;inicio rápido&quot;. Cuando hace doble clic en el archivo JAR por primera vez, todo lo que necesita se instala automáticamente. El JAR de inicio rápido incluye todos los archivos necesarios para el repositorio CRX (incluidas las instalaciones administrativas), los servicios de repositorio virtual, los servicios de índice y búsqueda, los servicios de flujo de trabajo, la seguridad y un servidor web, además del motor Servlet CQ (CQSE) y todos los servicios de AEM. No hay otros archivos para instalar: el inicio rápido es independiente.

La primera vez que inicie el inicio rápido, creará un repositorio compatible con JCR completo en segundo plano, que puede tardar varios minutos. Después de este inicio inicial, las siguientes iniciaciones son mucho más rápidas, ya que la infraestructura del repositorio ya se ha establecido.

Muchas opciones de inicio (como el número de puerto activo y si la instancia de AEM en cuestión debe ser una instancia de publicación en lugar de una instancia de autor); y mucho más) se puede controlar cambiando el nombre del archivo de inicio rápido de forma adecuada. Para ver una lista de opciones a este respecto, ejecute el JAR con &quot;-help&quot; en la línea de comandos:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes de replicación** : los agentes de replicación son fundamentales para AEM como mecanismo utilizado para publicar (activar) contenido de un autor en un entorno de publicación; vaciar contenido de la caché de Dispatcher; devuelva contenido generado por el usuario (por ejemplo, entrada de formulario) desde el entorno Publicar al entorno Autor.

**Scaffolding** : con scaffolding, puede crear un formulario (un scaffold) con campos que reflejen la estructura que desee para sus páginas y luego usar este formulario para crear fácilmente páginas basadas en esta estructura.

**Segmentación** : los visitantes del sitio tienen diferentes intereses y objetivos cuando acceden al sitio. Comprender los objetivos de los visitantes y cumplir sus expectativas es un requisito previo importante para el marketing en línea. La segmentación ayuda a conseguirlo mediante el análisis y la caracterización de los detalles de un visitante.

**Barra de tareas** : la barra de tareas es una ventana flotante parecida a una paleta que aparece en la página editable y desde la cual se pueden arrastrar componentes nuevos y ejecutar acciones aplicables a la página.

**SiteCatalyst** : SiteCatalyst proporciona a los especialistas en marketing un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea a través de varios canales de marketing. Puede utilizar Adobe SiteCatalyst para analizar los datos de AEM sitios web.

**Almacenamiento Tar (TarMK)** : TarMK es el sistema de persistencia predeterminado en AEM. Aunque AEM puede configurarse para utilizar un sistema de persistencia diferente (como MongoDB), TarMK tiene ciertas ventajas en que está optimizado para el rendimiento para casos de uso JCR típicos (por lo tanto es muy rápido), utiliza un formato de datos estándar en el sector y puede ser respaldado rápida y fácilmente.

**Plantilla** : En AEM, una plantilla especifica un tipo concreto de página. Define la estructura de una página (aunque también suele especificar una imagen en miniatura y varias propiedades). Por ejemplo, puede tener plantillas diferentes para páginas de producto, mapas del sitio e información de contacto.

**Flujo de trabajo** : el sistema Flujo de trabajo AEM permite crear procesos automatizados que impliquen páginas o recursos.
