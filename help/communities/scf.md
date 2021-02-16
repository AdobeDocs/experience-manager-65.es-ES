---
title: Marco de componentes sociales
seo-title: Marco de componentes sociales
description: El marco de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de los componentes de Comunidades
seo-description: El marco de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de los componentes de Comunidades
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---


# Marco de componentes sociales {#social-component-framework}

El marco de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de los componentes de Communities tanto en el servidor como en el cliente.

Los beneficios del marco:

* **Funcional**: Facilidad de integración predeterminada con poca o ninguna personalización para el 80 % de los casos de uso.
* **Skinnable**: Uso coherente de atributos HTML para estilos CSS.
* **Extensible**: La implementación de componentes está orientada a objetos y se basa en la lógica empresarial: es fácil agregar inicios de sesión comerciales incrementales en el servidor.
* **Flexible**: Plantillas de javascript sencillas y sin lógica que se pueden superponer y personalizar fácilmente.
* **Accesible**: La API HTTP admite la publicación desde cualquier cliente, incluidas las aplicaciones móviles.
* **Portátil**: Integrar/integrar en cualquier página web creada con cualquier tecnología.

Explore en una instancia de autor o publicación mediante la [guía interactiva de componentes de comunidad](components-guide.md).

## Información general {#overview}

En SCF, un componente está compuesto por un POJO de componente de Social, una plantilla JS de controladores (para representar el componente) y CSS (para aplicar estilo al componente).

Una plantilla JS de Handlebars puede extender los componentes JS de modelo o vista para manejar la interacción del usuario con el componente en el cliente.

Si un componente necesita admitir la modificación de datos, la implementación de la API de SocialComponent se puede escribir para admitir la edición/guardado de datos similares a objetos de modelo/datos en aplicaciones web tradicionales. Además, se pueden añadir operaciones (controladores) y un servicio de operación para gestionar solicitudes de operación, llevar a cabo lógica empresarial e invocar las API en objetos de modelo o datos.

La API de SocialComponent se puede ampliar para proporcionar los datos que un cliente necesita para una capa de vista o un cliente HTTP.

### Cómo se procesan las páginas para el cliente {#how-pages-are-rendered-for-client}

![scf-page-renderizado](assets/scf-overview.png)

### Personalización y extensión de componentes {#component-customization-and-extension}

Para personalizar o ampliar los componentes, solo debe escribir las superposiciones y extensiones en el directorio /apps, lo que simplifica el proceso de actualización a versiones futuras.

