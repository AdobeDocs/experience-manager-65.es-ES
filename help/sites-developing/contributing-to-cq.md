---
title: Contribuir a AEM
seo-title: Contribuir a AEM
description: AEM se desarrolla siguiendo metodologías probadas que se practican comúnmente en grandes proyectos de código abierto
seo-description: AEM se desarrolla siguiendo metodologías probadas que se practican comúnmente en grandes proyectos de código abierto
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2726'
ht-degree: 1%

---


# Contribuyendo a AEM{#contributing-to-aem}

## Metodología de desarrollo {#development-methodology}

AEM se desarrolla siguiendo metodologías probadas que se practican comúnmente en grandes proyectos de código abierto. Muchos elementos principales de AEM pila de tecnología se mantienen como proyectos activos de código abierto, como Sling y Jackrabbit, que fueron aportados a la Fundación de Software Apache. Un aspecto importante de este espíritu que está presente en AEM es que se le anima a utilizar las listas de correo y los foros en línea disponibles para interactuar directamente con el equipo de desarrollo.

Si está contribuyendo a componentes de AEM, debe familiarizarse con AEM como lo haría al contribuir a un proyecto de código abierto, y comunicarse con el equipo básico existente como lo haría cuando pretendiera contribuir a dicho proyecto.

## Experiencia requerida {#required-experience}

El Protocolo de transferencia de hipertexto (HTTP) es fundamental para todo lo que hacemos. Por lo tanto, antes de contribuir a la AEM, debe tener una comprensión profunda de HTTP, idealmente en la medida en que sea capaz de escribir su propia implementación de Java de un servidor HTTP multiproceso con agrupación de subprocesos. También debe comprender el comportamiento de mantenimiento de HTTP/1.1 y tener un conocimiento profundo de las interacciones entre el servidor y el cliente con JavaScript, en particular el estilo de interacción asincrónica representado por AJAX.

Dado que el dinamismo de las páginas y el contenido interactivo son claves para la experiencia WM, es esencial que se tenga una comprensión bastante profunda del Modelo de objetos de Documento y su potencial de manipulación programática en respuesta a eventos. Debería tener algún conocimiento, por ejemplo, de la manipulación DOM en tiempo real y del comportamiento de arrastrar y soltar en varios documentos del explorador (por ejemplo, utilizando iframes).

En el nivel más alto, debe tener una comprensión sólida de:

