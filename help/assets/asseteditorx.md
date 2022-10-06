---
title: Ampliar editor de recursos
description: Obtenga información sobre cómo ampliar las capacidades del Editor de recursos mediante componentes personalizados.
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 11%

---

# Ampliar editor de recursos {#extending-asset-editor}

El Editor de recursos es la página que se abre cuando se hace clic en un recurso que se encuentra a través de Asset Share, lo que permite al usuario editar aspectos del recurso como metadatos, miniaturas, títulos y etiquetas.

La configuración del editor que utiliza los componentes de edición predefinidos se explica en [Creación y configuración de una página del editor de recursos](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

Además de utilizar componentes de editor preexistentes, [!DNL Adobe Experience Manager] los desarrolladores también pueden crear sus propios componentes.

## Crear una plantilla de Editor de recursos {#creating-an-asset-editor-template}

En Geometrixx se incluyen las siguientes páginas de muestra:

* Página de muestra de Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Plantilla de ejemplo: `/apps/geometrixx/templates/asseteditor`
* Componente de página de muestra: `/apps/geometrixx/components/asseteditor`

### Configurar Clientlib {#configuring-clientlib}

[!DNL Assets] los componentes utilizan una extensión de WCM edit clientlib. Los clientlibs suelen cargarse en `init.jsp`.

Comparado con la carga de clientlib predeterminada (en el `init.jsp`), y [!DNL Assets] debe tener lo siguiente:

* La plantilla debe incluir la variable `cq.dam.edit` clientlib (en lugar de `cq.wcm.edit`).

* La clientlib también debe incluirse en el modo WCM desactivado (por ejemplo, cargado en la **publicación**) para poder procesar los predicados, las acciones y las lentes.

En la mayoría de los casos, copiar el ejemplo existente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) debe satisfacer estas necesidades.

### Configurar acciones JS {#configuring-js-actions}

Algunos de los [!DNL Assets] los componentes requieren funciones JS definidas en `component.js`. Copie este archivo en el directorio de componentes y vincúlelo.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

El ejemplo carga este origen JavaScript en `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Hojas de estilo adicionales {#additional-style-sheets}

Algunos de los [!DNL Assets] los componentes utilizan la biblioteca widgets . Para que se represente correctamente en el contexto de contenido, se debe cargar una hoja de estilo adicional. El componente de acción de etiqueta requiere uno más.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Hoja de estilo de Geometrixx {#geometrixx-style-sheet}

Los componentes de la página de muestra requieren que todos los selectores empiecen por `.asseteditor` de `static.css` (`/etc/designs/geometrixx/static.css`). Práctica recomendada: Copiar todo `.asseteditor` a la hoja de estilo y ajuste las reglas como desee.

### Selector de formulario: Ajustes para recursos cargados finalmente {#formchooser-adjustments-for-eventually-loaded-resources}

El Editor de recursos utiliza el Selector de formularios, que le permite editar recursos (en este caso, recursos) en la misma página de formulario simplemente añadiendo un selector de formulario y la ruta del formulario a la dirección URL del recurso.

Por ejemplo:

* Página de formato normal: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Recurso cargado en la página del formulario: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

El ejemplo gestiona en `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) haga lo siguiente:

* Detectan si se carga un recurso o si se debe mostrar el formulario.
* Si se carga un recurso, se desactiva el modo WCM, ya que parsys solo se puede editar en una página de formulario.
* Si se carga un recurso, utiliza su título en lugar del de la página del formulario.

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

En la parte del HTML, utilice el conjunto de títulos anterior (ya sea un recurso o un título de página):

```html
<title><%= title %></title>
```

## Creación de un componente de campo de formulario sencillo {#creating-a-simple-form-field-component}

En este ejemplo se describe cómo crear un componente que muestre y muestre los metadatos de un recurso cargado.

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo: `/apps/geometrixx/components/samplemeta`.
1. Agregar `content.xml` con el siguiente fragmento:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Agregar `samplemeta.jsp` con el siguiente fragmento:

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

1. Para que el componente esté disponible, hace falta poder editarlo. Para que un componente se pueda editar, en CRXDE Lite, agregue un nodo `cq:editConfig` de tipo principal `cq:EditConfig`. Para poder eliminar párrafos, agregue una propiedad de varios valores `cq:actions` con un solo valor de `DELETE`.

1. Vaya al explorador y a la página de muestra (por ejemplo, `asseteditor.html`) cambiar al modo de diseño y activar el nuevo componente para el sistema de párrafos.

1. En el modo de **edición**, el nuevo componente (por ejemplo, **Metadatos de muestra**) ya está disponible en la barra de tareas (que se encuentra en el grupo **Editor de recursos**). Inserte el componente. Para poder almacenar los metadatos, estos se deben agregar al formulario de metadatos.

## Modificación de las opciones de metadatos {#modifying-metadata-options}

Puede modificar las áreas de nombres disponibles en el [formulario de metadatos](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

Los metadatos disponibles actualmente están definidos en `/libs/dam/options/metadata`:

* El primer nivel dentro de este directorio contiene los espacios de nombres.
* Los elementos dentro de cada área de nombres representan un metadato, como los resultados en un elemento de parte local.
* El contenido de los metadatos contiene la información del tipo y las opciones de varios valores.

Las opciones se pueden sobrescribir en `/apps/dam/options/metadata`:

1. Copiar el directorio de `/libs` a `/apps`.

1. Elimine, modifique o agregue elementos.

>[!NOTE]
>
>Si agrega nuevas áreas de nombres, deben estar registradas en su repositorio/CRX. De lo contrario, el envío del formulario de metadatos generará un error.
