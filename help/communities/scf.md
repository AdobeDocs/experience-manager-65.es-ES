---
title: Marco de componentes sociales
seo-title: Social Component Framework
description: El marco de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de componentes de Communities
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: 1d5cfff10735ea31dc0289b6909851b8717936eb
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 0%

---

# Marco de componentes sociales {#social-component-framework}

El marco de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de componentes de Communities en el lado del servidor y del lado del cliente.

Ventajas del marco:

* **Funcional**: Facilidad de integración predeterminada con poca o ninguna personalización para el 80 % de los casos de uso.
* **Skinnable**: Uso coherente de los atributos de HTML para el estilo CSS.
* **Extensible**: La implementación de componentes está orientada a objetos y tiene en cuenta la lógica empresarial: es fácil agregar inicio de sesión empresarial incremental en el servidor.
* **Flexibilidad**: Plantillas javascript simples sin lógica que se superponen y personalizan fácilmente.
* **Accesible**: La API HTTP admite la publicación desde cualquier cliente, incluidas las aplicaciones móviles.
* **Portátil**: Integrar/integrar en cualquier página web creada con cualquier tecnología.

Explorar en un autor o publicar una instancia con la [Guía de componentes de comunidad](components-guide.md).

## Información general {#overview}

En SCF, un componente está formado por un POJO de componente social, una plantilla de JS de controladores (para procesar el componente) y CSS (para aplicar estilo al componente).

Una plantilla de JS de Handlebars puede ampliar los componentes de JS de modelo/vista para gestionar la interacción del usuario con el componente en el cliente.

Si un componente necesita admitir la modificación de datos, la implementación de la API SocialComponent se puede escribir para admitir la edición o guardado de datos similares a los objetos de datos o modelos en aplicaciones web tradicionales. Además, se pueden añadir operaciones (controladores) y un servicio de operación para gestionar solicitudes de operación, realizar lógica empresarial e invocar las API en los objetos de modelo/datos.

La API SocialComponent se puede ampliar para proporcionar los datos que un cliente necesita para una capa de vista o un cliente HTTP.

### Cómo se procesan las páginas para el cliente {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### Personalización y extensión de componentes {#component-customization-and-extension}

Para personalizar o ampliar los componentes, solo debe escribir las superposiciones y extensiones en el directorio /apps , lo que simplifica el proceso de actualización a futuras versiones.

