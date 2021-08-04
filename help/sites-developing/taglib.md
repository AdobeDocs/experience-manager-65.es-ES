---
title: Bibliotecas de etiquetas
seo-title: Bibliotecas de etiquetas
description: Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para su uso en el script JSP de sus plantillas y componentes
seo-description: Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para su uso en el script JSP de sus plantillas y componentes
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: de5eb53f6160991ca0718d61afaeed2078a4fa88
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 1%

---

# Bibliotecas de etiquetas{#tag-libraries}

Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para su uso en el script JSP de sus plantillas y componentes.

## Biblioteca de etiquetas de Granite {#granite-tag-library}

La biblioteca de etiquetas Granite contiene funciones útiles.

Al desarrollar el script jsp de un componente de interfaz de usuario de Granite, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

El global también declara la [biblioteca Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeclientlib> {#ui-includeclientlib}

La etiqueta `<ui:includeClientLib>` incluye una biblioteca de cliente html AEM, que puede ser un js, un css o una biblioteca de temas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe usarse varias veces en el jsp. Esta etiqueta es un envoltorio práctico para la interfaz de servicio ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Tiene los siguientes atributos:

**categorías** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas Javascript y CSS para las categorías dadas. El nombre del tema se extrae de la solicitud.

Equivale a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas relacionadas con temas (CSS y JS) para las categorías dadas. El nombre del tema se extrae de la solicitud.

Equivale a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas JavaScript de las categorías dadas.

Equivale a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas CSS de las categorías dadas.

Equivale a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**tema** : se debe incluir un indicador que indique únicamente bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a las inclusiones JS o CSS puras (no para categorías o temas incluidos).

La etiqueta `<ui:includeClientLib>` puede usarse de la siguiente manera en un jsp:

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

Para utilizar la biblioteca de etiquetas CQ en el script, el script debe comenzar con el siguiente código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Cuando el archivo `/libs/foundation/global.jsp` está incluido en el script, la biblioteca de etiquetas se declara automáticamente.

Al desarrollar el script jsp de un componente AEM, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Declara las etiquetas sling, CQ y jstl y expone los objetos de secuencias de comandos utilizados regularmente definidos por la etiqueta [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) . Esto acorta y simplifica el código jsp de su componente.

### &lt;cq:text> {#cq-text}

La etiqueta `<cq:text>` es una etiqueta de conveniencia que genera texto de componente en un JSP.

Tiene los siguientes atributos opcionales:

**propiedad** : nombre de la propiedad que se va a utilizar. El nombre es relativo al recurso actual.

**value** : valor que se utilizará para la salida. Si este atributo está presente, sobrescribe el uso del atributo de propiedad.

**oldValue** : valor que se utilizará para la salida de diferencias. Si este atributo está presente, sobrescribe el uso del atributo de propiedad.

**escapeXml** : define si los caracteres  &lt;>, &amp;, &#39; y &quot; de la cadena resultante deben convertirse a sus códigos de entidad de carácter correspondientes. El valor predeterminado es false. Tenga en cuenta que el escape se aplica después del formato opcional.

**formato** : java.text.Format opcional para usar para dar formato al texto.

**noDiff** : suprime el cálculo de una salida de diferencia, incluso si existe información de diferencia.

**tagClass** : nombre de clase CSS de un elemento que rodeará una salida no vacía. Si está vacío, no se agrega ningún elemento.

**tagName** : nombre del elemento que rodeará una salida no vacía. Su valor predeterminado es DIV.

**marcador de posición** : valor predeterminado que se utiliza para texto nulo o vacío en el modo de edición, es decir, el marcador de posición. Tenga en cuenta que la comprobación predeterminada se realiza después del formato opcional y el escape, es decir, se escribe tal cual en la salida. El valor predeterminado es:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** : valor predeterminado que se usará para texto nulo o vacío. Tenga en cuenta que la comprobación predeterminada se realiza después del formato opcional y el escape, es decir, se escribe tal cual en la salida.

Algunos ejemplos de cómo se puede utilizar la etiqueta `<cq:text>` en un JSP:

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

### &lt;cq:setcontentbundle> {#cq-setcontentbundle}

La etiqueta `<cq:setContentBundle>` crea un contexto de localización de i18n y lo almacena en la variable de configuración `javax.servlet.jsp.jstl.fmt.localizationContext`.

Tiene los siguientes atributos:

**language** : idioma de la configuración regional para la que se recupera el paquete de recursos.

**fuente** : la fuente desde la que se debe tomar la configuración regional. Se puede establecer en uno de los siguientes valores:

* **static** : la configuración regional se toma del  `language` atributo si está disponible, de lo contrario se toma de la configuración regional predeterminada del servidor.

* **página** : la configuración regional se toma del idioma de la página o recurso actual si está disponible, de lo contrario del  `language` atributo si está disponible, en lugar de la configuración regional predeterminada del servidor.

* **solicitud** : la configuración regional se toma de la configuración regional de la solicitud (  `request.getLocale()`).

* **auto** : la configuración regional se toma del  `language` atributo si está disponible, de lo contrario se toma del idioma de la página actual o del recurso si está disponible, en caso contrario, de la solicitud.

Si el atributo `source` no está establecido:

* Si se establece el atributo `language`, el atributo `source` toma el valor predeterminado &quot;`static`.

* Si no se establece el atributo `language`, el atributo `source` toma el valor predeterminado `auto`.

El &quot;paquete de contenido&quot; se puede usar simplemente con etiquetas estándar JSTL `<fmt:message>`. La búsqueda de mensajes por claves es doble:

1. En primer lugar, las propiedades JCR del recurso subyacente que se procesa actualmente se buscan traducciones. Esto le permite definir un cuadro de diálogo de componente simple para editar esos valores.
1. Si el nodo no contiene una propiedad con el mismo nombre que la clave, la alternativa es cargar un paquete de recursos de la solicitud de sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). El idioma o la configuración regional de este paquete se define mediante los atributos de idioma y origen de la etiqueta `<cq:setContentBundle>` .

La etiqueta `<cq:setContentBundle>` puede usarse de la siguiente manera en un jsp.

Para páginas que definen su idioma:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Para páginas personalizadas del usuario:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

La etiqueta `<cq:include>` incluye un recurso en la página actual.

Tiene los siguientes atributos:

**flush**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**path**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuya secuencia de comandos incluye el recurso dado. Se deben especificar la ruta y el resourceType o la secuencia de comandos.

**resourceType**

* Tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo path que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y este tipo de recurso.
* Se deben especificar la ruta y el resourceType o la secuencia de comandos.

**script**

* El script jsp que se va a incluir. Se deben especificar la ruta y el resourceType o la secuencia de comandos.

**ignoreComponentHierarchy**

* Un booleano que controla si se debe ignorar la jerarquía de componentes para la resolución de secuencias de comandos. Si es verdadera, solo se respetan las rutas de búsqueda.

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

* La directiva `<%@ include file="myScript.jsp" %>` informa al compilador JSP para incluir un archivo completo en el archivo actual. Es como si el contenido del archivo incluido se hubiera pegado directamente en el archivo original.
* Con la etiqueta `<cq:include script="myScript.jsp">` , el archivo se incluye durante la ejecución.

¿Debe utilizar `<cq:include>` o `<sling:include>`?

* Al desarrollar componentes de AEM, Adobe recomienda utilizar `<cq:include>`.
* `<cq:include>` permite incluir directamente archivos de secuencias de comandos por su nombre al utilizar el atributo script. Esto tiene en cuenta la herencia de componentes y recursos y, a menudo, es más sencillo que cumplir estrictamente la resolución de script de Sling mediante selectores y extensiones.

### &lt;cq:includeclientlib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` ha quedado obsoleto desde AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) debe usarse en su lugar.

La etiqueta `<cq:includeClientLib>` incluye una biblioteca de cliente html AEM, que puede ser un js, un css o una biblioteca de temas. Para varias inclusiones de diferentes tipos, por ejemplo js y css, esta etiqueta debe usarse varias veces en el jsp. Esta etiqueta es un envoltorio práctico para la interfaz de servicio `com.day.cq.widget.HtmlLibraryManager`.

Tiene los siguientes atributos:

**categorías** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas Javascript y CSS para las categorías dadas. El nombre del tema se extrae de la solicitud.

Equivale a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas relacionadas con temas (CSS y JS) para las categorías dadas. El nombre del tema se extrae de la solicitud.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas JavaScript de las categorías dadas.

Equivale a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** : una lista de categorías de biblioteca de cliente separadas por coma. Esto incluirá todas las bibliotecas CSS de las categorías dadas.

Equivale a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**tema** : se debe incluir un indicador que indique únicamente bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a las inclusiones JS o CSS puras (no para categorías o temas incluidos).

La etiqueta `<cq:includeClientLib>` puede usarse de la siguiente manera en un jsp:

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

### &lt;cq:defineobjects> {#cq-defineobjects}

La etiqueta `<cq:defineObjects>` expone los siguientes objetos de secuencias de comandos, utilizados con regularidad, a los que el desarrollador puede hacer referencia. También muestra los objetos definidos por la etiqueta [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* el objeto de contexto del componente actual de la solicitud (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* el objeto de componente AEM actual del recurso actual (com.day.cq.wcm.api.components.Component interfaz).

**currentDesign**

* objeto de diseño actual de la página actual (interfaz com.day.cq.wcm.api.designer.Design ).

**currentPage**

* el objeto de página WCM AEM actual (interfaz com.day.cq.wcm.api.Page).

**currentStyle**

* el objeto de estilo actual de la celda actual (interfaz com.day.cq.wcm.api.designer.Style ).

**designer**

* el objeto designer utilizado para acceder a la información de diseño (interfaz com.day.cq.wcm.api.designer.Designer).

**editContext**

* el objeto de edición de contexto del componente AEM (interfaz com.day.cq.wcm.api.components.EditContext).

**pageManager**

* el objeto del administrador de páginas para operaciones a nivel de página (interfaz com.day.cq.wcm.api.PageManager ).

**pageProperties**

* el objeto de propiedades de página de la página actual (org.apache.sling.api.resource.ValueMap).

**propiedades**

* el objeto properties del recurso actual (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* el objeto de diseño de la página de recursos (interfaz com.day.cq.wcm.api.designer.Design ).

**resourcePage**

* el objeto de página del recurso (interfaz com.day.cq.wcm.api.Page).
* Tiene los siguientes atributos:

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

* específico para wcm

**editContextName**

* específico para wcm

**propertiesName**

* específico para wcm

**pageManagerName**

* específico para wcm

**currentPageName**

* específico para wcm

**resourcePageName**

* específico para wcm

**pagePropertiesName**

* específico para wcm

**componentName**

* específico para wcm

**designerName**

* específico para wcm

**currentDesignName**

* específico para wcm

**resourceDesignName**

* específico para wcm

**currentStyleName**

* específico para wcm

**Ejemplo**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Cuando el archivo `/libs/foundation/global.jsp` está incluido en el script, la etiqueta `<cq:defineObjects />` se incluye automáticamente.

### &lt;cq:requesturl> {#cq-requesturl}

La etiqueta `<cq:requestURL>` escribe la dirección URL de solicitud actual en JspWriter. Las dos etiquetas [ `<cq:addParam>`](#amp-lt-cq-addparam) y [ `<cq:removeParam>`](#amp-lt-cq-removeparam) y se pueden usar dentro del cuerpo de esta etiqueta para modificar la dirección URL de solicitud actual antes de que se escriba.

Permite crear vínculos a la página actual con parámetros variables. Por ejemplo, permite transformar la solicitud:

`mypage.html?mode=view&query=something` en `mypage.html?query=something`.

El uso de `addParam` o `removeParam` solo cambia la incidencia del parámetro dado, los demás parámetros no se ven afectados.

`<cq:requestURL>` no tiene ningún atributo.

Ejemplos:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addparam> {#cq-addparam}

La etiqueta `<cq:addParam>` agrega un parámetro de solicitud con el nombre y valor dados a la etiqueta [ `<cq:requestURL>`](#amp-lt-cq-requesturl) que la rodea.

Tiene los siguientes atributos:

**name**

* nombre del parámetro que se va a añadir

**seleccionado**

* valor del parámetro que se va a añadir

**Ejemplo:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeparam> {#cq-removeparam}

La etiqueta `<cq:removeParam>` elimina un parámetro de solicitud con el nombre y valor dados de la etiqueta [ `<cq:requestURL>`](#amp-lt-cq-requesturl) que la rodea. Si no se proporciona ningún valor, se eliminan todos los parámetros con el nombre dado.

Tiene los siguientes atributos:

**name**

* nombre del parámetro que se va a eliminar

Ejemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling Tag Library {#sling-tag-library}

La biblioteca de etiquetas Sling contiene funciones Sling útiles.

Cuando se utiliza la biblioteca de etiquetas de Sling en el script, el script debe comenzar con el siguiente código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Cuando el archivo `/libs/foundation/global.jsp` está incluido en el script, la biblioteca de etiquetas de sling se declara automáticamente.

### &lt;sling:include> {#sling-include}

La etiqueta `<sling:include>` incluye un recurso en la página actual.

Tiene los siguientes atributos:

**flush**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**medio**

* El objeto de recurso que se va a incluir en el procesamiento de la solicitud actual. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**ruta**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuya secuencia de comandos incluye el recurso dado. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**resourceType**

* Tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo path que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y este tipo de recurso.

**replaceSelectors**

* Al enviar, los selectores se sustituyen por el valor de este atributo.

**addSelectors**

* Al enviar, el valor de este atributo se añade a los selectores.

**replaceSuffix**

* Al enviar, el sufijo se reemplaza por el valor de este atributo.

>[!NOTE]
>
>La resolución del recurso y la secuencia de comandos que se incluyen con la etiqueta `<sling:include>` es la misma que para una resolución de URL de sling normal. De forma predeterminada, los selectores, la extensión, etc. desde la solicitud actual también se utilizan para la secuencia de comandos incluida. Se pueden modificar a través de los atributos de etiqueta: por ejemplo, `replaceSelectors="foo.bar"` permite sobrescribir los selectores.

Ejemplos:

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

### &lt;sling:defineobjects> {#sling-defineobjects}

La etiqueta `<sling:defineObjects>` expone los siguientes objetos de secuencias de comandos, utilizados con regularidad, a los que el desarrollador puede hacer referencia:

**slingRequest**

* El objeto SlingHttpServletRequest , que proporciona acceso a la información del encabezado de la solicitud HTTP, amplía el HttpServletRequest estándar y proporciona acceso a elementos específicos de Sling, como recursos, información de ruta, selector, etc.

**slingResponse**

* Objeto SlingHttpServletResponse, que proporciona acceso a la respuesta HTTP creada por el servidor. Actualmente es el mismo que el HttpServletResponse desde el que se extiende.**solicitud**
* El objeto de solicitud JSP estándar que es un HttpServletRequest puro.**response**
* El objeto de respuesta JSP estándar que es un HttpServletResponse puro.

**resourceResolver**

* El objeto ResourceResolver actual. Es igual que slingRequest.getResourceResolver()

.**sling**

* Un objeto SlingScriptHelper que contiene métodos de conveniencia para secuencias de comandos, principalmente sling.include(&#39;/some/other/resource&#39;) para incluir las respuestas de otros recursos dentro de esta respuesta (por ejemplo, incrustar fragmentos html de encabezado) y sling.getService (foo.bar.Service.class) para recuperar los servicios OSGi disponibles en Sling (Notación de clase según el lenguaje de secuencias de comandos).

**medio**

* el objeto Resource actual que se va a gestionar, según la dirección URL de la solicitud. Es lo mismo que slingRequest.getResource().

**currentNode**

* Si el recurso actual apunta a un nodo JCR (que suele ser el caso en Sling), proporciona acceso directo al objeto Node . De lo contrario, este objeto no está definido.

**log**

* Proporciona un registrador SLF4J para iniciar sesión en el sistema de registro Sling desde scripts, por ejemplo. log.info(&quot;Ejecutando mi script&quot;).

* Tiene los siguientes atributos:

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**Ejemplo:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Biblioteca de etiquetas JSTL {#jstl-tag-library}

La [Biblioteca de etiquetas estándar de páginas de JavaServer](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contiene muchas etiquetas útiles y estándar. Las etiquetas de núcleo, formato y funciones se definen mediante el `/libs/foundation/global.jsp` como se muestra en el siguiente fragmento de código.

### Extracto de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Después de importar el archivo `/libs/foundation/global.jsp` como se describió anteriormente, puede utilizar los prefijos `c`, `fmt` y `fn` para acceder a esas etiquetas. La documentación oficial de JSTL está disponible en [Tutorial Java EE 5 - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
