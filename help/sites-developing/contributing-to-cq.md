---
title: AEM Contribución a la
description: AEM El desarrollo de la se basa en metodologías comprobadas que se practican habitualmente en grandes proyectos de código abierto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2635'
ht-degree: 0%

---

# AEM Contribución a la{#contributing-to-aem}

## Metodología de desarrollo {#development-methodology}

AEM El desarrollo de la se basa en metodologías probadas que se practican habitualmente en grandes proyectos de código abierto. AEM Muchos de los elementos principales de la pila de tecnología de la se mantienen de hecho como proyectos activos de código abierto, como Sling y Jackrabbit, que fueron aportados a la Apache Software Foundation. AEM Un aspecto importante de este espíritu que está presente en la es que se le anima a utilizar las listas de correo y los foros en línea disponibles para interactuar directamente con el equipo de desarrollo.

AEM AEM Si está contribuyendo a los componentes de un proyecto de código abierto, familiarícese con los componentes de un proyecto de código abierto y póngase en contacto con el equipo principal existente del mismo modo que lo haría cuando tuviera intención de contribuir a un proyecto de este tipo.

## Experiencia requerida {#required-experience}

El Protocolo de transferencia de hipertexto (HTTP) es fundamental para todo lo que hacemos. AEM Por lo tanto, antes de contribuir a la, debe tener una comprensión profunda de HTTP, idealmente en la medida en que pueda escribir su propia implementación Java™ de un servidor HTTP multiproceso con agrupación de subprocesos. También debe comprender el comportamiento de la conexión persistente HTTP/1.1 y debe tener un conocimiento profundo de las interacciones del lado del servidor/cliente con JavaScript AJAX, especialmente el estilo asincrónico de interacción representado por la función de conexión de red de servidor de tipo.

Dado que el dinamismo de la página y el contenido interactivo son clave para la experiencia de WM, es esencial que tenga una comprensión bastante profunda del Modelo de objetos de documento y su potencial para la manipulación programática en respuesta a eventos. Debería tener algún conocimiento, por ejemplo, de la manipulación DOM en tiempo real y del comportamiento de arrastrar y soltar sobre varios documentos del explorador (por ejemplo, mediante iframes).

En el nivel más alto, debería comprender bien lo siguiente:

