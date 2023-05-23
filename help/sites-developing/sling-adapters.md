---
title: Uso de los adaptadores de Sling
seo-title: Using Sling Adapters
description: Sling ofrece un patrón de adaptador para traducir convenientemente los objetos que implementan la interfaz adaptable
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 14%

---

# Uso de los adaptadores de Sling{#using-sling-adapters}

[Sling](https://sling.apache.org) ofrece un [Patrón de adaptador](https://sling.apache.org/site/adapters.html) para traducir convenientemente los objetos que implementan el [Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) interfaz. Esta interfaz proporciona un [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) que traducirá el objeto al tipo de clase que se pasa como argumento.

Por ejemplo, para traducir un objeto Resource al objeto Node correspondiente, puede hacer lo siguiente:

```java
Node node = resource.adaptTo(Node.class);
```

## Casos de uso {#use-cases}

Hay los siguientes casos de uso:

* Obtenga objetos específicos de la implementación.

   Por ejemplo, una implementación basada en JCR del genérico [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) proporciona acceso al JCR subyacente [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creación de acceso directo de objetos que requieren que se pasen objetos de contexto interno.

   Por ejemplo, el basado en JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) contiene una referencia al de la solicitud [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), que a su vez es necesaria para muchos objetos que funcionarán en función de esa sesión de solicitud, como la [`PageManager`](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Acceso directo a servicios.

   Un caso raro - `sling.getService()` es simple también.

### Valor devuelto nulo {#null-return-value}

`adaptTo()` puede devolver null.

Esto se debe a varios motivos, entre ellos:

* la implementación no admite el tipo de destinatario
* un adaptador de fábrica que maneja este caso no está activo (p. ej. debido a la falta de referencias de servicio)
* error de condición interna
* el servicio no está disponible

Es importante que gestione correctamente el caso nulo. Para las representaciones jsp, puede ser aceptable que jsp falle si esto resulta en un fragmento de contenido vacío.

### Almacenamiento en caché {#caching}

Para mejorar el rendimiento, las implementaciones pueden almacenar en caché el objeto devuelto por un `obj.adaptTo()` llamada. Si la variable `obj` es el mismo, el objeto devuelto es el mismo.

Este almacenamiento en caché se realiza para todos los `AdapterFactory` casos basados en.

Sin embargo, no hay una regla general: el objeto podría ser una instancia nueva o una existente. Esto significa que no puede confiar en ninguno de los comportamientos. Por lo tanto, es importante, especialmente en el interior `AdapterFactory`, que los objetos se pueden reutilizar en este escenario.

### Funcionamiento {#how-it-works}

Hay varias formas en que `Adaptable.adaptTo()` se puede implementar:

* Por el propio objeto; implementando el método en sí y asignándolo a determinados objetos.
* Por un [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que puede asignar objetos arbitrarios.

   Los objetos aún deben implementar el `Adaptable` interfaz y debe ampliarse [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (que pasa el `adaptTo` llamada a un administrador de adaptadores central).

   Esto permite la conexión a `adaptTo` mecanismo para clases existentes, como `Resource`.

* Una combinación de ambos.

En el primer caso, los javadocs pueden indicar lo siguiente `adaptTo-targets` son posibles. Sin embargo, para subclases específicas como el recurso basado en JCR, a menudo esto no es posible. En este último caso, las implementaciones de `AdapterFactory` suelen formar parte de las clases privadas de un paquete y, por lo tanto, no se exponen en una API de cliente ni se enumeran en javadocs. En teoría, sería posible acceder a todas las `AdapterFactory` implementaciones desde el [OSGi](/help/sites-deploying/configuring-osgi.md) tiempo de ejecución del servicio de y observe sus configuraciones &quot;adaptables&quot; (fuentes y destinos), pero no para asignarlas entre sí. Al final, esto depende de la lógica interna, que debe documentarse. De ahí esta referencia.

## Referencia {#reference}

### Sling {#sling}

[**Recurso**](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Si es un recurso basado en nodos JCR o una propiedad JCR que hace referencia a un nodo.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propiedad</a></td>
   <td>Si es un recurso basado en propiedades JCR.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Si es un recurso basado en JCR (nodo o propiedad).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Asignar</a></td>
   <td>Devuelve un mapa de las propiedades, si se trata de un recurso basado en nodos JCR (u otro recurso que admita asignaciones de valores).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Devuelve un mapa práctico de las propiedades, si se trata de un recurso basado en nodos JCR (u otro recurso que admita asignaciones de valores). También se puede lograr (de forma más sencilla) utilizando<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (gestiona casos nulos, etc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensión de <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite tener en cuenta la jerarquía de recursos al buscar propiedades.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModillableValueMap</a></td>
   <td>Una extensión del <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que le permite modificar las propiedades de ese nodo.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Devuelve el contenido binario de un recurso de archivo (si es un recurso basado en nodos JCR y el tipo de nodo es <code>nt:file</code> o <code>nt:resource</code>; si es un recurso de paquete; contenido de archivo (si es un recurso del sistema de archivos) o los datos de un recurso de propiedad JCR binario.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Devuelve una URL al recurso (URL del repositorio de este nodo si es un recurso basado en nodos JCR; URL del paquete jar si es un recurso del paquete; URL del archivo si es un recurso del sistema de archivos).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">Archivo</a></td>
   <td>Si se trata de un recurso del sistema de archivos.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Si este recurso es una secuencia de comandos (por ejemplo, un archivo jsp) para la que un motor de secuencias de comandos está registrado con sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Si este recurso es un script (por ejemplo, un archivo jsp) para el que un motor de scripts está registrado con sling o si es un recurso de servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">Cadena</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Largo</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">Doble</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendario</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">Cadena[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Booleano[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendario[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor[]</a></td>
   <td>Devuelve los valores si se trata de un recurso basado en una propiedad JCR (y encaja el valor).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Si es un recurso basado en nodos JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Si es un recurso basado en nodos JCR y el nodo es un <code>cq:Page</code> (o <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Si se trata de un <code>cq:Component</code> recurso de nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">Diseño</a></td>
   <td>Si es un nodo de diseño (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">Plantilla</a></td>
   <td>Si se trata de un <code>cq:Template</code> recurso de nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Modelo</a></td>
   <td>Si se trata de un <code>cq:Template</code> recurso de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">Recurso</a></td>
   <td>Si es un recurso de nodo dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Representación</a></td>
   <td>Si es una representación dam:Asset (nt:file bajo la carpeta de representación de dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Etiqueta</a></td>
   <td>Si se trata de un <code>cq:Tag</code> recurso de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Se basa en la sesión JCR si es un recurso basado en JCR y el usuario tiene permisos para acceder a UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Con autorización</a></td>
   <td>El autorizable es la interfaz base común para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuario</a></td>
   <td>El usuario es un autorizable especial que puede autenticarse y suplantarse.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Realiza búsquedas debajo del recurso (o utiliza setSearchIn()) si se trata de un recurso basado en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Estado del flujo de trabajo para el nodo de carga útil de página/flujo de trabajo determinado.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Estado de replicación para el recurso determinado o su subnodo jcr:content (comprobado primero).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Devuelve un recurso de conector adaptado para ciertos tipos, si es un recurso basado en nodos JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Configuración</a></td>
   <td>Si se trata de un <code>cq:ContentSyncConfig</code> recurso de nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Si es inferior a <code>cq:ContentSyncConfig</code> recurso de nodo.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>La sesión JCR de la solicitud, si se trata de una resolución de recursos basada en JCR (valor predeterminado).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>En función de la sesión JCR, si se trata de una resolución de recursos basada en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>En función de la sesión JCR, si se trata de una resolución de recursos basada en JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager proporciona acceso a objetos autorizables y medios para mantenerlos, es decir, usuarios y grupos. UserManager está enlazado a una sesión concreta.
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

[**SlingHttpServletRequest**](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) se adapta a:

Aún no hay destinos, pero implementa Adaptable y podría utilizarse como origen en un AdapterFactory personalizado.

[**SlingHttpServletResponse**](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Si es una respuesta de reescritura de sling.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Página](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>Recurso de la página.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Recurso etiquetado (==).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de la página.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la página.</td>
  </tr>
 </tbody>
</table>

**[Componente](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** se adapta a:

| [Resource](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del componente. |
|---|---|
| [EtiquetadoRecurso](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso etiquetado (==). |
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Todo a lo que se puede adaptar el recurso del componente. |

**[Plantilla](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso de la plantilla.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Recurso etiquetado (==).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de esta plantilla.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la plantilla.</td>
  </tr>
 </tbody>
</table>

#### Seguridad {#security}

**Autorizable**, **Usuario** y **Grupo** adaptar a:

| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Devuelve el nodo principal del usuario/grupo. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Devuelve el estado de replicación del nodo principal del usuario/grupo. |

#### DAM  {#dam}

**Recurso** se adapta a:

| [Resource](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del recurso. |
|---|---|
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del recurso. |
| ... | Todo a lo que se puede adaptar el recurso del recurso. |

#### Etiquetado {#tagging}

**Etiqueta** se adapta a:

| [Resource](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso de la etiqueta. |
|---|---|
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo de la etiqueta. |
| ... | Todo a lo que se puede adaptar el recurso de la etiqueta. |

#### Otro {#other}

Además, Sling/JCR/OCM también proporciona un ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` para OCM personalizado ([Asignación de contenido de objeto](https://jackrabbit.apache.org/object-content-mapping.html)) objetos.
