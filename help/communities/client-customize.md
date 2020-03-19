---
title: Personalización del lado del cliente
seo-title: Personalización del lado del cliente
description: Personalización del comportamiento o el aspecto del cliente en AEM Communities
seo-description: Personalización del comportamiento o el aspecto del cliente en AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# Personalización del lado del cliente {#client-side-customization}

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Manillares de SCF Ayudantes](handlebars-helpers.md)** |

Para personalizar el aspecto y/o el comportamiento de un componente de AEM Communities en el lado del cliente, existen varios métodos.

Dos enfoques principales son superponer o ampliar un componente.

[Al superponer](#overlays) un componente, se cambia el componente predeterminado y se afectan todas las referencias al mismo.

[La extensión](#extensions) de un componente, con un nombre exclusivo, limita el alcance de los cambios. El término &#39;extender&#39; se utiliza indistintamente con &#39;anular&#39;.

## Superposiciones {#overlays}

La superposición de un componente es un método para realizar modificaciones en un componente predeterminado y afectar a todas las instancias que lo utilicen.

La superposición se realiza modificando una copia del componente predeterminado en el directorio /**apps** , en lugar de modificar el componente original en el directorio /**libs** . El componente se construye con una ruta relativa idéntica, excepto que &#39;libs&#39; se sustituye por &#39;apps&#39;.

El directorio /apps es el primer lugar en el que se busca para resolver solicitudes y, si no se encuentra, se utiliza la versión predeterminada ubicada en el directorio /libs.

El componente predeterminado en el directorio /libs nunca debe modificarse, ya que los parches futuros y las actualizaciones son libres de alterar el directorio /libs de cualquier manera necesaria mientras se mantienen las interfaces públicas.

Esto es diferente a [ampliar](#extensions) un componente predeterminado donde el deseo es realizar modificaciones para un uso específico, crear una ruta única al componente y confiar en hacer referencia al componente predeterminado original en el directorio /libs como tipo de recurso superior.

Para ver un ejemplo rápido de superposición del componente de comentarios, pruebe el tutorial [](overlay-comments.md)Overlay Comments Component.

## Extensiones {#extensions}

Ampliar (anular) un componente es un método para realizar modificaciones para un uso específico sin afectar a todas las instancias que utilizan el valor predeterminado. El componente extendido tiene un nombre exclusivo en la carpeta /apps y hace referencia al componente predeterminado de la carpeta /libs, por lo que el diseño y el comportamiento predeterminados del componente no se modifican.

Esto es diferente de [superponer](#overlays) el componente predeterminado en el que la naturaleza de Sling resuelve las referencias relativas a las aplicaciones o la carpeta antes de buscar en la carpeta libs/, por lo que el diseño o el comportamiento de un componente se modifica globalmente.

Para ver un ejemplo rápido de ampliación del componente de comentarios, pruebe el tutorial [](extend-comments.md)Ampliar componente de comentarios.

## Enlace Javascript {#javascript-binding}

La secuencia de comandos de HBS para el componente debe enlazarse a los objetos, modelos y vistas de JavaScript que implementan esta función.

El valor del `data-scf-component` atributo puede ser el valor predeterminado, como **`social/tally/components/hbs/rating`** o un componente extendido (personalizado) para la funcionalidad personalizada, como **weretail/components/hbs/rating**.

Para enlazar un componente, toda la secuencia de comandos del componente debe estar encerrada dentro de un elemento &lt;div> con los atributos siguientes:

* `data-component-id`=&quot;{{id}}&quot;

   se resuelve en la propiedad id del contexto

* `data-scf-component`=&quot;*&lt;resourceType>*

Por ejemplo, desde `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propiedades personalizadas {#custom-properties}

Al ampliar o superponer un componente, es posible añadir propiedades a un cuadro de diálogo modificado.

Se puede acceder a todas las propiedades establecidas en un componente o recurso haciendo referencia a las claves de propiedad de la plantilla de controladores:

`{{properties.<property_name>}}`

## Aplicación de apariencia a CSS {#skinning-css}

La personalización de componentes para que coincidan con el tema general del sitio web se puede lograr &#39;desollando&#39;: cambiando colores, fuentes, imágenes, botones, vínculos, espaciado e incluso posicionamiento hasta cierto punto.

La apariencia se puede conseguir anulando selectivamente los estilos de marco o escribiendo hojas de estilo completamente nuevas. Los componentes SCF definen clases CSS con espacio de nombres, modulares y semánticas que afectan a los distintos elementos que conforman un componente.

Para aplicar máscara a un componente:

1. Identifique los elementos que desea cambiar (por ejemplo: área del compositor, botones de la barra de herramientas, fuente del mensaje, etc.).
1. Identifique la clase o las reglas CSS que afectan a estos elementos.
1. Cree un archivo de hoja de estilo (.css).
1. Incluya la hoja de estilo en una carpeta de la biblioteca del cliente ([clientlibs](#clientlibs-for-scf)) para su sitio y asegúrese de incluirla en las plantillas y páginas con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Vuelva a definir las clases y reglas CSS que ha identificado (#2) en la hoja de estilo y agregue estilos.

Los estilos personalizados ahora anularán los estilos de marco predeterminados y el componente se procesará con el nuevo aspecto.

>[!CAUTION]
>
>Cualquier nombre de clase CSS con el prefijo `scf-js` tiene un uso específico en el código javascript. Estas clases afectan al estado de un componente (por ejemplo, alternar entre oculto y visible) y no deben superarse ni eliminarse.
>
>Aunque las `scf-js` clases no afectan a los estilos, los nombres de clase pueden utilizarse en hojas de estilo con la advertencia de que, al controlar los estados de los elementos, puede haber efectos secundarios.

## Ampliación de Javascript {#extending-javascript}

Para ampliar una implementación de componentes Javascript, solo necesita

1. Cree un componente para su aplicación con un jcr:resourceSuperType definido en el valor de jcr:resourceType del componente extendido, por ejemplo, social/forum/components/hbs/forum
1. Examine el JavaScript predeterminado del componente SCF para determinar qué métodos deben registrarse mediante SCF.registerComponent()
1. Copie el JavaScript del componente extendido o comience desde cero
1. Ampliar el método
1. Utilice SCF.registerComponent() para registrar todos los métodos con los valores predeterminados o con los objetos y las vistas personalizados.

### forum.js: Extensión de muestra del foro - HBS {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## Etiquetas de script {#script-tags}

Las etiquetas de script son una parte inherente del entorno de cliente. Son el pegamento que ayuda a enlazar el marcado generado en el servidor con los modelos y las vistas del lado del cliente.

Las etiquetas de script de los scripts SCF no deben eliminarse al superponer o anular componentes. Las etiquetas de script SCF creadas automáticamente para insertar JSON en el HTML se identifican con el atributo `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

El uso de las bibliotecas [del lado del](../../help/sites-developing/clientlibs.md) cliente (clientlibs), proporciona un medio para organizar y optimizar el Javascript y CSS utilizado para procesar contenido en el cliente.

Los clientlibs para SCF siguen un patrón de nombres muy específico para dos variantes, que varía solamente por la presencia de &quot;autor&quot; en el nombre de la categoría:

| Clientlib Variant | Patrón de la propiedad Categorías |
|--- |--- |
| clientlib completa | cq.social.hbs.&lt;nombre del componente> |
| clientlib autor | cq.social.author.hbs.&lt;nombre del componente> |

### Completar Clientlibs {#complete-clientlibs}

Los clientlibs completos (no autores) incluyen dependencias y son convenientes para incluirlos con ui:includeClientLib.

Estas versiones se encuentran en:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por ejemplo:

* Nodo de carpeta de cliente: `/etc/clientlibs/social/hbs/forum`
* Propiedad Categories: `cq.social.hbs.forum`

La guía [Componentes](components-guide.md) comunitarios enumera los clientlibs completos requeridos para cada componente SCF.

[Clientlibs for Communities Components](clientlibs.md) describe cómo agregar clientlibs a una página.

### Author Clientlibs {#author-clientlibs}

Los clientes de la versión de creación se eliminan al mínimo JavaScript necesario para implementar el componente.

Estos clientes no deberían incluirse nunca directamente, sino que están disponibles para ser incorporados a otros clientes, que son hechos a mano para un sitio.

Estas versiones se encuentran en la carpeta de bibliotecas de SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por ejemplo:

* Nodo de carpeta de cliente: `/libs/social/forum/hbs/forum/clientlibs`
* Propiedad Categories: `cq.social.author.hbs.forum`

Nota: aunque los clientlibs de autor nunca incorporan otras bibliotecas, sí enumeran sus dependencias. Cuando se incrustan en otras bibliotecas, las dependencias no se extraen automáticamente y también se deben incrustar.

Los clientlibs de creación requeridos pueden identificarse insertando &quot;author&quot; en los clientlibs enumerados para cada componente SCF en la guía [Componentes de](components-guide.md)comunidad.

### Consideraciones de uso {#usage-considerations}

Cada sitio es diferente en la forma en que administra las bibliotecas de cliente. Entre los diversos factores se incluyen:

* Velocidad global: Tal vez el deseo sea que el sitio responda, pero es aceptable que la primera página sea un poco lenta de cargar. Si muchas de las páginas utilizan el mismo JavaScript, los distintos JavaScript se pueden incorporar en una clientlib y se puede hacer referencia a ellos desde la primera página que se va a cargar. El Javascript de esta descarga única permanece en la caché, lo que minimiza la cantidad de datos que descargar para las páginas posteriores.
* Tiempo corto hasta la primera página: Quizás el deseo es que la primera página se cargue rápidamente. En este caso, Javascript se encuentra en varios archivos pequeños para que solo se haga referencia a ellos cuando sea necesario.
* Un equilibrio entre la primera carga de página y las descargas posteriores.

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Manillares de SCF Ayudantes](handlebars-helpers.md)** |