* el [protocolo HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferiblemente [HTML 5](https://html.spec.whatwg.org/))
* Hojas de estilos en cascada
* Lenguaje de marcado extensible (XML)
* Patrones de diseño asíncronos de JavaScript AJAX y XML ()
* Notación de objetos de JavaScript (JSON)
* el modelo de objetos de documento
* Interacciones con estado frente a sin estado
* [Identificadores uniformes de recursos](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies del explorador
* y otros conceptos modernos de desarrollo web

La pila de tecnología de Adobe Experience Manager se basa en el contenedor OSGI [Apache Felix](https://felix.apache.org/documentation/index.html) con el marco web [Apache Sling](https://sling.apache.org/index.html) e incrusta un repositorio de contenido Java™ ([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)) basado en [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html). Familiarícese con estos proyectos individuales y con cualquier otro componente de código abierto (por ejemplo, Apache Lucene) que se utilice en el área en la que pretenda contribuir.

## Conocimiento tribal {#tribal-knowledge}

Ciertos conceptos y principios rectores están profundamente arraigados en la antigua cultura del Día. En esta sección se enumeran algunos de los problemas &quot;profundamente insertados en el ADN&quot; que debe tener en cuenta.

### Todo está contenido {#everything-is-content}

El contenido incluye no solo todos los datos que mantiene la aplicación web. El código de programa, las bibliotecas, los scripts, las plantillas, el HTML, el CSS, las imágenes y los artefactos de todo tipo, cualquier cosa y todo se mantienen en el repositorio de contenido y se importan o exportan en forma de paquetes a través del administrador de paquetes y el uso compartido de paquetes.

### El modelo de David {#david-s-model}

La forma en que el contenido debe modelarse en un repositorio de contenido Java™ requiere una forma de pensar completamente diferente a la práctica habitual en la industria del software para el modelado de datos en el mundo relacional. La lectura esencial para cualquier recién llegado a la administración de contenido de la manera JCR es [David&#39;s Model: A guide for content modeling](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

El enfoque REST está profundamente arraigado en lo que hacemos. Esto significa, entre otras cosas, evitar interacciones con estado y tener en cuenta que los URI son direcciones definitivas para el contenido y los servicios.

REST (REpresentational State Transfer) hace referencia al estilo arquitectónico de software en el que se basa la World Wide Web. Describe los elementos clave que hacen que la Web funcione y proporciona un conjunto de principios para el diseño del software basado en la Web. Por lo tanto, al diseñar una API para utilizarla en la web, tiene sentido adherirse a estas &quot;prácticas recomendadas&quot;.

Debido a que REST proporciona la filosofía guía detrás de gran parte de lo que hacemos, debe considerar esencial estar bien versado en los principios del diseño RESTful. Un buen punto de partida es la [tesis de Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Resolución de solicitud de Sling {#sling-request-resolution}

AEM AEM Un aspecto clave para comprender el contenido es cómo se relacionan las solicitudes entrantes con el comportamiento del contenido y la aplicación, cómo se estructura el contenido en el repositorio de contenido y dónde busca la lógica de la aplicación para gestionar la solicitud. Obtenga información acerca de la descomposición de la URL de Apache [Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html) y la forma en que aplica el estilo arquitectónico REST y sus restricciones del sistema sin estado, almacenables en caché y por capas.

Los aspectos clave para comprender la resolución de solicitudes de Apache Sling son cómo las solicitudes se asignan principalmente a un recurso específico en el repositorio de contenido, cómo las propiedades adicionales de la solicitud, junto con las propiedades de estos objetos de contenido, determinan qué código de aplicación se invoca para procesar el contenido y cómo el código de /apps anula el código de /libs.

### Guía de inicio rápido {#quickstart}

Sin tercer paso: Para instalar y ejecutar, simplemente se descarga y se hace doble clic en el archivo JAR de Quickstart. No hay paso tres. Cualquier funcionalidad opcional adicional no debería requerir nada más que la instalación del paquete apropiado desde Package Share.

Tamaño pequeño de Quickstart: mantenga el tamaño mínimo del archivo JAR de Quickstart. Haga un uso inteligente y optimizado de las bibliotecas, trasladando la funcionalidad opcional a Uso compartido de paquetes.

Tiempo de inicio más rápido: cuando realice un cambio que pueda afectar al tiempo de inicio, asegúrese de que sea más corto, no más largo.

### Inclinación y media {#lean-and-mean}

Favorecemos códigos y proyectos que sean ligeros, pequeños, rápidos y elegantes. &quot;Lo suficientemente bueno&quot; no es suficiente.

Reutilización del código: nuestra arquitectura de productos basada en OSGi y la filosofía de &quot;todo es contenido&quot; significan que tenemos oportunidades inusualmente buenas para reutilizar código y artefactos. Tratamos de aprovechar ese hecho siempre que sea posible para mantener las características limpias y medias.

Acoplamiento suelto: Favorecemos las interacciones de acoplamiento flexible sobre las dependencias estrechas y la &quot;intimidad no deseada&quot;. El acoplamiento suelto también permite una mayor reutilización del código.

### No interrumpa la demostración {#don-t-break-the-demo}

Familiarícese con los scripts de demostración y las funcionalidades de producto que se muestran con más frecuencia en las demostraciones. Tenga en cuenta que nada de lo que haga debería interrumpir la función de &quot;script de demostración&quot;. El producto principal siempre debe estar listo para la demostración, incluso durante el desarrollo.

### Diseño para la fiabilidad {#design-for-reliability}

Nos esforzamos por diseñar y codificar las funciones de forma flexible, de modo que (por ejemplo) un problema con un solo elemento DOM no cause que una página entera no se procese. En otras palabras: Hacer cosas que deberían ser fatales, fatales. Haz que todo lo demás sobreviva. Haga que el producto sea &quot;indulgente&quot;.

### Anormal es la nueva normalidad {#abnormal-is-the-new-normal}

No dependa de los enlaces de apagado, asegúrese de realizar la limpieza al iniciar. La terminación anormal es la terminación normal.

`shutdown == kill -9 == power outage`

### Prepárese para la agrupación elástica {#be-ready-for-elastic-clustering}

Esté siempre listo para el agrupamiento elástico; siempre suponga que hay un agrupamiento. Por lo general, cumplir con todo lo que se encuentra en el repositorio de contenido significa admitir clústeres.

### Diseño para compatibilidad con versiones anteriores {#design-for-backward-compatibility}

Nada de lo que haga debe romper el código antiguo de un cliente. Considere solamente `/libs` para que contenga código de producto que se pueda actualizar durante una actualización. La sección `/apps` del repositorio es código de proyecto y la sección `/etc` contiene configuraciones personalizadas que deben conservarse. Por lo general, no sobrescriba nada en `/apps`, `/content` ni `/home`. Después de una actualización, el código de proyecto, las configuraciones y el contenido antiguos deben seguir funcionando como antes de la actualización.

El diseño para la compatibilidad con versiones anteriores también garantiza que la experiencia de actualización coincida con la simplicidad de la instalación inicial. AEM AEM Solo tiene que detener la, sustituir el archivo JAR de inicio rápido y volver a empezar a utilizar el archivo de inicio de la aplicación, debería ser suficiente. Con una base de instalación en rápido crecimiento, la eficiencia de la actualización es una ventaja cada vez más significativa.

Aunque las API existentes pueden y deben marcarse como obsoletas cuando las nuevas y mejores funciones las sustituyen, todas las API que se hicieron públicas en una versión 5.x anterior deben seguir funcionando, ya que pueden estar en uso en el código de aplicación personalizado. Estas API no deben eliminarse.

La compatibilidad con versiones anteriores también debe tenerse en cuenta con respecto a la coherencia general de la estructura de contenido y la experiencia del usuario.

## Conceptos principales {#core-concepts}

**Instancia de autor**: normalmente, por motivos de seguridad, gobernanza y de otro tipo, un sitio de producción divide las instancias de creación en instancias de autor y de Publish para las instancias de creación de la instancia de creación de la instancia de creación de la instancia de creación de la instancia de creación de la instancia de creación de la instancia de creación de AEM. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/Publish AEM), consulte la documentación sobre instancias de.

**Almacenamiento en caché, freír y hornear**: Tradicionalmente, los conceptos de hornear y freír son una distinción importante entre los distintos sistemas de administración de contenido web. En la jerga de CMS, &quot;procesamiento&quot; se refiere al concepto de comprometer datos en archivos estáticos en el momento de la publicación, mientras que &quot;freír&quot; se refiere al concepto de procesar datos para la presentación final en el momento de la solicitud (es decir, justo a tiempo).

**Clúster y equilibrio de carga**: para aumentar la disponibilidad y mejorar el rendimiento de un entorno de producción, es común combinar varias instancias de autor o Publish (en clústeres), poniéndolas a disposición de diferentes grupos de usuarios o equilibrándolas de carga detrás de una configuración de Dispatcher.

AEM También es posible combinar varias instancias del repositorio de contenido para crear una solución JCR de *alta disponibilidad*, que luego se puede integrar con su solución de para maximizar la protección contra fallos de hardware y software. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obtener más información.

AEM **Componente**: en la práctica, un componente es un tipo de objeto, cuyas instancias generalmente se pueden crear arrastrándolas y soltándolas desde, por ejemplo, el Sidekick. AEM Por ejemplo, los componentes listos para usar que se envían con los componentes Texto, Título, Nube de etiquetas, Carrusel, Imagen y Lista, todos disponibles en el Sidekick durante la ejecución.

**Buscador de contenido**: en el modo de creación, el Buscador de contenido es un panel especial (marco) en el lado izquierdo de la página que, según la pestaña que seleccione en la parte superior, muestra listas de imágenes, documentos, recursos de Flash, páginas, párrafos o recursos del repositorio que puede arrastrar y soltar desde el Buscador de contenido en la página en la que está trabajando (a la derecha).

AEM **Recursos digitales**: en la práctica, los Assets digitales son (por lo general) imágenes y archivos multimedia enriquecidos. Para obtener más información, consulte Trabajar con Digital Assets en DAM.

**Dispatcher**: Dispatcher es una herramienta de almacenamiento en caché y de equilibrio de carga, y proporciona ciertas protecciones de seguridad.

AEM **Widgets de ExtJS**: la mayoría de los elementos de la interfaz de usuario de los que se dispone utilizan en el uso de ExtJS, que es una biblioteca de widgets de terceros escrita en JavaScript. ExtJS ofrece un alto rendimiento, widgets de interfaz de usuario personalizables y un modelo de componentes bien diseñado y ampliable.

**JCR, repositorio de contenido Java™**: la especificación del repositorio de contenido Java™ (JSR-283) proporciona un modelo de datos abstracto y una interfaz de programación de aplicaciones para crear un repositorio de datos NoSQL escalable que combina características de un sistema de archivos y una base de datos de objetos. AEM Aunque no necesita comprender JSR-283 con detalle exhaustivo, debe dedicar tiempo a familiarizarse con las capacidades básicas de JCR y con el modelo de datos subyacente, ya que JCR es lo que hace posible la filosofía de &quot;todo es contenido&quot; de la.

En esencia, JCR es un sistema de nodos y propiedades, en el que los nodos pueden heredar de otros nodos y todo el contenido se almacena como propiedad *values*. Tenga en cuenta que, además de la herencia ordinaria, JCR permite un concepto de nodos de &quot;mezcla&quot;, que permite modelar la herencia múltiple.

JCR tiene varios tipos de nodos predefinidos y tipos de propiedades, pero en general el sistema de escritura es flexible, y (de hecho) una de las fortalezas de JCR es que permite almacenar/administrar contenido estructurado y no estructurado con igual facilidad. Es decir, JCR puede admitir datos altamente estructurados, pero también puede admitir estructuras de datos dinámicas arbitrarias sin restricciones de esquema.

El JavaDoc para la API Java™ de JCR es [aquí](https://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de intentar leer el JavaDoc o la propia especificación JCR, es posible que quiera ver [esta explicación de alto nivel](/help/sites-developing/the-basics.md#java-content-repository) de JCR implementada por los servicios de Adobe Experience.

AEM **Administrador de varios sitios (MSM)**: la función MSM de ayuda a los clientes a gestionar contenido multilingüe y multinacional, lo que les permite equilibrar la promoción de la marca centralizada con el contenido localizado.

AEM **OSGi**: OSGi es la tecnología de tiempo de ejecución basada en servicios que proporciona la base para el desarrollo modular de Java™ en el espacio de trabajo de los usuarios de la red de área de trabajo de. Es un marco de trabajo que proporciona no solo un entorno de carga de clases y ejecución altamente dinámico (y seguro) para los recursos de código (conocidos como paquetes), sino también un control total sobre la visibilidad y el ciclo de vida de los distintos servicios expuestos por los paquetes. Un registro de servicios proporciona un modelo de cooperación para paquetes que tiene en cuenta la dinámica del ciclo vital (y los requisitos de versión). OSGi resuelve muchos de los problemas que los servidores de aplicaciones pretendían resolver, pero lo hace de una manera ligera y altamente dinámica, lo que permite, por ejemplo, implementar servicios en caliente (haciendo que el nuevo código esté disponible inmediatamente sin reiniciar el servidor).

**Parsys, Paragraph System**: el sistema de párrafos (parsys) es un componente compuesto que permite a los autores agregar componentes de diferentes tipos a una página y contiene otros componentes de párrafo. Cada tipo de párrafo se representa como un componente. El sistema de párrafos en sí también es un componente, que contiene los demás componentes de párrafo.

**Microkernel**: cada espacio de trabajo del repositorio se puede configurar por separado para almacenar sus datos a través de un microkernel específico (una clase que administra la lectura y escritura de los datos). Del mismo modo, el almacén de versiones en todo el repositorio también puede configurarse de forma independiente para utilizar un microkernel en particular. Hay varios microkernels diferentes disponibles, capaces de almacenar datos en varios formatos de archivo o bases de datos relacionales. (Por ejemplo, hay administradores de persistencia para MongoDB, DB2® o Oracle AEM) El microkernel predeterminado para la creación de un núcleo es TarMK (ver más abajo).

**Instancia de Publish AEM**: por motivos de seguridad, gobernanza y de otro tipo, un sitio de producción suele dividir las instancias de la en instancias de autor y de Publish. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/Publish AEM), consulte la documentación sobre instancias de.

AEM **Quickstart**: a diferencia de muchos otros programas, la instalación se realiza utilizando un solo archivo JAR autoextraíble de &quot;Quickstart&quot;. Cuando haga doble clic en el archivo JAR por primera vez, todo lo que necesite se instalará automáticamente. El JAR de inicio rápido incluye todos los archivos necesarios para el repositorio de CRX AEM (incluidos los servicios administrativos), los servicios de repositorio virtual, los servicios de índice y búsqueda, los servicios de flujo de trabajo, la seguridad y un servidor web, además del motor de servlets CQ (CQSE) y todos los servicios de. No hay otros archivos que instalar: Quickstart es independiente.

La primera vez que se inicia el Inicio rápido, se crea un repositorio compatible con JCR completo en segundo plano, lo que puede tardar varios minutos. Después de este inicio inicial, los inicios posteriores son mucho más rápidos, ya que la infraestructura del repositorio ya se ha establecido.

AEM Muchas opciones de inicio (como el número de puerto activo y si la instancia de inicio en cuestión debe ser una instancia de Publish en lugar de una instancia de autor; y mucho más) se pueden controlar cambiando el nombre del archivo de inicio rápido de la forma adecuada. Para ver una lista de opciones a este respecto, ejecute el JAR con &quot;-help&quot; en la línea de comandos:

```shell
java -jar <quickstartfilename>.jar -help
```

AEM **Agentes de replicación**: los agentes de replicación son fundamentales para su uso como mecanismo para la activación del contenido de Publish de un autor a un entorno de publicación; el vaciado del contenido de la caché de Dispatcher; la devolución del contenido generado por el usuario (por ejemplo, la entrada de formulario) desde el entorno de Publish al entorno de creación.

**Andamiaje**: con el andamiaje puede crear un formulario (un andamiaje) con campos que reflejen la estructura que desee para sus páginas y, a continuación, utilizar este formulario para crear fácilmente páginas basadas en esta estructura.

**Segmentación**: Los visitantes del sitio tienen intereses y objetivos diferentes cuando llegan a un sitio. Comprender los objetivos de los visitantes y cumplir sus expectativas es un requisito previo importante para el éxito del marketing en línea. La segmentación ayuda a conseguirlo al analizar y caracterizar los detalles de un visitante.

**Sidekick**: el Sidekick es una ventana flotante de tipo paleta que aparece en la página editable, desde la cual se pueden arrastrar nuevos componentes y se pueden ejecutar acciones que se apliquen a la página.

**Site Catalyst**: SiteCatalyst proporciona a los especialistas en mercadotecnia un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de mercadotecnia. Puede utilizar Adobe SiteCatalyst AEM para analizar datos de sitios web de la.

AEM **Almacenamiento de Tar (TarMK)**: TarMK es el sistema de persistencia predeterminado en los entornos de almacenamiento de la base de datos de. AEM Aunque se puede configurar para que utilice un sistema de persistencia diferente (como MongoDB), TarMK tiene ciertas ventajas, ya que está optimizado para el rendimiento de casos de uso típicos de JCR (por lo tanto, es rápido), utiliza un formato de datos estándar en la industria y se puede realizar una copia de seguridad rápida y fácilmente.

AEM **Plantilla**: en el código de tiempo, una plantilla especifica un tipo concreto de página. Define la estructura de una página (a la vez que especifica una imagen en miniatura y varias propiedades). Por ejemplo, puede tener plantillas independientes para páginas de productos, mapas del sitio e información de contacto.

AEM **Flujo de trabajo**: el sistema de flujo de trabajo de permite la creación de procesos automatizados que involucran páginas o recursos.
