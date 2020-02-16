---
title: AEM Tagging Framework
seo-title: AEM Tagging Framework
description: Etiquete el contenido y aproveche la infraestructura de etiquetado de AEM
seo-description: Etiquete el contenido y aproveche la infraestructura de etiquetado de AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM Tagging Framework{#aem-tagging-framework}

Para etiquetar contenido y aprovechar la infraestructura de etiquetado de AEM:

* La etiqueta debe existir como nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)` bajo el nodo raíz de [taxonomía](#taxonomy-root-node)

* NodeType del nodo de contenido etiquetado debe incluir la [`cq:Taggable`](#taggable-content-cq-taggable-mixin) combinación
* El [TagID](#tagid) se agrega a la [ propiedad `cq:tags`](#tagged-content-cq-tags-property) del nodo de contenido y se resuelve en un nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Etiquetas: cq:Tipo de nodo de etiqueta {#tags-cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

Una etiqueta puede ser una palabra simple (por ejemplo, cielo) o representar una taxonomía jerárquica (por ejemplo, fruta/manzana, lo que significa tanto la fruta genérica como la manzana más específica).

Las etiquetas se identifican mediante un TagID único.

Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar del TagID, cuando esté presente.

El marco de etiquetado también permite restringir el uso de etiquetas específicas predefinidas por los autores y visitantes del sitio.

### Características de la etiqueta {#tag-characteristics}

* el tipo de nodo es `cq:Tag`
* el nombre del nodo es un componente de ` [TagID](#tagid)`
* el ` [TagID](#tagid)` siempre incluye un [espacio de nombres](#tag-namespace)

* propiedad opcional `jcr:title` (el título que se mostrará en la interfaz de usuario)

* opcional `jcr:description` , propiedad

* cuando contiene nodos secundarios, se denomina etiqueta de [contenedor](#container-tags)
* se almacena en el repositorio debajo de una ruta base denominada nodo raíz de [taxonomía](#taxonomy-root-node)

### ID de etiqueta {#tagid}

Un TagID identifica una ruta que se resuelve en un nodo de etiqueta en el repositorio.

Normalmente, TagID es un TagID abreviado que comienza con el espacio de nombres o puede ser un TagID absoluto que comienza en el nodo [raíz de](#taxonomy-root-node)taxonomía.

Cuando el contenido está etiquetado, si aún no existe, la ` [cq:tags](#tagged-content-cq-tags-property)` propiedad se agrega al nodo de contenido y el TagID se agrega al valor de matriz String de la propiedad.

TagID consiste en un [espacio de nombres](#tag-namespace) seguido del TagID local. [Las etiquetas](#container-tags) de contenedor tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a etiquetas igual que cualquier TagID local. Por ejemplo, se permite etiquetar contenido con &quot;fruta&quot;, incluso si se trata de una etiqueta contenedora con subetiquetas, como &quot;fruta/manzana&quot; y &quot;fruta/plátano&quot;.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía *no debe* ser un nodo de tipo `  cq   :Tag`.

En AEM, la ruta de acceso base es `/content/  cq   :tags` y el nodo raíz es de tipo `  cq   :Folder`.

### Espacio de nombres de etiqueta {#tag-namespace}

Los espacios de nombres permiten agrupar cosas. El caso de uso más típico es tener un espacio de nombres por sitio (web) (por ejemplo, público, interno y portal) o por aplicación mayor (por ejemplo, WCM, Assets, Communities), pero los espacios de nombres se pueden utilizar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario para mostrar únicamente el subconjunto de etiquetas (es decir, etiquetas de un espacio de nombres determinado) que se aplica al contenido actual.

El espacio de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al nodo [raíz de](#taxonomy-root-node)taxonomía. Un espacio de nombres es un nodo de tipo `cq:Tag` cuyo principal no es un tipo de `cq:Tag`nodo.

Todas las etiquetas tienen un espacio de nombres. Si no se especifica ningún espacio de nombres, la etiqueta se asigna al espacio de nombres predeterminado, que es TagID `default` (el título es `Standard Tags),`decir `/content/cq:tags/default.`

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contiene cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) de una taxonomía sirven como subsuma de todas las subetiquetas: por ejemplo, el contenido etiquetado con fruta/manzana también se considera etiquetado con fruta, es decir, la búsqueda de contenido que se acaba de etiquetar con fruta también encontraría el contenido etiquetado con fruta/manzana.

### Resolución de TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos &quot;:&quot;, los dos puntos separan el espacio de nombres de la etiqueta o subtaxonomía, que luego se separan con barras normales &quot;/&quot;. Si el ID de etiqueta no tiene dos puntos, se da a entender el espacio de nombres predeterminado.

La ubicación estándar y única de las etiquetas está por debajo de /content/cq:tags.

Las etiquetas que hacen referencia a rutas o rutas no existentes que no apuntan a un nodo cq:Tag se consideran no válidas y se omiten.

La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

<table>
 <tbody>
  <tr>
   <td><strong>ID de etiqueta<br /> </strong></td>
   <td><strong>Espacio de nombres</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Etiquetas de contenedor</strong></td>
   <td><strong>Etiqueta de hoja</strong></td>
   <td><strong>Ruta de la etiqueta absoluta del repositorio<br /></strong></td>
  </tr>
  <tr>
   <td>represa:fruta/manzana/braeburn</td>
   <td>dam</td>
   <td>fruta/manzana/pechuga</td>
   <td>fruta, manzana</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruta/manzana/braeburn</td>
  </tr>
  <tr>
   <td>color/rojo</td>
   <td>predeterminada</td>
   <td>color/rojo</td>
   <td>color</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>sky</td>
   <td>predeterminada</td>
   <td>sky</td>
   <td>(ninguno)</td>
   <td>sky</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(ninguno)</td>
   <td>(ninguno)</td>
   <td>(ninguno, el espacio de nombres)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>category</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional ( `jcr:title`), es posible localizar el título para que se muestre agregando la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte

* [Etiquetas en distintos idiomas](/help/sites-developing/building.md#tags-in-different-languages) : que describe el uso de las API
* [Administración de etiquetas en distintos idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) , que describe el uso de la consola de etiquetado

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio bajo el nodo [raíz de](#taxonomy-root-node)taxonomía. Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en un espacio de nombres determinado se puede lograr configurando las ACL apropiadas en el repositorio.

Además, la denegación de permisos de lectura para determinadas etiquetas o espacios de nombres controlará la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitir el acceso de escritura de grupo o función a todos los espacios de nombres (agregar/modificar en `tag-administrators` `/content/cq:tags`). Este grupo viene con AEM incorporado.

* Permitir que los usuarios/autores lean acceso a todos los espacios de nombres que deberían ser legibles para ellos (en su mayoría, todos).
* Permitir que los usuarios/autores escriban acceso a los espacios de nombres en los que los usuarios/autores deben definir libremente las etiquetas (agregar nodo en `/content/cq:tags/some_namespace`)

## Contenido etiquetable: cq:Mezcla etiquetable {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones puedan adjuntar el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir la `cq:Taggable` mezcla o la `cq:OwnerTaggable` mezcla.

La `cq:OwnerTaggable` mezcla, que hereda de `cq:Taggable`, tiene como objetivo indicar que el contenido puede ser clasificado por el propietario/autor. En AEM, solo es un atributo del `cq:PageContent` nodo. El marco de etiquetado no requiere la `cq:OwnerTaggable` mezcla.

>[!NOTE]
>
>Se recomienda activar únicamente etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo jcr:content). Algunos ejemplos son:
>
>* páginas ( `cq:Page`) donde el `jcr:content`nodo es del tipo `cq:PageContent` que incluye la `cq:Taggable` mezcla.
   >
   >
* recursos ( `cq:Asset`) donde el `jcr:content/metadata` nodo siempre tiene la `cq:Taggable` mezcla.
>



### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Existen definiciones de tipo de nodo en el repositorio como archivos CND. La notación CND se define como parte de la documentación de JCR [aquí](https://jackrabbit.apache.org/node-type-notation.html).

Las definiciones esenciales para los tipos de nodos incluidos en AEM son las siguientes:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## Contenido etiquetado: cq:tags (propiedad) {#tagged-content-cq-tags-property}

La `cq:tags` propiedad es una matriz de cadena que se utiliza para almacenar una o varias TagID cuando los autores o visitantes del sitio las aplican al contenido. La propiedad sólo tiene significado cuando se agrega a un nodo que se define con la ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` mezcla.

>[!NOTE]
>
>Para aprovechar la funcionalidad de etiquetado AEM, las aplicaciones desarrolladas personalizadas no deben definir otras propiedades de etiqueta que no sean `cq:tags`.

## Movimiento y combinación de etiquetas {#moving-and-merging-tags}

A continuación se muestra una descripción de los efectos del repositorio al mover o combinar etiquetas mediante la consola [Etiquetado](/help/sites-administering/tags.md):

* Cuando se mueve o combina una etiqueta A en la etiqueta B en `/content/cq:tags`:

   * la etiqueta A no se elimina y obtiene una `cq:movedTo` propiedad.
   * se crea la etiqueta B (en caso de movimiento) y obtiene una `cq:backlinks` propiedad.

* `cq:movedTo` apunta a la etiqueta B.
Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B. Al mover la etiqueta B se actualizará esta propiedad como corresponda. La etiqueta A se oculta por lo tanto y solo se mantiene en el repositorio para resolver los ID de etiquetas de los nodos de contenido que apuntan a la etiqueta A. El recolector de elementos no utilizados de etiquetas elimina etiquetas como la etiqueta A cuando ya no hay más nodos de contenido que apunten a ellas.
Un valor especial para la `cq:movedTo` propiedad es `nirvana`: se aplica cuando se elimina la etiqueta pero no se puede eliminar del repositorio porque hay subetiquetas con una `cq:movedTo` que se deben guardar.

   >[!NOTE]
   >
   >La propiedad `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* `cq:backlinks` mantiene las referencias en la otra dirección, es decir, mantiene una lista de todas las etiquetas que se han movido a la etiqueta B o que se han combinado con ella. Esto se requiere principalmente para mantener `cq:movedTo`las propiedades actualizadas cuando la etiqueta B se mueve/combina/elimina también o cuando se activa la etiqueta B, en cuyo caso también se deben activar todas sus etiquetas de vínculos atrasados.

   >[!NOTE]
   >
   >La propiedad `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* La lectura de una `cq:tags` propiedad de un nodo de contenido implica la siguiente resolución:

   1. Si no hay coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
   1. Si la etiqueta tiene un conjunto de `cq:movedTo` propiedades, se sigue el ID de etiqueta al que se hace referencia.
Este paso se repite siempre que la etiqueta seguida tenga una `cq:movedTo` propiedad.

   1. Si la etiqueta seguida no tiene una `cq:movedTo` propiedad, se lee.

* Para publicar el cambio cuando una etiqueta se ha movido o combinado, se debe replicar el `cq:Tag` nodo y todos sus vínculos posteriores: esto se realiza automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

* Las actualizaciones posteriores a la propiedad de la página `cq:tags` limpian automáticamente las referencias &quot;antiguas&quot;. Esto se activa porque al resolver una etiqueta movida a través de la API se devuelve la etiqueta de destino, proporcionando así el ID de la etiqueta de destino.
