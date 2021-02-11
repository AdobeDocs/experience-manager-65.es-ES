---
title: Desarrollo del editor en masa
seo-title: Desarrollo del editor en masa
description: El etiquetado permite categorizar y organizar el contenido
seo-description: El etiquetado permite categorizar y organizar el contenido
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 1%

---


# Desarrollo del Editor masivo{#developing-the-bulk-editor}

En esta sección se describe cómo desarrollar la herramienta de edición masiva y cómo extender el componente de Lista del producto, que se basa en el editor masivo.

## Parámetros de Consulta del Editor masivo {#bulk-editor-query-parameters}

Al trabajar con el editor masivo, hay varios parámetros de consulta que puede agregar a la URL para llamar al editor masivo con una configuración específica. Si desea que el editor masivo siempre se utilice con una configuración determinada, por ejemplo, como en el componente Lista de productos, deberá modificar bulkeditor.jsp (ubicado en /libs/wcm/core/components/bulkeditor) o crear un componente con la configuración específica. Los cambios realizados con parámetros de consulta no son permanentes.

Por ejemplo, si escribe lo siguiente en la dirección URL del explorador:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

el editor masivo se muestra sin el campo **Ruta de raíz** como hrp=true oculta el campo. Con el parámetro hrp=false, se muestra el campo (el valor predeterminado).

A continuación se muestra una lista de los parámetros de consulta del editor masivo:

>[!NOTE]
>
>Cada parámetro puede tener un nombre largo y corto. Por ejemplo: el nombre largo de la ruta raíz de búsqueda es `rootPath`, el corto es `rp`. Si no se define el nombre largo, se lee el corto de la solicitud.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Parámetro</p> <p>(nombre largo/nombre corto)<br /> </p> </td>
   <td> Tipo <br /> </td>
   <td> Descripción <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> Cadena </td>
   <td> ruta raíz de búsqueda</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Cadena</td>
   <td> consulta de búsqueda</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, el modo de contenido está habilitado<br /> </td>
  </tr>
  <tr>
   <td> ixValue / cv<br /> </td>
   <td> Cadena[]</td>
   <td> propiedades de búsqueda (valores marcados de olesSelection mostrados como casillas de verificación)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> Cadena[]</td>
   <td> propiedades de búsqueda extra (se muestran en un campo de texto separado por comas)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, la consulta se realiza al cargar la página<br /> </td>
  </tr>
  <tr>
   <td> olesSelection / cs<br /> </td>
   <td> Cadena[]</td>
   <td> selección de propiedades de búsqueda (se muestran como casillas de verificación)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, muestra solamente la cuadrícula y no el panel de búsqueda <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> Booleano</td>
   <td> cuando el valor es true, el panel de búsqueda se contrae al cargarse</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de ruta raíz</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de consulta</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de modo de contenido</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de selección de columnas</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de columnas adicionales</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de búsqueda</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> Booleano</td>
   <td> cuando el valor es true, oculta el botón Guardar</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de exportación</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de importación</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el texto del número de resultados de búsqueda de cuadrícula</td>
  </tr>
  <tr>
   <td> hideInsertButton/hinsertb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de inserción de cuadrícula</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de eliminación de cuadrícula</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> Booleano</td>
   <td> cuando es true, oculta la columna "ruta" de la cuadrícula</td>
  </tr>
 </tbody>
</table>

### Desarrollo de un componente basado en un editor masivo: el componente Lista del producto {#developing-a-bulk-editor-based-component-the-product-list-component}

Esta sección proporciona información general sobre cómo utilizar el editor masivo y proporciona una descripción del componente de Geometrixx existente basada en el editor masivo: el componente Lista del producto.

El componente Lista del producto permite a los usuarios mostrar y editar una tabla de datos. Por ejemplo, puede utilizar el componente Lista del producto para representar los productos de un catálogo. La información se presenta en una tabla HTML estándar y cualquier edición se realiza en el cuadro de diálogo **Editar**, que contiene un widget de Editor masivo. (Este Editor masivo es exactamente el mismo que el accesible en /etc/importers/bulkeditor.html o a través del menú Herramientas). El componente Lista del producto se ha configurado para la funcionalidad específica del editor masivo. Se pueden configurar todas las partes del editor masivo (o los componentes derivados del editor masivo).

Con el editor masivo, puede agregar, modificar, eliminar, filtrar y exportar las filas, guardar las modificaciones e importar un conjunto de filas. Cada fila se almacena como nodo en la propia instancia del componente Lista del producto. Cada celda es una propiedad de cada nodo. Se trata de una opción de diseño que se puede cambiar fácilmente; por ejemplo, se pueden almacenar nodos en otro lugar del repositorio. La función del servlet de consulta es devolver la lista de los nodos que se van a mostrar; la ruta de búsqueda se define como una instancia de Lista de productos.

