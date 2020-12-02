---
title: AEM marco de etiquetado
seo-title: AEM marco de etiquetado
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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# Marco de etiquetado de AEM {#aem-tagging-framework}

Para etiquetar contenido y aprovechar la infraestructura de etiquetado de AEM:

* La etiqueta debe existir como un nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)` en el nodo raíz de taxonomía [a2/>](#taxonomy-root-node)

* NodeType del nodo de contenido etiquetado debe incluir la mezcla [ `cq:Taggable`](#taggable-content-cq-taggable-mixin)
* El [TagID](#tagid) se agrega a la propiedad [ `cq:tags`](#tagged-content-cq-tags-property) del nodo de contenido y se resuelve en un nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Etiquetas: cq:Tipo de nodo de etiqueta {#tags-cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

Una etiqueta puede ser una palabra simple (por ejemplo, cielo) o representar una taxonomía jerárquica (por ejemplo, fruta/manzana, lo que significa tanto la fruta genérica como la manzana más específica).

Las etiquetas se identifican mediante un TagID único.

Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar del TagID, cuando esté presente.

El marco de etiquetado también permite restringir el uso de visitantes predefinidos y específicos por parte de los autores y del sitio.

### Características de la etiqueta {#tag-characteristics}

* el tipo de nodo es `cq:Tag`
* el nombre del nodo es un componente de ` [TagID](#tagid)`
* el ` [TagID](#tagid)` siempre incluye una [Área de nombres](#tag-namespace)

* propiedad opcional `jcr:title` (el Título que se mostrará en la interfaz de usuario)

* opcional `jcr:description`, propiedad

* cuando contiene nodos secundarios, se denomina una etiqueta [contenedor](#container-tags)
* se almacena en el repositorio debajo de una ruta de acceso base denominada [nodo raíz de taxonomía](#taxonomy-root-node)

### ID de etiqueta {#tagid}

Un TagID identifica una ruta que se resuelve en un nodo de etiqueta en el repositorio.

Normalmente, TagID es un TagID abreviado que comienza con la Área de nombres o puede ser un TagID absoluto que comienza en el nodo [raíz de taxonomía](#taxonomy-root-node).

Cuando se etiqueta contenido, si no existe todavía, la propiedad ` [cq:tags](#tagged-content-cq-tags-property)` se agrega al nodo de contenido y TagID se agrega al valor de matriz String de la propiedad.

TagID consiste en una [Área de nombres](#tag-namespace) seguida del TagID local. [Los ](#container-tags) etiquetas de contenedor tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a etiquetas igual que cualquier TagID local. Por ejemplo, se permite etiquetar contenido con &quot;fruta&quot;, incluso si se trata de una etiqueta de contenedor con subetiquetas, como &quot;fruta/manzana&quot; y &quot;fruta/plátano&quot;.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *no* ser un nodo de tipo `  cq   :Tag`.

En AEM, la ruta de acceso base es `/content/  cq   :tags` y el nodo raíz es de tipo `  cq   :Folder`.

### Área de nombres de etiquetas {#tag-namespace}

Las Áreas de nombres permiten agrupar cosas. El caso de uso más típico es tener una Área de nombres por (web) sitio (por ejemplo, pública, interna y portal) o por aplicación mayor (por ejemplo, WCM, Assets, Communities), pero las Áreas de nombres pueden utilizarse para otras necesidades. Las Áreas de nombres se utilizan en la interfaz de usuario para mostrar únicamente el subconjunto de etiquetas (es decir, las etiquetas de una determinada Área de nombres) que se aplica al contenido actual.

La Área de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al nodo [raíz de taxonomía](#taxonomy-root-node). Una Área de nombres es un nodo de tipo `cq:Tag` cuyo principal no es un tipo de nodo `cq:Tag`.

Todas las etiquetas tienen una Área de nombres. Si no se especifica ninguna Área de nombres, la etiqueta se asigna a la Área de nombres predeterminada, que es TagID `default` (el título es `Standard Tags),`es `/content/cq:tags/default.`

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedor es un nodo de tipo `cq:Tag` que contiene cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) de una taxonomía sirven de subsuma de todas las subetiquetas: por ejemplo, el contenido etiquetado con fruta/manzana también se considera etiquetado con fruta, es decir, la búsqueda de contenido que se acaba de etiquetar con fruta también encontraría el contenido etiquetado con fruta/manzana.

### Resolución de TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos &quot;:&quot;, los dos puntos separan la Área de nombres de la etiqueta o subtaxonomía, que se separan con barras normales &quot;/&quot;. Si el ID de etiqueta no tiene dos puntos, se da a entender la Área de nombres predeterminada.

La ubicación estándar y única de las etiquetas está por debajo de /content/cq:tags.

Las etiquetas que hacen referencia a rutas o rutas no existentes que no apuntan a un nodo cq:Tag se consideran no válidas y se omiten.

La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:
La siguiente tabla muestra algunos de los TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

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
   <td>(ninguno, la Área de nombres)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/categoría/car</td>
   <td>categoría</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq:tags/categoría/car</td>
  </tr>
 </tbody>
</table>

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional ( `jcr:title`), es posible localizar el título para la visualización agregando la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte

* [Etiquetas en distintos idiomas](/help/sites-developing/building.md#tags-in-different-languages) , que describen el uso de las API
* [Administración de etiquetas en distintos idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) , que describe el uso de la consola de etiquetado

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio bajo el nodo [raíz de taxonomía](#taxonomy-root-node). Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en una Área de nombres determinada se puede lograr configurando las ACL apropiadas en el repositorio.

Además, la denegación de permisos de lectura para determinadas etiquetas o Áreas de nombres controlará la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitir el acceso de escritura de grupo/rol `tag-administrators` a todas las Áreas de nombres (agregar/modificar en `/content/cq:tags`). Este grupo viene con AEM lista para usar.

* Permitir que los usuarios/autores lean el acceso a todas las Áreas de nombres que deberían ser legibles para ellos (en su mayoría, todas).
* Permitir que los usuarios/autores escriban acceso a esas Áreas de nombres en las que los usuarios/autores deben definir libremente las etiquetas (add_node en `/content/cq:tags/some_namespace`)

## Contenido etiquetable: cq:Mezclador etiquetable {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones puedan adjuntar el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir la mezcla `cq:Taggable` o la mezcla `cq:OwnerTaggable`.

La mezcla `cq:OwnerTaggable`, que hereda de `cq:Taggable`, está pensada para indicar que el propietario/autor puede clasificar el contenido. En AEM, es sólo un atributo del nodo `cq:PageContent`. El marco de etiquetado no requiere la mezcla `cq:OwnerTaggable`.

>[!NOTE]
>
>Se recomienda activar únicamente etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo jcr:content). Algunos ejemplos son:
>
>* ( `cq:Page`) donde el nodo `jcr:content`es de tipo `cq:PageContent`, que incluye la mezcla `cq:Taggable`.
   >
   >
* recursos ( `cq:Asset`) donde el nodo `jcr:content/metadata` siempre tiene la mezcla `cq:Taggable`.

>



### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Existen definiciones de tipo de nodo en el repositorio como archivos CND. La notación CND se define como parte de la documentación de JCR [aquí](https://jackrabbit.apache.org/node-type-notation.html).

Las definiciones esenciales para los tipos de nodos incluidos en la AEM son las siguientes:

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

La propiedad `cq:tags` es una matriz de cadena que se utiliza para almacenar una o más TagIDs cuando se aplican al contenido por autores o visitantes del sitio. La propiedad sólo tiene significado cuando se agrega a un nodo definido con la mezcla `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Para aprovechar AEM funcionalidad de etiquetado, las aplicaciones desarrolladas personalizadas no deben definir propiedades de etiquetas distintas de `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación se muestra una descripción de los efectos en el repositorio al mover o combinar etiquetas mediante la [consola de etiquetado](/help/sites-administering/tags.md):

* Cuando se mueve o combina una etiqueta A en la etiqueta B en `/content/cq:tags`:

   * la etiqueta A no se elimina y obtiene una propiedad `cq:movedTo`.
   * se crea la etiqueta B (en caso de movimiento) y obtiene una propiedad `cq:backlinks`.

* `cq:movedTo` apunta a la etiqueta B. Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B. Al mover la etiqueta B se actualizará esta propiedad como corresponda. La etiqueta A se oculta por lo tanto y solo se mantiene en el repositorio para resolver los ID de etiquetas de los nodos de contenido que apuntan a la etiqueta A. El recolector de elementos no utilizados de etiquetas elimina etiquetas como la etiqueta A cuando ya no hay más nodos de contenido que apunten a ellas.
Un valor especial para la propiedad `cq:movedTo` es `nirvana`: se aplica cuando se elimina la etiqueta pero no se puede eliminar del repositorio porque hay subetiquetas con `cq:movedTo` que deben mantenerse.

   >[!NOTE]
   >
   >La propiedad `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* `cq:backlinks` mantiene las referencias en la otra dirección, es decir, mantiene una lista de todas las etiquetas que se han movido a la etiqueta B o que se han combinado con ella. Esto se requiere principalmente para mantener  `cq:movedTo`las propiedades actualizadas cuando la etiqueta B se mueve/combina/elimina también o cuando se activa la etiqueta B, en cuyo caso también se deben activar todas sus etiquetas de vínculos atrasados.

   >[!NOTE]
   >
   >La propiedad `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple alguna de estas condiciones:
   >
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O    >
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* La lectura de una propiedad `cq:tags` de un nodo de contenido implica la siguiente resolución:

   1. Si no hay coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
   1. Si la etiqueta tiene una propiedad `cq:movedTo` establecida, se sigue la ID de etiqueta a la que se hace referencia.
Este paso se repite siempre que la etiqueta seguida tenga una propiedad `cq:movedTo`.

   1. Si la etiqueta seguida no tiene una propiedad `cq:movedTo`, se lee la etiqueta.

* Para publicar el cambio cuando se ha movido o combinado una etiqueta, se debe replicar el nodo `cq:Tag` y todos sus vínculos posteriores: esto se realiza automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

* Las actualizaciones posteriores a la propiedad `cq:tags` de la página limpian automáticamente las referencias &quot;antiguas&quot;. Esto se activa porque al resolver una etiqueta movida a través de la API se devuelve la etiqueta de destino, proporcionando así el ID de la etiqueta de destino.

>[!NOTE]
>
>El movimiento de etiquetas es diferente de la migración de etiquetas.

## Migración de etiquetas {#tags-migration}

Las etiquetas Experience Manager 6.4 y posteriores se almacenan en `/content/cq:tags`, que antes se almacenaban en `/etc/tags`. Sin embargo, en situaciones en las que se ha actualizado Adobe Experience Manager de la versión anterior, las etiquetas siguen presentes en la ubicación anterior `/etc/tags`. En los sistemas actualizados, las etiquetas deben migrarse en `/content/cq:tags`.

>[!NOTE]
>
>En la página Propiedades de la página de etiquetas, se recomienda utilizar el ID de la etiqueta (`geometrixx-outdoors:activity/biking`) en lugar de codificar la ruta de la base de etiquetas (por ejemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para las etiquetas de lista, se puede utilizar `com.day.cq.tagging.servlets.TagListServlet`.

>[!NOTE]
>
>Se recomienda utilizar la API del administrador de etiquetas como recurso.

### Si la instancia de AEM actualizada admite la API de TagManager {#upgraded-instance-support-tagmanager-api}

1. En el inicio del componente, la API de TagManager detecta si se trata de una instancia de AEM actualizada. En el sistema actualizado, las etiquetas se almacenan en `/etc/tags`.

1. A continuación, la API de TagManager se ejecuta en modo de compatibilidad con versiones anteriores, lo que significa que la API utiliza `/etc/tags` como ruta de acceso base. Si no es así, utiliza la nueva ubicación `/content/cq:tags`.

1. Actualice la ubicación de las etiquetas.

1. Después de migrar las etiquetas a la nueva ubicación, ejecute la siguiente secuencia de comandos:

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

La secuencia de comandos obtiene todas las etiquetas que tienen `/etc/tags` en el valor de la propiedad `cq:movedTo/cq:backLinks`. A continuación, se repite a través del conjunto de resultados recuperados y resuelve los valores de las propiedades `cq:movedTo` y `cq:backlinks` en `/content/cq:tags` paths (en el caso de que `/etc/tags` se detecte en el valor).

### Si la instancia de AEM actualizada se ejecuta en la IU clásica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>La IU clásica no es compatible con cero tiempos de inactividad y no admite la nueva ruta de base de etiquetas. Si desea utilizar la IU clásica, debe crear `/etc/tags` seguido de `cq-tagging` reinicio del componente.

En el caso de instancias de AEM actualizadas admitidas por la API de TagManager y ejecutadas en la IU clásica:

1. Una vez que las referencias a la ruta de base de etiquetas antigua `/etc/tags` se sustituyen mediante tagId o la nueva ubicación de etiquetas `/content/cq:tags`, puede migrar las etiquetas a la nueva ubicación `/content/cq:tags` en CRX seguida de un reinicio del componente.

1. Después de migrar las etiquetas a la nueva ubicación, ejecute la secuencia de comandos mencionada anteriormente.
