---
title: Bibliotecas de etiquetas
description: Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para utilizarlas en el script JSP de sus plantillas y componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '2465'
ht-degree: 0%

---

# Bibliotecas de etiquetas{#tag-libraries}

Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para utilizarlas en el script JSP de sus plantillas y componentes.

## Biblioteca de etiquetas de Granite {#granite-tag-library}

La biblioteca de etiquetas Granite contiene funciones útiles.

Al desarrollar el script jsp de un componente de la interfaz de usuario de Granite, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

El global también declara el [Biblioteca de Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

El `<ui:includeClientLib>` AEM etiqueta Incluye una biblioteca de cliente de html de, que puede ser una biblioteca js, css o de temáticas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe utilizarse varias veces en jsp. Esta etiqueta es un envoltorio cómodo para el ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` interfaz de servicio de.

Tiene los atributos siguientes:

**categorías** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas de JavaScript y CSS para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas relacionadas con temáticas (tanto CSS como JS) para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas JavaScript para las categorías dadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas CSS para las categorías dadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temático** : Se debe incluir un indicador que indique que solo hay bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a inclusiones JS o CSS puras (no para categorías ni inclusiones de temas).

El `<ui:includeClientLib>` la etiqueta se puede utilizar de la siguiente manera en un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## Biblioteca de etiquetas CQ {#cq-tag-library}

La biblioteca de etiquetas CQ contiene funciones útiles.

Para utilizar la biblioteca de etiquetas CQ en el script, este debe comenzar con el siguiente código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Si la variable `/libs/foundation/global.jsp` se incluye en el script, la etiqueta se declara automáticamente.

AEM Al desarrollar el script jsp de un componente de la, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Declara las etiquetas sling, CQ y jstl y expone los objetos de script utilizados regularmente definidos por [`<cq:defineObjects />`](#amp-lt-cq-defineobjects) etiqueta. Esto acorta y simplifica el código jsp del componente.

### &lt;cq:text> {#cq-text}

El `<cq:text>` es una etiqueta de conveniencia que genera texto de componente en un JSP.

Tiene los siguientes atributos opcionales:

**propiedad** : nombre de la propiedad que se va a utilizar. El nombre es relativo al recurso actual.

**valor** : valor que se utilizará para la salida. Si este atributo está presente, sobrescribe el uso del atributo property.

**oldValue** : valor que se utilizará para la salida de diferencia. Si este atributo está presente, sobrescribe el uso del atributo property.

**escapeXml** - Define si los caracteres &lt;, >, &amp;, &#39; y &quot; de la cadena resultante deben convertirse a sus códigos de entidad de caracteres correspondientes. El valor predeterminado es false. El escape se aplica después del formato opcional.

**formato** : java.text.Format opcional que se utilizará para dar formato al texto.

**noDiff** : Suprime el cálculo de una salida de diferencia, incluso si hay una información de diferencia presente.

**tagClass** : nombre de clase CSS de un elemento que rodeará una salida no vacía. Si está vacío, no se agrega ningún elemento.

**tagName** : nombre del elemento que rodeará una salida no vacía. El valor predeterminado es DIV.

**placeholder** : valor predeterminado que se utilizará para el texto nulo o vacío en el modo de edición, es decir, el marcador de posición. Tenga en cuenta que la comprobación predeterminada se realiza después del formato y el escape opcionales, es decir, se escribe tal cual en la salida. El valor predeterminado es:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**predeterminado** - Valor predeterminado que se utilizará para el texto nulo o vacío. La comprobación predeterminada se realiza después del formato opcional y el escape, es decir, se escribe tal cual en la salida.

Algunos ejemplos muestran cómo la variable `<cq:text>` La etiqueta se puede utilizar en un JSP:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

El `<cq:setContentBundle>` crea un contexto de localización i18n y lo almacena en el `javax.servlet.jsp.jstl.fmt.localizationContext` variable de configuración.

Tiene los atributos siguientes:

**idioma** : El idioma de la configuración regional para la que se recupera el paquete de recursos.

**origen** : origen desde el que se debe tomar la configuración regional. Se puede establecer en uno de los siguientes valores:

* **estático** - la configuración regional se toma del `language` atributo si está disponible; en caso contrario, desde la configuración regional predeterminada del servidor.

* **página** : la configuración regional se toma del idioma de la página o el recurso actual si está disponible; de lo contrario, se toma del `language` atributo si está disponible; en caso contrario, desde la configuración regional predeterminada del servidor.

* **solicitud** - la configuración regional se toma de la configuración regional de la solicitud ( `request.getLocale()`).

* **auto** - la configuración regional se toma del `language` atributo si está disponible; de lo contrario, desde el idioma de la página o el recurso actual, si está disponible; de lo contrario, desde la solicitud.

Si la variable `source` no se ha establecido el atributo:

* Si la variable `language` se ha establecido el atributo, la variable `source` el atributo toma el valor predeterminado &quot; `static`.

* Si la variable `language` no se ha definido el atributo, la variable `source` el atributo toma el valor predeterminado `auto`.

El &quot;paquete de contenido&quot; lo puede usar el JSTL estándar `<fmt:message>` etiquetas. La búsqueda de mensajes por claves es doble:

1. En primer lugar, se buscan traducciones en las propiedades JCR del recurso subyacente que se procesa. Esto permite definir un cuadro de diálogo de componente simple para editar esos valores.
1. Si el nodo no contiene una propiedad denominada exactamente como la clave, la alternativa es cargar un paquete de recursos desde la solicitud de sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). El idioma o la configuración regional de este paquete se define mediante los atributos de idioma y origen del `<cq:setContentBundle>` etiqueta.

El `<cq:setContentBundle>` la etiqueta se puede utilizar de la siguiente manera en un jsp.

Para páginas que definen su idioma:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Para páginas personalizadas de usuario:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

El `<cq:include>` incluye un recurso en la página actual.

Tiene los atributos siguientes:

**vaciar**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**ruta**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuyo script incluye el recurso dado. Se debe especificar la ruta y el tipo de recurso o el script.

**resourceType**

* El tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo de ruta que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y de este tipo de recurso.
* Se debe especificar la ruta y el tipo de recurso o el script.

**script**

* Script jsp que se va a incluir. Se debe especificar la ruta y el tipo de recurso o el script.

**ignoreComponentHierarchy**

* Un booleano que controla si la jerarquía de componentes debe ignorarse para la resolución de scripts. Si es true, solo se respetan las rutas de búsqueda.

**Ejemplo:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

¿Debe utilizar `<%@ include file="myScript.jsp" %>` o `<cq:include script="myScript.jsp" %>` para incluir un script?

* El `<%@ include file="myScript.jsp" %>` indica al compilador de JSP que incluya un archivo completo en el archivo actual. Es como si el contenido del archivo incluido se hubiera pegado directamente en el archivo original.
* Con el `<cq:include script="myScript.jsp">` , el archivo se incluye durante la ejecución.

¿Debe utilizar `<cq:include>` o `<sling:include>`?

* AEM A la hora de desarrollar componentes de la, Adobe recomienda utilizar `<cq:include>`.
* `<cq:include>` permite incluir directamente archivos de script por su nombre cuando se utiliza el atributo script. Esto tiene en cuenta la herencia de componentes y tipos de recursos, y a menudo es más sencillo que el cumplimiento estricto de la resolución de scripts de Sling mediante selectores y extensiones.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` AEM Obsoleto desde la versión 5.. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) debe utilizarse en su lugar.