El código fuente del componente Lista del producto está disponible en el repositorio en /apps/geometrixx/components/productlist y consta de varias partes, como todos los componentes AEM:

* Representación HTML: el procesamiento se realiza en un archivo JSP (/apps/geometrixx/components/productlist/productlist.jsp). El JSP lee los subnodos del componente de Lista de productos actual y muestra cada uno de ellos como una fila de una tabla HTML.
* Cuadro de diálogo Editar, donde se define la configuración del Editor masivo. Configure el cuadro de diálogo para que coincida con las necesidades del componente: columnas disponibles y posibles acciones realizadas en la cuadrícula o en la búsqueda. Consulte [propiedades de configuración del editor masivo](#bulk-editor-configuration-properties) para obtener información sobre todas las propiedades de configuración.

Esta es una representación XML de los subnodos de cuadro de diálogo:

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Propiedades de configuración del editor masivo {#bulk-editor-configuration-properties}

Se pueden configurar todas las partes del editor masivo. La siguiente tabla lista todas las propiedades de configuración del editor masivo.

<table>
 <tbody>
  <tr>
   <td>Nombre de la propiedad </td>
   <td>Definición</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Buscar ruta raíz</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Consulta de búsqueda</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>True para activar el modo de contenido: las propiedades se leen en el nodo jcr:content y no en el nodo de resultados de búsqueda</td>
  </tr>
  <tr>
   <td>ixValue</td>
   <td>Propiedades de búsqueda (valores marcados de los protocolosSelección mostrados como casillas de verificación)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Propiedades de búsqueda adicional (se muestran en una coma de campo de texto separada)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True para realizar consultas al cargar la página</td>
  </tr>
  <tr>
   <td>olesSelection</td>
   <td>Selección de propiedades de búsqueda (se muestran como casillas de verificación)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True para mostrar solo la cuadrícula y no el panel de búsqueda (no olvide establecer el valor de initialSearch en true)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True para contraer el panel de búsqueda de forma predeterminada</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Ocultar campo de ruta raíz</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>Ocultar campo de consulta</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Ocultar campo de modo de contenido</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Ocultar campo de selección de protocolos</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Ocultar campo de protocolos extra</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Ocultar botón de búsqueda</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Ocultar botón Guardar</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Ocultar botón de exportación</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Ocultar botón de importación</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Ocultar texto del número de resultados de búsqueda de cuadrícula</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Ocultar botón de inserción de cuadrícula</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Ocultar botón de eliminación de cuadrícula</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Ocultar la columna "ruta" de la cuadrícula</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Ruta al servlet de consulta</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Ruta para exportar servlet</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>Ruta para importar servlet</td>
  </tr>
  <tr>
   <td>insertResourceType</td>
   <td>Tipo de recurso agregado al nodo cuando se inserta una fila</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Configuración del widget de botón Guardar</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Configuración del widget de botón de búsqueda</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Configuración del widget de botón de exportación</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Configuración del widget de botón de importación</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configuración del widget del panel de búsqueda</td>
  </tr>
  <tr>
   <td>cuadrícula</td>
   <td>Configuración del widget de cuadrícula</td>
  </tr>
  <tr>
   <td>store</td>
   <td>Configuración de almacenamiento</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configuración del modelo de columna de cuadrícula</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>config del widget de rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>configuración del widget queryParams</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>configuración de la utilidad contentMode</td>
  </tr>
  <tr>
   <td>olesSelectionInput</td>
   <td>config del widget de la selección de protocolos</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>Configuración del widget extraCols</td>
  </tr>
  <tr>
   <td>olesMetadata</td>
   <td>Configuración de metadatos de columna. Las propiedades posibles son (aplicadas a todas las celdas de la columna): <br />
    <ul>
     <li>cellStyle: estilo HTML </li>
     <li>cellCls: clase css </li>
     <li>readOnly: true para no poder cambiar el valor </li>
     <li>casilla de verificación: true para definir todas las celdas de la columna como casillas de verificación (valores true/false) </li>
     <li>forcePosition: valor entero para especificar dónde se debe colocar la columna en la cuadrícula (entre 0 y el número de columnas-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuración de metadatos de columnas {#columns-metadata-configuration}

Puede configurar para cada columna:

* propiedades de visualización: estilo HTML, clase CSS y solo lectura

* una casilla de verificación
* una posición forzada

CSS y columnas de solo lectura

El editor masivo tiene tres configuraciones de columna:

* Nombre de clase CSS de celda (cellCls): un nombre de clase CSS que se agrega a cada celda de la columna configurada.
* Estilo de celda (cellStyle): un estilo HTML que se agrega a cada celda de la columna configurada.
* Sólo lectura (readOnly): sólo lectura se establece para cada celda de la columna configurada.

La configuración debe definirse como la siguiente:

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

El siguiente ejemplo se encuentra en el componente de lista de productos (/apps/geometrixx/components/productlist/dialog/items/editor/olesMetadata):

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**Casilla de verificación**

Si la propiedad de configuración de la casilla de verificación está establecida en true, todas las celdas de la columna se procesan como casillas de verificación. Una casilla de verificación envía **true** al servidor Guardar servlet, **false** en caso contrario. En el menú de encabezado, también puede **seleccionar todo** o **seleccionar ninguno**. Estas opciones se activan si el encabezado seleccionado es el encabezado de una columna de casilla de verificación.

En el ejemplo anterior, la columna de selección solo contiene casillas de verificación como checkboxes=&quot;true&quot;.

**Posición forzada**

Los metadatos de posición forzada forcePosition permiten especificar dónde se coloca la columna en la cuadrícula: 0 es el primer lugar y &lt;número de columnas>-1 es la última posición. Se ignora cualquier otro valor.

En el ejemplo anterior, la columna de selección es la primera columna como forcePosition=&quot;0&quot;.

### Servlet de consulta {#query-servlet}

De forma predeterminada, el servlet de Consulta se encuentra en `/libs/wcm/core/components/bulkeditor/json.java`. Puede configurar otra ruta para recuperar los datos.

El servlet de Consulta funciona de la siguiente manera: recibe una consulta GQL y las columnas que se van a devolver, calcula los resultados y envía los resultados al editor masivo como flujo JSON.

En el caso del componente Lista del producto, los dos parámetros enviados al servlet de Consulta son los siguientes:

* consulta: &quot;path:/content/geometrixx/es/customers/jcr:content/par/product-list Cubo&quot;
* Todos: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

y el flujo JSON devuelto es el siguiente:

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

Cada visita individual corresponde a un nodo y sus propiedades, y se muestra como una fila en la cuadrícula.

Puede extender el servlet de Consulta para devolver un modelo de herencia complejo o nodos de retorno almacenados en un lugar lógico específico. El servlet de Consulta puede utilizarse para realizar cualquier tipo de cálculo complejo. A continuación, la cuadrícula puede mostrar filas que son acumuladas de varios nodos en el repositorio. En ese caso, la modificación y el guardado de estas filas deben ser administrados por el servlet Guardar.

### Guardar servlet {#save-servlet}

En la configuración predeterminada del editor masivo, cada fila es un nodo y la ruta de este nodo se almacena en el registro de fila. El editor masivo mantiene el vínculo entre la fila y el nodo a través de la ruta jcr. Cuando un usuario edita la cuadrícula, se genera una lista de todas las modificaciones. Cuando un usuario hace clic en **Guardar**, se envía una consulta de POST a cada ruta con los valores de propiedades actualizados. Esta es la base del concepto Sling y funciona bien si cada celda es una propiedad del nodo. Sin embargo, si el servlet de Consulta se implementa para realizar el cálculo de herencia, este modelo no puede funcionar como una propiedad devuelta por el servlet de Consulta puede heredarse de otro nodo.

El concepto de servlet Guardar es que las modificaciones no se publican directamente en cada nodo, sino que se publican en un servlet que realiza el trabajo de guardado. Esto proporciona a este servlet la posibilidad de analizar las modificaciones y guardar las propiedades en el nodo derecho.

Cada propiedad actualizada se envía al servlet en el siguiente formato:

* Nombre del parámetro: &lt;jcr path>/&lt;nombre de propiedad>

   Ejemplo: /content/geometrixx/es/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valor: &lt;valor>

   Ejemplo: 12123

El servlet necesita saber dónde se almacena la propiedad catalogCode.

La implementación predeterminada del servlet Guardar está disponible en /libs/wcm/bulkeditor/save/POST.jsp y se utiliza en el componente Lista del producto. Toma todos los parámetros de la solicitud (con un formato &lt;jcr path>/&lt;property name>) y escribe las propiedades en los nodos mediante la API de JCR. También crea nodos si no existen (filas insertadas en la cuadrícula).

El código predeterminado no debe utilizarse tal cual, ya que vuelve a implementar lo que hace el servidor de forma nativa (un POST en &lt;jcr path>/&lt;property name>) y, por lo tanto, es sólo un buen punto de partida para crear un servlet Guardar que administrará un modelo de herencia de propiedades.
