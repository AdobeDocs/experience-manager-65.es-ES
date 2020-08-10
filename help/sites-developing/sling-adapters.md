---
title: Usar los adaptadores de Sling
seo-title: Usar los adaptadores de Sling
description: Sling oferta un patrón de adaptador para traducir convenientemente objetos que implementan la interfaz adaptable
seo-description: Sling oferta un patrón de adaptador para traducir convenientemente objetos que implementan la interfaz adaptable
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 36cc5ca0de9ae2933a0d7585a00f26cc984d24db
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 1%

---


# Usar los adaptadores de Sling{#using-sling-adapters}

[Sling](https://sling.apache.org) oferta un patrón [Adapter](https://sling.apache.org/site/adapters.html) para traducir convenientemente objetos que implementan la interfaz [Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) . Esta interfaz proporciona un método [adaptableTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) genérico que traducirá el objeto al tipo de clase que se pasa como argumento.

Por ejemplo, para traducir un objeto Resource al objeto Node correspondiente, simplemente puede hacer lo siguiente:

```java
Node node = resource.adaptTo(Node.class);
```

## Use Cases {#use-cases}

Existen los siguientes casos de uso:

* Obtenga objetos específicos de la implementación.

   Por ejemplo, una implementación basada en JCR de la [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) interfaz genérica proporciona acceso al JCR subyacente [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creación de accesos directos de objetos que requieren que se pasen objetos de contexto internos.

   Por ejemplo, la aplicación basada en JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) contiene una referencia al [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)de la solicitud, que a su vez es necesaria para muchos objetos que funcionarán en función de esa sesión de solicitud, como el [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Acceso directo a servicios.

   Un caso raro - `sling.getService()` también es simple.

### Valor devuelto nulo {#null-return-value}

`adaptTo()` puede devolver null.

Esto se debe a varios motivos, entre ellos:

* la implementación no admite el tipo de destinatario
* no está activo un generador de adaptador que maneje este caso (p. ej. debido a que faltan referencias de servicio)
* error en la condición interna
* el servicio no está disponible

Es importante que gestione el caso nulo con gracia. En el caso de las representaciones jsp, puede ser aceptable que el jsp falle si el resultado es un fragmento de contenido vacío.

### Almacenamiento en caché {#caching}

Para mejorar el rendimiento, las implementaciones pueden almacenar en caché el objeto devuelto por una `obj.adaptTo()` llamada. Si el `obj` valor es el mismo, el objeto devuelto es el mismo.

Este almacenamiento en caché se realiza en todos los casos `AdapterFactory` basados.

Sin embargo, no hay ninguna regla general: el objeto puede ser una instancia nueva o una existente. Esto significa que no se puede confiar en ninguno de los comportamientos. Por lo tanto, es importante, especialmente dentro `AdapterFactory`, que los objetos se reutilicen en este escenario.

### Cómo funciona {#how-it-works}

Existen varias maneras de `Adaptable.adaptTo()` implementarlas:

* Por el objeto mismo; implementar el propio método y asignar a determinados objetos.
* Por un [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que puede asignar objetos arbitrarios.

   Los objetos deben seguir implementando la `Adaptable` interfaz y extenderse [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (lo que pasa la `adaptTo` llamada a un administrador central de adaptadores).

   Esto permite enganchar el `adaptTo` mecanismo de las clases existentes, como `Resource`.

* Una combinación de ambos.

En el primer caso, los javadocs pueden indicar lo que `adaptTo-targets` es posible. Sin embargo, para subclases específicas como el recurso basado en JCR, a menudo esto no es posible. En este último caso, las implementaciones de `AdapterFactory` suelen formar parte de las clases privadas de un paquete y, por lo tanto, no están expuestas en una API de cliente ni están enumeradas en javadocs. En teoría, sería posible acceder a todas `AdapterFactory` las implementaciones desde el tiempo de ejecución del servicio [OSGi](/help/sites-deploying/configuring-osgi.md) y observar sus configuraciones &quot;adaptables&quot; (fuentes y destinatarios), pero no asignarlas entre sí. Al final, esto depende de la lógica interna, que debe ser documentada. De ahí esta referencia.

## Referencia {#reference}

### Sling {#sling}

[**El recurso **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Si se trata de un recurso basado en nodos JCR o una propiedad JCR que hace referencia a un nodo.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propiedad</a></td>
   <td>Si se trata de un recurso basado en propiedades JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Si se trata de un recurso basado en JCR (nodo o propiedad).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Asignar</a></td>
   <td>Devuelve un mapa de las propiedades, si se trata de un recurso basado en nodos JCR (u otro recurso que admita mapas de valores).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Devuelve un mapa práctico de las propiedades, si se trata de un recurso basado en nodos JCR (u otros mapas de valores de soporte de recursos). También se puede lograr (más simplemente) utilizando<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (gestiona mayúsculas y minúsculas nulas, etc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">HerenciaValueMap</a></td>
   <td>Extensión de <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite tener en cuenta la jerarquía de recursos al buscar propiedades.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiedValueMap</a></td>
   <td>Extensión de <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que permite modificar las propiedades de ese nodo.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Devuelve el contenido binario de un recurso de archivo (si se trata de un recurso basado en nodos JCR y el tipo de nodo es <code>nt:file</code> o <code>nt:resource</code>; si se trata de un recurso de paquete; contenido del archivo si se trata de un recurso del sistema de archivos) o los datos de un recurso de propiedad JCR binario.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Devuelve una URL al recurso (URL del repositorio de este nodo si se trata de un recurso basado en nodos JCR; jar URL del paquete si se trata de un recurso del paquete; URL de archivo si se trata de un recurso del sistema de archivos).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">Archivo</a></td>
   <td>Si se trata de un recurso del sistema de archivos.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Si este recurso es una secuencia de comandos (por ejemplo, un archivo jsp) para la que se ha registrado un motor de secuencias de comandos con sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Si este recurso es una secuencia de comandos (por ejemplo, un archivo jsp) para la que se ha registrado un motor de secuencias de comandos con sling o si se trata de un recurso servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">Cadena</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Largo</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">Doble</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendario</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">ValorString[]Boolean[][]Long[]Calendario[]Valor[]Value[]</a></td>
   <td>Devuelve los valores si se trata de un recurso basado en la propiedad JCR (y el valor se ajusta).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabledResource</a></td>
   <td>Si se trata de un recurso basado en nodos JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Si se trata de un recurso basado en nodos JCR y el nodo es <code>cq:Page</code> (o <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Si se trata de un recurso <code>cq:Component</code> de nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">Diseño</a></td>
   <td>Si es un nodo de diseño (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">Plantilla</a></td>
   <td>Si se trata de un recurso <code>cq:Template</code> de nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Modelo</a></td>
   <td>Si se trata de un recurso <code>cq:Template</code> de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">Recurso</a></td>
   <td>Si se trata de un recurso de nodo dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Representación</a></td>
   <td>Si se trata de una representación dam:Asset (nt:file en la carpeta de representación de un dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Etiqueta</a></td>
   <td>Si se trata de un recurso <code>cq:Tag</code> de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>En función de la sesión JCR, si se trata de un recurso basado en JCR y el usuario tiene permisos para acceder a UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Con autorización</a></td>
   <td>Autorizable es la interfaz de base común para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuario</a></td>
   <td>El usuario es un usuario con autorización especial que se puede autenticar y suplantar.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Busca debajo del recurso (o utilice setSearchIn()) si se trata de un recurso basado en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Estado del flujo de trabajo para el nodo de carga útil de página/flujo de trabajo determinado.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Estado de replicación para el recurso dado o su subnodo jcr:content (marcado primero).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Devuelve un recurso de conector adaptado para determinados tipos, si se trata de un recurso basado en nodos JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Configuración</a></td>
   <td>Si se trata de un recurso <code>cq:ContentSyncConfig</code> de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Si está debajo de un recurso <code>cq:ContentSyncConfig</code> de nodo.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sesión</a></td>
   <td>La sesión JCR de la solicitud, si es una resolución de recursos basada en JCR (predeterminada).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Diseñador</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>En función de la sesión de JCR, si se trata de una resolución de recursos basada en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>En función de la sesión de JCR, si se trata de una resolución de recursos basada en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager proporciona acceso a los objetos autorizados, es decir, usuarios y grupos, y los medios para mantenerlos. UserManager está enlazado a una sesión en particular.
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Con autorización</a> </td>
   <td>El usuario actual.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuario</a><br /> </td>
   <td>El usuario actual.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar direcciones URL absolutas, incluso sin el objeto de solicitud.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)se adapta a:

Aún no hay destinatarios, pero implementa Adaptable y se puede usar como fuente en un AdapterFactory personalizado.

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Si esta es una respuesta de reescritor inteligente.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[La página](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)**se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Medio</a><br /> </td>
   <td>Recurso de la página.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabledResource</a></td>
   <td>Recurso etiquetado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de la página.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la página.</td>
  </tr>
 </tbody>
</table>

**[El componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)**se adapta a:

| [Medio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del componente. |
|---|---|
| [LabledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso etiquetado (== this). |
| [Nodo](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Todo a lo que se puede adaptar el recurso del componente. |

**[La plantilla](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)**se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso de la plantilla.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabledResource</a></td>
   <td>Recurso etiquetado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de esta plantilla.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la plantilla.</td>
  </tr>
 </tbody>
</table>

#### Seguridad {#security}

**Autorizable**, **Usuario** y **Grupo** se adaptan a:

| [Nodo](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Devuelve el nodo principal del usuario o grupo. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Devuelve el estado de replicación del nodo principal del usuario o grupo. |

#### DAM {#dam}

**El recurso** se adapta a:

| [Medio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del recurso. |
|---|---|
| [Nodo](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del recurso. |
| ... | Todo a lo que se puede adaptar el recurso del recurso. |

#### Etiquetado {#tagging}

**La etiqueta** se adapta a:

| [Medio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso de la etiqueta. |
|---|---|
| [Nodo](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo de la etiqueta. |
| ... | Todo a lo que se puede adaptar el recurso de la etiqueta. |

#### Otras {#other}

Además, Sling / JCR / OCM también proporciona un ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` para objetos OCM ([Object Content Mapping](https://jackrabbit.apache.org/object-content-mapping.html)) personalizados.