El `<cq:includeClientLib>` AEM etiqueta Incluye una biblioteca de cliente html de la comunidad, que puede ser una biblioteca js, una css o una biblioteca de temáticas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe utilizarse varias veces en jsp. Esta etiqueta es un envoltorio cómodo para el `com.day.cq.widget.HtmlLibraryManager` interfaz de servicio de.

Tiene los atributos siguientes:

**categorías** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas de JavaScript y CSS para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas relacionadas con temáticas (tanto CSS como JS) para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas JavaScript para las categorías dadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - Una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas CSS para las categorías dadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temático** : Se debe incluir un indicador que indique que solo hay bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a inclusiones JS o CSS puras (no para categorías ni inclusiones de temas).

El `<cq:includeClientLib>` la etiqueta se puede utilizar de la siguiente manera en un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

El `<cq:defineObjects>` expone los siguientes objetos de script, que se utilizan con regularidad y a los que el desarrollador puede hacer referencia. También expone los objetos definidos por la variable [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) etiqueta.

**componentContext**

* el objeto de contexto del componente actual de la solicitud (com.day.cq.wcm.api.components.ComponentContext.interface).

**componente**

* AEM el objeto de componente de la actual del recurso actual (com.day.cq.wcm.api.components.Component (interfaz).

**currentDesign**

* el objeto de diseño actual de la página actual (com.day.cq.wcm.api.designer.Design interface).

**currentPage**

* AEM el objeto de página actual de WCM de la (interfaz com.day.cq.wcm.api.Page).

**currentStyle**

* el objeto style actual de la celda actual (com.day.cq.wcm.api.designer.Style interfaz).

**diseñador**

* el objeto designer utilizado para tener acceso a la información de diseño (interfaz com.day.cq.wcm.api.designer.Designer).

**editContext**

* AEM el objeto de contexto de edición del componente de (interfaz com.day.cq.wcm.api.components.EditContext).

**pageManager**

* el objeto administrador de páginas para operaciones de nivel de página (interfaz com.day.cq.wcm.api.PageManager).

**pageProperties**

* el objeto page properties de la página actual (org.apache.sling.api.resource.ValueMap).

**propiedades**

* el objeto properties del recurso actual (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* el objeto design de la página de recursos (com.day.cq.wcm.api.designer.Design interface).

**resourcePage**

* el objeto de página de recursos (interfaz com.day.cq.wcm.api.Page).
* Tiene los atributos siguientes:

**requestName**

* heredado de sling

**responseName**

* heredado de sling

**resourceName**

* heredado de sling

**nodeName**

* heredado de sling

**logName**

* heredado de sling

**resourceResolverName**

* heredado de sling

**slingName**

* heredado de sling

**componentContextName**

* específico de wcm

**editContextName**

* específico de wcm

**propertiesName**

* específico de wcm

**pageManagerName**

* específico de wcm

**currentPageName**

* específico de wcm

**resourcePageName**

* específico de wcm

**pagePropertiesName**

* específico de wcm

**componentName**

* específico de wcm

**designerName**

* específico de wcm

**currentDesignName**

* específico de wcm

**resourceDesignName**

* específico de wcm

**currentStyleName**

* específico de wcm

**Ejemplo**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Si la variable `/libs/foundation/global.jsp` se incluye en la secuencia de comandos, la variable `<cq:defineObjects />` se incluye automáticamente.

### &lt;cq:requestURL> {#cq-requesturl}

El `<cq:requestURL>` escribe la dirección URL de la solicitud actual en JspWriter. Las dos etiquetas [`<cq:addParam>`](#amp-lt-cq-addparam) y [`<cq:removeParam>`](#amp-lt-cq-removeparam) y se pueden usar dentro del cuerpo de esta etiqueta para modificar la URL de la solicitud actual antes de que se escriba.

Permite crear vínculos a la página actual con distintos parámetros. Por ejemplo, permite transformar la solicitud:

`mypage.html?mode=view&query=something` en `mypage.html?query=something`.

El uso de `addParam` o `removeParam` Si solo cambia la aparición del parámetro determinado, el resto de parámetros no se verán afectados.

`<cq:requestURL>` no tiene ningún atributo.

Por ejemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

El `<cq:addParam>` agrega un parámetro de solicitud con el nombre y valor dados al contenedor [`<cq:requestURL>`](#amp-lt-cq-requesturl) etiqueta.

Tiene los atributos siguientes:

**name**

* nombre del parámetro que se va a agregar

**valor**

* valor del parámetro que se va a agregar

**Ejemplo:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

El `<cq:removeParam>` elimina un parámetro de solicitud con el nombre y valor dados del contenedor [`<cq:requestURL>`](#amp-lt-cq-requesturl) etiqueta. Si no se proporciona ningún valor, se eliminan todos los parámetros con el nombre dado.

Tiene los atributos siguientes:

**name**

* nombre del parámetro que se va a eliminar

Ejemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Biblioteca de etiquetas de Sling {#sling-tag-library}

La biblioteca de etiquetas Sling contiene funciones Sling útiles.

Cuando se utiliza la biblioteca de etiquetas Sling en el script, este debe comenzar con el siguiente código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Si la variable `/libs/foundation/global.jsp` se incluye en el script, la etiqueta sling se declara automáticamente.

### &lt;sling:include> {#sling-include}

El `<sling:include>` incluye un recurso en la página actual.

Tiene los atributos siguientes:

**vaciar**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**resource**

* El objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**ruta**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuyo script incluye el recurso dado. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**resourceType**

* El tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo de ruta que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y de este tipo de recurso.

**replaceSelectors**

* Al realizar el envío, los selectores se sustituyen por el valor de este atributo.

**addSelectors**

* Al realizar el envío, el valor de este atributo se añade a los selectores.

**replaceSuffix**

* Al realizar el envío, el sufijo se reemplaza por el valor de este atributo.

>[!NOTE]
>
>La resolución del recurso y la secuencia de comandos que se incluyen con el `<sling:include>` es la misma que para una resolución de URL normal de sling. De forma predeterminada, los selectores, la extensión, etc. de la solicitud actual también se utilizan para el script incluido. Se pueden modificar mediante los atributos de etiqueta: por ejemplo `replaceSelectors="foo.bar"` permite sobrescribir los selectores.

Por ejemplo:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

El `<sling:defineObjects>` expone los siguientes objetos de script, que se utilizan con regularidad y a los que el desarrollador puede hacer referencia:

**slingRequest**

* El objeto SlingHttpServletRequest, que proporciona acceso a la información del encabezado de solicitud HTTP (amplía el objeto HttpServletRequest estándar) y proporciona acceso a elementos específicos de Sling como recursos, información de ruta y selector.

**slingResponse**

* Objeto SlingHttpServletResponse, que proporciona acceso a la respuesta HTTP creada por el servidor. Es igual que el HttpServletResponse desde el que se extiende.**solicitud**
* El objeto de solicitud JSP estándar que es HttpServletRequest puro.**respuesta**
* El objeto de respuesta JSP estándar que es HttpServletResponse puro.

**resourceResolver**

* El objeto ResourceResolver actual. Es lo mismo que slingRequest.getResourceResolver()

.**sling**

* Un objeto SlingScriptHelper, que contiene métodos de conveniencia para scripts, principalmente sling.include(&#39;/some/other/resource&#39;) para incluir las respuestas de otros recursos dentro de esta respuesta (por ejemplo, incrustar fragmentos html de encabezado) y sling.getService(foo.bar.Service.class) para recuperar los servicios OSGi disponibles en Sling (notación de clase según el lenguaje de script).

**resource**

* el objeto Resource actual que se va a controlar, según la dirección URL de la solicitud. Es lo mismo que slingRequest.getResource().

**currentNode**

* Si el recurso actual apunta a un nodo JCR (como suele ocurrir en Sling), proporciona acceso directo al objeto Node. De lo contrario, este objeto no está definido.

**registro**

* Proporciona un registrador SLF4J para registrar en el sistema de registro de Sling desde scripts, por ejemplo, log.info(&quot;Ejecutando mi script&quot;).

* Tiene los atributos siguientes:

**requestName**

**responseName**

**nodeName**

l **resourceResolverName de logName**

**slingName**

**Ejemplo:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Biblioteca de etiquetas JSTL {#jstl-tag-library}

El [Biblioteca de etiquetas estándar de páginas de JavaServer](https://www.oracle.com/java/technologies/java-server-tag-library.html) contiene muchas etiquetas útiles y estándar. Las etiquetas core, formatting y functions se definen mediante la variable `/libs/foundation/global.jsp` como se muestra en el siguiente fragmento de código.

### Extracto de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Después de importar el `/libs/foundation/global.jsp` como se ha descrito anteriormente, puede utilizar el `c`, `fmt` y `fn` prefijos para acceder a esas etiquetas. La documentación oficial del JSTL está disponible en [Tutorial de Java™ EE 5: Biblioteca de etiquetas estándar de JavaServer Pages](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
