---
title: Marco del componente social
description: El marco de trabajo de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de los componentes de las comunidades
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# Marco del componente social {#social-component-framework}

El marco de trabajo de componentes sociales (SCF) simplifica el proceso de configuración, personalización y ampliación de los componentes de las comunidades en el lado del servidor y del cliente.

Las ventajas del marco:

* **Funcional**: facilidad de integración predeterminada con poca o ninguna personalización en el 80% de los casos de uso.
* **Aspirable**: Uso coherente de atributos de HTML para el estilo CSS.
* **Extensible**: La implementación de componentes está orientada a objetos y es ligera en cuanto a lógica empresarial. Es fácil agregar el inicio de sesión empresarial incremental en el servidor.
* **Flexible**: Plantillas de JavaScript simples sin lógica que se superponen y personalizan fácilmente.
* **Accesible**: la API HTTP admite la publicación desde cualquier cliente, incluidas las aplicaciones móviles.
* **Portátil**: integrar en cualquier página web basada en cualquier tecnología.

Explore en una instancia de autor o publicación mediante la [guía interactiva de componentes de la comunidad](components-guide.md).

## Información general {#overview}

En SCF, un componente está compuesto por un POJO de componente social, una plantilla JS de Handlebars (para procesar el componente) y CSS (para aplicar estilo al componente).

Una plantilla JS de Handlebars puede ampliar los componentes JS de modelo/vista para administrar la interacción del usuario con el componente en el cliente.

Si un componente debe admitir la modificación de datos, la implementación de la API de SocialComponent se puede escribir para admitir la edición o el guardado de datos similares a objetos de modelo/datos en aplicaciones web tradicionales. Además, se pueden agregar operaciones (controladores) y un servicio de operación para administrar solicitudes de operación, realizar lógica empresarial e invocar las API en el modelo u objetos de datos.

La API de SocialComponent se puede ampliar para proporcionar los datos requeridos por un cliente para una capa de vista o un cliente HTTP.

### Cómo se representan las páginas para el cliente {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### Personalización y extensión de componentes {#component-customization-and-extension}

Para personalizar o ampliar los componentes, solo escribe las superposiciones y extensiones en el directorio /apps, lo que simplifica el proceso de actualización a futuras versiones.