* Para la apariencia:
   * Solo el [CSS necesita edición](client-customize.md#skinning-css).
* Para apariencia:
   * Cambie la plantilla JS y la CSS.
* Para Look, Feel y UX:
   * Cambie la plantilla JS, CSS y [extienda/sobrescriba Javascript](client-customize.md#extending-javascript).
* Para modificar la información disponible en la plantilla JS o en el extremo de GET:
   * Extienda el [componente de Social](server-customize.md#socialcomponent-interface).
* Para agregar procesamiento personalizado durante las operaciones:
   * Escriba [OperationExtension](server-customize.md#operationextension-class).
* Para agregar una nueva operación personalizada:
   * Cree una nueva [Operación posterior de Sling](server-customize.md#postoperation-class).
   * Utilice los [OperationServices](server-customize.md#operationservice-class) existentes según sea necesario.
   * Añada el código Javascript para invocar la operación desde el cliente según sea necesario.

## Módulo del lado del servidor {#server-side-framework}

La estructura proporciona API para acceder a la funcionalidad en el servidor y admite la interacción entre el cliente y el servidor.

### API de Java {#java-apis}

Las API de Java proporcionan clases e interfaces abstractas que se heredan o subclasifican fácilmente.

Las clases principales se describen en la página [Personalización del lado del servidor](server-customize.md).

Visite [Información general del proveedor de recursos de Almacenamiento](srp.md) para obtener información sobre cómo trabajar con UGC.

### API HTTP {#http-api}

La API HTTP admite la facilidad de personalización y elección de plataformas de cliente para aplicaciones PhoneGap, aplicaciones nativas y otras integraciones y mashups. Además, la API de HTTP permite que un sitio de comunidad se ejecute como un servicio sin cliente, de modo que los componentes del marco se pueden integrar en cualquier página web creada con cualquier tecnología.

### API HTTP - Solicitudes de GET {#http-api-get-requests}

Para cada componente de Social, la estructura proporciona un extremo de API basado en HTTP. Se accede al extremo enviando una solicitud de GET al recurso con un selector &#39;.social.json&#39; + extensión. Con Sling, la solicitud se entrega a `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Pasa el recurso (resourceType) a `SocialComponentFactoryManager` y recibe un SocialComponentFactory capaz de seleccionar un `SocialComponent` que representa el recurso.

1. Invoca la fábrica y recibe un `SocialComponent` capaz de administrar el recurso y la solicitud.
1. Invoca el `SocialComponent`, que procesa la solicitud y devuelve una representación JSON de los resultados.
1. Devuelve la respuesta JSON al cliente.

**`GET Request`**

Un servlet de GET predeterminado escucha las solicitudes .social.json a las que SocialComponent responde con JSON personalizable.

![scf-framework](assets/scf-framework.png)

### API HTTP - Solicitudes de POST {#http-api-post-requests}

Además de las operaciones de GET (lectura), la estructura define un patrón de extremo para habilitar otras operaciones en un componente, como Crear, Actualizar y Eliminar. Estos extremos son API HTTP que aceptan entradas y responden con códigos de estado HTTP o con un objeto de respuesta JSON.

Este patrón de punto final del marco hace que las operaciones de CUD sean extensibles, reutilizables y comprobables.

**`POST Request`**

Hay una operación Sling POST:para cada operación SocialComponent. La lógica empresarial y el código de mantenimiento de cada operación están agrupados en un OperationService al que se puede acceder a través de la API HTTP o desde cualquier otro lugar como servicio OSGi. Se proporcionan ganchos que admiten extensiones de operación conectables para acciones anteriores y posteriores.

![scf-post-request](assets/scf-post-request.png)

### Proveedor de recursos de almacenamiento (SRP) {#storage-resource-provider-srp}

Para obtener más información sobre la administración de UGC almacenada en el [almacén de contenido de la comunidad](working-with-srp.md), consulte:

* [Almacenamiento Resource Provider Overview](srp.md) : Introducción y uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md)  - Métodos y ejemplos de utilidad de la API de SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.

### Personalizaciones del lado del servidor {#server-side-customizations}

Visite [Personalizaciones del lado del servidor](server-customize.md) para obtener información sobre cómo personalizar la lógica y el comportamiento de negocios de un componente de comunidades en el lado del servidor.

## Lenguaje de plantillas JS de controladores {#handlebars-js-templating-language}

Uno de los cambios más notables en el nuevo marco de trabajo es el uso del [lenguaje de plantilla JS Handlebars (HBS)](https://www.handlebarsjs.com/), una tecnología de código abierto popular para el procesamiento servidor-cliente.

Los scripts HBS son sencillos, sin lógica, se compilan tanto en el servidor como en el cliente, son fáciles de superponer y personalizar, y se enlazan naturalmente con el cliente UX, ya que HBS admite el procesamiento en el cliente.

La estructura proporciona varios [controladores de ayuda](handlebars-helpers.md) que son útiles al desarrollar SocialComponents.

En el servidor, cuando Sling resuelve una solicitud de GET, identifica la secuencia de comandos que se utilizará para responder a la solicitud. Si la secuencia de comandos es una plantilla HBS (.hbs), Sling delegará la solicitud al motor de controladores. El motor de controladores obtendrá el componente SocialComponent de la SocialComponentFactory adecuada, generará un contexto y representará el HTML.

### Sin restricción de acceso {#no-access-restriction}

Los archivos de plantilla de las barras de administración (HBS) (.hbs) son análogos a los archivos de plantilla .jsp y .html, excepto que pueden utilizarse para procesar tanto en el navegador del cliente como en el servidor. Por lo tanto, un navegador cliente que solicite una plantilla de cliente recibirá un archivo .hbs del servidor.

Esto requiere que cualquier usuario pueda recuperar todas las plantillas HBS de la ruta de búsqueda sling (cualquier archivo .hbs en /libs/ o /apps) desde el autor o la publicación.

No se puede prohibir el acceso HTTP a los archivos .hbs.

### Añadir o incluir un componente de comunidades {#add-or-include-a-communities-component}

La mayoría de los componentes de Communities deben *agregarse* como recurso direccionable de Sling. Algunos de los componentes de Communities pueden *incluirse* en una plantilla como recurso no existente para permitir la inclusión dinámica y la personalización de la ubicación en la que se escribe contenido generado por el usuario (UGC).

En cualquier caso, también deben estar presentes las [bibliotecas de cliente requeridas](clientlibs.md) del componente.

**Añadir un componente**

Añadir un componente se refiere al proceso de agregar una instancia de un recurso (componente), como cuando se arrastra desde el navegador de componentes (barra de tareas) a una página en modo de edición de autor.

El resultado es un nodo secundario JCR bajo un nodo par, que es direccionable Sling.

**Incluir un componente**

La inclusión de un componente se refiere al proceso de agregar una referencia a un recurso [&quot;no existente&quot;](srp.md#for-non-existing-resources-ners) (sin nodo JCR) dentro de la plantilla, como el uso de un lenguaje de secuencias de comandos.

A partir de AEM 6.1, cuando un componente se incluye dinámicamente en lugar de agregarse, es posible editar las propiedades del componente en el *modo *diseño *del autor.

Solo se pueden incluir dinámicamente algunos de los componentes de AEM Communities seleccionados. Son:

* [Comentarios](essentials-comments.md)
* [Clasificación](rating-basics.md)
* [Críticas](reviews-basics.md)
* [Votación](essentials-voting.md)

La [Guía de componentes de la comunidad](components-guide.md) permite que los componentes incluibles no se agreguen a la inclusión.

**Al utilizar el lenguaje** Handlebarstemplating, el recurso no existente se incluye mediante el  [asistente ](handlebars-helpers.md#include) include especificando su resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Al utilizar JSP**, se incluye un recurso con la etiqueta  [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Para agregar un componente a una página de forma dinámica, en lugar de agregarlo o incluirlo en una plantilla, consulte [Descarga de componentes](sideloading.md).

### Ayudas para manillares {#handlebars-helpers}

Consulte [SCF Handlebars Helpers](handlebars-helpers.md) para obtener una lista y una descripción de los ayudantes personalizados disponibles en SCF.

## Client-Side Framework {#client-side-framework}

### Modelo-Vista Javascript Framework {#model-view-javascript-framework}

La estructura incluye una extensión de [Backbone.js](https://www.backbonejs.org/), un marco de trabajo JavaScript de vista de modelo, para facilitar el desarrollo de componentes interactivos y enriquecidos. La naturaleza orientada a objetos admite un marco extensible/reutilizable. La comunicación entre cliente y servidor se simplifica mediante la API HTTP.

El marco aprovecha las plantillas de controladores del lado del servidor para procesar los componentes para el cliente. Los modelos se basan en las respuestas JSON generadas por la API HTTP. Las vistas se enlazan a HTML generado por las plantillas de controladores y proporcionan interactividad.

### Convenciones CSS {#css-conventions}

Se recomiendan las siguientes convenciones para definir y utilizar clases CSS:

* Utilice nombres selectores de clase CSS claramente con espacios de nombres y evite nombres genéricos como &#39;encabezado&#39;, &#39;imagen&#39;, etc.
* Defina estilos de selector de clase específicos para que las hojas de estilo CSS funcionen correctamente con otros elementos y estilos de la página. Por ejemplo: `.social-forum .topic-list .li { color: blue; }`
* Mantenga las clases CSS para estilos separados de las clases CSS para UX impulsadas por JavaScript.

### Personalizaciones del lado del cliente {#client-side-customizations}

Para personalizar la apariencia y el comportamiento de un componente Communities en el cliente, consulte [Personalizaciones del cliente](client-customize.md), que incluye información sobre:

* [Superposiciones](client-customize.md#overlays)
* [Extensiones](client-customize.md#extensions)
* [Código HTML](client-customize.md#htmlmarkup)
* [Aplicación de apariencia a CSS](client-customize.md#skinning-css)
* [Ampliación de Javascript](client-customize.md#extending-javascript)
* [Clientlibs para SCF](client-customize.md#clientlibs-for-scf)

## Elementos esenciales de funciones y componentes {#feature-and-component-essentials}

La información esencial para los desarrolladores se describe en la sección [Funciones y elementos esenciales](essentials.md).

Puede encontrar información adicional para desarrolladores en la sección [Pautas de codificación](code-guide.md).

## Solución de problemas {#troubleshooting}

Las preocupaciones comunes y los problemas conocidos se describen en la sección [Resolución de problemas](troubleshooting.md).

