---
title: AEM Contribución a la
description: AEM El desarrollo de la se basa en metodologías comprobadas que se practican habitualmente en grandes proyectos de código abierto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2635'
ht-degree: 0%

---

# AEM Contribución a la{#contributing-to-aem}

## Metodología de desarrollo {#development-methodology}

AEM El desarrollo de la se basa en metodologías probadas que se practican habitualmente en grandes proyectos de código abierto. AEM Muchos de los elementos principales de la pila de tecnología de la se mantienen de hecho como proyectos activos de código abierto, como Sling y Jackrabbit, que fueron aportados a la Apache Software Foundation. AEM Un aspecto importante de este espíritu que está presente en la es que se le anima a utilizar las listas de correo y los foros en línea disponibles para interactuar directamente con el equipo de desarrollo.

AEM AEM Si está contribuyendo a los componentes de un proyecto de código abierto, familiarícese con los componentes de un proyecto de código abierto y póngase en contacto con el equipo principal existente del mismo modo que lo haría cuando tuviera intención de contribuir a un proyecto de este tipo.

## Experiencia requerida {#required-experience}

El Protocolo de transferencia de hipertexto (HTTP) es fundamental para todo lo que hacemos. AEM Por lo tanto, antes de contribuir a la, debe tener una comprensión profunda de HTTP, idealmente en la medida en que pueda escribir su propia implementación Java™ de un servidor HTTP multiproceso con agrupación de subprocesos. AJAX También debe comprender el comportamiento de la conexión persistente HTTP/1.1 y debe tener conocimientos profundos de las interacciones del lado del servidor/cliente con JavaScript, especialmente el estilo asincrónico de interacción representado por el código de tiempo de ejecución ().

Dado que el dinamismo de la página y el contenido interactivo son clave para la experiencia de WM, es esencial que tenga una comprensión bastante profunda del Modelo de objetos de documento y su potencial para la manipulación programática en respuesta a eventos. Debería tener algún conocimiento, por ejemplo, de la manipulación DOM en tiempo real y del comportamiento de arrastrar y soltar sobre varios documentos del explorador (por ejemplo, mediante iframes).

En el nivel más alto, debería comprender bien lo siguiente:

