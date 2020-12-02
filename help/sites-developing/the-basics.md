---
title: Conceptos principales AEM
seo-title: Conceptos básicos
description: Una visión general de los conceptos básicos de cómo se estructura la AEM y cómo desarrollarse sobre ella, incluyendo la comprensión del JCR, Sling, OSGi, el expedidor, los flujos de trabajo y MSM
seo-description: Una visión general de los conceptos básicos de cómo se estructura la AEM y cómo desarrollarse sobre ella, incluyendo la comprensión del JCR, Sling, OSGi, el expedidor, los flujos de trabajo y MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: d621a612556f0bea032444c2e07be101868b1905
workflow-type: tm+mt
source-wordcount: '3371'
ht-degree: 0%

---


# Conceptos principales de AEM {#aem-core-concepts}

>[!NOTE]
>
>Antes de profundizar en los conceptos básicos de AEM, Adobe recomienda completar el tutorial de WKND en el documento [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md) para obtener una visión general del proceso de desarrollo de AEM e introducción a los conceptos básicos.

## Requisitos previos para desarrollar en AEM {#prerequisites-for-developing-on-aem}

Necesitará las siguientes habilidades para desarrollar sobre AEM:

* Conocimientos básicos de las técnicas de aplicación web, incluidos:

   * ciclo de solicitud -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conocimientos prácticos de Experience Server (CRX), incluido Content Explorer
* Para desarrollarse en la IU clásica, también se requieren conocimientos básicos de JSP (JavaServer Pages), incluida la capacidad de comprender y modificar ejemplos JSP sencillos.

