---
title: AEM Conceptos principales
seo-title: Conceptos básicos
description: Una visión general de los conceptos principales de cómo se estructura la AEM y cómo desarrollarse sobre ella, incluida la comprensión de JCR, Sling, OSGi, Dispatcher, flujos de trabajo y MSM
seo-description: Una visión general de los conceptos principales de cómo se estructura la AEM y cómo desarrollarse sobre ella, incluida la comprensión de JCR, Sling, OSGi, Dispatcher, flujos de trabajo y MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
translation-type: tm+mt
source-git-commit: 78e28636eec331314c2f29c93d516215b1572f20
workflow-type: tm+mt
source-wordcount: '3367'
ht-degree: 0%

---

# Conceptos principales de AEM {#aem-core-concepts}

>[!NOTE]
>
>Antes de profundizar en los conceptos básicos de AEM, Adobe recomienda completar el tutorial de WKND en el documento [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md) para obtener una descripción general del proceso de desarrollo de AEM e introducción a los conceptos principales.

## Requisitos previos para el desarrollo en AEM {#prerequisites-for-developing-on-aem}

Necesitará las siguientes habilidades para desarrollar sobre AEM:

* Conocimientos básicos de las técnicas de aplicación web, incluidos:

   * ciclo request -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conocimientos prácticos de Experience Server (CRX), incluido el Explorador de contenido
* Para desarrollar en la IU clásica, también se requiere conocimiento básico de JSP (páginas de JavaServer), incluida la capacidad de comprender y modificar ejemplos JSP simples.

