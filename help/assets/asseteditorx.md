---
title: Ampliar editor de recursos
description: Obtenga información sobre cómo ampliar las capacidades del editor de recursos con componentes personalizados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 11%

---


# Extend Asset Editor {#extending-asset-editor}

El Editor de recursos es la página que se abre cuando se hace clic en un recurso encontrado a través del recurso compartido, lo que permite al usuario editar aspectos del recurso como metadatos, miniaturas, título y etiquetas.

La configuración del editor mediante los componentes de edición predefinidos se trata en [Creación y configuración de una página](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)del editor de recursos.

Además de utilizar componentes de editor preexistentes, los desarrolladores también pueden crear sus [!DNL Adobe Experience Manager] propios componentes.

## Creación de una plantilla de editor de recursos {#creating-an-asset-editor-template}

En Geometrixx se incluyen las siguientes páginas de muestra:

* Página de muestra de Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Plantilla de muestra: `/apps/geometrixx/templates/asseteditor`
* Componente de página de muestra: `/apps/geometrixx/components/asseteditor`

### Configurar Clientlib {#configuring-clientlib}

[!DNL Assets] los componentes utilizan una extensión de la clientlib de edición de WCM. Los clientes suelen estar cargados en `init.jsp`.

En comparación con la carga de clientlib predeterminada (en core `init.jsp`), una [!DNL Assets] plantilla debe tener lo siguiente:

* La plantilla debe incluir la `cq.dam.edit` clientlib (en lugar de `cq.wcm.edit`).

* La clientlib también debe incluirse en el modo WCM desactivado (por ejemplo, cargado en la **publicación**) para poder procesar los predicados, las acciones y las lentes.

En la mayoría de los casos, la copia de la muestra existente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) debe satisfacer estas necesidades.

### Configurar acciones de JS {#configuring-js-actions}

Algunos de los [!DNL Assets] componentes requieren funciones JS definidas en `component.js`. Copie este archivo en el directorio de componentes y vincúlelo.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

El ejemplo carga este origen JavaScript en `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Hojas de estilo adicionales {#additional-style-sheets}

Algunos de los [!DNL Assets] componentes utilizan la biblioteca de widgets. Para procesarse correctamente en el contexto de contenido, se debe cargar una hoja de estilo adicional. El componente de acción de etiqueta requiere uno más.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Hoja de estilo de Geometrixx {#geometrixx-style-sheet}

Los componentes de página de ejemplo requieren que todos los selectores tengan inicio con `.asseteditor` de `static.css` (`/etc/designs/geometrixx/static.css`). Práctica recomendada: Copie todos los `.asseteditor` selectores en la hoja de estilo y ajuste las reglas como desee.

### FormChooser: Ajustes para recursos eventualmente cargados {#formchooser-adjustments-for-eventually-loaded-resources}

El Editor de recursos utiliza el Selector de formularios, que le permite editar recursos (en este caso, recursos) en la misma página de formulario simplemente agregando un selector de formularios y la ruta del formulario a la dirección URL del recurso.

Por ejemplo:

* Página de formato normal: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Recurso cargado en la página de formulario: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Los controladores de muestra `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) hacen lo siguiente:

* Detectan si se carga un recurso o si se debe mostrar el formulario sin formato.
* Si se carga un recurso, se desactiva el modo WCM, ya que parsys solo se puede editar en una página de formulario sin formato.
* Si se carga un recurso, utiliza su título en lugar del de la página de formulario.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

En la parte HTML, utilice el conjunto de títulos anterior (ya sea un recurso o un título de página):

```html
<title><%= title %></title>
```

## Creación de un componente de campo de formulario sencillo {#creating-a-simple-form-field-component}

En este ejemplo se describe cómo crear un componente que muestre y muestre los metadatos de un recurso cargado.

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo `/apps/geometrixx/components/samplemeta`.
1. Añada `content.xml` con el siguiente fragmento:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Añada `samplemeta.jsp` con el siguiente fragmento:

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Para que el componente esté disponible, hace falta poder editarlo. To make a component editable, in CRXDE Lite, add a node `cq:editConfig` of primary type `cq:EditConfig`. So that you can remove paragraphs, add a multi-value property `cq:actions` with a single value of `DELETE`.

1. Vaya al navegador y, en la página de muestra (por ejemplo, `asseteditor.html`), cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos.

1. En el modo de **edición**, el nuevo componente (por ejemplo, **Metadatos de muestra**) ya está disponible en la barra de tareas (que se encuentra en el grupo **Editor de recursos**). Inserte el componente. Para poder almacenar los metadatos, estos se deben agregar al formulario de metadatos.

## Modificar opciones de metadatos {#modifying-metadata-options}

Puede modificar las Áreas de nombres disponibles en el formulario [de](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)metadatos.

Los metadatos disponibles actualmente se definen en `/libs/dam/options/metadata`:

* El primer nivel dentro de este directorio contiene las Áreas de nombres.
* Los elementos dentro de cada Área de nombres representan metadatos, como resultados en un elemento de artículo local.
* El contenido de metadatos contiene la información del tipo y las opciones de varios valores.

Las opciones se pueden sobrescribir en `/apps/dam/options/metadata`:

1. Copie el directorio de `/libs` a `/apps`.

1. Eliminar, modificar o agregar elementos.

>[!NOTE]
>
>Si agrega nuevas Áreas de nombres, deben estar registradas en su repositorio/CRX. De lo contrario, el envío del formulario de metadatos generará un error.
