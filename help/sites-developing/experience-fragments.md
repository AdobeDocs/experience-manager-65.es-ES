---
title: Fragmentos de experiencias
seo-title: Fragmentos de experiencias
description: Obtenga información sobre cómo personalizar fragmentos de experiencias.
seo-description: Obtenga información sobre cómo personalizar fragmentos de experiencias.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b

---


# Fragmentos de experiencias{#experience-fragments}

## Conceptos básicos {#the-basics}

Un [fragmento de experiencias](/help/sites-authoring/experience-fragments.md) es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas.

Un patrón de fragmentos de experiencia y/o una variante utiliza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como no hay `/libs/cq/experience-fragments/components/xfpage/xfpage.html` se vuelve a

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Representación HTML sin formato {#the-plain-html-rendition}

Con el `.plain.` selector de la URL, puede acceder a la representación HTML sin formato.

Está disponible desde el navegador, pero su principal objetivo es permitir que otras aplicaciones (por ejemplo, aplicaciones web de terceros, implementaciones móviles personalizadas) accedan al contenido del fragmento de experiencias directamente, utilizando solo la URL.

La representación HTML sin formato agrega el protocolo, el host y la ruta de contexto a las rutas que son:

* del tipo: `src`, `href`o `action`

* o finalizar con: `-src`o `-href`

Por ejemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Los vínculos siempre hacen referencia a la instancia de publicación. Están pensados para ser consumidos por terceros, por lo que el vínculo siempre se llamará desde la instancia de publicación, no desde el autor.

![xf-14](assets/xf-14.png)

El selector de representación sin formato utiliza un transformador en lugar de secuencias de comandos adicionales; el [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) se utiliza como transformador. Se configura en

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variaciones sociales {#social-variations}

Las variantes sociales se pueden publicar en los medios sociales (texto e imagen). En AEM, estas variantes sociales pueden contener componentes; por ejemplo, componentes de texto, componentes de imagen.

La imagen y el texto de la publicación social se pueden tomar de cualquier tipo de recurso de imagen o de recurso de texto en cualquier nivel de profundidad (en el bloque de creación o en el contenedor de diseño).

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
>***Solo*** se admiten plantillas [](/help/sites-developing/page-templates-editable.md) editables para fragmentos de experiencia.

Al desarrollar una nueva plantilla para fragmentos de experiencia, puede seguir las prácticas estándar de una plantilla [](/help/sites-developing/page-templates-editable.md)editable.

Para crear una plantilla de fragmento de experiencia detectada por el asistente **Crear fragmento** de experiencia, debe seguir uno de estos conjuntos de reglas:

1. Ambas:

   1. El tipo de recurso de la plantilla (el nodo inicial) debe heredar de:
      `cq/experience-fragments/components/xfpage`

   1. Y el nombre de la plantilla debe comenzar por:
      `experience-fragments`
Esto permite a los usuarios crear fragmentos de experiencia en /content/experience-fragments, ya que la `cq:allowedTemplates` propiedad de esta carpeta incluye todas las plantillas con nombres que comienzan por `experience-fragment`. Los clientes pueden actualizar esta propiedad para incluir su propio esquema de nombres o ubicaciones de plantillas.

1. [Las plantillas](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) permitidas se pueden configurar en la consola Fragmentos de experiencia.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiencias {#components-for-experience-fragments}

[El desarrollo de componentes](/help/sites-developing/components.md) para su uso con o en fragmentos de experiencia sigue las prácticas estándar.

La única configuración adicional es asegurarse de que los componentes están [permitidos en la plantilla, esto se logra con la Política](/help/sites-developing/page-templates-editable.md#content-policies)de contenido.

## El proveedor de la reescritura de los vínculos de los fragmentos de experiencia: HTML {#the-experience-fragment-link-rewriter-provider-html}

En AEM puede crear fragmentos de experiencia. Un fragmento de experiencias:

* consiste en un grupo de componentes junto con una presentación,
* puede existir independientemente de una página de AEM.

Uno de los casos de uso de estos grupos es para incrustar contenido en puntos de contacto de terceros, como Adobe Target.

### Reescritura de vínculos predeterminada {#default-link-rewriting}

Con la función [Exportar a Target](/help/sites-administering/experience-fragments-target.md) , puede:

* crear un fragmento de experiencia,
* añadir componentes a la misma,
* y, a continuación, expórtela como una oferta de Adobe Target, en formato HTML o JSON.

Esta función se puede [activar en una instancia de autor de AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Requiere una configuración válida de Adobe Target y configuraciones para el Externalizador de vínculos.

El Externalizador de vínculos se utiliza para determinar las direcciones URL correctas necesarias al crear la versión HTML de la oferta de Target, que se envía posteriormente a Adobe Target. Esto es necesario, ya que Adobe Target requiere que todos los vínculos dentro de la oferta HTML de Target puedan ser de acceso público; esto significa que los recursos a los que hacen referencia los vínculos y el propio fragmento de experiencias deben publicarse antes de poder utilizarse.

De forma predeterminada, al crear una oferta HTML de Target, se envía una solicitud a un selector de Sling personalizado en AEM. Se llama a este selector `.nocloudconfigs.html`. Como su nombre lo indica, crea una representación HTML sin formato de un fragmento de experiencias, pero no incluye configuraciones de nube (que sería información superflua).

Después de generar la página HTML, la canalización de Sling Rewriter realiza modificaciones en el resultado:

1. Los elementos `html`, `head`y `body` se reemplazan por `div` elementos. Los elementos `meta`, `noscript` y `title` se eliminan (son elementos secundarios del `head` elemento original y no se tienen en cuenta cuando se reemplaza por el `div` elemento).

   Esto se realiza para garantizar que la oferta de HTML Target se pueda incluir en las actividades de Target.

1. AEM modifica los vínculos internos presentes en el HTML para que señalen a un recurso publicado.

   Para determinar los vínculos que se van a modificar, AEM sigue este patrón para los atributos de los elementos HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src, etc.)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href`, etc.)
   >[!NOTE]
   >
   >En la mayoría de los casos, los vínculos internos en el HTML son vínculos relativos, pero puede haber casos en los que los componentes personalizados proporcionen direcciones URL completas en el HTML. De forma predeterminada, AEM omite estas direcciones URL completas y no realiza ninguna modificación.

   Los vínculos de estos atributos se ejecutan a través del Externalizador de vínculos de AEM `publishLink()` para recrear la dirección URL como si estuviera en una instancia publicada y, como tal, disponible públicamente.

Al utilizar una implementación lista para usar, el proceso descrito anteriormente debería ser suficiente para generar la oferta de Target a partir del fragmento de experiencias y luego exportarla a Adobe Target. Sin embargo, hay algunos casos de uso que no se tienen en cuenta en este proceso; entre ellos se incluyen:

* Asignación de Sling disponible solo en la instancia de publicación
* Redirecciones de Dispatcher

En estos casos de uso, AEM proporciona la interfaz del proveedor de reescritores de vínculos.

### Vincular interfaz de proveedor de reescritores {#link-rewriter-provider-interface}

>[!NOTE]
>
>Esta interfaz se introdujo en [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Para casos más complicados, no cubiertos por la [opción predeterminada](#default-link-rewriting), AEM ofrece la interfaz del proveedor de reescritores de vínculos. Se trata de una `ConsumerType` interfaz que puede implementar en los paquetes, como un servicio. Omite las modificaciones que AEM realiza en los vínculos internos de una oferta HTML tal como se representa desde un fragmento de experiencia. Esta interfaz le permite personalizar el proceso de reescritura de los vínculos HTML internos para adaptarlos a sus necesidades comerciales.

Algunos ejemplos de casos de uso para implementar esta interfaz como servicio son:

* Las asignaciones de desplazamiento están activadas en las instancias de publicación, pero no en la instancia de autor
* Un despachante o tecnología similar se utiliza para redireccionar las direcciones URL internamente
* Existen `sling:alias mechanisms` recursos

>[!NOTE]
>
>Esta interfaz solo procesa los vínculos HTML internos desde la oferta de Target generada.

La interfaz del proveedor de reescritores de vínculos ( `ExperienceFragmentLinkRewriterProvider`) es la siguiente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Cómo utilizar la interfaz del proveedor de reescritores de vínculos {#how-to-use-the-link-rewriter-provider-interface}

Para utilizar la interfaz, primero debe crear un paquete que contenga un nuevo componente de servicio que implemente la interfaz del proveedor de reescritores de vínculos.

Este servicio se utilizará para realizar la reescritura de la exportación de fragmentos de experiencia a Target a fin de tener acceso a los distintos vínculos.

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

#### mustRewrite {#shouldrewrite}

Debe indicar al sistema si necesita reescribir los vínculos cuando se realiza una llamada para Exportar a Target con una determinada variación de fragmento de experiencia. Para ello, implemente el método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por ejemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Este método recibe, como parámetro, la variación del fragmento de experiencia que el sistema Exportar a Target está reescribiendo.

En el ejemplo anterior, nos gustaría reescribir:

* vínculos presentes en `src`

* `href` sólo atributos

* para un fragmento de experiencia específico:
   `/content/experience-fragment/master`

Cualquier otro fragmento de experiencia que pase por el sistema Exportar a Target se ignora y no se ve afectado por los cambios implementados en este servicio.

#### rewriteLink {#rewritelink}

Para la variación del fragmento de experiencias que se ve afectada por el proceso de reescritura, el servicio podrá administrar la reescritura del vínculo. Cada vez que se encuentra un vínculo en el HTML interno, se invoca el siguiente método:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, el método recibe los parámetros:

* `link`
La `String` representación del vínculo que se está procesando actualmente. Generalmente es una URL relativa que apunta al recurso en la instancia de autor.

* `tag`
Nombre del elemento HTML que se está procesando en este momento.

* `attribute`
El nombre exacto del atributo.

Si, por ejemplo, el sistema Exportar a Target está procesando este elemento en este momento, puede definirlo `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La llamada al `rewriteLink()` método se realiza utilizando estos parámetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Al crear el servicio, puede tomar decisiones en función de la entrada dada y, a continuación, volver a escribir el vínculo en consecuencia.

Para nuestro ejemplo, nos gustaría quitar la parte `/etc.clientlibs` de la dirección URL y agregar el dominio externo apropiado. Para simplificar las cosas, consideraremos que tenemos acceso a un Resoltor de recursos para su servicio, como en `rewriteLinkExample2`:

>[!NOTE]
>
>Para obtener más información sobre cómo obtener una resolución de recursos a través de un usuario de servicios, consulte Usuarios [de servicios en AEM](/help/sites-administering/security-service-users.md).

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
>Si se devuelve el método anterior `null`, el sistema Exportar a Target dejará el vínculo tal como está, un vínculo relativo a un recurso.

#### Prioridades - getPriority {#priorities-getpriority}

No es raro necesitar varios servicios para atender diferentes tipos de fragmentos de experiencia, o incluso para tener un servicio genérico que gestione la externalización y la asignación de todos los fragmentos de experiencia. En estos casos, surgen conflictos sobre qué servicio utilizar, por lo que AEM ofrece la posibilidad de definir **prioridades** para distintos servicios. Las prioridades se especifican mediante el método:

* `getPriority()`

Este método permite el uso de varios servicios en los que el `shouldRewrite()` método devuelve true para el mismo fragmento de experiencia. El servicio que devuelve el número más alto de su `getPriority()`método es el servicio que gestiona la variación del fragmento de experiencias.

Por ejemplo, puede tener un `GenericLinkRewriterProvider` que gestione la asignación básica para todos los fragmentos de experiencia y cuando el `shouldRewrite()` método se devuelva `true` para todas las variaciones de fragmento de experiencia. Para varios fragmentos de experiencia específicos, es posible que desee una gestión especial, por lo que en este caso, puede proporcionar un `SpecificLinkRewriterProvider` método para el que el `shouldRewrite()` método devuelve true solo para algunas variaciones de fragmento de experiencia. Para asegurarse de que `SpecificLinkRewriterProvider` se elige gestionar esas variaciones de fragmento de experiencia, debe devolver en su `getPriority()` método un número mayor que `GenericLinkRewriterProvider.`
