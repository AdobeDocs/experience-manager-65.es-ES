---
title: AEM Conceptos principales de
seo-title: The Basics
description: AEM Una descripción general de los conceptos principales de cómo se estructura la y cómo desarrollarla, incluidos los conceptos básicos de JCR, Sling, OSGi, Dispatcher, flujos de trabajo y MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 1%

---

# AEM Conceptos principales de {#aem-core-concepts}

>[!NOTE]
>
>AEM Antes de sumergirse en los conceptos básicos de la, Adobe recomienda completar el Tutorial de WKND en la [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md) AEM documento para obtener una descripción general del proceso de desarrollo de la e introducción a los conceptos principales.

## AEM Requisitos previos para el desarrollo de la {#prerequisites-for-developing-on-aem}

AEM Necesita las siguientes habilidades para desarrollar sobre la parte superior de la:

* Conocimientos básicos de las técnicas de aplicación web, incluidos:

   * el ciclo de solicitud-respuesta (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conocimientos prácticos de Experience Server (CRX), incluido el Explorador de contenido
* Para desarrollar en la IU clásica, también se requieren conocimientos básicos de JSP (JavaServer Pages), incluida la capacidad de comprender y modificar ejemplos de JSP simples.

También se recomienda que lea y siga las [Directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositorio de contenido de Java™ {#java-content-repository}

El estándar Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido.

El plomo de la especificación es poseído por Adobe Research (Suiza) AG.

El [API JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) paquete, javax.jcr.&amp;ast; se utiliza para el acceso directo y la manipulación del contenido del repositorio.

## Experience Server (CRX) y Jackrabbit {#experience-server-crx-and-jackrabbit}

AEM El servidor de experiencia proporciona los servicios de experiencia en los que se basa la y que pueden utilizarse para crear aplicaciones personalizadas e incrusta el repositorio de contenido basado en Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) es una implementación de código abierto, totalmente conforme, de la API 2.0 de JCR.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

### Introducción a Sling {#introduction-to-sling}

AEM se crea usando el [Sling](https://sling.apache.org/index.html), un marco de trabajo de aplicaciones web basado en principios REST que proporciona un fácil desarrollo de aplicaciones orientadas a contenido. AEM Sling utiliza un repositorio JCR, como Apache Jackrabbit o, en el caso de los recursos, el repositorio de contenido CRX, como repositorio de datos. Sling ha sido colaborador de Apache Software Foundation; puede encontrar más información en Apache.

Con Sling, el tipo de contenido que se procesará no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL responde a un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Esto proporciona una excelente compatibilidad para que los autores de contenido web creen páginas que se personalicen fácilmente según sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando necesita páginas que se puedan personalizar fácilmente. AEM En particular, al implementar un sistema de administración de contenido web como WCM en la solución de la aplicación de la interfaz de usuario de la aplicación de la aplicación de la solución de la aplicación de la solución de la aplicación de la plataforma de administración de contenido web.

Consulte [Descubra Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución de scripts de Sling: se muestra cómo ir de una solicitud HTTP al nodo de contenido, de un nodo de contenido al tipo de recurso, de un tipo de recurso al script y qué variables de scripts están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos, pero útiles, que puede utilizar al trabajar con SlingPostServlet, el controlador predeterminado para todas las solicitudes de POST, que le ofrece un sinfín de opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling es *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* el primer destino es el recurso (nodo JCR) que contiene el contenido
* en segundo lugar, la representación o script se encuentra en las propiedades del recurso combinadas con ciertas partes de la solicitud (por ejemplo, los selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a la filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* muy RESTful, no solo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* elimina uno o varios modelos de datos

   * anteriormente se necesitaban los siguientes elementos: estructura URL, objetos empresariales, esquema de base de datos;
   * esto ahora se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se basa en la dirección URL de la solicitud del usuario. Esto define el contenido que deben mostrar los scripts adecuados. Para ello, se extrae información de la dirección URL.

Si analizamos la siguiente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividirlo en sus partes compuestas:

| protocolo | host | ruta de contenido | selector(es) | extensión |  | sufijo |  | parámetro(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | herramientas/espía | .printable.a4. | html | / | a/b | ? | x=12 |

**protocolo** HTTP

**host** Nombre del sitio web.

**ruta de contenido** Ruta que especifica el contenido que se va a procesar. Se utiliza en combinación con la extensión; en este ejemplo, se traducen a tools/spy.html.

**selector(es)** Se utiliza para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4.

**extensión** Formato del contenido; también especifica el script que se utilizará para el procesamiento.

**sufijo** Se puede utilizar para especificar información adicional.

**parámetro(s)** Cualquier parámetro necesario para el contenido dinámico.

#### De la URL al contenido y los scripts {#from-url-to-content-and-scripts}

Uso de estos principios:

* la asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso
* cuando se encuentra el recurso adecuado, se extrae el tipo de recurso sling y se utiliza para localizar la secuencia de comandos que se utilizará para representar el contenido

La figura siguiente ilustra el mecanismo utilizado, que se analizará con más detalle en las secciones siguientes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, puede especificar qué secuencia de comandos procesa una entidad determinada (configurando la variable `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como lo haría una instrucción SQL en un script PHP), ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca el recurso solicitado en el repositorio (nodo de contenido):

* first Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; por ejemplo, `../content/corporate/jobs/developer.html`
* si no se encuentra ningún nodo, la extensión se suelta y la búsqueda se repite; por ejemplo, `../content/corporate/jobs/developer`
* si no se encuentra ningún nodo, Sling devolverá el código http 404 (no encontrado).

Sling también permite que otras cosas que no sean nodos JCR sean recursos, pero esta es una función avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso adecuado (nodo de contenido), la variable **tipo de recurso de sling** se ha extraído. Esta es una ruta que localiza el script que se utilizará para procesar el contenido.

La ruta especificada por el `sling:resourceType` puede ser:

* absoluto
* relativo, a un parámetro de configuración

  El Adobe recomienda las rutas relativas a medida que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` o `/libs`, que se buscarán en este orden (consulte [Personalizar componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Otros puntos que hay que tener en cuenta son:

* cuando se requiere el método (GET, POST), se especifica en mayúsculas como según la especificación HTTP, por ejemplo, jobs.POST.esp (consulte a continuación)
* se admiten varios motores de scripts:

   * HTL (lenguaje de plantilla de HTML: el sistema de plantillas del lado de servidor recomendado por Adobe Experience Manager para HTML): `.html`
   * Páginas de ECMAScript (JavaScript) (ejecución del lado del servidor): `.esp, .ecma`
   * Java™ Server Pages (ejecución del lado del servidor): `.jsp`
   * Compilador de servlet Java™ (ejecución del lado del servidor): `.java`
   * Plantillas JavaScript (ejecución del lado del cliente): `.jst`

AEM La lista de motores de scripts admitidos por la instancia determinada de se enumera en la consola de administración de Felix ( ). `http://<host>:<port>/system/console/slingscripting`).

Además, Apache Sling admite la integración con otros motores de scripts populares (por ejemplo, Groovy, JRuby, Freemarker) y proporciona una forma de integrar nuevos motores de scripts.

En el ejemplo anterior, si la variable `sling:resourceType` es `hr/jobs` y luego para:

* Solicitudes de GET/HEAD y direcciones URL que terminan en .html (tipos de solicitud predeterminados, formato predeterminado)

  La secuencia de comandos es /apps/hr/jobs/jobs.esp; la última sección de sling:resourceType forma el nombre del archivo.

* Solicitudes de POST (todos los tipos de solicitud excepto GET/HEAD, el nombre del método debe estar en mayúsculas)

  Se utiliza el POST en el nombre del script.

  El script es `/apps/hr/jobs/jobs.POST.esp`.

* Direcciones URL en otros formatos que no terminan con .html

  Por ejemplo, `../content/corporate/jobs/developer.pdf`

  El script será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre del script.

* URL con selectores

  Los selectores se pueden utilizar para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente RSS o un resumen.

  Si miramos una versión compatible con la impresora donde el selector podría ser *imprimir*; como en `../content/corporate/jobs/developer.print.html`

  El script será `/apps/hr/jobs/jobs.print.esp`; el selector se añade al nombre del script.

* Si no se ha definido sling:resourceType:

   * la ruta de contenido se utilizará para buscar un script adecuado (si el ResourceTypeProvider basado en la ruta está activo).

     Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.

   * se utilizará el tipo de nodo principal.

* Si no se encuentra ninguna secuencia de comandos, se utilizará la predeterminada.

  Actualmente, la representación predeterminada es compatible con texto sin formato (.txt), HTML (.html) y JSON (.json), todos los cuales enumeran las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión .res o las solicitudes sin extensión de solicitud es poner en cola el recurso (cuando sea posible).
* Para la gestión de errores http (códigos 403 o 404), Sling buscará un script en:

   * la ubicación /apps/sling/servlet/errorhandler para [scripts personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la ubicación de las secuencias de comandos estándar /libs/sling/servlet/errorhandler/403.esp o 404.esp respectivamente.

Si se aplican varios scripts a una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; es decir, cuanto más coincida el selector, mejor, independientemente de la coincidencia de cualquier extensión de solicitud o nombre de método.

Por ejemplo, considere una solicitud de acceso al recurso
`/content/corporate/jobs/developer.print.a4.html`
de tipo
`sling:resourceType="hr/jobs"`

Suponiendo que tenemos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por el `sling:resourceType` propiedad) también está el supertipo de recurso. Esto generalmente se indica mediante la variable `sling:resourceSuperType` propiedad. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos donde el tipo de recurso predeterminado es `sling/servlet/default` (utilizado por los servlets predeterminados) es en realidad la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por el `sling:resourceSuperType` propiedad del recurso.
* por el `sling:resourceSuperType` propiedad del nodo al que se va a `sling:resourceType` puntos.

Por ejemplo:

* /

   * a
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

Esto se debe a `/y` tiene el `sling:resourceSuperType` propiedad mientras que `/x` no y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### Los scripts de Sling no se pueden llamar directamente {#sling-scripts-cannot-be-called-directly}

En Sling, no se puede llamar directamente a los scripts, ya que esto rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculta el recurso dentro de la secuencia de comandos, por lo que el marco de trabajo (Sling) ya no sabe nada de él. Por lo tanto, se pierden ciertas funciones:

* administración automática de métodos http distintos de la GET, incluidos:

   * POST, PUT y DELETE que se gestionan con una implementación predeterminada de sling
   * el `POST.jsp` en la ubicación sling:resourceType

* su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; es de vital importancia para el desarrollo a gran escala

### API Sling {#sling-api}

Utiliza el paquete de API de Sling, org.apache.sling.&amp;ast; y bibliotecas de etiquetas.

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los guiones.

Es posible que los scripts más complejos (agregar scripts) necesiten acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página, elementos de una lista) y hacerlo incluyendo la variable *resource*.

Para ello, puede utilizar el sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Esto incluirá efectivamente la definición del recurso al que se hace referencia, como en la siguiente instrucción que hace referencia a una definición existente para procesar imágenes:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se conoce como Sistema de módulos dinámicos para Java). Los contenedores OSGi le permiten dividir la aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en la terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* servicios implementados dentro del contenedor
* un contrato entre el contenedor y la aplicación

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse dinámicamente entre sí para colaborar.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [Sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. Sling, y por lo tanto CQ5, utiliza el [Apache Felix](https://felix.apache.org/documentation/index.html) Implementación de OSGI (iniciativa Open Services Gateway) y se basa en las especificaciones de la versión 4.2 de la plataforma de servicio OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* instalar
* start
* parada
* actualizar
* desinstalar
* ver el estado actual
* acceda a información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [la consola web](/help/sites-deploying/web-console.md), [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) y [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener más información.

## AEM Objetos de desarrollo en el entorno de la {#development-objects-in-the-aem-environment}

Los siguientes son de interés para el desarrollo:

**Elemento** Un elemento es un nodo o una propiedad.

Para obtener información detallada sobre la manipulación de objetos Item, consulte la [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) de la interfaz javax.jcr.Item

**Nodo (y sus propiedades)** Los nodos y sus propiedades se definen en la especificación JCR API 2.0 (JSR 283). Almacenan contenido, definiciones de objetos, secuencias de comandos de procesamiento y otros datos.

Los nodos definen la estructura de contenido y sus propiedades almacenan el contenido y los metadatos reales.

Los nodos de contenido dirigen la renderización. Sling obtiene el nodo de contenido de la solicitud entrante. La propiedad sling:resourceType de este nodo señala al componente de procesamiento Sling que se va a utilizar.

Un nodo, que es un nombre JCR, también se denomina recurso en el entorno de Sling.

Por ejemplo, para obtener las propiedades del nodo actual, puede utilizar el siguiente código en el script:

`PropertyIterator properties = currentNode.getProperties();`

Con currentNode siendo el objeto de nodo actual.

Para obtener más información sobre la manipulación de objetos Node, consulte la [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** AEM En todos los casos, los widgets administran la entrada del usuario. Suelen utilizarse para controlar la edición de un fragmento de contenido.

Los cuadros de diálogo se crean combinando widgets.

AEM Se ha desarrollado la biblioteca de widgets de ExtJS para utilizar.

**Diálogo** Un cuadro de diálogo es un tipo especial de widget.

AEM Para editar contenido, utiliza los cuadros de diálogo definidos por el desarrollador de la aplicación. Estos combinan una serie de widgets para presentar al usuario todos los campos y acciones necesarios para editar el contenido relacionado.

Los cuadros de diálogo también se utilizan para editar metadatos y para varias herramientas administrativas.

**Componente** Un componente de software es un elemento del sistema que ofrece un servicio o evento predefinido y que puede comunicarse con otros componentes.

AEM Dentro de un componente se utiliza a menudo para representar el contenido de un recurso. Cuando el recurso es una página, el componente que lo procesa se denomina componente de nivel superior o componente de página. Sin embargo, un componente no tiene que procesar contenido ni estar vinculado a un recurso específico; por ejemplo, un componente de navegación mostrará información sobre varios recursos.

La definición de un componente incluye:,

* el código utilizado para procesar el contenido
* un cuadro de diálogo para la entrada del usuario y la configuración del contenido resultante.

**Plantilla** Una plantilla es la base de un tipo de página específico. Al crear una página en la pestaña Sitios web, el usuario debe seleccionar una plantilla. A continuación, la nueva página se crea copiando esta plantilla.

Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Define el componente de página utilizado para procesar la página y el contenido predeterminado (contenido principal de nivel superior). AEM El contenido define cómo se procesa, ya que está centrado en el contenido.

**Componente Página (componente de nivel superior)** Componente que se utilizará para procesar la página.

**Página** Una página es una &quot;instancia&quot; de plantilla.

Una página tiene un nodo de jerarquía de tipo cq:Page y un nodo de contenido de tipo cq:PageContent. La propiedad sling:resourceType del nodo de contenido señala al componente de página utilizado para procesar la página.

Por ejemplo, para obtener el nombre de la página actual, puede utilizar el siguiente código en el script:

S`tring pageName = currentPage.getName();`

Con currentPage como objeto de la página actual. Para obtener más información sobre la manipulación de objetos Page, consulte la [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**Administrador de páginas** El administrador de páginas es una interfaz que proporciona métodos para operaciones de nivel de página.

Por ejemplo, para obtener la página contenedora de un recurso, puede utilizar el siguiente código en el script:

Página myPage = pageManager.getContainingPage(myResource);

Con pageManager como objeto de administrador de páginas y myResource como objeto de recurso. Para obtener más información sobre los métodos proporcionados por el administrador de página, consulte la [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece información general sobre la estructura que se ve dentro del repositorio.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado.
>
>Los cambios son necesarios cuando está desarrollando, pero debe tener cuidado de comprender completamente las implicaciones de cualquier cambio que realice.

>[!CAUTION]
>
>No cambie nada en `/libs` ruta. Para cambios de configuración y de otro tipo, copie el elemento de `/libs` hasta `/apps` y realice cualquier cambio en `/apps`.

* `/apps`

  Relacionado con la aplicación; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/foundation/components`.

* `/content`

  Contenido creado para su sitio web.

* `/etc`

* `/home`

  Información de usuario y grupo.

* `/libs`

  AEM Bibliotecas y definiciones que pertenecen al núcleo de la. Las subcarpetas de `/libs` AEM representan las funciones de administración de listas para usar, como la búsqueda o la replicación, de forma predeterminada. El contenido de `/libs` AEM no debe modificarse, ya que afecta al modo en que funciona la. Las funciones específicas del sitio web deben desarrollarse en `/apps` (consulte [Personalizar componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

  Zona de trabajo temporal.

* `/var`

  Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y control de eventos.

## Entornos {#environments}

AEM Con un entorno de producción de datos a menudo consta de dos tipos diferentes de instancias: una [Instancias de autor y publicación](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher es la herramienta de Adobe para el almacenamiento en caché o el equilibrio de carga. Encontrará más información en [el Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

## FileVault (sistema de revisión de origen) {#filevault-source-revision-system}

FileVault proporciona a su repositorio JCR la asignación del sistema de archivos y el control de versiones. AEM Se puede utilizar para administrar proyectos de desarrollo de la con soporte total para almacenar y crear versiones del código del proyecto, contenido, configuraciones, etc., en sistemas estándar de control de versiones (por ejemplo, Subversion).

Consulte la [Herramienta FileVault](/help/sites-developing/ht-vlttool.md) para obtener información detallada.

## Flujos de trabajo {#workflows}

El contenido suele estar sujeto a procesos organizativos, incluidos pasos como la aprobación y la aprobación por parte de varios participantes. Estos procesos se pueden representar como flujos de trabajo, [AEM definido y desarrollado dentro de la red de](/help/sites-developing/workflows-models.md)y luego se aplica a [páginas de contenido apropiadas](/help/sites-administering/workflows.md) o [recursos digitales](/help/assets/assets-workflow.md) según sea necesario.

El motor de flujo de trabajo se utiliza para administrar la implementación de los flujos de trabajo y la aplicación posterior al contenido.

## Administración de varios sitios {#multi-site-management}

El Administrador de varios sitios (MSM) le permite administrar fácilmente varios sitios web que comparten contenido común. MSM le permite definir relaciones entre los sitios para que los cambios de contenido en un sitio se dupliquen automáticamente en otros.

Por ejemplo, los sitios web a menudo se ofrecen en varios idiomas para audiencias internacionales. Cuando el número de sitios en el mismo idioma es bajo (de tres a cinco), es posible realizar un proceso manual de sincronización de contenido entre sitios. Sin embargo, cuando el número de sitios aumenta o cuando hay varios idiomas implicados, es más eficiente automatizar el proceso.

* Gestionar de forma eficaz las distintas versiones lingüísticas de un sitio web.
* Actualizar automáticamente uno o varios sitios en función de un sitio de origen:

   * Haga cumplir una estructura base común y utilice contenido común en varios sitios.
   * Maximice el uso de los recursos disponibles.
   * Mantenga un aspecto común.
   * Centrar los esfuerzos en administrar el contenido que difiere entre los sitios.

Para obtener más información, consulte [Administrador de varios sitios](/help/sites-administering/msm.md).