* Para el desollado:
   * Solo [CSS necesita editarse](client-customize.md#skinning-css).
* Para el aspecto:
   * Cambie la plantilla JS y CSS.
* Para Look, Feel y UX:
   * Cambie la plantilla JS, CSS y [extender/anular JavaScript](client-customize.md#extending-javascript).
* Para modificar la información disponible para la plantilla JS o para el extremo de GET:
   * Extender [SocialComponent](server-customize.md#socialcomponent-interface).
* Para agregar un procesamiento personalizado durante las operaciones:
   * Escriba una [OperationExtension](server-customize.md#operationextension-class).
* Para agregar una operación personalizada:
   * Crear una [operación de Sling Post](server-customize.md#postoperation-class).
   * Use [OperationServices](server-customize.md#operationservice-class) existentes según sea necesario.
   * Agregue código JavaScript para invocar la operación desde el lado del cliente según sea necesario.

## Marco del lado del servidor {#server-side-framework}

El marco de trabajo proporciona API para acceder a la funcionalidad en el servidor y admitir la interacción entre el cliente y el servidor.

### API de Java™ {#java-apis}

Las API de Java™ proporcionan clases e interfaces abstractas que se heredan o subclasifican fácilmente.

Las clases principales se describen en la página [Personalización del lado del servidor](server-customize.md).

Visite [Resumen del proveedor de recursos de almacenamiento](srp.md) para obtener más información sobre cómo trabajar con UGC.

### API del HTTP {#http-api}

La API HTTP admite la facilidad de personalización y la elección de plataformas de cliente para aplicaciones PhoneGap, aplicaciones nativas y otras integraciones y mezclas. Además, la API HTTP permite que un sitio de la comunidad se ejecute como un servicio sin un cliente, de modo que los componentes de marco de trabajo se puedan integrar en cualquier página web basada en cualquier tecnología.

### API HTTP: solicitudes de GET {#http-api-get-requests}

Para cada SocialComponent, el marco de trabajo proporciona un extremo de API basado en HTTP. Se accede al extremo enviando una solicitud de GET al recurso con un selector + extensión &#39;.social.json&#39;. Con Sling, la solicitud se entrega a `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Pasa el recurso (resourceType) al `SocialComponentFactoryManager` y recibe un SocialComponentFactory capaz de seleccionar un `SocialComponent` que represente el recurso.

1. Invoca la fábrica y recibe un `SocialComponent` capaz de administrar el recurso y la solicitud.
1. Invoca el `SocialComponent`, que procesa la solicitud y devuelve una representación JSON de los resultados.
1. Devuelve la respuesta JSON al cliente.

**`GET Request`**

Un servlet de GET predeterminado escucha solicitudes .social.json a las que el componente social responde con un JSON personalizable.

![scf-framework](assets/scf-framework.png)

### API HTTP: solicitudes del POST {#http-api-post-requests}

Además de las operaciones de GET (lectura), el marco de trabajo define un patrón de extremo para habilitar otras operaciones en un componente, como Crear, Actualizar y Eliminar. Estos extremos son API HTTP que aceptan entradas y responden con un código de estado HTTP o con un objeto de respuesta JSON.

Este patrón de extremo de marco de trabajo hace que las operaciones de CUD sean extensibles, reutilizables y comprobables.

**`POST Request`**

Hay una operación Sling POST:para cada operación de SocialComponent. La lógica empresarial y el código de mantenimiento de cada operación se encapsulan en un OperationService, al que se puede acceder a través de la API HTTP o desde cualquier otro lugar como servicio OSGi. Se proporcionan enlaces que admiten extensiones de operación conectables para acciones antes/después.

![scf-post-request](assets/scf-post-request.png)

### Proveedor de recursos de almacenamiento (SRP) {#storage-resource-provider-srp}

Para obtener más información sobre la administración de UGC almacenados en el [almacén de contenido de la comunidad](working-with-srp.md), consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de la utilidad API de SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.

### Personalizaciones del lado del servidor {#server-side-customizations}

Visite [Personalizaciones del lado del servidor](server-customize.md) para obtener información sobre cómo personalizar la lógica empresarial y el comportamiento de un componente de Communities en el lado del servidor.

## Idioma de plantilla JS de Handlebars {#handlebars-js-templating-language}

Uno de los cambios más notables en el nuevo marco de trabajo es el uso del lenguaje de plantilla `Handlebars JS` (HBS), una popular tecnología de código abierto para el procesamiento de cliente-servidor.

Los scripts HBS son simples, sin lógica, se compilan tanto en el servidor como en el cliente, son fáciles de superponer y personalizar, y se enlazan naturalmente con el UX del cliente porque HBS admite el procesamiento en el lado del cliente.

El marco de trabajo proporciona varios [ayudantes de Handlebars](handlebars-helpers.md) que son útiles al desarrollar SocialComponents.

En el servidor, cuando Sling resuelve una solicitud de GET, identifica el script que se utiliza para responder a la solicitud. Si el script es una plantilla HBS (.hbs), Sling delegará la solicitud al motor de Handlebars. El motor de Handlebars obtiene el SocialComponent desde el SocialComponentFactory adecuado, crea un contexto y procesa el HTML.

### Sin restricciones de acceso {#no-access-restriction}

Los archivos de plantilla (.hbs) de Handlebars (HBS) son análogos a los archivos de plantilla .jsp y .html, excepto que se pueden utilizar para procesar tanto en el explorador del cliente como en el servidor. Por lo tanto, un explorador del cliente que solicita una plantilla del lado del cliente recibe un archivo .hbs del servidor.

Esto requiere que cualquier usuario pueda recuperar todas las plantillas HBS en la ruta de búsqueda de Sling (cualquier archivo .hbs en /libs/ o /apps) desde Autor o Publicación.

Puede que no esté prohibido el acceso HTTP a los archivos .hbs.

### Agregar o incluir un componente de Communities {#add-or-include-a-communities-component}

La mayoría de los componentes de las comunidades deben *agregarse* como un recurso con dirección Sling. Es posible que se *incluyan* algunos de los componentes de la comunidad en una plantilla como recurso no existente para permitir la inclusión dinámica y la personalización de la ubicación en la que se va a escribir contenido generado por el usuario (UGC).

En cualquier caso, las [bibliotecas de cliente requeridas](clientlibs.md) del componente también deben estar presentes.

**Agregar un componente**

Añadir un componente hace referencia al proceso de añadir una instancia de un recurso (componente), como cuando se arrastra desde el navegador de componentes (barra de tareas) a una página en modo de edición de autor.

El resultado es un nodo secundario JCR bajo un nodo par, que es direccionable por Sling.

**Incluir un componente**

Incluir un componente hace referencia al proceso de agregar una referencia a un recurso [ &quot;no existente&quot;](srp.md#for-non-existing-resources-ners) (sin nodo JCR) dentro de la plantilla, como el uso de un lenguaje de script.

A partir de Adobe Experience Manager AEM () 6.1, cuando se incluye dinámicamente un componente en lugar de agregarlo, es posible editar las propiedades del componente en el modo de autor *design*.

Solo se pueden incluir dinámicamente algunos de los componentes de AEM Communities. Estos son:

* [Comentarios](essentials-comments.md)
* [Clasificación](rating-basics.md)
* [Repasos](reviews-basics.md)
* [Votación](essentials-voting.md)

La [Guía de componentes de la comunidad](components-guide.md) permite que los componentes que se incluyen se alternen de agregarse a incluirse.

**Cuando se usa el idioma de creación de plantillas Handlebars**, el recurso no existente se incluye usando el [ayudante include](handlebars-helpers.md#include) especificando su resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Al usar JSP**, se incluye un recurso con la etiqueta [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Para agregar un componente a una página de forma dinámica, en lugar de agregarlo o incluirlo en una plantilla, consulte [Carga lateral del componente](sideloading.md).

### Ayudantes de manillar {#handlebars-helpers}

Consulte [SCF Handlebars Helpers](handlebars-helpers.md) para obtener una lista y una descripción de los ayudantes personalizados disponibles en SCF.

## Client-Side Framework {#client-side-framework}

### Marco de trabajo de JavaScript de vista de modelo {#model-view-javascript-framework}

El módulo incluye una extensión de [Backbone.js](https://backbonejs.org/), un módulo de JavaScript de vista de modelo, para facilitar el desarrollo de componentes interactivos enriquecidos. La naturaleza orientada a objetos admite un marco de trabajo extensible/reutilizable. La comunicación entre el cliente y el servidor se simplifica con la API HTTP.

El marco de trabajo utiliza plantillas Handlebars del lado del servidor para procesar los componentes para el cliente. Los modelos se basan en las respuestas JSON generadas por la API HTTP. Las vistas se enlazan a HTML generado por las plantillas Handlebars y proporcionan interactividad.

### Convenciones CSS {#css-conventions}

Se recomiendan las siguientes convenciones para definir y utilizar clases CSS:

* Utilice nombres de selectores de clase CSS con espacios de nombres claros y evite nombres genéricos como &quot;encabezado&quot; e &quot;imagen&quot;.
* Defina estilos específicos de selector de clase para que las hojas de estilos CSS funcionen bien con otros elementos y estilos de la página. Por ejemplo: `.social-forum .topic-list .li { color: blue; }`
* Mantenga las clases CSS para el estilo separadas de las clases CSS para UX impulsadas por JavaScript.

### Personalizaciones del lado del cliente {#client-side-customizations}

Para personalizar el aspecto y el comportamiento de un componente de Communities en el lado del cliente, haga referencia a [Personalizaciones del lado del cliente](client-customize.md), que incluye información sobre:

* [Superposiciones](client-customize.md#overlays)
* [Extensiones ](client-customize.md#extensions)
* [Marcado de HTML](client-customize.md#htmlmarkup)
* [Aplicación de máscara CSS](client-customize.md#skinning-css)
* [Ampliación de JavaScript](client-customize.md#extending-javascript)
* [Clientlibs para SCF](client-customize.md#clientlibs-for-scf)

## Aspectos básicos de funciones y componentes {#feature-and-component-essentials}

La información esencial para los desarrolladores se describe en la sección [Aspectos básicos de características y componentes](essentials.md).

Encontrará información adicional para desarrolladores en la sección [Directrices de codificación](code-guide.md).

## Resolución de problemas {#troubleshooting}

En la sección [Solución de problemas](troubleshooting.md) se describen problemas comunes y problemas conocidos.