* el [Protocolo HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferiblemente) [HTML 5](https://html.spec.whatwg.org/))
* Hojas de estilos en cascada
* Lenguaje de marcado extensible (XML)
* AJAX Patrones de diseño asíncronos de JavaScript y XML ()
* Notación de objetos JavaScript (JSON)
* el modelo de objetos de documento
* Interacciones con estado frente a sin estado
* [Identificadores de recursos uniformes](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies del explorador
* y otros conceptos modernos de desarrollo web

La pila tecnológica de Adobe Experience Manager se basa en [Apache Felix](https://felix.apache.org/documentation/index.html) El contenedor OSGI con [Apache Sling](https://sling.apache.org/index.html) marco web e incrusta un repositorio de contenido Java™ ([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)) basado en [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html). Familiarícese con estos proyectos individuales y con cualquier otro componente de código abierto (por ejemplo, Apache Lucene) que se utilice en el área en la que pretenda contribuir.

## Conocimiento tribal {#tribal-knowledge}

Ciertos conceptos y principios rectores están profundamente arraigados en la antigua cultura del Día. En esta sección se enumeran algunos de los problemas &quot;profundamente insertados en el ADN&quot; que debe tener en cuenta.

### Todo está contenido {#everything-is-content}

El contenido incluye no solo todos los datos que mantiene la aplicación web. El código de programa, las bibliotecas, los scripts, las plantillas, el HTML, el CSS, las imágenes y los artefactos de todo tipo, cualquier cosa y todo se mantienen en el repositorio de contenido y se importan o exportan en forma de paquetes a través del administrador de paquetes y el uso compartido de paquetes.

### El modelo de David {#david-s-model}

La forma en que el contenido debe modelarse en un repositorio de contenido Java™ requiere una forma de pensar completamente diferente a la práctica habitual en la industria del software para el modelado de datos en el mundo relacional. La lectura esencial para cualquier recién llegado a la administración de contenido al modo JCR es [David&#39;s Model: Una guía para el modelado de contenido](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

El enfoque REST está profundamente arraigado en lo que hacemos. Esto significa, entre otras cosas, evitar interacciones con estado y tener en cuenta que los URI son direcciones definitivas para el contenido y los servicios.

REST (REpresentational State Transfer) hace referencia al estilo arquitectónico de software en el que se basa la World Wide Web. Describe los elementos clave que hacen que la Web funcione y proporciona un conjunto de principios para el diseño del software basado en la Web. Por lo tanto, al diseñar una API para utilizarla en la web, tiene sentido adherirse a estas &quot;prácticas recomendadas&quot;.

Debido a que REST proporciona la filosofía guía detrás de gran parte de lo que hacemos, debe considerar esencial estar bien versado en los principios del diseño RESTful. Un buen punto de partida es con [Tesis de Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Resolución de solicitud de Sling {#sling-request-resolution}

AEM AEM Un aspecto clave para comprender el contenido es cómo se relacionan las solicitudes entrantes con el comportamiento del contenido y la aplicación, cómo se estructura el contenido en el repositorio de contenido y dónde busca la lógica de la aplicación para gestionar la solicitud. Obtenga información acerca de Apache [Descomposición de URL de Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html) y la forma en que aplica el estilo arquitectónico REST y sus restricciones de sistema apátridas, almacenables en caché y por capas.

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

Nada de lo que haga debe romper el código antiguo de un cliente. Considerar solo `/libs` para contener código de producto que se pueda actualizar durante una actualización. El `/apps` del repositorio es el código del proyecto y la sección `/etc` contiene configuraciones personalizadas que deben conservarse. Generalmente, no sobrescriba nada en `/apps`, `/content`, y `/home`. Después de una actualización, el código de proyecto, las configuraciones y el contenido antiguos deben seguir funcionando como antes de la actualización.

El diseño para la compatibilidad con versiones anteriores también garantiza que la experiencia de actualización coincida con la simplicidad de la instalación inicial. AEM AEM Solo tiene que detener la, sustituir el archivo JAR de inicio rápido y volver a empezar a utilizar el archivo de inicio de la aplicación, debería ser suficiente. Con una base de instalación en rápido crecimiento, la eficiencia de la actualización es una ventaja cada vez más significativa.

Aunque las API existentes pueden y deben marcarse como obsoletas cuando las nuevas y mejores funciones las sustituyen, todas las API que se hicieron públicas en una versión 5.x anterior deben seguir funcionando, ya que pueden estar en uso en el código de aplicación personalizado. Estas API no deben eliminarse.

La compatibilidad con versiones anteriores también debe tenerse en cuenta con respecto a la coherencia general de la estructura de contenido y la experiencia del usuario.

## Conceptos principales {#core-concepts}

**Instancia de autor** AEM : Normalmente, por motivos de seguridad, gobernanza y de otro tipo, un sitio de producción divide las instancias de la aplicación en instancias de autor y de publicación. AEM Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre instancias de.

**Almacenamiento en caché, freír y hornear** - Tradicionalmente, los conceptos de hornear versus freír son una distinción importante entre diferentes sistemas de administración de contenido web. En la jerga de CMS, &quot;procesamiento&quot; se refiere al concepto de comprometer datos en archivos estáticos en el momento de la publicación, mientras que &quot;freír&quot; se refiere al concepto de procesar datos para la presentación final en el momento de la solicitud (es decir, justo a tiempo).

**Clúster y equilibrio de carga** : Para aumentar la disponibilidad y mejorar el rendimiento de un entorno de producción, es común combinar varias instancias de autor o publicación (en clústeres), poniéndolas a disposición de diferentes grupos de usuarios o equilibrándolas de carga detrás de una configuración de Dispatcher.

También es posible combinar varias instancias del repositorio de contenido para crear una *de alta disponibilidad* AEM Solución JCR, que puede integrarse con su solución de para maximizar la protección contra fallos de hardware y software. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obtener más información.

**Componente** AEM - En la práctica, un componente es un tipo de objeto, cuyas instancias generalmente se pueden crear arrastrando y soltando desde, por ejemplo, el Sidekick. AEM Por ejemplo, los componentes listos para usar que se envían con los componentes Texto, Título, Nube de etiquetas, Carrusel, Imagen y Lista, todos disponibles en el Sidekick durante la ejecución.

**Buscador de contenido** : En el modo de creación, el Buscador de contenido es un panel especial (marco) en el lado izquierdo de la página que, según la pestaña que seleccione en la parte superior, muestra listas de imágenes, documentos, recursos de Flash, páginas, párrafos o recursos del repositorio que puede arrastrar y soltar desde el Buscador de contenido en la página en la que está trabajando (a la derecha).

**Recursos digitales** AEM : En la práctica, los recursos digitales son (por lo general) imágenes y archivos multimedia enriquecidos. Para obtener más información, consulte Uso de recursos digitales en DAM.

**Dispatcher** : Dispatcher es una herramienta de almacenamiento en caché y de equilibrio de carga que proporciona ciertas garantías de seguridad.

**Widgets de ExtJS** AEM : La mayoría de los elementos de la interfaz de usuario de utilizan ExtJS, que es una biblioteca de widgets de terceros escrita en JavaScript. ExtJS ofrece un alto rendimiento, widgets de interfaz de usuario personalizables y un modelo de componentes bien diseñado y ampliable.

**JCR, Java™ Repositorio de contenido** : la especificación del repositorio de contenido Java™ (JSR-283) proporciona un modelo de datos abstracto y una interfaz de programación de aplicaciones para crear un repositorio de datos NoSQL escalable que combina las características de un sistema de archivos y una base de datos de objetos. AEM Aunque no necesita comprender JSR-283 con detalle exhaustivo, debe dedicar tiempo a familiarizarse con las capacidades básicas de JCR y con el modelo de datos subyacente, ya que JCR es lo que hace posible la filosofía de &quot;todo es contenido&quot; de la.

Básicamente, JCR es un sistema de nodos y propiedades, en el que los nodos pueden heredar de otros nodos y todo el contenido se almacena como propiedad *values*. Tenga en cuenta que, además de la herencia ordinaria, JCR permite un concepto de nodos de &quot;mezcla&quot;, que permite modelar la herencia múltiple.

JCR tiene varios tipos de nodos predefinidos y tipos de propiedades, pero en general el sistema de escritura es flexible, y (de hecho) una de las fortalezas de JCR es que permite almacenar/administrar contenido estructurado y no estructurado con igual facilidad. Es decir, JCR puede admitir datos altamente estructurados, pero también puede admitir estructuras de datos dinámicas arbitrarias sin restricciones de esquema.

El JavaDoc para la API de Java™ de JCR es [aquí](https://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de intentar leer el JavaDoc o la propia especificación JCR, es posible que desee consultar [esta explicación de alto nivel](/help/sites-developing/the-basics.md#java-content-repository) de JCR implementado por Adobe Experience Services.

**Administrador de varios sitios (MSM)** AEM : La función MSM de la ayuda a los clientes a gestionar contenido multilingüe y multinacional, lo que les permite equilibrar la marca centralizada con el contenido localizado.

**OSGi** AEM - OSGi es la tecnología de tiempo de ejecución basada en servicios que proporciona la base para el desarrollo modularizado de Java™ en el mundo de la de la. Es un marco de trabajo que proporciona no solo un entorno de carga de clases y ejecución altamente dinámico (y seguro) para los recursos de código (conocidos como paquetes), sino también un control total sobre la visibilidad y el ciclo de vida de los distintos servicios expuestos por los paquetes. Un registro de servicios proporciona un modelo de cooperación para paquetes que tiene en cuenta la dinámica del ciclo vital (y los requisitos de versión). OSGi resuelve muchos de los problemas que los servidores de aplicaciones pretendían resolver, pero lo hace de una manera ligera y altamente dinámica, lo que permite, por ejemplo, implementar servicios en caliente (haciendo que el nuevo código esté disponible inmediatamente sin reiniciar el servidor).

**Parsys, sistema de párrafos** - El sistema de párrafos (parsys) es un componente compuesto que permite a los autores añadir componentes de diferentes tipos a una página y contiene otros componentes de párrafo. Cada tipo de párrafo se representa como un componente. El sistema de párrafos en sí también es un componente, que contiene los demás componentes de párrafo.

**Microkernel** - Cada espacio de trabajo del repositorio puede configurarse por separado para almacenar sus datos a través de un microkernel específico (una clase que administra la lectura y escritura de los datos). Del mismo modo, el almacén de versiones en todo el repositorio también puede configurarse de forma independiente para utilizar un microkernel en particular. Hay varios microkernels diferentes disponibles, capaces de almacenar datos en varios formatos de archivo o bases de datos relacionales. (Por ejemplo, hay administradores de persistencia para MongoDB, DB2® o Oracle AEM) El microkernel predeterminado para la creación de un núcleo es TarMK (ver más abajo).

**Instancia de publicación** AEM : Por motivos de seguridad, gobernanza y de otro tipo, un sitio de producción suele dividir instancias de en instancias de autor y publicación. AEM Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre instancias de.

**Quickstart** AEM - A diferencia de muchos otros programas, usted instala el archivo JAR usando un solo archivo &quot;Quickstart&quot; de extracción automática. Cuando haga doble clic en el archivo JAR por primera vez, todo lo que necesite se instalará automáticamente. AEM El JAR de inicio rápido incluye todos los archivos necesarios para el repositorio CRX (incluidos los servicios administrativos), los servicios de repositorio virtual, los servicios de índice y búsqueda, los servicios de flujo de trabajo, la seguridad y un servidor web, además del motor de servlets CQ (CQSE) y todos los servicios de. No hay otros archivos que instalar: Quickstart es independiente.

La primera vez que se inicia el Inicio rápido, se crea un repositorio compatible con JCR completo en segundo plano, lo que puede tardar varios minutos. Después de este inicio inicial, los inicios posteriores son mucho más rápidos, ya que la infraestructura del repositorio ya se ha establecido.

AEM Muchas opciones de inicio (como el número de puerto activo y si la instancia de inicio en cuestión debe ser una instancia de publicación en lugar de una instancia de autor; y mucho más) se pueden controlar cambiando el nombre del archivo de inicio rápido. Para ver una lista de opciones a este respecto, ejecute el JAR con &quot;-help&quot; en la línea de comandos:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes de replicación** AEM : los agentes de replicación son fundamentales para la creación, ya que el mecanismo utilizado para publicar (activar) contenido de un autor en un entorno de publicación; vaciar contenido de la caché de Dispatcher; devolver contenido generado por el usuario (por ejemplo, entrada de formulario) desde el entorno de publicación al entorno de creación.

**Andamiaje** : Con el andamiaje puede crear un formulario (un andamio) con campos que reflejen la estructura que desee para sus páginas y, a continuación, utilizar este formulario para crear fácilmente páginas basadas en esta estructura.

**Segmentación** - Los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Comprender los objetivos de los visitantes y cumplir sus expectativas es un requisito previo importante para el éxito del marketing en línea. La segmentación ayuda a conseguirlo al analizar y caracterizar los detalles de un visitante.

**Sidekick** : El Sidekick es una ventana flotante similar a una paleta que aparece en la página editable desde la que se pueden arrastrar nuevos componentes y ejecutar acciones que se apliquen a la página.

**Site Catalyst** : SiteCatalyst proporciona a los especialistas en marketing un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en varios canales de marketing. Puede utilizar Adobe SiteCatalyst AEM para analizar datos de sitios web de la.

**Almacenamiento de Tar (TarMK)** AEM - TarMK es el sistema de persistencia por defecto en el mundo de la. AEM Aunque se puede configurar para que utilice un sistema de persistencia diferente (como MongoDB), TarMK tiene ciertas ventajas, ya que está optimizado para el rendimiento de casos de uso típicos de JCR (por lo tanto, es rápido), utiliza un formato de datos estándar en la industria y se puede realizar una copia de seguridad rápida y fácilmente.

**Plantilla** AEM - En la plantilla, se especifica un tipo de página en particular. Define la estructura de una página (a la vez que especifica una imagen en miniatura y varias propiedades). Por ejemplo, puede tener plantillas independientes para páginas de productos, mapas del sitio e información de contacto.

**Flujo de trabajo** AEM : El sistema de flujo de trabajo de la permite la creación de procesos automatizados que implican páginas o activos.