También se recomienda leer y seguir las [Directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositorio de contenido Java {#java-content-repository}

El estándar del repositorio de contenido Java (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido.

El responsable de la especificación es Adobe Research (Suiza) AG.

El paquete [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), javax.jcr.&amp;ast; se utiliza para el acceso directo y la manipulación del contenido del repositorio.

## Experience Server (CRX) y Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server proporciona los servicios de Experience AEM que se han creado y que se pueden aprovechar para crear aplicaciones personalizadas, e incrusta el repositorio de contenido basado en Jackrabbit.

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis es un código abierto, totalmente conforme, implementación de la API JCR 2.0.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

### Introducción a Sling {#introduction-to-sling}

AEM se crea utilizando [Sling](https://sling.apache.org/site/index.html), un marco de aplicaciones web basado en los principios de REST que proporciona un fácil desarrollo de aplicaciones orientadas al contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit, o en el caso de AEM, el Repositorio de Contenido CRX, como su almacén de datos. Sling ha sido contribuido a la Apache Software Foundation - puede encontrar más información en Apache.

Con Sling, el tipo de contenido que se va a procesar no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL se resuelve en un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Esto proporciona una excelente compatibilidad a los autores de contenido web para crear páginas que se adapten fácilmente a sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes, o cuando necesita páginas que se puedan personalizar fácilmente. En particular, al implementar un sistema de administración de contenido web como WCM en la solución AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución del script Sling: muestra cómo pasar de una solicitud HTTP al nodo de contenido, de un nodo de contenido a un tipo de recurso, de un tipo de recurso a un script y qué variables de secuencias de comandos están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos pero poderosos que puede utilizar al tratar con SlingPostServlet, el controlador predeterminado para todas las solicitudes de POST que le ofrece infinitas opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling es centrado en el contenido {#sling-is-content-centric}

Sling es *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* el primer destino es el recurso (nodo JCR) que contiene el contenido
* en segundo lugar, la representación o la secuencia de comandos se encuentran en las propiedades del recurso en combinación con ciertas partes de la solicitud (por ejemplo, selectores o la extensión)

### Sling RESTful {#restful-sling}

Debido a la filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* muy RESTful, no solo en la superficie; los recursos y las representaciones están modelados correctamente dentro del servidor
* elimina uno o varios modelos de datos

   * anteriormente se necesitaban las siguientes opciones: estructura URL, objetos empresariales, esquema de base de datos;
   * ahora se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se controla mediante la dirección URL de la solicitud del usuario. Define el contenido que se mostrará en las secuencias de comandos correspondientes. Para ello, la información se extrae de la dirección URL.

Si analizamos la siguiente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividirla en sus partes compuestas:

| protocol | host | ruta de contenido | selector(s) | Extensión |  | sufijo |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | herramientas/espía | .printable.a4. | html | / | a/b | ? | x=12 |

**** protocolHTTP

**** hostName del sitio web.

**content** pathPath que especifica el contenido que se va a procesar. se utiliza en combinación con la extensión; en este ejemplo traducen a tools/spy.html.

**selector(s)** Se utiliza para métodos alternativos de renderización del contenido; en este ejemplo, una versión compatible con impresora en formato A4.

**formato** extensionContent; también especifica la secuencia de comandos que se utilizará para la renderización.

**** suffixCan para especificar información adicional.

**param(s)** Cualquier parámetro requerido para el contenido dinámico.

#### De URL a contenido y scripts {#from-url-to-content-and-scripts}

Con estos principios:

* la asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso
* cuando se encuentra el recurso adecuado, se extrae el tipo de recurso sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido

En la figura siguiente se ilustra el mecanismo utilizado, que se examinará con más detalle en las secciones siguientes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, se especifica qué secuencia de comandos procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como haría una instrucción SQL en un script PHP) ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca en el repositorio el recurso solicitado (nodo de contenido):

* el primer Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; p. ej. `../content/corporate/jobs/developer.html`
* si no se encuentra ningún nodo, se abandona la extensión y se repite la búsqueda; p. ej. `../content/corporate/jobs/developer`
* si no se encuentra ningún nodo, Sling devolverá el código http 404 (no encontrado).

Sling también permite que otras cosas que no sean nodos JCR sean recursos, pero esta es una característica avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae el **tipo de recurso de sling**. Esta es una ruta, que localiza la secuencia de comandos que se utilizará para procesar el contenido.

La ruta especificada por el `sling:resourceType` puede ser:

* absoluto
* relativo, a un parámetro de configuración

   Las rutas relativas se recomiendan por Adobe, ya que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` o `/libs`, que se buscarán en este orden (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Otros puntos a tener en cuenta son:

* cuando el método (GET, POST) sea obligatorio, se especificará en mayúsculas según la especificación HTTP, por ejemplo jobs.POST.esp (ver a continuación)
* se admiten varios motores de secuencia de comandos:

   * HTL (lenguaje de plantilla HTML: sistema de plantillas del lado del servidor recomendado por Adobe Experience Manager para HTML): `.html`
   * Páginas de ECMAScript (JavaScript) (ejecución del lado del servidor): `.esp, .ecma`
   * Páginas del servidor Java (ejecución del lado del servidor): `.jsp`
   * Compilador de Servlet Java (ejecución del lado del servidor): `.java`
   * Plantillas JavaScript (ejecución del lado del cliente): `.jst`

La lista de motores de secuencia de comandos admitidos por la instancia dada de AEM se muestra en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

Además, Apache Sling admite la integración con otros motores de secuencias de comandos populares (por ejemplo, Groovy, JRuby, Freemarker) y proporciona una forma de integrar nuevos motores de secuencias de comandos.

Utilizando el ejemplo anterior, si el `sling:resourceType` es `hr/jobs` entonces para:

* solicitudes de GET/HEAD y direcciones URL que terminan en .html (tipos de solicitud predeterminados, formato predeterminado)

   El script será /apps/hr/jobs/jobs.esp; la última sección de sling:resourceType forma el nombre del archivo.

* solicitudes del POST (todos los tipos de solicitud, excepto el GET/HEAD, el nombre del método debe estar en mayúsculas)

   se utilizará el POST en el nombre de la secuencia de comandos.

   El script será `/apps/hr/jobs/jobs.POST.esp`.

* URL en otros formatos, sin terminar con .html

   Por ejemplo `../content/corporate/jobs/developer.pdf`

   El script será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre de la secuencia de comandos.

* Direcciones URL con selectores

   Los selectores pueden utilizarse para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente rss o un resumen.

   Si vemos una versión fácil de imprimir en la que el selector podría ser *print*; como en `../content/corporate/jobs/developer.print.html`

   El script será `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre de la secuencia de comandos.

* Si no se ha definido ningún sling:resourceType , entonces:

   * la ruta de contenido se utilizará para buscar una secuencia de comandos adecuada (si la ruta basada en ResourceTypeProvider está activa).

      Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.

   * se utilizará el tipo de nodo principal.

* Si no se encuentra ningún script, se utilizará el script predeterminado.

   Actualmente, la representación predeterminada es compatible con texto sin formato (.txt), HTML (.html) y JSON (.json), y en todos ellos se enumerarán las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión .res, o solicitudes sin extensión de solicitud, es agrupar el recurso (siempre que sea posible).
* Para la gestión de errores http (códigos 403 o 404) Sling buscará un script en:

   * la ubicación /apps/sling/servlet/errorhandler para [scripts personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la ubicación de los scripts estándar /libs/sling/servlet/errorhandler/403.esp, o 404.esp respectivamente.

Si se aplican varios scripts para una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; en otras palabras, cuanto más selector coincida, mejor, independientemente de cualquier extensión de solicitud o coincidencia de nombre de método.

Por ejemplo, considere una solicitud para acceder al recurso
`/content/corporate/jobs/developer.print.a4.html`
de tipo
`sling:resourceType="hr/jobs"`

Suponiendo que tengamos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recurso (definidos principalmente por la propiedad `sling:resourceType` ), también está el supertipo de recurso. Esto se indica generalmente con la propiedad `sling:resourceSuperType` . Estos supertipos también se tienen en cuenta al intentar encontrar un script. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos donde el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) es efectivamente la raíz.

El supertipo de recurso de un recurso se puede definir de dos formas:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que apunta el `sling:resourceType`.

Por ejemplo:

* /

   * una
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




La jerarquía de tipo de:

* `/x`
   *  es`[ c, b, a, <default>]`
* while para `/y`
   * la jerarquía es `[ c, a, <default>]`

Esto se debe a que `/y` tiene la propiedad `sling:resourceSuperType` mientras que `/x` no lo tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### Los scripts de Sling no se pueden llamar directamente {#sling-scripts-cannot-be-called-directly}

Dentro de Sling, no se pueden llamar directamente a los scripts, ya que esto rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculte el recurso dentro de la secuencia de comandos, de modo que la estructura (Sling) ya no lo sepa. Por lo tanto, se pierden algunas funciones:

* administración automática de métodos http distintos de la GET, que incluyen:

   * POST, PUT y DELETE que se administran con una implementación predeterminada de sling
   * la secuencia de comandos `POST.jsp` en la ubicación sling:resourceType

* su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; de gran importancia para el desarrollo a gran escala

### API de Sling {#sling-api}

Utiliza el paquete de la API de Sling, org.apache.sling.Bibliotecas de etiquetas &amp;ast; y .

### Referencia a elementos existentes utilizando sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los scripts.

Es posible que las secuencias de comandos más complejas (agregación de secuencias de comandos) necesiten acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página y elementos de una lista) y hacerlo incluyendo el *recurso*.

Para ello, puede utilizar el comando sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Esto incluirá efectivamente la definición del recurso al que se hace referencia, como en la siguiente instrucción que hace referencia a una definición existente para procesar imágenes:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se denomina Sistema de módulos dinámicos para Java). Los contenedores OSGi le permiten dividir su aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* servicios implementados dentro del contenedor
* un contrato entre el contenedor y su solicitud

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse entre sí de forma dinámica para la colaboración.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de aplicaciones. Sling, y por lo tanto CQ5, utiliza la implementación [Apache Felix](https://felix.apache.org/) de OSGI (iniciativa de puerta de enlace de servicios abiertos) y se basa en las especificaciones de la versión 4.2 de OSGi Service Platform. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* instalar
* start
* stop
* actualizar
* desinstalar
* ver el estado actual
* acceda a información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [Configuración de la consola web](/help/sites-deploying/web-console.md), [OSGI](/help/sites-deploying/configuring-osgi.md) y [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener más información.

## Objetos de desarrollo en el entorno de AEM {#development-objects-in-the-aem-environment}

Las siguientes son de interés para el desarrollo:

**** ElementoUn elemento es un nodo o una propiedad.

Para obtener información detallada sobre la manipulación de objetos Item, consulte [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) de la interfaz javax.jcr.Item

**Nodo (y sus propiedades)**  Los nodos y sus propiedades se definen en la especificación JCR API 2.0 (JSR 283). Almacenan contenido, definiciones de objetos, secuencias de comandos de renderización y otros datos.

Los nodos definen la estructura de contenido y sus propiedades almacenan el contenido real y los metadatos.

Los nodos de contenido dirigen el procesamiento. Sling obtiene el nodo de contenido de la solicitud entrante. La propiedad sling:resourceType de este nodo apunta al componente de renderización Sling que se va a utilizar.

Un nodo, que es un nombre JCR, también se denomina recurso en el entorno Sling.

Por ejemplo, para obtener las propiedades del nodo actual, puede utilizar el siguiente código en la secuencia de comandos:

`PropertyIterator properties = currentNode.getProperties();`

Con currentNode siendo el objeto node actual.

Para obtener más información sobre la manipulación de objetos Node, consulte [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**** WidgetIn AEM todas las entradas del usuario están administradas por widgets. A menudo se utilizan para controlar la edición de un fragmento de contenido.

Los cuadros de diálogo se crean combinando utilidades.

AEM ha sido desarrollado utilizando la biblioteca de widgets de ExtJS.

**** El cuadro de diálogoA es un tipo especial de utilidad.

Para editar contenido, AEM utiliza los cuadros de diálogo definidos por el desarrollador de la aplicación. Combinan una serie de utilidades para presentar al usuario todos los campos y acciones necesarios para editar el contenido relacionado.

Los cuadros de diálogo también se utilizan para editar metadatos y por diversas herramientas administrativas.

**** ComponenteUn componente de software es un elemento del sistema que ofrece un servicio o evento predefinido y que puede comunicarse con otros componentes.

En AEM, un componente se utiliza a menudo para representar el contenido de un recurso. Cuando el recurso es una página, el componente que lo procesa se denomina componente de nivel superior o componente de página. Sin embargo, un componente no tiene que representar contenido ni estar vinculado a un recurso específico; por ejemplo, un componente de navegación mostrará información sobre varios recursos.

La definición de un componente incluye:,

* el código utilizado para procesar el contenido
* un cuadro de diálogo para la entrada del usuario y la configuración del contenido resultante.

**** PlantillaUna plantilla es la base de un tipo específico de página. Al crear una página en la ficha Sitios web , el usuario debe seleccionar una plantilla. La nueva página se crea copiando esta plantilla.

Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Define el componente de página que se utiliza para procesar la página y el contenido predeterminado (contenido principal de nivel superior). El contenido define cómo se procesa como AEM está centrado en el contenido.

**Componente de página (componente de nivel superior)** El componente que se utilizará para procesar la página.

**** PáginaA es una &quot;instancia&quot; de una plantilla.

Una página tiene un nodo de jerarquía de tipo cq:Page y un nodo de contenido de tipo cq:PageContent. La propiedad sling:resourceType del nodo de contenido apunta al componente de página utilizado para procesar la página.

Por ejemplo, para obtener el nombre de la página actual, puede utilizar el siguiente código en la secuencia de comandos:

S`tring pageName = currentPage.getName();`

Con currentPage como el objeto de página actual. Para obtener más información sobre la manipulación de objetos de página, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Administrador** de páginasEl administrador de páginas es una interfaz que proporciona métodos para las operaciones a nivel de página.

Por ejemplo, para obtener la página contenedora de un recurso, puede utilizar el siguiente código en el script:

Page myPage = pageManager.getContainPage(myResource);

Con pageManager como el objeto de administrador de páginas y myResource como un objeto de recurso. Para obtener más información sobre los métodos proporcionados por el administrador de páginas, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece una descripción general de la estructura que verá dentro del repositorio.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado.
>
>Los cambios son necesarios cuando se desarrolla, pero debe asegurarse de comprender plenamente las implicaciones de cualquier cambio que realice.

>[!CAUTION]
>
>No debe cambiar nada en la ruta `/libs`. Para cambios de configuración y otros cambios, copie el elemento de `/libs` a `/apps` y realice cualquier cambio dentro de `/apps`.

* `/apps`

   Aplicación relacionada; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/foundation/components`.

* `/content`

   Contenido creado para el sitio web.

* `/etc`

* `/home`

   Información de usuarios y grupos.

* `/libs`

   Bibliotecas y definiciones que pertenecen al núcleo de AEM. Las subcarpetas de `/libs` representan las funciones predeterminadas de AEM como, por ejemplo, búsqueda o replicación. El contenido de `/libs` no debe modificarse ya que afecta al modo en que funciona AEM. Las funciones específicas del sitio web deben desarrollarse en `/apps` (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Área de trabajo temporal.

* `/var`

   Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y gestión de eventos.

## Entornos {#environments}

Con AEM, un entorno de producción a menudo consta de dos tipos diferentes de instancias: un [Autor y una instancia de publicación](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher es la herramienta de Adobe tanto para el almacenamiento en caché como para el equilibrio de carga. Encontrará más información en [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema de revisión de origen) {#filevault-source-revision-system}

FileVault proporciona su repositorio JCR con asignación de sistemas de archivos y control de versiones. Se puede utilizar para administrar AEM proyectos de desarrollo con compatibilidad total para almacenar y versionar código de proyecto, contenido, configuraciones, etc., en sistemas de control de versiones estándar (por ejemplo, Subversion).

Consulte la documentación [FileVault tool](/help/sites-developing/ht-vlttool.md) para obtener información detallada.

## Flujos de trabajo {#workflows}

El contenido suele estar sujeto a procesos organizativos, incluidos pasos como la aprobación y la desactivación por parte de varios participantes. Estos procesos pueden representarse como flujos de trabajo, [definidos y desarrollados dentro de AEM](/help/sites-developing/workflows-models.md) y luego aplicarse a las [páginas de contenido apropiadas](/help/sites-administering/workflows.md) o [activos digitales](/help/assets/assets-workflow.md) según sea necesario.

El motor de flujo de trabajo se utiliza para administrar la implementación de los flujos de trabajo y su aplicación posterior al contenido.

## Administración de varios sitios {#multi-site-management}

Multi Site Manager (MSM) le permite administrar fácilmente varios sitios web que comparten contenido común. MSM permite definir relaciones entre los sitios para que los cambios de contenido en un sitio se replicen automáticamente en otros.

Por ejemplo, los sitios web se proporcionan a menudo en varios idiomas para audiencias internacionales. Cuando el número de sitios en el mismo idioma es bajo (de tres a cinco), es posible realizar un proceso manual para sincronizar el contenido entre sitios. Sin embargo, tan pronto como el número de sitios crece o cuando hay varios idiomas involucrados, se vuelve más eficiente automatizar el proceso.

* Administre de manera eficiente versiones de diferentes idiomas de un sitio web.
* Actualizar automáticamente uno o más sitios según un sitio de origen:

   * Aplique una estructura de base común y utilice contenido común en varios sitios.
   * Maximice el uso de los recursos disponibles.
   * Mantenga un aspecto común.
   * Enfoque los esfuerzos en la administración del contenido que difiere entre los sitios.

Para obtener más información, consulte [Multi Site Manager](/help/sites-administering/msm.md).
