---
title: Ampliación de la funcionalidad de búsqueda de Recursos AEM
description: Extienda las capacidades de búsqueda de Recursos AEM más allá de los valores predeterminados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Ampliar búsqueda de recursos {#extending-assets-search}

Puede ampliar las capacidades de búsqueda de recursos de Adobe Experience Manager (AEM). De forma predeterminada, Recursos AEM busca recursos por cadenas.

La búsqueda se realiza a través de la interfaz de QueryBuilder para que la búsqueda se pueda personalizar con varios predicados. Puede superponer el conjunto predeterminado de predicados en el siguiente directorio: `/apps/dam/content/search/searchpanel/facets`.

También puede añadir fichas adicionales al panel de administración de Recursos AEM.

>[!CAUTION]
>
>A partir de AEM 6.4, la IU clásica ya no se utiliza. Para ver el anuncio, consulte Funciones [obsoletas y eliminadas](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html). Se le recomienda utilizar la IU táctil. Para personalizar, consulte Facetas [de búsqueda](/help/assets/search-facets.md).

## Superposición {#overlaying}

Para superponer los predicados preconfigurados, copie el `facets` nodo de `/libs/dam/content/search/searchpanel` a `/apps/dam/content/search/searchpanel/` o especifique otra `facetURL` propiedad en la `searchpanel` configuración (el valor predeterminado es a `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>De forma predeterminada, la estructura de directorio bajo / `apps` no existe y debe crearse. Asegúrese de que los tipos de nodo coinciden con los de / `libs`.


## Agregar fichas {#adding-tabs}

Puede agregar fichas de búsqueda adicionales configurándolas en el administrador de AEM Assets. Para crear fichas adicionales:

1. Cree la estructura de carpetas `/apps/wcm/core/content/damadmin/tabs,`si aún no existe, copie el `tabs` nodo `/libs/wcm/core/content/damadmin` y péguelo.
1. Cree y configure la segunda ficha como desee.

   >[!NOTE]
   >
   >Cuando cree un segundo `siteadminsearchpanel`, asegúrese de establecer una `id` propiedad para evitar conflictos de formularios.

## Crear predicados personalizados {#creating-custom-predicates}

Recursos AEM incluye un conjunto de predicados predefinidos que se pueden utilizar para personalizar una página de uso compartido de recursos. La personalización de un recurso compartido de este modo se trata en [Creación y configuración de una página](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)de uso compartido de recursos.

Además de utilizar predicados preexistentes, los desarrolladores de AEM también pueden crear sus propios predicados mediante la API [de](/help/sites-developing/querybuilder-api.md)Query Builder.

La creación de predicados personalizados requiere conocimientos básicos sobre el marco [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)utilidades.

Se recomienda copiar un predicado existente y ajustarlo. Los predicados de muestra se encuentran en **/libs/cq/search/components/predicates**.

### Ejemplo: Generar un predicado de propiedades simple {#example-build-a-simple-property-predicate}

Para generar un predicado de propiedad:

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo **/apps/geometrixx/components/titlepredicate**.
1. Agregar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Añada `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Para que el componente esté disponible, debe poder editarlo. Para que un componente se pueda editar, en CRXDE, agregue un nodo **cq:editConfig** de tipo principal **cq:EditConfig**. Para poder eliminar párrafos, agregue una propiedad de varios valores **cq:actions** con un único valor de **ELIMINAR**.
1. Vaya al navegador y, en la página de muestra (por ejemplo, **press.html**), cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos de predicado (por ejemplo, **izquierda**).

1. En el modo **Editar** , el nuevo componente ahora está disponible en la barra de tareas (que se encuentra en el grupo **Buscar** ). Inserte el componente en la columna **Predicados** y escriba una palabra de búsqueda, por ejemplo, **Diamante** y haga clic en la lupa para iniciar la búsqueda.

   >[!NOTE]
   >
   >Al buscar, asegúrese de escribir el término exactamente, incluyendo el caso correcto.

### Ejemplo: Crear un predicado de grupo simple {#example-build-a-simple-group-predicate}

Para crear un predicado de grupo:

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo **/apps/geometrixx/components/picspredicate.**
1. Agregar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Agregar **titlepredicate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Para que el componente esté disponible, debe poder editarlo. Para que un componente se pueda editar, en CRXDE, agregue un nodo **cq:editConfig** de tipo principal **cq:EditConfig**. Para poder eliminar párrafos, agregue una propiedad de varios valores **cq:actions** con un único valor de **ELIMINAR**.
1. Vaya al navegador y, en la página de muestra (por ejemplo, **press.html**), cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos de predicado (por ejemplo, **izquierda**).
1. En el modo **Editar** , el nuevo componente ahora está disponible en la barra de tareas (que se encuentra en el grupo **Buscar** ). Inserte el componente en la columna **Predicados** .

## Widgets de predicado instalados {#installed-predicate-widgets}

Los siguientes predicados están disponibles como utilidades preconfiguradas de ExtJS.

### FulltextPredicate {#fulltextpredicate}

| Propiedad | Tipo | Descripción |
|---|---|---|
| predicateName | Cadena | Nombre del predicado. El valor predeterminado es `fulltext` |
| searchCallback | Función | Llamada de retorno para activar la búsqueda en el evento `keyup`. El valor predeterminado es `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| Propiedad | Tipo | Descripción |
|---|---|---|
| predicateName | Cadena | Nombre del predicado. El valor predeterminado es `property` |
| propertyName | Cadena | Nombre de la propiedad JCR. El valor predeterminado es `jcr:title` |
| defaultValue | Cadena | Valor predeterminado prerelleno. |

### PathPredicate {#pathpredicate}

| Propiedad | Tipo | Descripción |
|---|---|---|
| predicateName | Cadena | Nombre del predicado. El valor predeterminado es `path` |
| rootPath | Cadena | Ruta raíz del predicado. El valor predeterminado es `/content/dam` |
| pathFieldPredicateName | Cadena | El valor predeterminado es `folder` |
| showFlatOption | Booleano | Marca para mostrar la casilla de verificación `search in subfolders`. La opción predeterminada es true. |

### DatePredicate {#datepredicate}

| Propiedad | Tipo | Descripción |
|---|---|---|
| predicateName | Cadena | Nombre del predicado. El valor predeterminado es `daterange` |
| propertyname | Cadena | Nombre de la propiedad JCR. El valor predeterminado es `jcr:content/jcr:lastModified` |
| defaultValue | Cadena | Valor predeterminado previo |

### OptionsPredicate {#optionspredicate}

| Propiedad | Tipo | Descripción |
|---|---|---|
| el título | Cadena | Agrega un título superior adicional |
| predicateName | Cadena | Nombre del predicado. El valor predeterminado es `daterange` |
| propertyname | Cadena | Nombre de la propiedad JCR. El valor predeterminado es `jcr:content/metadata/cq:tags` |
| contraer | Cadena | Contraer nivel. El valor predeterminado es `level1` |
| desencadenadorBúsqueda | Booleano | Marca para activar la búsqueda al marcar. Predeterminado en false |
| searchCallback | Función | Llamada de retorno para activar la búsqueda. El valor predeterminado es `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Número | Tiempo de espera antes de que se active searchCallback. Valores predeterminados de 800 ms |

## Personalizar resultados de búsqueda {#customizing-search-results}

La presentación de los resultados de la búsqueda en una página de uso compartido de recursos se rige por la lente seleccionada. Recursos AEM incorpora un conjunto de objetivos predefinidos que se pueden utilizar para personalizar una página de uso compartido de recursos. La personalización de un recurso compartido de este modo se trata en [Creación y configuración de una página](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)de uso compartido de recursos.

Además de utilizar objetivos preexistentes, los desarrolladores de AEM también pueden crear sus propios objetivos.
