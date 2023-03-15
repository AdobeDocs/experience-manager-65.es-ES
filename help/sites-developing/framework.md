---
title: Marco de trabajo de etiquetado de AEM
seo-title: AEM Tagging Framework
description: AEM Etiquetado de contenido y aprovechamiento de la infraestructura de etiquetado de
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: efb4f9f8a97baf8d3d02160226e4f4d3f8f64c89
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# Marco de trabajo de etiquetado de AEM {#aem-tagging-framework}

AEM Para etiquetar contenido y aprovechar la infraestructura de etiquetado de la:

* La etiqueta debe existir como nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)` en el [nodo raíz de taxonomía](#taxonomy-root-node)

* El NodeType del nodo de contenido etiquetado debe incluir el [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* El [TagID](#tagid) se añade al nodo de contenido [ `cq:tags`](#tagged-content-cq-tags-property) y se resuelve en un nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Etiquetas : cq:Tipo de nodo de etiqueta  {#tags-cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

Una etiqueta puede ser una palabra simple (por ejemplo, cielo) o representar una taxonomía jerárquica (por ejemplo, fruta/manzana, es decir, tanto la fruta genérica como la manzana más específica).

Las etiquetas se identifican con un TagID único.

Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar del TagID, cuando esté presente.

El marco de etiquetado también permite restringir la capacidad de los autores y visitantes del sitio para utilizar solo etiquetas específicas predefinidas.

### Características de etiquetas {#tag-characteristics}

* el tipo de nodo es `cq:Tag`
* el nombre de nodo es un componente del ` [TagID](#tagid)`
* el ` [TagID](#tagid)` siempre incluye un [namespace](#tag-namespace)

* opcional `jcr:title` (la propiedad Title que se mostrará en la interfaz de usuario)

* opcional `jcr:description` propiedad

* cuando contiene nodos secundarios, se denomina [etiqueta contenedora](#container-tags)
* se almacena en el repositorio debajo de una ruta base denominada [nodo raíz de taxonomía](#taxonomy-root-node)

### ID de etiqueta {#tagid}

TagID identifica una ruta que se resuelve en un nodo de etiqueta del repositorio.

Normalmente, TagID es un TagID abreviado que comienza con el área de nombres o puede ser un TagID absoluto que comience por [nodo raíz de taxonomía](#taxonomy-root-node).

Cuando se etiqueta contenido, si aún no existe, la variable ` [cq:tags](#tagged-content-cq-tags-property)` La propiedad se agrega al nodo de contenido y TagID se agrega al valor de matriz de cadenas de la propiedad.

TagID consta de un [namespace](#tag-namespace) seguido del TagID local. [Etiquetas de contenedor](#container-tags) tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden utilizar para hacer referencia a las etiquetas del mismo modo que cualquier TagID local. Por ejemplo, se permite etiquetar contenido con &quot;fruta&quot;, incluso si es una etiqueta contenedora con subetiquetas, como &quot;fruta/manzana&quot; y &quot;fruta/plátano&quot;.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *no* ser un nodo de tipo `  cq   :Tag`.

AEM En el caso de los usuarios, la ruta base es `/content/  cq   :tags` y el nodo raíz es del tipo `  cq   :Folder`.

### Área de nombres de etiqueta {#tag-namespace}

Las áreas de nombres permiten agrupar cosas. El caso de uso más habitual es tener un área de nombres por sitio (web) (por ejemplo, público, interno y portal) o por aplicación más grande (por ejemplo, WCM, Assets, Communities), pero las áreas de nombres se pueden utilizar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario de para mostrar únicamente el subconjunto de etiquetas (es decir, las etiquetas de un determinado espacio de nombres) que se aplica al contenido actual.

El área de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo situado inmediatamente debajo de [nodo raíz de taxonomía](#taxonomy-root-node). Un área de nombres es un nodo de tipo `cq:Tag` cuyo elemento principal no es un `cq:Tag`tipo de nodo.

Todas las etiquetas tienen un área de nombres. Si no se especifica ningún área de nombres, la etiqueta se asigna al área de nombres predeterminada, que es TagID `default` (El título es `Standard Tags),`es decir `/content/cq:tags/default.`

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contenga cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) en una taxonomía sirven como subsuma de todas las subetiquetas: por ejemplo, el contenido etiquetado con fruta/manzana se considera etiquetado con fruta también, es decir, la búsqueda de contenido etiquetado con fruta también encontraría el contenido etiquetado con fruta/manzana.

### Resolver TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos &quot;:&quot;, los dos puntos separan el área de nombres de la etiqueta o subtaxonomía, que luego se separan con barras normales &quot;/&quot;. Si el ID de etiqueta no tiene dos puntos, el área de nombres predeterminada es implícita.

La ubicación estándar y única de las etiquetas es inferior a /content/cq:tags.

Las etiquetas que hacen referencia a rutas no existentes o que no apuntan a un nodo cq:Tag se consideran no válidas y se omiten.

En la tabla siguiente se muestran algunos ejemplos de TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

En la tabla siguiente se muestran algunos ejemplos de TagID, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

<table>
 <tbody>
  <tr>
   <td><strong>ID de etiqueta<br /> </strong></td>
   <td><strong>Espacio de nombres</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Etiqueta(s) de contenedor</strong></td>
   <td><strong>Etiqueta de hoja</strong></td>
   <td><strong>Repositorio<br /> Ruta de etiqueta absoluta</strong></td>
  </tr>
  <tr>
   <td>dam:fruta/manzana/braeburn</td>
   <td>presa</td>
   <td>fruta/manzana/cereza</td>
   <td>fruta, manzana</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruta/manzana/braeburn</td>
  </tr>
  <tr>
   <td>color/rojo</td>
   <td>predeterminada</td>
   <td>color/rojo</td>
   <td>color</td>
   <td>rojo</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>cielo</td>
   <td>predeterminada</td>
   <td>cielo</td>
   <td>(ninguno)</td>
   <td>cielo</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>presa</td>
   <td>(ninguno)</td>
   <td>(ninguno)</td>
   <td>(ninguno, el área de nombres)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>categoría</td>
   <td>coche</td>
   <td>coche</td>
   <td>coche</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional ( `jcr:title`) es posible localizar el título para mostrarlo añadiendo la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte

* [Etiquetas en diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages) - que describe el uso de las API
* [Administración de etiquetas en diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) - que describe el uso de la consola de etiquetado

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio en la variable [nodo raíz de taxonomía](#taxonomy-root-node). Permitir o denegar a los autores y visitantes del sitio la creación de etiquetas en un área de nombres determinada se puede lograr estableciendo las ACL adecuadas en el repositorio.

Además, la denegación de permisos de lectura para determinadas etiquetas o áreas de nombres controlará la capacidad de aplicar etiquetas a contenido específico.

Una práctica típica incluye:

* Permitir el `tag-administrators` acceso de escritura de grupo/función a todas las áreas de nombres (agregar/modificar en `/content/cq:tags`). AEM Este grupo incluye a los usuarios que ya están preparados para su uso en el momento de la compra.

* Permite a los usuarios/autores acceder a todas las áreas de nombres que deben poder leerlas (principalmente todas).
* Permitir a usuarios/autores escribir en aquellas áreas de nombres en las que los usuarios/autores deben poder definir libremente las etiquetas (add_node en `/content/cq:tags/some_namespace`)

## Contenido etiquetable : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones adjunten el etiquetado a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir el `cq:Taggable` mixin o el `cq:OwnerTaggable` mixin.

El `cq:OwnerTaggable` mixin, que hereda de `cq:Taggable`, tiene la intención de indicar que el propietario/autor puede clasificar el contenido. AEM En el caso de los informes, solo es un atributo de la variable `cq:PageContent` nodo. El `cq:OwnerTaggable` El marco de etiquetado no requiere el mixin.

>[!NOTE]
>
>Se recomienda habilitar etiquetas únicamente en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo jcr:content). Algunos ejemplos son:
>
>* páginas ( `cq:Page`) donde la variable `jcr:content`el nodo es del tipo `cq:PageContent` que incluye el `cq:Taggable` mixin.
>
>* recursos ( `cq:Asset`) donde la variable `jcr:content/metadata` El nodo siempre tiene el `cq:Taggable` mixin.
>


### Notación de tipo de nodo (CND) {#node-type-notation-cnd}

Las definiciones del tipo de nodo existen en el repositorio como archivos CDN. La notación CDN se define como parte de la documentación JCR [aquí](https://jackrabbit.apache.org/node-type-notation.html).

AEM Las definiciones esenciales para los tipos de nodo incluidos en la lista de nombres de dominio son las siguientes:

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

El `cq:tags` La propiedad es una matriz de cadenas que se utiliza para almacenar uno o más TagID cuando los autores o visitantes del sitio los aplican al contenido. La propiedad solo tiene significado cuando se agrega a un nodo que se define con la variable `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>AEM Para aprovechar la funcionalidad de etiquetado de etiquetas, las aplicaciones desarrolladas personalizadas no deben definir propiedades de etiquetas distintas de `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación se describen los efectos del repositorio al mover o combinar etiquetas utilizando [Consola de etiquetado](/help/sites-administering/tags.md):

* Cuando una etiqueta A se mueve o se combina con la etiqueta B en `/content/cq:tags`:

   * La etiqueta A no se elimina y obtiene un `cq:movedTo` propiedad.
   * La etiqueta B se crea (en caso de movimiento) y obtiene un `cq:backlinks` propiedad.

* `cq:movedTo` apunta a la etiqueta B. Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B. Al mover la etiqueta B, se actualizará esta propiedad en consecuencia. Por lo tanto, la etiqueta A está oculta y solo se mantiene en el repositorio para resolver los ID de etiqueta en los nodos de contenido que apuntan a la etiqueta A. El recolector de elementos no utilizados de etiquetas elimina las etiquetas como la etiqueta A una vez que los nodos de contenido no las señalan.
Un valor especial para `cq:movedTo` la propiedad es `nirvana`: se aplica cuando se elimina la etiqueta, pero no se puede eliminar del repositorio porque hay subetiquetas con un `cq:movedTo` eso debe mantenerse.

   >[!NOTE]
   >
   >El `cq:movedTo` La propiedad solo se añade a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
   >
   >1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia) O
   >1. La etiqueta tiene elementos secundarios que ya se han movido.


* `cq:backlinks` mantiene las referencias en la otra dirección, es decir, conserva una lista de todas las etiquetas que se han movido o combinado con la etiqueta B. Esto es necesario principalmente para mantener `cq:movedTo`propiedades actualizadas cuando la etiqueta B se mueve, combina o elimina, o cuando la etiqueta B está activada, en cuyo caso todas sus etiquetas de backlinks deben activarse también.

   >[!NOTE]
   >
   >El `cq:backlinks` La propiedad solo se añade a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
   >
   >1. La etiqueta se utiliza en el contenido (lo que significa que tiene una referencia) O
   >1. La etiqueta tiene elementos secundarios que ya se han movido.


* Leer un `cq:tags` La propiedad de un nodo de contenido implica la siguiente resolución:

   1. Si no hay ninguna coincidencia en `/content/cq:tags`, no se devuelve ninguna etiqueta.
   1. Si la etiqueta tiene un `cq:movedTo` establecida, se sigue el ID de etiqueta al que se hace referencia.
Este paso se repite siempre que la etiqueta seguida tenga un `cq:movedTo` propiedad.

   1. Si la etiqueta seguida no tiene un `cq:movedTo` propiedad, se lee la etiqueta.

* Para publicar el cambio cuando se haya movido o combinado una etiqueta, la variable `cq:Tag` el nodo y todos sus backlinks deben replicarse: esto se hace automáticamente cuando la etiqueta se activa en la consola de administración de etiquetas.

* Actualizaciones posteriores en la página `cq:tags` limpie automáticamente las referencias &quot;antiguas&quot;. Esto se activa porque la resolución de una etiqueta desplazada a través de la API devuelve la etiqueta de destino, proporcionando así el ID de etiqueta de destino.

>[!NOTE]
>
>El movimiento de etiquetas es diferente de la migración de etiquetas.

## Migración de etiquetas {#tags-migration}

Las etiquetas de Experience Manager 6.4 y posteriores se almacenan en `/content/cq:tags`, que anteriormente se almacenaban en `/etc/tags`. Sin embargo, en los casos en los que Adobe Experience Manager se ha actualizado desde la versión anterior, las etiquetas siguen estando presentes en la ubicación antigua `/etc/tags`. En los sistemas actualizados, las etiquetas deben migrarse a `/content/cq:tags`.

>[!NOTE]
>
>En la página Propiedades de página de las etiquetas, se recomienda utilizar el ID de etiqueta (`geometrixx-outdoors:activity/biking`) en lugar de codificar la ruta base de la etiqueta (por ejemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para enumerar etiquetas, `com.day.cq.tagging.servlets.TagListServlet` se puede utilizar.

>[!NOTE]
>
>Se recomienda utilizar la API del administrador de etiquetas como recurso.

### AEM Si la instancia actualizada de la aplicación admite la API de TagManager {#upgraded-instance-support-tagmanager-api}

1. AEM Al principio del componente, la API de TagManager detecta si se trata de una instancia de actualizada. En el sistema actualizado, las etiquetas se almacenan en `/etc/tags`.

1. La API de TagManager se ejecuta en modo de compatibilidad con versiones anteriores, lo que significa que la API utiliza `/etc/tags` como ruta base. Si no es así, utiliza una nueva ubicación `/content/cq:tags`.

1. Actualice la ubicación de las etiquetas.

1. Después de migrar las etiquetas a la nueva ubicación, ejecute el siguiente script:

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

El script recupera todas las etiquetas que tienen `/etc/tags` en el valor de `cq:movedTo/cq:backLinks` propiedad. A continuación, se repite por el conjunto de resultados recuperado y se resuelve el `cq:movedTo` y `cq:backlinks` valores de propiedad a `/content/cq:tags` rutas (en el caso de que `/etc/tags` se detecta en el valor).

### AEM Si la instancia de se ejecuta en la IU clásica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>La IU clásica no es compatible con el tiempo de inactividad cero y no admite la nueva ruta base de etiquetas. Si desea utilizar la IU clásica de `/etc/tags` debe crearse seguido de `cq-tagging` reinicio del componente.

AEM En el caso de instancias actualizadas de la aplicación admitidas por la API de TagManager y que se ejecuten en la IU clásica, haga lo siguiente:

1. Una vez referencias a la ruta base de etiqueta antigua `/etc/tags` se reemplazan con tagId o la nueva ubicación de la etiqueta `/content/cq:tags`, puede migrar etiquetas a la nueva ubicación `/content/cq:tags` en CRX seguido del reinicio del componente.

1. Después de migrar las etiquetas a la nueva ubicación, ejecute el script mencionado anteriormente.
