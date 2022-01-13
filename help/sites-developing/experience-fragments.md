---
title: Fragmentos de experiencias
seo-title: Experience Fragments
description: Obtenga información sobre la personalización de fragmentos de experiencias.
seo-description: Learn about customizing Experience Fragments.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 3%

---

# Fragmentos de experiencias{#experience-fragments}

## Conceptos básicos {#the-basics}

Un [fragmento de experiencias](/help/sites-authoring/experience-fragments.md) es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas.

Un patrón de fragmentos de experiencias y/o una variante utilizan:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como no hay `/libs/cq/experience-fragments/components/xfpage/xfpage.html` vuelve a

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Representación HTML sin formato {#the-plain-html-rendition}

Al usar la variable `.plain.` en la URL, puede acceder a la representación del HTML sin formato.

Está disponible desde el explorador, pero su principal propósito es permitir que otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) accedan al contenido del fragmento de experiencia directamente, únicamente mediante la URL.

La representación del HTML sin formato agrega el protocolo, el host y la ruta de contexto a las rutas que son:

* del tipo: `src`, `href`o `action`

* o finalizar con: `-src`o `-href`

Por ejemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Los vínculos siempre hacen referencia a la instancia de publicación. Están pensados para ser consumidos por terceros, por lo que siempre se llama al vínculo desde la instancia de publicación, no desde el autor.

![xf-14](assets/xf-14.png)