* Para la despellejamiento:
   * Solo el [CSS necesita edición](client-customize.md#skinning-css).
* Para apariencia:
   * Cambie la plantilla JS y la CSS.
* Para Look, Feel y UX:
   * Cambiar la plantilla JS, CSS y [ampliar/anular Javascript](client-customize.md#extending-javascript).
* Para modificar la información disponible para la plantilla JS o el extremo de la GET:
   * Amplíe el [Componente social](server-customize.md#socialcomponent-interface).
* Para agregar un procesamiento personalizado durante las operaciones:
   * Escriba un [Extensión de operación](server-customize.md#operationextension-class).
* Para agregar una nueva operación personalizada:
   * Cree una nueva [Operación posterior de Sling](server-customize.md#postoperation-class).
   * Usar existente [OperationServices](server-customize.md#operationservice-class) según sea necesario.
   * Agregue código Javascript para invocar la operación desde el lado del cliente según sea necesario.

## Marco del lado del servidor {#server-side-framework}

El marco de trabajo proporciona API para acceder a la funcionalidad en el servidor y admitir la interacción entre el cliente y el servidor.

### API de Java {#java-apis}

Las API de Java proporcionan clases e interfaces abstractas que se heredan o subclasifican fácilmente.

Las clases principales se describen en la sección [Personalización del lado del servidor](server-customize.md) página.

Visita [Información general del proveedor de recursos de almacenamiento](srp.md) para aprender a trabajar con UGC.

### API HTTP {#http-api}

La API HTTP admite la facilidad de personalización y elección de plataformas de cliente para aplicaciones PhoneGap, aplicaciones nativas y otras integraciones y mashups. Además, la API de HTTP permite que un sitio de comunidad se ejecute como un servicio sin cliente, de modo que los componentes del marco se puedan integrar en cualquier página web creada a partir de cualquier tecnología.

### API HTTP: solicitudes de GET {#http-api-get-requests}

Para cada SocialComponent, el marco proporciona un extremo de API basado en HTTP. Se accede al extremo enviando una solicitud de GET al recurso con un selector &#39;.social.json&#39; y una extensión. Con Sling, la solicitud se envía al `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Pasa el recurso (resourceType) al `SocialComponentFactoryManager` y recibe un SocialComponentFactory capaz de seleccionar un `SocialComponent` que representa el recurso.

1. Invoca la fábrica y recibe un `SocialComponent` capaz de gestionar el recurso y la solicitud.
1. Invoca el `SocialComponent`, que procesa la solicitud y devuelve una representación JSON de los resultados.
1. Devuelve la respuesta JSON al cliente.

**`GET Request`**

Un servlet de GET predeterminado escucha solicitudes .social.json a las que SocialComponent responde con JSON personalizable.

![scf-framework](assets/scf-framework.png)

### API HTTP: solicitudes de POST {#http-api-post-requests}

Además de las operaciones de GET (lectura), la estructura define un patrón de extremo para habilitar otras operaciones en un componente, incluidas Crear, Actualizar y Eliminar. Estos extremos son API HTTP que aceptan entradas y responden con códigos de estado HTTP o con un objeto de respuesta JSON.

Este patrón de extremo del marco hace que las operaciones de CUD sean extensibles, reutilizables y comprobables.

**`POST Request`**

Hay una operación Sling POST:para cada operación SocialComponent. La lógica empresarial y el código de mantenimiento de cada operación están agrupados en un OperationService al que se puede acceder mediante la API HTTP o desde cualquier otra parte como servicio OSGi. Se proporcionan enlaces que admiten extensiones de operación conectables para acciones anteriores/posteriores.

![scf-post-request](assets/scf-post-request.png)

### Proveedor de recursos de almacenamiento (SRP) {#storage-resource-provider-srp}

Para obtener información sobre la administración de UGC almacenado en la variable [tienda de contenido de la comunidad](working-with-srp.md), consulte:

* [Información general del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [Elementos esenciales de SRP y UGC](srp-and-ugc.md) : Métodos y ejemplos de utilidad de API de SRP.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.

### Personalizaciones del lado del servidor {#server-side-customizations}

Visita [Personalizaciones del lado del servidor](server-customize.md) para obtener información sobre la personalización de la lógica empresarial y el comportamiento de un componente de Communities en el servidor.

## Idioma de plantilla JS de Handlebars {#handlebars-js-templating-language}

Uno de los cambios más notables en el nuevo marco es el uso del `Handlebars JS` (HBS), una popular tecnología de código abierto para la representación servidor-cliente.

Los scripts HBS son sencillos, sin lógica, se compilan tanto en el servidor como en el cliente, son fáciles de superponer y personalizar y se enlazan naturalmente con el usuario cliente, ya que HBS admite el procesamiento en el lado del cliente.

El marco ofrece varias [Manillares de ayuda](handlebars-helpers.md) que son útiles para el desarrollo de componentes sociales.

En el servidor, cuando Sling resuelve una solicitud de GET, identifica la secuencia de comandos que se utilizará para responder a la solicitud. Si la secuencia de comandos es una plantilla HBS (.hbs), Sling delegará la solicitud al motor de controladores. El motor de controladores obtendrá el componente SocialComponent de la Fábrica de componentes de Social correspondiente, creará un contexto y renderizará el HTML.

### Sin restricción de acceso {#no-access-restriction}

Los archivos de plantilla Handlebars (HBS) (.hbs) son análogos a los archivos de plantilla .jsp y .html , excepto que pueden utilizarse para procesar tanto en el explorador del cliente como en el servidor. Por lo tanto, un explorador cliente que solicite una plantilla del lado del cliente recibirá un archivo .hbs del servidor.

Esto requiere que cualquier usuario pueda recuperar todas las plantillas HBS en la ruta de búsqueda de Sling (cualquier archivo .hbs en /libs/ o /apps) desde el autor o la publicación.

El acceso HTTP a archivos .hbs puede no estar prohibido.

### Agregar o incluir un componente de comunidades {#add-or-include-a-communities-component}

La mayoría de los componentes de Communities deben *added* como recurso direccionable de Sling. Algunos de los componentes Comunidades pueden ser *included* en una plantilla como recurso no existente para permitir la inclusión dinámica y la personalización de la ubicación en la que escribir contenido generado por el usuario (UGC).

En cualquier caso, el [bibliotecas de cliente necesarias](clientlibs.md) también debe estar presente.

**Agregar un componente**

Añadir un componente hace referencia al proceso de añadir una instancia de un recurso (componente), como cuando se arrastra desde el navegador de componentes (barra de tareas) a una página en modo de edición de autor.

El resultado es un nodo secundario JCR bajo un nodo par, que es direccionable Sling.

**Incluir un componente**

La inclusión de un componente hace referencia al proceso de adición de una referencia a una [recurso &quot;no existente&quot;](srp.md#for-non-existing-resources-ners) (sin nodo JCR) dentro de la plantilla, como el uso de un lenguaje de secuencias de comandos.

A partir de AEM 6.1, cuando un componente se incluye dinámicamente en lugar de añadirse, es posible editar las propiedades del componente en el modo *diseño *.

Solo se pueden incluir dinámicamente algunos de los componentes de AEM Communities. Son:

* [Comentarios](essentials-comments.md)
* [Clasificación](rating-basics.md)
* [Críticas](reviews-basics.md)
* [Votación](essentials-voting.md)

La variable [Guía de componentes de comunidad](components-guide.md) permite que los componentes inclusibles no se agreguen a se incluyan.

**Al utilizar controladores** idioma de plantilla, el recurso no existente se incluye utilizando la variable [incluir ayuda](handlebars-helpers.md#include) especificando su resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Al utilizar JSP**, se incluye un recurso mediante la etiqueta [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Para añadir un componente a una página de forma dinámica, en lugar de agregarlo o incluirlo en una plantilla, consulte [Carga de componentes](sideloading.md).

### Manillares de ayuda {#handlebars-helpers}

Consulte [SCF Handlebars Helpers](handlebars-helpers.md) para obtener una lista y una descripción de los asistentes personalizados disponibles en SCF.

## Marco del lado del cliente {#client-side-framework}

### Modelo-Ver Javascript Framework {#model-view-javascript-framework}

El marco incluye una extensión de [Backbone.js](https://www.backbonejs.org/), un marco JavaScript de vista de modelo, para facilitar el desarrollo de componentes interactivos y enriquecidos. La naturaleza orientada a objetos admite un marco extensible/reutilizable. La comunicación entre cliente y servidor se simplifica mediante la API HTTP.

El marco aprovecha las plantillas de controladores del lado del servidor para representar los componentes del cliente. Los modelos se basan en las respuestas JSON generadas por la API HTTP. Las vistas se vinculan al HTML generado por las plantillas Handlebars y proporcionan interactividad.

### Convenciones CSS {#css-conventions}

Las siguientes son convenciones recomendadas para definir y utilizar clases CSS:

* Utilice nombres selectores de clases CSS con espacios claros y evite nombres genéricos como &quot;encabezado&quot;, &quot;imagen&quot;, etc.
* Defina estilos de selector de clase específicos para que las hojas de estilo CSS funcionen bien con otros elementos y estilos de la página. Por ejemplo: `.social-forum .topic-list .li { color: blue; }`
* Mantenga las clases CSS para estilos separados de las clases CSS para UX impulsadas por JavaScript.

### Personalizaciones del lado del cliente {#client-side-customizations}

Para personalizar el aspecto y el comportamiento de un componente de Communities en el lado del cliente, consulte [Personalizaciones del lado del cliente](client-customize.md), que incluye información sobre:

* [Superposiciones](client-customize.md#overlays)
* [Extensiones ](client-customize.md#extensions)
* [HTML Markup](client-customize.md#htmlmarkup)
* [Skin CSS](client-customize.md#skinning-css)
* [Ampliación de Javascript](client-customize.md#extending-javascript)
* [Clientlibs para SCF](client-customize.md#clientlibs-for-scf)

## Elementos esenciales de funciones y componentes {#feature-and-component-essentials}

La información esencial para los desarrolladores se describe en la sección [Elementos esenciales de funciones y componentes](essentials.md) para obtener más información.

Puede encontrar información adicional para desarrolladores en el [Directrices de codificación](code-guide.md) para obtener más información.

## Solución de problemas {#troubleshooting}

Las preocupaciones comunes y los problemas conocidos se describen en la sección [Resolución de problemas](troubleshooting.md) para obtener más información.