* el protocolo [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferiblemente [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Hojas de estilo en cascada
* Lenguaje de marcado extensible (XML)
* Patrones de diseño asincrónicos de JavaScript y XML (AJAX)
* JavaScript Object Notation (JSON)
* el Modelo de objetos Documento
* Interacciones apátridas vs. apátridas
* [Identificadores de recursos uniformes](https://www.ietf.org/rfc/rfc2396.txt)
* Cookies del explorador
* y otros conceptos modernos de desarrollo web

La pila de tecnología de Adobe Experience Manager se basa en el contenedor [Apache Felix](https://felix.apache.org/) OSGI con el entorno web [Apache Sling](https://sling.apache.org/site/index.html) e incorpora un repositorio de contenido Java ([JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)) basado en [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Debe familiarizarse con estos proyectos individuales, así como con cualquier otro componente de código abierto (por ejemplo, Apache Lucene) utilizado en el área en la que desea contribuir.

## Conocimiento tribal {#tribal-knowledge}

Algunos conceptos y principios rectores están profundamente arraigados en la cultura del antiguo Día. Esta sección lista algunos de los problemas &quot;profundamente arraigados en el ADN&quot; que debe tener en cuenta.

### Todo es contenido {#everything-is-content}

El contenido incluye no sólo todos los datos que la aplicación web persiste. El código programa, las bibliotecas, las secuencias de comandos, las plantillas, HTML, CSS, las imágenes y los artefactos de todo tipo, todo y todo, se mantiene en el repositorio de contenido y se importa/exporta en forma de paquetes mediante el Administrador de paquetes y Uso compartido de paquetes.

### Modelo de David {#david-s-model}

La forma en que el contenido debe modelarse en un repositorio de contenido Java requiere una forma de pensar completamente diferente a la práctica común en el sector del software para el modelado de datos en el mundo relacional. La lectura esencial para cualquier recién llegado al gestor de contenido del modo JCR es el [Modelo de David: Una guía para el modelado de contenido](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTity {#restfulness}

El enfoque REST está profundamente arraigado en lo que hacemos. Esto significa, entre otras cosas, evitar las interacciones de estado y tener en cuenta que los URI son direcciones definitivas para el contenido y los servicios.

REST (REpresentational State Transfer) se refiere al estilo arquitectónico del software en el que se basa la World Wide Web. Describe los elementos clave que hacen que la Web funcione y, por lo tanto, proporciona un conjunto de principios sobre cómo se debe diseñar el software basado en la Web. Al diseñar una API que se va a usar en la Web, por lo tanto, tiene sentido adherir a estas &quot;optimizaciones&quot;.

Debido a que REST proporciona la filosofía guía detrás de tanto de lo que hacemos, usted debería considerar esencial ser muy versado en los principios del diseño RESTful. Un buen lugar para el inicio es con la disertación de [Roy Field](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Resolución de solicitud de Sling {#sling-request-resolution}

Un aspecto clave para comprender AEM es cómo las solicitudes entrantes se relacionan con el contenido y el comportamiento de la aplicación, cómo se estructura el contenido en el repositorio de contenido y dónde AEM la lógica de la aplicación para gestionar la solicitud. Obtenga información sobre la descomposición de la dirección URL de Apache [Sling](https://sling.apache.org/site/url-decomposition.html) y la manera en que aplica el estilo arquitectónico REST y sus restricciones de sistema apátridas, procesables y en capas.

Aspectos clave para comprender la resolución de solicitudes de Apache Sling son cómo las solicitudes se asignan principalmente a un recurso específico del Repositorio de contenido, cómo las propiedades adicionales de la solicitud, junto con las propiedades de estos objetos de contenido, determinan qué código de aplicación se invocará para representar el contenido y cómo el código en /apps sobrescribe el código en /libs.

### Quickstart {#quickstart}

No hay paso tres: Para instalar y ejecutar, basta con descargar y hacer clic con el doble en el archivo JAR de inicio rápido. No hay paso tres. Cualquier funcionalidad opcional adicional no debe requerir más que la instalación del paquete adecuado desde Package Share.

Tamaño de inicio rápido pequeño: Mantenga el tamaño del archivo JAR de inicio rápido como mínimo. Haga un uso inteligente y optimizado de las bibliotecas, moviendo la funcionalidad opcional al uso compartido de paquetes.

Tiempo de inicio más rápido: Cuando realice un cambio que pueda afectar al tiempo de inicio, asegúrese de que sea más corto, no más largo.

### Lean y Media {#lean-and-mean}

Favorecemos el código y los proyectos ligeros, pequeños, rápidos y elegantes. &quot;Suficientemente bueno&quot; no es suficiente.

Reutilización del código: Nuestra arquitectura de productos basada en OSGi y la filosofía de &quot;todo es contenido&quot; significa que tenemos oportunidades inusualmente buenas para reutilizar código y artefactos. Tratamos de aprovechar ese hecho siempre que sea posible para mantener las características de media y baja.

Acoplamiento suelto: Somos partidarios de interacciones unidas de manera flexible por encima de dependencias estrictas e &quot;intimidad no deseada&quot;. El acoplamiento suelto también permite una mayor reutilización del código.

### No romper la demostración {#don-t-break-the-demo}

Familiarícese con las secuencias de comandos de demostración y las funcionalidades del producto que se muestran con mayor frecuencia en las demostraciones. Entiendan que, por lo menos, nada que hagan debería romper alguna vez una función de &quot;secuencia de comandos de demostración&quot;. El producto principal debe estar siempre preparado para la demostración, incluso durante el desarrollo.

### Diseño para confiabilidad {#design-for-reliability}

Nos esforzamos por diseñar y codificar las funciones de manera que no se produzcan errores, de modo que (por ejemplo) un problema con un solo elemento DOM no provoque que una página entera no se procese. En otras palabras: Hagan cosas que sean fatales. Hacer que todo lo demás sea superable. Haga que el producto sea &quot;indulgente&quot;.

### La normalidad es anormal {#abnormal-is-the-new-normal}

No dependa de los ganchos de apagado, asegúrese de que la limpieza se realiza al iniciar. La terminación anormal es una terminación normal.

`shutdown == kill -9 == power outage`

### Estar listo para el clustering elástico {#be-ready-for-elastic-clustering}

Siempre esté listo para la agrupación elástica, siempre suponga que existe la agrupación en clúster. Como regla general, cumplir con todo lo que se encuentra en el repositorio de contenido significa contar con soporte para clustering integrado.

### Diseño para compatibilidad con versiones anteriores {#design-for-backward-compatibility}

Nada de lo que haga debe romper el código antiguo de un cliente. Considere sólo `/libs` para contener el código de producto que se puede actualizar durante una actualización. La sección `/apps` del repositorio es código de proyecto y la sección `/etc` contiene configuraciones personalizadas que deben preservarse. Generalmente, no sobrescriba nada en `/apps`, `/content` y `/home`. Después de una actualización, el código del proyecto antiguo, las configuraciones y el contenido deben seguir funcionando como lo hacían antes de la actualización.

El diseño para la compatibilidad con versiones anteriores también garantiza que la experiencia de actualización coincida con la simplicidad de la instalación inicial. Basta con detener AEM, reemplazar el archivo JAR de inicio rápido e iniciar AEM de nuevo. Con una base de instalación en rápido crecimiento, la eficacia de la actualización será una ventaja cada vez más importante.

Si bien las API existentes pueden y deben marcarse como obsoletas cuando una funcionalidad más nueva y mejor las reemplaza, todas las API que se hicieron públicas en una versión anterior de 5.x deben seguir funcionando, ya que pueden estar en uso en el código de la aplicación personalizada. Estas API no deben eliminarse.

La compatibilidad con versiones anteriores también debe tenerse en cuenta en lo que respecta a la coherencia general de la estructura de contenido y la experiencia del usuario.

## Conceptos principales {#core-concepts}

**Instancia**  de autor: por motivos de seguridad, gobernanza y otros, un sitio de producción divide las instancias de AEM en instancias de autor y publicación. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre instancias de AEM.

**Almacenamiento en caché, fritura y horneado** - Tradicionalmente, los conceptos de hornear y fritar son una importante distinción entre los diferentes sistemas de Gestor de contenido Web. En la jerga de CMS, &quot;agrupación&quot; se refiere al concepto de asignación de datos a archivos estáticos en tiempo de publicación, mientras que &quot;fritación&quot; se refiere al concepto de procesamiento de datos para la presentación final en el momento de la solicitud (es decir, justo a tiempo).

**Agrupamiento y equilibrio**  de carga: para aumentar la disponibilidad y mejorar el rendimiento de un entorno de producción, es común combinar varias instancias de creación y/o publicación (en clústeres), ya sea poniéndolas a disposición de diferentes grupos de usuarios o equilibrándolas de carga tras una configuración de Dispatcher.

También es posible combinar varias instancias del repositorio de contenido para crear una solución *JCR de alta disponibilidad*, que luego se puede integrar con la solución AEM para maximizar la protección contra fallas de hardware y software. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) para obtener más información.

**Componente** : en AEM, un componente es un tipo de objeto, cuyas instancias generalmente se pueden crear arrastrándolas y soltándolas desde, por ejemplo, la barra de tareas. Por ejemplo, los componentes listos para usar que se incluyen con AEM incluyen los componentes Texto, Título, Nube de etiquetas, Carrusel, Imagen y Lista, todos disponibles en la barra de tareas durante la ejecución.

**Buscador**  de contenido: en el modo de creación, el Buscador de contenido es un panel especial (marco) en la parte izquierda de la página que, según la ficha seleccionada en la parte superior, muestra listas de imágenes, documentos, recursos de Flash, páginas, párrafos o recursos de repositorio que puede arrastrar y soltar desde el Buscador de contenido en la página en la que está trabajando (a la derecha).

**Recursos**  digitales: En AEM, Recursos digitales son (normalmente) imágenes y archivos de medios enriquecidos. Para obtener más información, consulte Uso de recursos digitales en DAM.

**Dispatcher** : Dispatcher es a la vez una herramienta de almacenamiento en caché y equilibrio de carga, así como una herramienta que proporciona ciertas salvaguardias de seguridad.

**Widgets**  de ExtJS: la mayoría de los elementos de la interfaz de usuario de AEM utilizan ExtJS, que es una biblioteca de utilidades de terceros escrita en JavaScript. ExtJS cuenta con utilidades de interfaz de usuario personalizables de alto rendimiento y un modelo de componentes ampliable y bien diseñado.

**JCR, Java Content Repository** : la especificación Java Content Repository (JSR-283) proporciona un modelo de datos abstracto y una interfaz de programación de aplicaciones para crear un repositorio de datos NoSQL con capacidad de ampliación masiva que combina características de un sistema de archivos y una base de datos de objetos. Aunque no necesita comprender JSR-283 con detalle, debe tomarse tiempo para familiarizarse con las capacidades básicas de JCR y el modelo de datos subyacente, ya que JCR es lo que hace posible la filosofía de &quot;todo es contenido&quot; de AEM.

En esencia, JCR es un sistema de nodos y propiedades, en el que los nodos pueden heredar de otros nodos y todo el contenido se almacena como propiedad *valores*. Tenga en cuenta que, además de la herencia ordinaria, JCR permite un concepto de nodos de &quot;mezcla&quot;, que permite modelar múltiples herencia.

JCR tiene una serie de tipos de nodos predefinidos y tipos de propiedades, pero en general el sistema de escritura es bastante flexible, y (de hecho) una de las ventajas de JCR es que permite almacenar/administrar contenido estructurado y no estructurado con la misma facilidad. Es decir, JCR puede dar cabida a datos altamente estructurados, pero también puede dar cabida a estructuras de datos dinámicas arbitrarias sin restricciones de esquema.

El JavaDoc para la API de Java de JCR está [aquí](http://jackrabbit.apache.org/jcr/jcr-api.html).

Antes de intentar leer la especificación de JavaDoc o JCR, es posible que desee consultar [esta explicación de alto nivel](/help/sites-developing/the-basics.md#java-content-repository) de JCR implementada por Adobe Experience Services.

**Multi-Site Manager (MSM)** : la función MSM de AEM ayuda a los clientes a gestionar el contenido multilingüe y multinacional, lo que les permite equilibrar la marca centralizada con el contenido localizado.

**OSGi** - OSGi es la tecnología de tiempo de ejecución basada en servicios que proporciona la base para el desarrollo de Java modular en AEM. Es un entorno que proporciona no sólo un entorno de carga y ejecución de clases altamente dinámico (y seguro) para los recursos de código (conocidos como paquetes), sino también control total sobre la visibilidad y el ciclo vital de los distintos servicios expuestos por paquetes. Un registro de servicios proporciona un modelo de cooperación para paquetes que tiene en cuenta la dinámica del ciclo vital (y los requisitos de versión). OSGi resuelve muchos de los problemas que los servidores de aplicaciones pretendían solucionar, pero lo hace de una manera ligera y altamente dinámica, lo que permite, por ejemplo, implementar servicios en caliente (haciendo que el nuevo código esté disponible inmediatamente sin reiniciar el servidor).

**Parsys, Paragraph System** : el sistema de párrafos (parsys) es un componente compuesto que permite a los autores añadir componentes de distintos tipos a una página y contiene otros componentes de párrafos. Cada tipo de párrafo se representa como un componente. El propio sistema de párrafo también es un componente, que contiene los demás componentes del párrafo.

**Microkernel** : Cada espacio de trabajo del repositorio puede configurarse por separado para almacenar sus datos a través de un micronúcleo específico (una clase que administra la lectura y escritura de los datos). Del mismo modo, el almacén de versiones de todo el repositorio también puede configurarse de forma independiente para utilizar un micronúcleo concreto. Existen diversos micronúcleos disponibles, capaces de almacenar datos en diversos formatos de archivo o bases de datos relacionales. (Por ejemplo, hay administradores de persistencia para MongoDB, DB2 o Oracle) El microkernel predeterminado para AEM es TarMK (ver más abajo).

**Instancia**  de publicación: por motivos de seguridad, gobernanza y otros, un sitio de producción generalmente divide las instancias de AEM en instancias de creación y publicación. Para obtener más información sobre la arquitectura de implementación (incluidas las instancias de autor/publicación), consulte la documentación sobre instancias de AEM.

**Inicio rápido** : a diferencia de muchos otros programas, se instala AEM utilizando un solo archivo JAR de extracción automática &quot;QuickStart&quot;. Al hacer clic con el botón doble en el archivo JAR por primera vez, todo lo que necesita se instala automáticamente. El JAR de inicio rápido incluye todos los archivos necesarios para el repositorio de CRX (incluidas las instalaciones administrativas), los servicios de repositorio virtual, los servicios de índice y búsqueda, los servicios de flujo de trabajo, la seguridad y un servidor web, además del motor de servlet de CQ (CQSE) y todos los servicios de AEM. No hay otros archivos para instalar: el inicio rápido es independiente.

La primera vez que se inicio el inicio rápido, se crea un repositorio completo compatible con JCR en segundo plano, que puede tardar varios minutos. Después de este inicio inicial, las siguientes iniciaciones son mucho más rápidas, ya que la infraestructura del repositorio ya se ha establecido.

Muchas opciones de inicio (como el número de puerto activo y si la instancia de AEM en cuestión debe ser una instancia de Publish en lugar de una instancia de Author; y mucho más) se puede controlar cambiando correctamente el nombre del archivo de inicio rápido. Para ver una lista de opciones en este sentido, ejecute el JAR con &quot;-help&quot; en la línea de comandos:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agentes**  de replicación: los agentes de replicación son fundamentales para AEM como mecanismo utilizado para publicar (activar) contenido de un autor a un entorno de publicación; vaciar contenido de la caché de Dispatcher; devolver contenido generado por el usuario (por ejemplo, entrada de formulario) desde el entorno Publicar al entorno Autor.

**Andamiaje** : con scaffolding, puede crear un formulario (un scaffold) con campos que reflejen la estructura que desee para las páginas y, a continuación, utilizar este formulario para crear fácilmente páginas basadas en esta estructura.

**Segmentación** : los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Comprender los objetivos de los visitantes y cumplir sus expectativas es un requisito previo importante para el éxito del mercadotecnia en línea. La segmentación ayuda a lograr esto analizando y caracterizando los detalles de un visitante.

**Barra de tareas** : la barra de tareas es una ventana flotante parecida a una paleta que aparece en la página editable, desde la cual se pueden arrastrar nuevos componentes y ejecutar las acciones que se aplican a la página.

**SiteCatalyst de SiteCatalyst** : proporciona a los especialistas en mercadotecnia un lugar para medir, analizar y optimizar los datos integrados de todas las iniciativas en línea en múltiples canales de mercadotecnia. Puede utilizar Adobe SiteCatalyst para analizar datos de AEM sitios web.

**Tar Almacenamiento (TarMK)** : TarMK es el sistema de persistencia predeterminado en AEM. Aunque AEM puede configurarse para utilizar un sistema de persistencia diferente (como MongoDB), TarMK tiene ciertas ventajas en cuanto a que está optimizado para el rendimiento en los casos de uso típicos de JCR (por lo tanto es muy rápido), utiliza un formato de datos estándar del sector y puede realizarse una copia de seguridad rápida y sencilla.

**Plantilla** : en AEM, una plantilla especifica un tipo concreto de página. Define la estructura de una página (aunque también suele especificar una imagen en miniatura y varias propiedades). Por ejemplo, puede tener plantillas diferentes para páginas de producto, mapas del sitio e información de contacto.

**Flujo de trabajo** : el sistema de flujo de trabajo AEM permite la creación de procesos automatizados que involucren páginas o recursos.