También se recomienda leer y seguir las [Pautas y optimizaciones](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositorio de contenido Java {#java-content-repository}

El estándar de Java Content Repository (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica una manera independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido.

Adobe Research (Suiza) AG es el responsable de la especificación.

El paquete [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), javax.jcr.&amp;ast; se utiliza para el acceso directo y la manipulación del contenido del repositorio.

## Experience Server (CRX) y Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server proporciona los servicios de experiencia en los que se AEM y que se pueden aprovechar para crear aplicaciones personalizadas, e incrusta el repositorio de contenido basado en Jackrabbit.

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis es una implementación de código abierto, totalmente conforme, de la API de JCR 2.0.

## Procesamiento de solicitudes Sling {#sling-request-processing}

### Introducción a Sling {#introduction-to-sling}

AEM se crea mediante [Sling](https://sling.apache.org/site/index.html), un marco de Aplicación web basado en los principios REST que proporciona un fácil desarrollo de aplicaciones orientadas al contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit, o en el caso de AEM, el Repositorio de contenido CRX, como su almacén de datos. Sling ha sido aportado a la Apache Software Foundation - más información se puede encontrar en Apache.

Con Sling, el tipo de contenido que se va a procesar no es la primera consideración de procesamiento. En su lugar, la principal consideración es si la dirección URL se resuelve en un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la representación. Esto proporciona una excelente compatibilidad a los autores de contenido web para crear páginas que se adapten fácilmente a sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando se necesitan páginas que se puedan personalizar fácilmente. En particular, al implementar un sistema de Gestor de contenido Web como WCM en la solución AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución del script Sling: muestra cómo pasar de una solicitud HTTP a un nodo de contenido, de un nodo de contenido a un tipo de recurso, de un tipo de recurso a una secuencia de comandos y qué variables de secuencias de comandos están disponibles.

![Explicación de la resolución de secuencias de comandos de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos pero potentes que puede utilizar al trabajar con SlingPostServlet, el controlador predeterminado para todas las solicitudes de POST que le ofrece infinitas opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling está *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* el primer destinatario es el recurso (nodo JCR) que contiene el contenido
* en segundo lugar, la representación, o secuencia de comandos, se encuentra desde las propiedades del recurso en combinación con determinadas partes de la solicitud (por ejemplo, selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a la filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, presenta un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* muy RESTful, no sólo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* elimina uno o más modelos de datos

   * anteriormente se necesitaban los siguientes elementos: estructura URL, objetos comerciales, esquema de base de datos;
   * ahora se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se controla mediante la dirección URL de la solicitud de usuario. Define el contenido que deben mostrar las secuencias de comandos correspondientes. Para ello, la información se extrae de la dirección URL.

Si analizamos la siguiente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos desglosarlo en sus partes compuestas:

| protocolo | host | ruta de contenido | selector(s) | extension |  | sufijo |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | herramientas/espionaje | .printable.a4. | html | / | a/b | ? | x=12 |

**** protocolHTTP

**** hostName del sitio web.

**content** pathPath que especifica el contenido que se va a representar. Se utiliza en combinación con la extensión; en este ejemplo se traducen a tools/spy.html.

**selector(s)** Se utiliza para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4.

**formato** extensionContent; también especifica la secuencia de comandos que se utilizará para la representación.

**** sufijoSe puede utilizar para especificar información adicional.

**param(s)** Cualquier parámetro requerido para contenido dinámico.

#### De URL a contenido y secuencias de comandos {#from-url-to-content-and-scripts}

Utilizando estos principios:

* la asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso
* cuando se encuentra el recurso apropiado, se extrae el tipo de recurso sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido

En la figura siguiente se ilustra el mecanismo utilizado, que se analizará con más detalle en las secciones siguientes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, se especifica qué secuencia de comandos procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo oferta más libertad que uno en el que la secuencia de comandos accede a las entidades de datos (como haría una instrucción SQL en una secuencia de comandos PHP) ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca en el repositorio el recurso solicitado (nodo de contenido):

* first Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; p. ej. `../content/corporate/jobs/developer.html`
* si no se encuentra ningún nodo, se interrumpe la extensión y se repite la búsqueda; p. ej. `../content/corporate/jobs/developer`
* si no se encuentra ningún nodo, Sling devolverá el código http 404 (no encontrado).

Sling también permite que otros elementos que no sean nodos JCR sean recursos, pero se trata de una característica avanzada.

### Localización de la secuencia de comandos {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae el **tipo de recurso sling**. Se trata de una ruta que localiza la secuencia de comandos que se utilizará para procesar el contenido.

La ruta especificada por `sling:resourceType` puede ser:

* absoluto
* relativo, a un parámetro de configuración

   Las rutas relativas se recomiendan por Adobe, ya que aumentan la portabilidad.

Todas las secuencias de comandos de Sling se almacenan en subcarpetas de `/apps` o `/libs`, que se buscarán en este orden (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Otros puntos a tener en cuenta son:

* cuando se requiera el método (GET, POST), se especificará en mayúsculas según la especificación HTTP, por ejemplo: job.POST.esp (ver más abajo)
* se admiten varios motores de secuencias de comandos:

   * `.esp, .ecma`:: Páginas de ECMAScript (JavaScript) (ejecución en el servidor)
   * `.jsp`:: Java Server Pages (ejecución en el servidor)
   * `.java`:: Compilador de servlet Java (ejecución en el servidor)
   * `.jst`:: Plantillas de JavaScript (ejecución del cliente)

La lista de los motores de secuencias de comandos admitidos por la instancia de AEM dada se muestra en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

Además, Apache Sling admite la integración con otros motores de secuencias de comandos populares (por ejemplo, Groovy, JRuby, Freemarker) y proporciona una manera de integrar nuevos motores de secuencias de comandos.

Usando el ejemplo anterior, si `sling:resourceType` es `hr/jobs` entonces para:

* Solicitudes de GET/HEAD y direcciones URL que finalizan en .html (tipos de solicitud predeterminados, formato predeterminado)

   El script será /apps/hr/jobs/jobs.esp; la última sección de sling:resourceType forma el nombre del archivo.

* Solicitudes de POST (todos los tipos de solicitud, excluyendo GET/HEAD, el nombre del método debe estar en mayúsculas)

   POST se utilizará en el nombre de la secuencia de comandos.

   La secuencia de comandos será `/apps/hr/jobs/jobs.POST.esp`.

* Direcciones URL en otros formatos, sin terminar con .html

   Por ejemplo `../content/corporate/jobs/developer.pdf`

   La secuencia de comandos será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre de la secuencia de comandos.

* Direcciones URL con selectores

   Los selectores pueden utilizarse para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente RSS o un resumen.

   Si vemos una versión descriptiva de la impresora en la que el selector podría ser *print*; como en `../content/corporate/jobs/developer.print.html`

   La secuencia de comandos será `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre de la secuencia de comandos.

* Si no se ha definido ningún sling:resourceType:

   * la ruta de contenido se utilizará para buscar una secuencia de comandos adecuada (si la ruta basada en ResourceTypeProvider está activa).

      Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.

   * se utilizará el tipo de nodo principal.

* Si no se encuentra ninguna secuencia de comandos, se utilizará la secuencia de comandos predeterminada.

   La representación predeterminada se admite actualmente como texto sin formato (.txt), HTML (.html) y JSON (.json), todos los cuales lista las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión .res, o solicitudes sin extensión de solicitud, es bloquear el recurso (cuando sea posible).
* Para la gestión de errores http (códigos 403 o 404) Sling buscará una secuencia de comandos en:

   * la ubicación /apps/sling/servlet/errorhandler para [scripts personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la ubicación de las secuencias de comandos estándar /libs/sling/servlet/errorhandler/403.esp o 404.esp, respectivamente.

Si se aplican varias secuencias de comandos para una solicitud determinada, se selecciona la secuencia de comandos con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; en otras palabras, cuanto más selector coincida mejor, independientemente de la coincidencia de la extensión de solicitud o el nombre del método.

Por ejemplo, considere una solicitud de acceso al recurso
`/content/corporate/jobs/developer.print.a4.html`
de tipo
`sling:resourceType="hr/jobs"`

Supongamos que tenemos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por la propiedad `sling:resourceType`) también está el supertipo de recurso. Esto se indica generalmente mediante la propiedad `sling:resourceSuperType`. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos en la que el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) es la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que apunta `sling:resourceType`.

Por ejemplo:

* /

   * una
   * b)

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




La jerarquía de tipos de:

* `/x`
   *  es`[ c, b, a, <default>]`
* while para `/y`
   * la jerarquía es `[ c, a, <default>]`

Esto se debe a que `/y` tiene la propiedad `sling:resourceSuperType`, mientras que `/x` no la tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### No se puede llamar directamente a los scripts de Sling {#sling-scripts-cannot-be-called-directly}

Dentro de Sling, no se pueden llamar directamente a las secuencias de comandos, ya que esto rompería el concepto estricto de un servidor REST; combinaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculte el recurso dentro de la secuencia de comandos, de modo que la estructura (Sling) ya no lo sepa. Por lo tanto, se pierden ciertas funciones:

* administración automática de métodos http distintos de la GET, incluidos:

   * POST, PUT y DELETE que se administran con una implementación predeterminada de sling
   * la secuencia de comandos `POST.jsp` de la ubicación sling:resourceType

* su arquitectura de código ya no es tan limpia ni tan claramente estructurada como debería ser; de importancia primordial para el desarrollo a gran escala

### Sling API {#sling-api}

Utiliza el paquete de la API de Sling, org.apache.sling.Bibliotecas de etiquetas &amp;ast; y .

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los scripts.

Las secuencias de comandos más complejas (agregación de secuencias de comandos) pueden necesitar acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página, elementos de una lista) y hacerlo incluyendo el *recurso*.

Para ello, puede utilizar el comando sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Esto incluirá efectivamente la definición del recurso al que se hace referencia, como en la siguiente instrucción, que hace referencia a una definición existente para procesar imágenes:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se conoce como Sistema de módulos dinámicos para Java). Los contenedores OSGi permiten dividir la aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en terminología OSGi) y administrar las interdependencias entre ellos con:

* servicios implementados en el contenedor
* un contrato entre el contenedor y su solicitud

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrir entre sí dinámicamente para colaboración.

Una estructura OSGi le oferta la carga/descarga dinámica, la configuración y el control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [sitio Web OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. Sling, y por lo tanto CQ5, utiliza la implementación [Apache Felix](https://felix.apache.org/) de OSGI (iniciativa Open Services Gateway) y se basa en las especificaciones de la versión 4.2 de OSGi Service Platform. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* instalar
* inicio
* stop
* actualizar
* desinstalar
* ver el estado actual
* acceder a información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [Configuración de la consola web](/help/sites-deploying/web-console.md), [OSGI](/help/sites-deploying/configuring-osgi.md) y [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener más información.

## Objetos de desarrollo en el Entorno de AEM {#development-objects-in-the-aem-environment}

Los siguientes son de interés para el desarrollo:

**** ItemUn elemento es un nodo o una propiedad.

Para obtener información detallada sobre la manipulación de objetos Item, consulte [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) de la interfaz javax.jcr.Item

**Los nodos (y sus propiedades)** y sus propiedades se definen en la especificación JCR API 2.0 (JSR 283). Almacenan contenido, definiciones de objetos, secuencias de comandos de representación y otros datos.

Los nodos definen la estructura de contenido y sus propiedades almacenan el contenido y los metadatos reales.

Los nodos de contenido dirigen el procesamiento. Sling obtiene el nodo de contenido de la solicitud entrante. La propiedad sling:resourceType de este nodo apunta al componente de procesamiento Sling que se va a utilizar.

Un nodo, que es un nombre JCR, también se denomina recurso en el entorno Sling.

Por ejemplo, para obtener las propiedades del nodo actual, puede utilizar el siguiente código en la secuencia de comandos:

`PropertyIterator properties = currentNode.getProperties();`

Con currentNode siendo el objeto de nodo actual.

Para obtener más información sobre la manipulación de objetos Node, consulte [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**** WidgetEn AEM todos los datos introducidos por el usuario son administrados por widgets. A menudo se utilizan para controlar la edición de un fragmento de contenido.

Los cuadros de diálogo se crean combinando utilidades.

AEM ha sido desarrollado utilizando la biblioteca de utilidades ExtJS.

**** Cuadro de diálogoUn cuadro de diálogo es un tipo especial de utilidad.

Para editar contenido, AEM utiliza los cuadros de diálogo definidos por el desarrollador de la aplicación. Combinan una serie de utilidades para presentar al usuario todos los campos y acciones necesarios para editar el contenido relacionado.

Los diálogos también se utilizan para editar metadatos y por diversas herramientas administrativas.

**** ComponenteUn componente de software es un elemento del sistema que ofrece un servicio o evento predefinido y puede comunicarse con otros componentes.

En AEM, un componente se utiliza a menudo para representar el contenido de un recurso. Cuando el recurso es una página, el componente que lo procesa se denomina componente de nivel superior o componente de página. Sin embargo, un componente no tiene que representar contenido ni estar vinculado a un recurso específico; por ejemplo, un componente de navegación mostrará información sobre varios recursos.

La definición de un componente incluye:,

* el código utilizado para representar el contenido
* un cuadro de diálogo para la entrada del usuario y la configuración del contenido resultante.

**** PlantillaUna plantilla es la base para un tipo específico de página. Al crear una página en la ficha Sitios web, el usuario tiene que seleccionar una plantilla. La nueva página se crea copiando esta plantilla.

Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin ningún contenido real.

Define el componente de página utilizado para representar la página y el contenido predeterminado (contenido principal de nivel superior). El contenido define cómo se procesa como AEM se centra en el contenido.

**Componente de página (componente de nivel superior)** El componente que se utilizará para representar la página.

**** PáginaUna página es una &#39;instancia&#39; de una plantilla.

Una página tiene un nodo de jerarquía de tipo cq:Page y un nodo de contenido de tipo cq:PageContent. La propiedad sling:resourceType del nodo de contenido apunta al componente de página utilizado para procesar la página.

Por ejemplo, para obtener el nombre de la página actual, puede utilizar el siguiente código en la secuencia de comandos:

S`tring pageName = currentPage.getName();`

Con currentPage como objeto de página actual. Para obtener más información sobre la manipulación de objetos de página, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Administrador** de páginasEl administrador de páginas es una interfaz que proporciona métodos para las operaciones a nivel de página.

Por ejemplo, para obtener la página contenedora de un recurso, puede utilizar el siguiente código en la secuencia de comandos:

Page myPage = pageManager.getContainerPage(myResource);

Con pageManager como objeto de administrador de páginas y myResource como objeto de recurso. Para obtener más información sobre los métodos proporcionados por el administrador de páginas, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista proporciona una visión general de la estructura que verá dentro del repositorio.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben hacerse con cuidado.
>
>Los cambios son necesarios cuando se desarrolla, pero debe asegurarse de comprender completamente las implicaciones de cualquier cambio que realice.

>[!CAUTION]
>
>No debe cambiar nada en la ruta `/libs`. Para configuración y otros cambios, copie el elemento de `/libs` a `/apps` y realice cualquier cambio dentro de `/apps`.

* `/apps`

   Aplicación relacionada; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes listos para usar disponibles en `/libs/foundation/components`.

* `/content`

   Contenido creado para el sitio web.

* `/etc`

* `/home`

   Información de usuarios y grupos.

* `/libs`

   Bibliotecas y definiciones que pertenecen al núcleo del AEM. Las subcarpetas de `/libs` representan las funciones de AEM predeterminadas como, por ejemplo, búsqueda o replicación. El contenido de `/libs` no debe modificarse ya que afecta al modo de funcionamiento AEM. Las funciones específicas de su sitio Web deben desarrollarse en `/apps` (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Área de trabajo temporal.

* `/var`

   Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y gestión de eventos. La subcarpeta `/var/classes` contiene los servlets java en los formularios de origen y compilados que se han generado a partir de las secuencias de comandos de componentes.

## Entornos {#environments}

Con AEM, un entorno de producción suele constar de dos tipos diferentes de instancias: una [instancias de autor y publicación](/help/sites-deploying/deploy.md#author-and-publish-installs).

## El despachante {#the-dispatcher}

Dispatcher es la herramienta del Adobe para almacenamiento en caché y/o equilibrio de carga. Encontrará más información en [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema de revisión de origen) {#filevault-source-revision-system}

FileVault proporciona a su repositorio JCR asignación de file systems y control de versiones. Puede utilizarse para administrar proyectos de desarrollo AEM con total compatibilidad para almacenar y generar versiones del código del proyecto, el contenido, las configuraciones, etc., en sistemas de control de versiones estándar (por ejemplo, Subversion).

Consulte la documentación de la [herramienta FileVault](/help/sites-developing/ht-vlttool.md) para obtener información detallada.

## Flujos de trabajo {#workflows}

El contenido suele estar sujeto a procesos organizativos, incluidos pasos como aprobación y aprobación por parte de varios participantes. Estos procesos pueden representarse como flujos de trabajo, [definidos y desarrollados dentro de AEM](/help/sites-developing/workflows-models.md), luego aplicados a las [páginas de contenido apropiadas](/help/sites-administering/workflows.md) o [recursos digitales](/help/assets/assets-workflow.md) según sea necesario.

El Motor de flujos de trabajo se utiliza para administrar la implementación de sus flujos de trabajo y su aplicación posterior al contenido.

## Administración de múltiples sitios {#multi-site-management}

Multi Site Manager (MSM) le permite administrar fácilmente varios sitios Web que comparten contenido común. MSM le permite definir relaciones entre los sitios para que los cambios de contenido en un sitio se repliquen automáticamente en otros sitios.

Por ejemplo, los sitios Web suelen proporcionarse en varios idiomas para audiencias internacionales. Cuando el número de sitios en el mismo idioma es bajo (de tres a cinco), es posible un proceso manual para sincronizar el contenido entre los sitios. Sin embargo, tan pronto como el número de sitios crece o cuando hay varios idiomas involucrados, se vuelve más eficiente automatizar el proceso.

* Administre de manera eficaz las distintas versiones de idiomas de un sitio web.
* Actualizar automáticamente uno o varios sitios en función de un sitio de origen:

   * Aplicar una estructura base común y utilizar contenido común en varios sitios.
   * Maximice el uso de los recursos disponibles.
   * Mantenga un aspecto común.
   * Centre los esfuerzos en la administración del contenido que difiere entre los sitios.

Para obtener más información, consulte [Administrador de múltiples sitios](/help/sites-administering/msm.md).