---
title: Personalización del lado del cliente
description: Personalización del comportamiento o la apariencia del lado del cliente en AEM Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Personalización del lado del cliente  {#client-side-customization}

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización del lado del servidor](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

Existen varios métodos para personalizar el aspecto o el comportamiento de un componente de AEM Communities en el lado del cliente.

Dos enfoques principales son superponer o ampliar un componente.

[Superposición](#overlays) un componente cambia el componente predeterminado y afecta a cada referencia al componente.

[Ampliación](#extensions) un componente, al tener un nombre único, limita el ámbito de los cambios. El término &quot;ampliar&quot; se utiliza indistintamente con &quot;anular&quot;.

## Superposiciones {#overlays}

La superposición de un componente es un método para realizar modificaciones en un componente predeterminado y afectar a todas las instancias que utilizan el predeterminado.

La superposición se realiza modificando una copia del componente predeterminado en el icono /**apps** en lugar de modificar el componente original en el directorio /**libs** directorio. El componente se construye con una ruta relativa idéntica, excepto que &quot;libs&quot; se sustituye por &quot;apps&quot;.

El directorio /apps es el primer lugar en el que se buscan solicitudes para resolverlas y, si no se encuentra, se utiliza la versión predeterminada en el directorio /libs.

El componente predeterminado en el directorio /libs nunca debe modificarse, ya que los parches y las actualizaciones futuros pueden alterar el directorio /libs de la manera necesaria mientras se mantienen las interfaces públicas.

Esto es diferente a [extensivo](#extensions) un componente predeterminado en el que se desea realizar modificaciones para un uso específico, creando una ruta única al componente y basándose en la referencia al componente predeterminado original en el directorio /libs como tipo de superrecurso.

Para ver un ejemplo rápido de superposición del componente Comentarios, pruebe con el [Tutorial del componente Comentarios de superposición](overlay-comments.md).

## Extensiones  {#extensions}

Ampliar (anular) un componente es un método para realizar modificaciones para un uso específico sin afectar a todas las instancias que utilizan el predeterminado. El componente extendido tiene un nombre único en la carpeta /apps y hace referencia al componente predeterminado en la carpeta /libs, por lo que el diseño y el comportamiento predeterminados de un componente no se modifican.

Esto es diferente a [superposición](#overlays) es el componente predeterminado en el que la naturaleza de Sling resuelve las referencias relativas a la carpeta apps/ folder antes de buscar en la carpeta libs/ folder, por lo que el diseño o el comportamiento de un componente se modifican globalmente.

Para ver un ejemplo rápido de cómo ampliar el componente de comentarios, pruebe con el [Tutorial del componente Ampliar comentarios](extend-comments.md).

## Enlace de JavaScript {#javascript-binding}

El script HBS para el componente debe estar enlazado a los objetos, modelos y vistas de JavaScript que implementan esta función.

El valor del `data-scf-component` El atributo puede ser el predeterminado, como **`social/tally/components/hbs/rating`** o un componente ampliado (personalizado) para funcionalidades personalizadas, como **weretail/components/hbs/rating**.

Para enlazar un componente, todo el script del componente debe incluirse dentro de un &lt;div> con los atributos siguientes:

* `data-component-id`=&quot;`{{id}}`&quot;

  se resuelve en la propiedad id desde el contexto

* `data-scf-component`=&quot;*&lt;resourcetype>*

Por ejemplo, desde `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propiedades personalizadas {#custom-properties}

Al ampliar o superponer un componente, es posible añadir propiedades a un cuadro de diálogo modificado.

Se puede acceder a todas las propiedades configuradas en un componente o recurso haciendo referencia a las claves de propiedad en la plantilla handlebars:

`{{properties.<property_name>}}`

## Aplicación de máscara CSS {#skinning-css}

La personalización de los componentes para que coincidan con el tema general del sitio web se puede lograr &#39;desollando&#39;: cambiando colores, fuentes, imágenes, botones, vínculos, espaciado e incluso colocando hasta cierto punto.

El desollado se puede lograr anulando selectivamente los estilos del marco de trabajo o escribiendo hojas de estilo completamente nuevas. Los componentes de SCF definen clases CSS semánticas, modulares y con espacios de nombres que afectan a los distintos elementos que conforman un componente.

Para despellejar un componente:

1. Identifique los elementos que desee cambiar (por ejemplo, el área de composición, los botones de la barra de herramientas, la fuente del mensaje, etc.).
1. Identifique las clases o reglas CSS que afectan a estos elementos.
1. Cree un archivo de hoja de estilos (.css).
1. Incluya la hoja de estilos en una carpeta de biblioteca de cliente ([clientlibs](#clientlibs-for-scf)) para su sitio y asegúrese de que se incluye desde sus plantillas y páginas con [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redefina las clases y reglas CSS que ha identificado (#2) en la hoja de estilos y agregue estilos.

Los estilos personalizados ahora anularán los estilos de marco de trabajo predeterminados y el componente se procesará con la nueva apariencia.

>[!CAUTION]
>
>Cualquier nombre de clase CSS con el prefijo `scf-js` tiene un uso específico en el código JavaScript. Estas clases afectan al estado de un componente (por ejemplo, cambia de oculto a visible) y no se deben anular ni eliminar.
>
>Mientras que el `scf-js` las clases no afectan a los estilos, los nombres de clase pueden utilizarse en hojas de estilo con la advertencia de que, al controlar los estados de los elementos, pueden producirse efectos secundarios.

## Ampliación de JavaScript {#extending-javascript}

Para ampliar una implementación de JavaScript de componentes, debe:

1. Cree un componente para su aplicación con un jcr:resourceSuperType establecido en el valor del jcr:resourceType del componente ampliado; por ejemplo, social/forum/components/hbs/forum.
1. Examine el JavaScript del componente SCF predeterminado para determinar qué métodos deben registrarse con SCF.registerComponent().
1. Copie el JavaScript del componente ampliado o comience desde cero.
1. Amplíe el método.
1. Utilice SCF.registerComponent() para registrar todos los métodos con los valores predeterminados o con los objetos y vistas personalizados.

### forum.js: Extensión de muestra del foro - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

Las etiquetas de script son una parte inherente del marco de trabajo del lado del cliente. Son el pegado que ayuda a enlazar el marcado generado en el servidor con los modelos y vistas del lado del cliente.

Las etiquetas de script en los scripts SCF no deben eliminarse al superponer o anular componentes. Las etiquetas de script SCF creadas automáticamente para insertar JSON en el HTML se identifican con el atributo `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

El uso de [bibliotecas del lado del cliente](../../help/sites-developing/clientlibs.md) (clientlibs) proporciona un medio para organizar y optimizar el JavaScript y CSS utilizados para representar contenido en el cliente.

Los clientlibs para SCF siguen un patrón de nomenclatura muy específico para dos variantes, que varían solo por la presencia de &quot;author&quot; en el nombre de la categoría:

| Variante de Clientlib | Patrón para la propiedad Categorías |
|--- |--- |
| clientlib completo | cq.social.hbs.&lt;component name> |
| clientlib de autor | cq.social.author.hbs.&lt;component name> |

### Completar Clientlibs {#complete-clientlibs}

Los clientlibs completos (que no son de autor) incluyen dependencias y son prácticos para incluirlos en ui:includeClientLib.

Estas versiones se encuentran en:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por ejemplo:

* Nodo de la carpeta del cliente: `/etc/clientlibs/social/hbs/forum`
* Propiedad Categories: `cq.social.hbs.forum`

El [Guía de componentes de la comunidad](components-guide.md) enumera los clientlibs completos necesarios para cada componente de SCF.

[Componentes de Clientlibs para Communities](clientlibs.md) describe cómo agregar clientlibs a una página.

### Author Clientlibs {#author-clientlibs}

La versión de autor clientlibs se reduce al mínimo JavaScript necesario para implementar el componente.

Estos clientlibs nunca deben incluirse directamente, sino que están disponibles para incrustarse en otros clientlibs, que son hechos a mano para un sitio.

Estas versiones se encuentran en la carpeta de bibliotecas SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por ejemplo:

* Nodo de la carpeta del cliente: `/libs/social/forum/hbs/forum/clientlibs`
* Propiedad Categories: `cq.social.author.hbs.forum`

Nota: aunque los clientlibs de autor nunca incrustan otras bibliotecas, sí enumeran sus dependencias. Cuando se incrustan en otras bibliotecas, las dependencias no se extraen automáticamente y también deben incrustarse.

Los clientlibs de autor requeridos se pueden identificar insertando &quot;author&quot; en los clientlibs enumerados para cada componente SCF en el [Guía de componentes de la comunidad](components-guide.md).

### Consideraciones de uso {#usage-considerations}

Cada sitio es diferente en la forma en que administran las bibliotecas de cliente. Varios factores incluyen:

* Velocidad general: Tal vez el deseo es que el sitio sea adaptable, pero es aceptable que la primera página sea un poco lenta de cargar. Si muchas de las páginas utilizan el mismo JavaScript, los distintos JavaScript se pueden incrustar en una clientlib y se puede hacer referencia a ellos desde la primera página que se cargue. El JavaScript de esta descarga única permanece en la caché, lo que minimiza la cantidad de datos que se descargarán para las páginas siguientes.
* Breve tiempo hasta la primera página: tal vez lo que se desea es que la primera página se cargue rápidamente. En este caso, se hace referencia al JavaScript en varios archivos pequeños solo cuando es necesario.
* Un equilibrio entre la primera carga de página y las descargas posteriores.

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización del lado del servidor](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
