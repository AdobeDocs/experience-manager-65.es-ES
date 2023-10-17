---
title: Editor por lotes
description: Aprenda a utilizar el Editor por lotes para una edición eficaz cuando el contexto de la página visual no sea necesario.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 1%

---


# Editor por lotes{#the-bulk-editor}

El editor en bloque permite una edición eficaz cuando el contexto de la página visual no es necesario, ya que le permite:

* buscar (y mostrar) contenido de varias páginas; esto se hace con GQL (Google Query Language)
* edite este contenido directamente en el editor en bloque
* guardar los cambios (en las páginas de origen)
* exportar este contenido a un archivo de hoja de cálculo (.tsv) separado por tabuladores

>[!NOTE]
>
>También puede importar contenido en el repositorio, pero de forma predeterminada está desactivado para el Editor por lotes como está disponible en la **Herramientas** consola.

En esta sección se describe cómo trabajar con el editor en masa en **Herramientas** consola. Normalmente, los administradores utilizan el Editor por lotes para buscar y editar varios elementos. Para ello, rellene la tabla con una consulta GQL y, a continuación, seleccione los elementos de contenido en los que desea trabajar. Los autores suelen utilizar el Editor por lotes como parte de una aplicación de editor por lotes personalizada, accesible a través del [lista de productos](/help/sites-authoring/default-components.md#productlist) componente.

>[!CAUTION]
>
>Con el [desaprobación de la IU clásica](/help/release-notes/deprecated-removed-features.md) AEM En la versión 6.4, el editor en bloque también se ha quedado obsoleto y, por lo tanto, Adobe no tiene previsto mejorar aún más el editor en bloque.

## Ejemplo de caso de uso para el editor en bloque {#example-use-case-for-the-bulk-editor}

Por ejemplo, si necesita todos los nombres y direcciones de correo electrónico de los usuarios que han rellenado una encuesta determinada, el editor en masa puede proporcionar esa información y puede exportarla a una hoja de cálculo.

En el sitio web del Geometrixx se incluye un ejemplo que ilustra un caso de uso de este tipo:

1. Vaya a **Asistencia** y luego a la página **Satisfacción del servicio al cliente** encuesta.
1. **Editar** el **Inicio de formulario** párrafo. En el cuadro de diálogo, haga clic en **Avanzadas** , expanda la pestaña **Configuración de acción**, luego haga clic en **Ver datos...**.

   ![Ejemplo de encuesta de satisfacción del cliente](assets/custsatsurvey.png)

1. El editor en bloque es totalmente personalizable, aunque en este ejemplo el editor en bloque no permite a los usuarios editar el contenido, sino que solo les permite exportar la información a una hoja de cálculo.

   ![Consola de editor en lotes](assets/bulkeditor.png)

## Cómo utilizar el editor en masa {#how-to-use-the-bulk-editor}

El Editor por lotes le permite:

* [buscar contenido basado en parámetros de consulta, para mostrar propiedades especificadas de los resultados en columnas, para editar este contenido y guardar los cambios](#searching-and-editing-content)
* [para exportar este contenido a una hoja de cálculo separada por tabulaciones](#exporting-content)

* [para importar contenido desde una hoja de cálculo separada por tabulaciones](#importing-content)

### Búsqueda y edición de contenido {#searching-and-editing-content}

Para utilizar el Editor por lotes para editar varios elementos a la vez:

1. En el **Herramientas** consola, haga clic en **importadores** para expandirla.
1. Haga doble clic en **Editor por lotes**.
1. Introduzca los requisitos de selección:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Propiedad</td>
  </tr>
  <tr>
   <td>Ruta de acceso raíz</td>
   <td>Indica la ruta raíz que busca el editor en masa.<br /> Por ejemplo, <code>/content/geometrixx/en</code>. El editor en lotes busca en todos los nodos secundarios.</td>
  </tr>
  <tr>
   <td>Parámetros de consulta</td>
   <td>Con los parámetros GQL, introduzca la cadena de búsqueda que desea que busque el Editor por lotes en el repositorio. Por ejemplo, <code>type:Page</code> busca todas las páginas de la ruta raíz, <code>text:professional</code> busca todas las páginas que contengan la palabra "profesional", y <code>"jcr:title":English</code> busca todas las páginas que tengan el título en "inglés". Solo puede buscar cadenas.</td>
  </tr>
  <tr>
   <td>Casilla Modo de contenido</td>
   <td>Active esta casilla de verificación para poder leer las propiedades dentro del <code>jcr:content</code> subnodo de los resultados de búsqueda si existe. Se utiliza solo para páginas. Los nombres de propiedad llevan el prefijo <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propiedades / Columnas</td>
   <td>Seleccione las casillas de verificación de las propiedades que desea que devuelva el Editor por lotes. Las propiedades que seleccione son los encabezados de columna del panel de resultados. De forma predeterminada, la ruta del nodo se muestra en los resultados.</td>
  </tr>
  <tr>
   <td>Columnas / propiedades personalizadas</td>
   <td>Introduzca cualquier otra propiedad que no aparezca en la lista de <strong>Propiedades/Columnas</strong> field. Estas propiedades personalizadas aparecen en el panel de resultados. Puede agregar varias propiedades utilizando una coma para separar las propiedades. <i>Nota:</i> AEM Si agrega una propiedad personalizada que aún no existe, WCM muestra una celda vacía en la pantalla de WCM, en la que se muestra el nombre de la propiedad que aún no existe. Al modificar la celda vacía y guardarla, la propiedad se agrega al nodo. La propiedad recién creada debe respetar las restricciones de tipo de nodo y los espacios de nombres de propiedad.</td>
  </tr>
 </tbody>
</table>

Por ejemplo:

![Opciones de filtro del editor en lotes](assets/searchfilter.png)

1. Clic **Buscar**. El Editor por lotes muestra los resultados.
En el ejemplo anterior, todas las páginas que cumplen los criterios de búsqueda se devuelven y se muestran con las columnas solicitadas.

   ![Resultados del editor en lotes](assets/chlimage_1-39.png)

1. Haga doble clic en una celda para poder realizar cualquier cambio.

   ![Edición en lotes](assets/srchresultedit.png)

1. Clic **Guardar** para guardar los cambios (la variable **Guardar** se activa después de editar una celda).

   >[!CAUTION]
   >
   >Los cambios que realice aquí se escriben en el contenido del repositorio; por ejemplo, la página a la que se hace referencia en **Ruta**.

#### Parámetros de consulta GQL adicionales {#additional-gql-query-parameters}

* **ruta:** solo buscar nodos debajo de esta ruta. Si especifica más de un término con un prefijo de ruta, solo se tendrá en cuenta el último.
* **tipo:** solo devuelven nodos del tipo de nodo dado. Esto incluye los tipos principal y de mezcla. Puede especificar varios tipos de nodos separados por comas. GQL devuelve nodos que son de cualquiera de los tipos especificados.
* **pedido:** ordene el resultado según las propiedades dadas. Puede especificar varios nombres de propiedades separados por comas. Para ordenar el resultado en orden descendente, simplemente anteponga un signo menos al nombre de la propiedad. Por ejemplo, order:-name. El uso de un signo más devuelve el resultado en orden ascendente, que también es el valor predeterminado.
* **límite:** limita el número de resultados mediante un intervalo. Por ejemplo, límite:10..20 El intervalo está basado en cero, inicio es inclusivo y fin es exclusivo. También puede especificar un intervalo abierto:limit:10.. o límite:..20 Si se omiten los puntos y solo se especifica un valor, GQL devuelve como máximo este número de resultados. Por ejemplo, limit:10 (devuelve los diez primeros resultados).

### Exportación de contenido {#exporting-content}

Si es necesario, exporte el contenido a una hoja de cálculo de Excel para realizar cualquier cambio. Por ejemplo, puede exportar una lista de correo y cambiar el código de área de todos los números de teléfono enumerados directamente en Excel, o agregar líneas adicionales.

Para exportar contenido:

1. Busque contenido como se describe en [Búsqueda y edición de contenido](#searching-and-editing-content).
1. Clic **Exportar** para poder exportar los cambios a una hoja de cálculo de Excel separada por tabulaciones. AEM WCM le preguntará dónde desea descargar el archivo.

   >[!NOTE]
   >
   >De forma predeterminada, los cambios se codifican en [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (también conocido como CP-1252). Puede marcar UTF-8 para exportar los cambios en UTF-8.

   ![Exportación de resultados](assets/srchrsesultexport.png)

1. Seleccione la ubicación y confirme que desea descargar el archivo.
1. Después de descargar el archivo, puede abrirlo desde el programa de hoja de cálculo, por ejemplo, Microsoft® Excel. El programa de hoja de cálculo importa el archivo y lo convierte a un formato de hoja de cálculo.

   ![Resultados exportados en una hoja de cálculo](assets/exportinexcel.png)

### Importación de contenido {#importing-content}

De forma predeterminada, la funcionalidad de importación está oculta al abrir el Editor por lotes. Simplemente añadiendo el parámetro `hib=false` a la dirección URL muestra el **Importar** en la página Editor por lotes. Puede importar contenido desde cualquier archivo separado por tabulaciones ( `.tsv`) archivo. Para que la importación funcione correctamente, los encabezados de columna (primera fila de celdas) deben coincidir con los encabezados de columna de la tabla a la que se va a importar.

>[!NOTE]
>
>Al volver a importar contenido, se borra cualquier contenido anterior de esos nodos. Tenga cuidado de no sobrescribir información importante.

Para importar contenido:

1. Abra el Editor por lotes.
1. Añadir `?hib=false` a la dirección URL, por ejemplo:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Haga clic en **Importar**.
1. Seleccione el `.tsv` archivo. Los datos se importan en el repositorio.
