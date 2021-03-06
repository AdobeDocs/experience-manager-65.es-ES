---
title: Marco de etiquetado de AEM
seo-title: AEM Tagging Framework
description: Etiquetar contenido y aprovechar la infraestructura de etiquetado de AEM
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
source-git-commit: 4db9279f2d15f2e08939ba453ae8ddbbc3c3d69f
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# Marco de etiquetado de AEM {#aem-tagging-framework}

Para etiquetar contenido y aprovechar la infraestructura AEM Tagging :

* La etiqueta debe existir como nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)` en el [nodo raíz de taxonomía](#taxonomy-root-node)

* El nodo NodeType del nodo de contenido etiquetado debe incluir la variable [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixto
* La variable [TagID](#tagid) se agrega al nodo de contenido [ `cq:tags`](#tagged-content-cq-tags-property) y se resuelve en un nodo de tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Etiquetas : cq:Tag Node Type  {#tags-cq-tag-node-type}

La declaración de una etiqueta se captura en el repositorio en un nodo de tipo `cq:Tag.`

Una etiqueta puede ser una palabra simple (por ejemplo, cielo) o representar una taxonomía jerárquica (por ejemplo, fruta/manzana, que significa tanto la fruta genérica como la manzana más específica).

Las etiquetas se identifican mediante un TagID único.

Una etiqueta tiene información meta opcional, como un título, títulos localizados y una descripción. El título debe mostrarse en las interfaces de usuario en lugar del TagID, cuando esté presente.

El marco de etiquetado también permite restringir el uso de etiquetas predefinidas específicas por parte de los autores y visitantes del sitio.

### Características de las etiquetas {#tag-characteristics}

* el tipo de nodo es `cq:Tag`
* nombre de nodo es un componente de ` [TagID](#tagid)`
* el ` [TagID](#tagid)` siempre incluye un [namespace](#tag-namespace)

* opcional `jcr:title` propiedad (el título que se mostrará en la interfaz de usuario)

* opcional `jcr:description` property

* cuando contiene nodos secundarios, se denomina [etiqueta contenedora](#container-tags)
* se almacena en el repositorio debajo de una ruta base denominada [nodo raíz de taxonomía](#taxonomy-root-node)

### ID de etiqueta {#tagid}

TagID identifica una ruta que se resuelve en un nodo de etiqueta del repositorio.

Normalmente, TagID es un TagID abreviado que comienza con el espacio de nombres o puede ser un TagID absoluto que comienza con el [nodo raíz de taxonomía](#taxonomy-root-node).

Cuando el contenido está etiquetado, si aún no existe, la variable ` [cq:tags](#tagged-content-cq-tags-property)` se agrega al nodo de contenido y el TagID se agrega al valor de matriz String de la propiedad.

TagID consiste en un [namespace](#tag-namespace) seguido del TagID local. [Etiquetas de contenedor](#container-tags) tienen subetiquetas que representan un orden jerárquico en la taxonomía. Las subetiquetas se pueden usar para hacer referencia a las etiquetas del mismo modo que cualquier TagID local. Por ejemplo, se permite etiquetar contenido con &quot;fruta&quot;, aunque sea una etiqueta contenedora con subetiquetas, como &quot;fruta/manzana&quot; y &quot;fruta/plátano&quot;.

### Nodo raíz de taxonomía {#taxonomy-root-node}

El nodo raíz de taxonomía es la ruta base para todas las etiquetas del repositorio. El nodo raíz de taxonomía debe *not* ser un nodo de tipo `  cq   :Tag`.

En AEM, la ruta base es `/content/  cq   :tags` y el nodo raíz es del tipo `  cq   :Folder`.

### Área de nombres de la etiqueta {#tag-namespace}

Los espacios de nombres permiten agrupar las cosas. El caso de uso más típico es tener un espacio de nombres por sitio (web) (por ejemplo, público, interno y portal) o por aplicación mayor (por ejemplo, WCM, Assets, Communities), pero los espacios de nombres se pueden utilizar para otras necesidades. Los espacios de nombres se utilizan en la interfaz de usuario para mostrar solo el subconjunto de etiquetas (es decir, etiquetas de un determinado espacio de nombres) que se aplica al contenido actual.

El espacio de nombres de la etiqueta es el primer nivel del subárbol de taxonomía, que es el nodo inmediatamente inferior al [nodo raíz de taxonomía](#taxonomy-root-node). Un área de nombres es un nodo de tipo `cq:Tag` cuyo padre no es un `cq:Tag`tipo de nodo.

Todas las etiquetas tienen un espacio de nombres. Si no se especifica ningún espacio de nombres, la etiqueta se asigna al espacio de nombres predeterminado, que es TagID `default` (El título es `Standard Tags),`que es `/content/cq:tags/default.`

### Etiquetas de contenedor {#container-tags}

Una etiqueta contenedora es un nodo de tipo `cq:Tag` que contenga cualquier número y tipo de nodos secundarios, lo que permite mejorar el modelo de etiquetas con metadatos personalizados.

Además, las etiquetas de contenedor (o superetiquetas) de una taxonomía sirven como subsuma de todas las subetiquetas: por ejemplo, el contenido etiquetado con fruta/manzana también se considera etiquetado con fruta, es decir, la búsqueda de contenido que se acaba de etiquetar con fruta también encontraría el contenido etiquetado con fruta/manzana.

### Resolución de TagID {#resolving-tagids}

Si el ID de etiqueta contiene dos puntos &quot;:&quot;, los dos puntos separan el área de nombres de la etiqueta o subtaxonomía, que después se separan con barras normales &quot;/&quot;. Si el ID de etiqueta no tiene dos puntos, se da a entender el espacio de nombres predeterminado.

La ubicación estándar y única de las etiquetas es debajo de /content/cq:tags.

Las etiquetas que hacen referencia a rutas o rutas no existentes que no apuntan a un nodo cq:Tag se consideran no válidas y se ignoran.

La siguiente tabla muestra algunos TagIDs de muestra, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio:

La siguiente tabla muestra algunos TagIDs de muestra, sus elementos y cómo TagID se resuelve en una ruta absoluta en el repositorio :

<table>
 <tbody>
  <tr>
   <td><strong>ID de etiqueta<br /> </strong></td>
   <td><strong>Espacio de nombres</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Etiquetas de contenedores</strong></td>
   <td><strong>Etiqueta de hoja</strong></td>
   <td><strong>Repositorio<br /> Ruta absoluta de la etiqueta</strong></td>
  </tr>
  <tr>
   <td>dam:fruta/manzana/braeburn</td>
   <td>dam</td>
   <td>frutal/manzana/pechuga</td>
   <td>fruta, manzana</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/frutal/apple/braeburn</td>
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
   <td>categoría</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localización del título de la etiqueta {#localization-of-tag-title}

Cuando la etiqueta incluye la cadena de título opcional ( `jcr:title`) es posible localizar el título para mostrar añadiendo la propiedad `jcr:title.<locale>`.

Para obtener más información, consulte

* [Etiquetas en diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages) - que describe el uso de las API
* [Administración de etiquetas en diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) - que describe el uso de la consola Tagging

### Control de acceso {#access-control}

Las etiquetas existen como nodos en el repositorio en el [nodo raíz de taxonomía](#taxonomy-root-node). Permitir o denegar a autores y visitantes del sitio la creación de etiquetas en un espacio de nombres determinado se puede lograr estableciendo las ACL adecuadas en el repositorio.

Además, negar permisos de lectura para ciertas etiquetas o áreas de nombres controlará la capacidad de aplicar etiquetas a contenido específico.

Una práctica habitual incluye:

* Permitiendo el `tag-administrators` acceso de escritura de grupo/función a todas las áreas de nombres (añadir/modificar en `/content/cq:tags`). Este grupo viene con AEM listo para usar.

* Permitir que los usuarios/autores lean acceso a todas las áreas de nombres que deberían ser legibles para ellos (en su mayoría, todas).
* Permitir que los usuarios/autores escriban acceso a las áreas de nombres en las que los usuarios/autores deben definir las etiquetas libremente (add_node en `/content/cq:tags/some_namespace`)

## Contenido etiquetable : cq:Mezcla etiquetable {#taggable-content-cq-taggable-mixin}

Para que los desarrolladores de aplicaciones puedan adjuntar etiquetas a un tipo de contenido, el registro del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) debe incluir el `cq:Taggable` mezcla o `cq:OwnerTaggable` mixin.

La variable `cq:OwnerTaggable` mixin, que hereda de `cq:Taggable`, está pensado para indicar que el contenido puede ser clasificado por el propietario/autor. En AEM, solo es un atributo de la variable `cq:PageContent` nodo . La variable `cq:OwnerTaggable` la mezcla no es necesaria para el marco de etiquetado.

>[!NOTE]
>
>Se recomienda habilitar únicamente las etiquetas en el nodo de nivel superior de un elemento de contenido agregado (o en su nodo jcr:content). Algunos ejemplos son:
>
>* páginas ( `cq:Page`) donde la variable `jcr:content`el nodo es de tipo `cq:PageContent` que incluye el `cq:Taggable` mixin.
>
>* assets ( `cq:Asset`) donde la variable `jcr:content/metadata` el nodo siempre tiene la variable `cq:Taggable` mixin.

>


### Anotación de tipo de nodo (CND) {#node-type-notation-cnd}

Las definiciones de Tipo de nodo existen en el repositorio como archivos CND. La notación CND se define como parte de la documentación de JCR [here](https://jackrabbit.apache.org/node-type-notation.html).

Las definiciones esenciales para los tipos de nodo incluidos en AEM son las siguientes:

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

La variable `cq:tags` es una matriz de cadenas que se utiliza para almacenar una o más TagID cuando los autores o los visitantes del sitio las aplican al contenido. La propiedad solo tiene significado cuando se agrega a un nodo que se define con la variable `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Para aprovechar AEM funcionalidad de etiquetado, las aplicaciones desarrolladas a medida no deben definir propiedades de etiqueta que no sean `cq:tags`.

## Mover y combinar etiquetas {#moving-and-merging-tags}

A continuación, se muestra una descripción de los efectos que se producen en el repositorio al mover o combinar etiquetas utilizando la variable [Consola de etiquetado](/help/sites-administering/tags.md):

* Cuando una etiqueta A se mueve o combina en la etiqueta B debajo de `/content/cq:tags`:

   * La etiqueta A no se elimina y obtiene un `cq:movedTo` propiedad.
   * la etiqueta B se crea (en caso de un movimiento) y obtiene un `cq:backlinks` propiedad.

* `cq:movedTo` señala a la etiqueta B. Esta propiedad significa que la etiqueta A se ha movido o combinado en la etiqueta B. Al mover la etiqueta B se actualizará esta propiedad en consecuencia. Por lo tanto, la etiqueta A está oculta y solo se mantiene en el repositorio para resolver los ID de etiqueta en los nodos de contenido que apuntan a la etiqueta A. El recolector de residuos de etiquetas elimina etiquetas como la etiqueta A una vez que no más nodos de contenido les señalan.
Un valor especial para la variable `cq:movedTo` la propiedad es `nirvana`: se aplica cuando se elimina la etiqueta, pero no se puede eliminar del repositorio porque hay subetiquetas con un `cq:movedTo` eso debe mantenerse.

   >[!NOTE]
   >
   >La variable `cq:movedTo` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* `cq:backlinks` mantiene las referencias en la otra dirección, es decir, mantiene una lista de todas las etiquetas que se han movido a la etiqueta B o que se han combinado con ella. Esto es necesario principalmente para mantener `cq:movedTo`propiedades actualizadas cuando la etiqueta B también se mueve, combina o elimina, o cuando la etiqueta B está activada, en cuyo caso todas sus etiquetas backlinks también deben activarse.

   >[!NOTE]
   >
   >La variable `cq:backlinks` solo se agrega a la etiqueta movida o combinada si se cumple cualquiera de estas condiciones:
   >
   > 1. La etiqueta se utiliza en el contenido (es decir, tiene una referencia) O >
   > 1. La etiqueta tiene elementos secundarios que ya se han movido.


* Leer un `cq:tags` la propiedad de un nodo de contenido implica la siguiente resolución:

   1. Si no hay coincidencia en `/content/cq:tags`, no devuelve ninguna etiqueta.
   1. Si la etiqueta tiene un `cq:movedTo` conjunto de propiedades, se sigue el ID de etiqueta al que se hace referencia.
Este paso se repite siempre y cuando la etiqueta siguiente tenga una `cq:movedTo` propiedad.

   1. Si la etiqueta siguiente no tiene un valor `cq:movedTo` , se lee la etiqueta .

* Para publicar el cambio cuando una etiqueta se ha movido o combinado, la variable `cq:Tag` y todos sus vínculos secundarios deben replicarse: esto se realiza automáticamente cuando la etiqueta está activada en la consola de administración de etiquetas.

* Actualizaciones posteriores en el informe `cq:tags` limpie automáticamente las referencias &quot;antiguas&quot;. Esto se activa porque la resolución de una etiqueta movida a través de la API devuelve la etiqueta de destino, proporcionando así el ID de etiqueta de destino.

>[!NOTE]
>
>El movimiento de etiquetas es diferente de la migración de etiquetas.

## Migración de etiquetas {#tags-migration}

Las etiquetas de Experience Manager 6.4 y posteriores se almacenan en `/content/cq:tags`, que anteriormente se almacenaban en `/etc/tags`. Sin embargo, en los casos en que Adobe Experience Manager se haya actualizado desde la versión anterior, las etiquetas siguen presentes en la ubicación antigua `/etc/tags`. En sistemas actualizados, es necesario migrar las etiquetas en `/content/cq:tags`.

>[!NOTE]
>
>En la página Propiedades de página de etiquetas , se recomienda utilizar el ID de etiqueta (`geometrixx-outdoors:activity/biking`) en lugar de codificar la ruta de base de etiquetas (por ejemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para enumerar etiquetas, `com.day.cq.tagging.servlets.TagListServlet` se puede usar.

>[!NOTE]
>
>Se recomienda utilizar la API del administrador de etiquetas como recurso.

### Si la instancia de AEM actualizada es compatible con la API de TagManager {#upgraded-instance-support-tagmanager-api}

1. Al principio del componente, la API de TagManager detecta si se trata de una instancia de AEM actualizada. En el sistema actualizado, las etiquetas se almacenan en `/etc/tags`.

1. A continuación, la API de TagManager se ejecuta en modo de compatibilidad con versiones anteriores, lo que significa que la API utiliza `/etc/tags` como ruta base. Si no es así, utiliza una nueva ubicación `/content/cq:tags`.

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

La secuencia de comandos recupera todas las etiquetas que tienen `/etc/tags` en el valor de `cq:movedTo/cq:backLinks` propiedad. A continuación, se repite a través del conjunto de resultados recuperados y resuelve el `cq:movedTo` y `cq:backlinks` valores de propiedad a `/content/cq:tags` rutas (en caso de que `/etc/tags` se detecta en el valor ).

### Si la instancia de AEM actualizada se ejecuta en la IU clásica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>La IU clásica no es compatible con el tiempo de inactividad cero y no admite la nueva ruta de base de etiquetas. Si desea utilizar la IU clásica que `/etc/tags` debe crearse seguido de `cq-tagging` reiniciar el componente.

En el caso de instancias de AEM actualizadas compatibles con la API de TagManager y que se ejecuten en la IU clásica:

1. Una vez hace referencia a la ruta de base de etiquetas antigua `/etc/tags` se reemplazan utilizando tagId o una nueva ubicación de etiqueta `/content/cq:tags`, puede migrar etiquetas a la nueva ubicación `/content/cq:tags` en CRX seguido del reinicio de componentes.

1. Después de migrar las etiquetas a la nueva ubicación, ejecute el script mencionado anteriormente.
