---
title: Personalización del lado del cliente
seo-title: Client-side Customization
description: Personalización del comportamiento o el aspecto del lado del cliente en AEM Communities
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Personalización del lado del cliente  {#client-side-customization}

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Manillares SCF Helpers](handlebars-helpers.md)** |

Para personalizar el aspecto y/o el comportamiento de un componente de AEM Communities en el lado del cliente, existen varios enfoques.

Dos enfoques principales son superponer o ampliar un componente.

[Superposición](#overlays) un componente cambia el componente predeterminado y afecta a todas las referencias al componente.

[Ampliación](#extensions) un componente, al tener un nombre único, limita el alcance de los cambios. El término &quot;ampliar&quot; se utiliza de forma intercambiable con &quot;anular&quot;.

## Superposiciones {#overlays}

Superponer un componente es un método para realizar modificaciones en un componente predeterminado y afectar a todas las instancias que lo utilicen.

La superposición se realiza modificando una copia del componente predeterminado en /**apps** en lugar de modificar el componente original en /**libs** directorio. El componente se construye con una ruta relativa idéntica, excepto que &quot;libs&quot; se sustituye por &quot;apps&quot;.

El directorio /apps es el primer lugar en el que se busca para resolver las solicitudes y, si no se encuentra, se utiliza la versión predeterminada ubicada en el directorio /libs.

El componente predeterminado del directorio /libs nunca debe modificarse, ya que los parches y actualizaciones futuros son libres de alterar el directorio /libs de cualquier manera necesaria mientras se mantienen las interfaces públicas.

Esto es diferente de [ampliar](#extensions) componente predeterminado en el que se desea realizar modificaciones para un uso específico, crear una ruta única al componente y confiar en hacer referencia al componente predeterminado original en el directorio /libs como tipo de superrecurso.

Para ver un ejemplo rápido de superposición del componente de comentarios, pruebe con la [Tutorial del componente Comentarios de superposición](overlay-comments.md).

## Extensiones  {#extensions}

La ampliación (anulación) de un componente es un método para realizar modificaciones para un uso específico sin afectar a todas las instancias que utilizan el valor predeterminado. El componente extendido tiene un nombre único en la carpeta /apps y hace referencia al componente predeterminado en la carpeta /libs, por lo que el diseño y el comportamiento predeterminados de un componente no se modifican.

Esto es diferente de [superposición](#overlays) el componente predeterminado en el que la naturaleza de Sling resuelve las referencias relativas a las aplicaciones/carpeta antes de buscar en la carpeta libs/ , por lo que el diseño o el comportamiento de un componente se modifican globalmente.

Para ver un ejemplo rápido de cómo ampliar el componente de comentarios, pruebe con la [Tutorial del componente Extensión de comentarios](extend-comments.md).

## Enlace De Javascript {#javascript-binding}

El script HBS del componente debe enlazarse a los objetos, modelos y vistas de JavaScript que implementan esta función.

El valor de la variable `data-scf-component` puede ser el valor predeterminado, como **`social/tally/components/hbs/rating`** o un componente extendido (personalizado) para funciones personalizadas, como **weretail/components/hbs/rating**.

Para enlazar un componente, todo el script de componente debe estar dentro de un &lt;div> con los siguientes atributos:

* `data-component-id`=&quot;{{id}}&quot;

   resuelve en la propiedad id desde el contexto

* `data-scf-component`=&quot;*&lt;resourcetype>*

Por ejemplo, desde `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propiedades personalizadas {#custom-properties}

Al ampliar o superponer un componente, es posible añadir propiedades a un cuadro de diálogo modificado.

Se puede acceder a todas las propiedades establecidas en un componente/recurso haciendo referencia a las claves de propiedad de la plantilla de controladores:

`{{properties.<property_name>}}`

## Skin CSS {#skinning-css}

La personalización de componentes para que coincidan con el tema general del sitio web se puede lograr &#39;desollando&#39;: cambiando colores, fuentes, imágenes, botones, enlaces, espaciado e incluso posicionamiento en cierta medida.

El desollado se puede lograr anulando selectivamente los estilos de marco o escribiendo hojas de estilo completamente nuevas. Los componentes SCF definen clases CSS espaciadas por nombres, modulares y semánticas que afectan a los distintos elementos que conforman un componente.

Para deslizar un componente:

1. Identifique los elementos que desee cambiar (por ejemplo, área del compositor, botones de la barra de herramientas, fuente del mensaje, etc.).
1. Identifique la clase o reglas CSS que afectan a estos elementos.
1. Cree un archivo de hoja de estilo (.css).
1. Incluya la hoja de estilo en una carpeta de la biblioteca del cliente ([clientlibs](#clientlibs-for-scf)) para su sitio y asegúrese de que se incluye desde sus plantillas y páginas con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redefina las clases CSS y las reglas que ha identificado (#2) en la hoja de estilo y añada estilos.

Los estilos personalizados ahora anulan los estilos de marco predeterminados y el componente se procesará con el nuevo aspecto.

>[!CAUTION]
>
>Cualquier nombre de clase CSS con el prefijo `scf-js` tiene un uso específico en código javascript. Estas clases afectan al estado de un componente (por ejemplo, cambiar de oculto a visible) y no deben anularse ni eliminarse.
>
>Mientras que la variable `scf-js` las clases no afectan a los estilos, los nombres de las clases pueden utilizarse en hojas de estilo con la advertencia de que, como controlan los estados de los elementos, puede haber efectos secundarios.

## Ampliación de Javascript {#extending-javascript}

Para ampliar una implementación de Javascript de componentes, debe:

1. Cree un componente para su aplicación con un jcr:resourceSuperType establecido en el valor del jcr:resourceType del componente extendido, por ejemplo social/forum/components/hbs/forum.
1. Examine el JavaScript predeterminado del componente SCF para determinar qué métodos deben registrarse mediante SCF.registerComponent().
1. Copie el Javascript del componente extendido o comience desde cero.
1. Amplíe el método .
1. Utilice SCF.registerComponent() para registrar todos los métodos con los valores predeterminados o con los objetos y vistas personalizados.

### forum.js: Extensión de muestra del Foro - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

## Etiquetas de secuencias de comandos {#script-tags}

Las etiquetas de script son una parte inherente del marco del lado del cliente. Son el pegamento que ayuda a enlazar el marcado generado en el servidor con los modelos y vistas en el lado del cliente.

Las etiquetas de script de los scripts SCF no deben eliminarse al superponer o anular componentes. Las etiquetas de script de SCF creadas automáticamente para inyectar JSON en el HTML se identifican con el atributo . `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

El uso de [bibliotecas del lado del cliente](../../help/sites-developing/clientlibs.md) (clientlibs), proporciona un medio para organizar y optimizar el JavaScript y CSS utilizado para procesar contenido en el cliente.

Las clientlibs para SCF siguen un patrón de nomenclatura muy específico para dos variantes, que solo varía por la presencia de &quot;autor&quot; en el nombre de la categoría:

| Clientlib Variant | Patrón de la propiedad Categorías |
|--- |--- |
| clientlib completa | cq.social.hbs.&lt;component name> |
| author clientlib | cq.social.author.hbs.&lt;component name> |

### Clientlibs completos {#complete-clientlibs}

Las clientlibs completas (no de autor) incluyen dependencias y resultan adecuadas para incluirlas con ui:includeClientLib.

Estas versiones se encuentran en:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por ejemplo:

* Nodo de carpeta del cliente: `/etc/clientlibs/social/hbs/forum`
* Propiedad Categories: `cq.social.hbs.forum`

La variable [Guía de componentes de comunidad](components-guide.md) enumera todas las clientlibs necesarias para cada componente SCF.

[Clientlibs para componentes de Communities](clientlibs.md) describe cómo agregar clientlibs a una página.

### Author Clientlibs {#author-clientlibs}

La versión de autor clientlibs se elimina al código Javascript mínimo necesario para implementar el componente.

Estos clientlibs nunca deben incluirse directamente, sino que están disponibles para incrustarse en otros clientlibs, que están diseñados a mano para un sitio.

Estas versiones se encuentran en la carpeta de bibliotecas de SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por ejemplo:

* Nodo de carpeta del cliente: `/libs/social/forum/hbs/forum/clientlibs`
* Propiedad Categories: `cq.social.author.hbs.forum`

Nota: aunque clientlibs de autor nunca incrusta otras bibliotecas, sí enumeran sus dependencias. Cuando se incrustan en otras bibliotecas, las dependencias no se extraen automáticamente y también deben incrustarse.

Los clientlibs de autor requeridos se pueden identificar insertando &quot;author&quot; en los clientlibs enumerados para cada componente SCF en el [Guía de componentes de comunidad](components-guide.md).

### Consideraciones de uso {#usage-considerations}

Cada sitio es diferente en la forma en que administra las bibliotecas de cliente. Varios factores incluyen:

* Velocidad global: Tal vez el deseo sea que el sitio responda, pero es aceptable que la primera página sea un poco lenta de cargar. Si muchas de las páginas utilizan el mismo JavaScript, los distintos Javascript se pueden integrar en una clientlib y se puede hacer referencia a ellos desde la primera página que se cargará. El Javascript de esta descarga única permanece en la caché, lo que minimiza la cantidad de datos que se descargarán para las páginas siguientes.
* Tiempo corto hasta la primera página: Tal vez el deseo sea que la primera página se cargue rápidamente. En este caso, el Javascript está en varios archivos pequeños a los que solo se hará referencia cuando sea necesario.
* Un equilibrio entre la primera carga de página y las descargas posteriores.

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del servidor](server-customize.md)** |
|---|---|
|  | **[Manillares SCF Helpers](handlebars-helpers.md)** |