El selector de representaciones simples utiliza un transformador en lugar de secuencias de comandos adicionales; el [Reescritura de Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) se utiliza como transformador. Esto se configura en

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variaciones sociales {#social-variations}

Las variantes sociales se pueden publicar en medios sociales (texto e imagen). En AEM estas variantes sociales pueden contener componentes; por ejemplo, componentes de texto o componentes de imagen.

La imagen y el texto del anuncio social se pueden tomar de cualquier tipo de recurso de imagen o tipo de recurso de texto con cualquier nivel de profundidad (en el bloque de creación o en el contenedor de diseño).

Las variaciones sociales también permiten componentes básicos y los tienen en cuenta al realizar acciones sociales (en el entorno de publicación).

Para publicar el texto y la imagen correctos en la red de medios sociales, algunas convenciones deben respetarse si está desarrollando sus propios componentes personalizados.

Para ello, se deben utilizar las siguientes propiedades:

* Para extraer la imagen

   * `fileReference`
   * `fileName`

* Para extraer el texto

   * `text`

Los componentes que no utilicen esta convención no se tendrán en cuenta.

## Plantillas para fragmentos de experiencias {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo*** [plantillas editables](/help/sites-developing/page-templates-editable.md) son compatibles con los fragmentos de experiencias.

Al desarrollar una plantilla nueva para fragmentos de experiencias, puede seguir las prácticas estándar de un [plantilla editable](/help/sites-developing/page-templates-editable.md).

Para crear una plantilla de fragmento de experiencia que detecte el **Crear fragmento de experiencia** , debe seguir uno de estos conjuntos de reglas:

1. Ambas:

   1. El tipo de recurso de la plantilla (el nodo inicial) debe heredar de:
      `cq/experience-fragments/components/xfpage`

   1. Y el nombre de la plantilla debe comenzar por:
      `experience-fragments`
Esto permite a los usuarios crear fragmentos de experiencia en /content/experience-fragments como 
`cq:allowedTemplates` la propiedad de esta carpeta incluye todas las plantillas que tienen nombres que comienzan por `experience-fragment`. Los clientes pueden actualizar esta propiedad para incluir su propio esquema de nombres o ubicaciones de plantillas.

1. [Plantillas permitidas](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) se puede configurar en la consola Fragmentos de experiencias .

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiencias {#components-for-experience-fragments}

[Desarrollo de componentes](/help/sites-developing/components.md) para su uso con o en fragmentos de experiencias, siga las prácticas estándar.

La única configuración adicional es garantizar que los componentes sean [permitido en la plantilla, esto se logra con la Política de contenido](/help/sites-developing/page-templates-editable.md#content-policies).

## El proveedor de la reescritura de los vínculos de los fragmentos de experiencia: HTML {#the-experience-fragment-link-rewriter-provider-html}

En AEM tiene la posibilidad de crear fragmentos de experiencias. Un fragmento de experiencia:

* consta de un grupo de componentes junto con una presentación,
* puede existir independientemente de una página AEM.

Uno de los casos de uso de estos grupos es la incrustación de contenido en puntos de contacto de terceros, como Adobe Target.

### Reescribir vínculo predeterminado {#default-link-rewriting}

Al usar la variable [Exportar a Target](/help/sites-administering/experience-fragments-target.md) , puede:

* crear un fragmento de experiencia,
* añadir componentes a él,
* y luego exportarlo como una oferta de Adobe Target, ya sea en formato de HTML o JSON.

Esta función puede [habilitado en una instancia de autor de AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Requiere una configuración de Adobe Target válida y configuraciones para el externalizador de vínculos.

El externalizador de vínculos se utiliza para determinar las direcciones URL correctas necesarias al crear la versión de HTML de la oferta de Target, que se envía posteriormente a Adobe Target. Esto es necesario, ya que Adobe Target requiere que todos los vínculos dentro de la oferta de HTML de Target puedan ser accesibles al público; esto significa que todos los recursos a los que hacen referencia los vínculos y el propio fragmento de experiencia deben publicarse antes de poder utilizarse.

De forma predeterminada, al crear una oferta de HTML de Target, se envía una solicitud a un selector de Sling personalizado en AEM. Se llama a este selector `.nocloudconfigs.html`. Como su nombre lo indica, crea una renderización HTML sencilla de un fragmento de experiencia, pero no incluye configuraciones de nube (que sería información superflua).

Después de generar la página HTML, la canalización de Sling Rewriter realiza modificaciones en la salida:

1. La variable `html`, `head`y `body` los elementos se sustituyen por `div` elementos. La variable `meta`, `noscript` y `title` se eliminan (son elementos secundarios del original) `head` y no se tienen en cuenta cuando se reemplaza por el `div` elemento).

   Esto se hace para garantizar que la oferta de Target de HTML se pueda incluir en las actividades de Target.

1. AEM modifica los vínculos internos presentes en el HTML, de modo que apunten a un recurso publicado.

   Para determinar los vínculos que se van a modificar, AEM sigue este patrón para los atributos de los elementos del HTML:

   1. `src` attributes
   1. `href` attributes
   1. `*-src` atributos (como data-src, custom-src, etc.)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href`, etc.

   >[!NOTE]
   >
   >En la mayoría de los casos, los vínculos internos en el HTML son vínculos relativos, pero puede haber casos en que los componentes personalizados proporcionen direcciones URL completas en el HTML. De forma predeterminada, AEM ignora estas direcciones URL completas y no realiza ninguna modificación.

   Los vínculos de estos atributos se ejecutan a través del AEM Link Externalizer `publishLink()` para recrear la URL como si estuviera en una instancia publicada, y como tal, esté disponible públicamente.

Cuando se utiliza una implementación predeterminada, el proceso descrito anteriormente debe ser suficiente para generar la oferta de destino desde el fragmento de experiencia y luego exportarla a Adobe Target. Sin embargo, hay algunos casos de uso que no se tienen en cuenta en este proceso; entre ellos se incluyen:

* Asignación de Sling disponible solo en la instancia de publicación
* Redirecciones de Dispatcher

Para estos casos de uso AEM proporciona la interfaz del proveedor de reescritura de vínculos.

### Interfaz de proveedor de reescritura de vínculos {#link-rewriter-provider-interface}

>[!NOTE]
>
>Esta interfaz se introdujo en [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/previous/6.5.1.md).

Para casos más complicados, no cubiertos por la variable [default](#default-link-rewriting), AEM ofrece la interfaz de proveedor de reescritura de vínculos. Esto es un `ConsumerType` que puede implementar en sus paquetes, como un servicio. Evita las modificaciones AEM realiza en los vínculos internos de una oferta de HTML representada desde un fragmento de experiencia. Esta interfaz le permite personalizar el proceso de reescritura de vínculos de HTML internos para adaptarlos a sus necesidades comerciales.

Algunos ejemplos de casos de uso para implementar esta interfaz como servicio son:

* Las asignaciones de Sling están habilitadas en las instancias de publicación, pero no en la instancia de autor
* Dispatcher o tecnología similar se usan para redireccionar direcciones URL internamente
* Hay `sling:alias mechanisms` en su lugar para los recursos

>[!NOTE]
>
>Esta interfaz solo procesa los vínculos de HTML internos de la oferta de Target generada.

Interfaz del proveedor de reescritura de vínculos ( `ExperienceFragmentLinkRewriterProvider`) es el siguiente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Cómo utilizar la interfaz del proveedor de reescritura de vínculos {#how-to-use-the-link-rewriter-provider-interface}

Para utilizar la interfaz primero debe crear un paquete que contenga un nuevo componente de servicio que implemente la interfaz del proveedor de reescritura de vínculos.

Este servicio se utilizará para conectar con la reescritura de la exportación de fragmentos de experiencias a Target para tener acceso a los distintos vínculos.

Por ejemplo, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Para que el servicio funcione, ahora hay tres métodos que deben implementarse dentro del servicio:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Debe indicar al sistema si necesita reescribir los vínculos cuando se realiza una llamada para Exportar a Target en una variación de fragmento de experiencia determinada. Para ello, implemente el método :

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por ejemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Este método recibe, como parámetro, la variación del fragmento de experiencia que el sistema Exportar a destino está reescribiendo actualmente.

En el ejemplo anterior, nos gustaría reescribir:

* vínculos presentes en `src`

* `href` solo atributos

* para un fragmento de experiencia específico:
   `/content/experience-fragment/master`

Los demás fragmentos de experiencias que pasan por el sistema Exportar a Target se ignoran y no se ven afectados por los cambios implementados en este servicio.

#### rewriteLink {#rewritelink}

Para la variación del fragmento de experiencia afectada por el proceso de reescritura, este deja que el servicio gestione la reescritura de vínculos. Cada vez que se encuentra un vínculo en el HTML interno, se invoca el siguiente método:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, el método recibe los parámetros:

* `link`
El 
`String` representación del vínculo que se está procesando actualmente. Normalmente es una URL relativa que señala al recurso en la instancia de autor.

* `tag`
Nombre del elemento de HTML que se está procesando actualmente.

* `attribute`
El nombre exacto del atributo.

Si, por ejemplo, el sistema Exportar a destino está procesando actualmente este elemento, puede definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La llamada a la función `rewriteLink()` se realiza utilizando estos parámetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Al crear el servicio, puede tomar decisiones basadas en la entrada dada y luego reescribir el vínculo en consecuencia.

Para nuestro ejemplo, nos gustaría quitar la variable `/etc.clientlibs` parte de la dirección URL y añada el dominio externo correspondiente. Para que las cosas sean simples, consideraremos que tenemos acceso a Resource Resolver para su servicio, como en `rewriteLinkExample2`:

>[!NOTE]
>
>Para obtener más información sobre cómo obtener una resolución de recursos a través de un usuario de servicio, consulte [Usuarios de servicio en AEM](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Si el método anterior devuelve `null`y, a continuación, el sistema Exportar a Target dejará el vínculo tal cual, un vínculo relativo a un recurso.

#### Prioridades - getPriority {#priorities-getpriority}

No es inusual que se necesiten varios servicios para cubrir diferentes tipos de fragmentos de experiencias, o incluso que tengan un servicio genérico que gestione la externalización y la asignación para todos los fragmentos de experiencias. En estos casos, surgen conflictos sobre qué servicio utilizar, por lo que AEM permite definir **Prioridades** para diferentes servicios. Las prioridades se especifican mediante el método :

* `getPriority()`

Este método permite el uso de varios servicios donde la variable `shouldRewrite()` devuelve el valor &quot;True&quot; para el mismo fragmento de experiencia. El servicio que devuelve el número más alto de su `getPriority()`es el servicio que gestiona la variación del fragmento de experiencia.

Por ejemplo, puede tener un `GenericLinkRewriterProvider` que gestiona la asignación básica para todos los fragmentos de experiencias y cuando la variable `shouldRewrite()` devuelve el método `true` para todas las variaciones de fragmento de experiencia. Para varios fragmentos de experiencias específicos, es posible que desee un tratamiento especial, por lo que en este caso puede proporcionar un `SpecificLinkRewriterProvider` para los que `shouldRewrite()` devuelve true solo para algunas variaciones de fragmento de experiencia. Para asegurarse de que `SpecificLinkRewriterProvider` se elige para gestionar esas variaciones de fragmento de experiencia, debe devolver en su `getPriority()` método un número mayor que `GenericLinkRewriterProvider.`
