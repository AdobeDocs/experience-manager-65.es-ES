---
title: Editor masivo
seo-title: Editor masivo
description: Aprenda a utilizar el Editor masivo.
seo-description: Aprenda a utilizar el Editor masivo.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
translation-type: tm+mt
source-git-commit: 743512254850698a32fd77151e2278dd8cc4ce7d

---


# Editor masivo{#the-bulk-editor}

El Editor en masa permite una edición muy eficaz cuando el contexto visual de la página no es necesario, ya que le permite:

* buscar (y mostrar) contenido de varias páginas; esto se realiza con GQL (Google Query Language)
* editar este contenido directamente en el editor masivo
* guardar los cambios (en las páginas de origen)
* exportar este contenido a un archivo de hoja de cálculo separado por tabuladores (.tsv)

>[!NOTE]
>
>También puede importar contenido en el repositorio, pero de forma predeterminada está deshabilitado para el Editor masivo como está disponible en la consola **Herramientas** .

En esta sección se describe cómo trabajar con el editor masivo en la consola **Herramientas** . Normalmente, los administradores utilizan el editor masivo para buscar y editar varios elementos. Esto se realiza rellenando la tabla con una consulta GQL y seleccionando los elementos de contenido en los que trabajar. Los autores suelen utilizar el editor masivo como parte de una aplicación de editor masivo personalizada a la que se puede acceder a través del componente de listado [de](/help/sites-authoring/default-components.md#productlist) productos.

>[!CAUTION]
>
>Con la [desaprobación de la IU](/help/release-notes/deprecated-removed-features.md) clásica en AEM 6.4, el Editor masivo también se ha desaprobado y, por lo tanto, Adobe no tiene pensado mejorar aún más el Editor masivo.

## Ejemplo de caso de uso para el Editor masivo {#example-use-case-for-the-bulk-editor}

Por ejemplo: si necesita todos los nombres y direcciones de correo electrónico de los usuarios que completaron un estudio en particular, el Editor masivo puede proporcionar esa información y puede exportarla a una hoja de cálculo.

En el sitio web de Geometrixx se incluye un ejemplo para ilustrar este caso de uso:

1. Vaya a la página **Asistencia** y, a continuación, a la encuesta de satisfacción **del servicio** al cliente.
1. **Edite** el párrafo **Inicio de formulario** . **En el cuadro de diálogo, haga clic en la ficha** Avanzadas **, expanda Configuración** de **acción y, a continuación, haga clic en** Ver datos... .

   ![](assets/custsatsurvey.png)

1. El Editor masivo es totalmente personalizable. Sin embargo, en este ejemplo el editor masivo no permite que los usuarios editen el contenido, pero solo les permite exportar la información a una hoja de cálculo.

   ![](assets/bulkeditor.png)

## Cómo utilizar el Editor masivo {#how-to-use-the-bulk-editor}

El editor masivo le permite:

* [buscar contenido basado en parámetros de consulta, para mostrar las propiedades especificadas de los resultados en columnas, para editar este contenido y guardar los cambios](#searching-and-editing-content)
* [para exportar este contenido a una hoja de cálculo separada por tabuladores](#exporting-content)

* [para importar contenido desde una hoja de cálculo separada por tabuladores](#importing-content)

### Búsqueda y edición de contenido {#searching-and-editing-content}

Para utilizar el editor masivo para editar varios elementos simultáneamente:

1. En la consola **Herramientas** , haga clic en la carpeta **Importadores** para expandirla.
1. Haga doble clic en el Editor **masivo** para abrirlo.
1. Especifique los requisitos de selección:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Propiedad</td>
  </tr>
  <tr>
   <td>Ruta de acceso raíz</td>
   <td>Indica la ruta raíz que busca el editor masivo.<br /> Por ejemplo, <code>/content/geometrixx/en</code>. El editor masivo busca en todos los nodos secundarios.</td>
  </tr>
  <tr>
   <td>Parámetros de consulta</td>
   <td>Mediante los parámetros de GQL, introduzca la cadena de búsqueda que desea que busque el editor masivo en el repositorio; por ejemplo: <code>type:Page</code> busca todas las páginas de la ruta raíz, busca todas las páginas que tengan la palabra "profesional" en ellas y busca todas las páginas que <code>text:professional</code> <code>"jcr:title":English</code> tengan el título "inglés". Solo puede buscar cadenas.</td>
  </tr>
  <tr>
   <td>Casilla de verificación Modo de contenido</td>
   <td>Seleccione esta casilla de verificación para leer las propiedades dentro del <code>jcr:content</code> subnodo de los resultados de búsqueda, si existe. Se utiliza solo para páginas. Los nombres de propiedad llevan el prefijo <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propiedades / Columnas</td>
   <td>Seleccione las casillas de verificación de las propiedades que desea que devuelva el editor por lotes. Las propiedades que seleccione son los encabezados de columna en el panel de resultados. De forma predeterminada, la ruta del nodo se muestra en los resultados.</td>
  </tr>
  <tr>
   <td>Columnas / propiedades personalizadas</td>
   <td>Introduzca cualquier otra propiedad que no aparezca en el campo <strong>Propiedades/Columnas</strong> . Estas propiedades personalizadas aparecen en el panel de resultados. Puede agregar varias propiedades mediante una coma para separar las propiedades. <i></i> Nota: Si agrega una propiedad personalizada que aún no existe, AEM WCM muestra una celda vacía. Cuando se modifica la celda vacía y se guarda, la propiedad se agrega al nodo. La propiedad recién creada debe respetar las restricciones de tipo de nodo y los espacios de nombres de propiedad.</td>
  </tr>
 </tbody>
</table>

Por ejemplo:

![](assets/searchfilter.png)

1. Haga clic en **Buscar**. El Editor masivo muestra los resultados.
Para el ejemplo anterior, se devuelven todas las páginas que cumplen los criterios de búsqueda y se muestran con las columnas solicitadas.

   ![](assets/chlimage_1-39.png)

1. Haga doble clic en una celda para realizar los cambios que necesite.

   ![](assets/srchresultedit.png)

1. Haga clic en **Guardar** para guardar los cambios (el botón **Guardar** se activará una vez editada la celda).

   >[!CAUTION]
   >
   >Los cambios que realice aquí se escribirán en el contenido del repositorio; por ejemplo, la página a la que se hace referencia en **Ruta**.

#### Parámetros de consulta GQL adicionales {#additional-gql-query-parameters}

* **** path: solo los nodos de búsqueda situados debajo de esta ruta. Si especifica más de un término con un prefijo de ruta, solo se considerará el último.
* **** type: solo los nodos de retorno de los tipos de nodo dados. Esto incluye tanto tipos primarios como mixtos. Puede especificar varios tipos de nodos separados por comas. GQL devolverá nodos que sean de cualquiera de los tipos especificados.
* **** order: ordene el resultado según las propiedades especificadas. Puede especificar varios nombres de propiedades separados por comas. Para ordenar el resultado en orden descendente, simplemente anteponga el nombre de la propiedad con un signo menos. Por ejemplo: order:-name. El uso de un signo más devolverá el resultado en orden ascendente, que también es el valor predeterminado.
* **** límite: limita el número de resultados mediante un intervalo. Por ejemplo: limit:10..20 Tenga en cuenta que el intervalo está basado en cero, el inicio es inclusivo y el final es exclusivo. También puede especificar un intervalo abierto:limit:10. o límite:..20 Si se omiten los puntos y se especifica un solo valor, GQL devolverá como máximo este número de resultados. Por ejemplo, limit:10 (devolverá los primeros 10 resultados)

### Exportación de contenido {#exporting-content}

Es posible que necesite exportar contenido y realizar cambios en él en una hoja de cálculo de Excel. Por ejemplo, puede que desee exportar una lista de correo y cambiar el código de área de todos los números de teléfono enumerados directamente en Excel, agregar líneas adicionales, etc.

Para exportar contenido:

1. Busque contenido como se describe en [Búsqueda y edición de contenido](#searching-and-editing-content).
1. Haga clic en **Exportar** para exportar los cambios a una hoja de cálculo de Excel separada por tabuladores. AEM WCM le pregunta dónde desea descargar el archivo.

   >[!NOTE]
   >
   >De forma predeterminada, los cambios se codifican en [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (también conocido como CP-1252). Puede marcar UTF-8 para exportar los cambios en UTF-8.

   ![](assets/srchrsesultexport.png)

1. Seleccione la ubicación y confirme que desea descargar el archivo.
1. Después de descargar el archivo, puede abrirlo desde su programa de hojas de cálculo, por ejemplo, Microsoft Excel. El programa de hoja de cálculo importa el archivo y lo convierte en un formato de hoja de cálculo.

   ![](assets/exportinexcel.png)

### Importación de contenido {#importing-content}

De forma predeterminada, la funcionalidad de importación se oculta al abrir el Editor masivo. Al agregar el parámetro `hib=false` a la dirección URL, se mostrará el botón **Importar** en la página Editor masivo. Puede importar contenido desde cualquier archivo separado por tabuladores ( `.tsv`). Para que la importación funcione correctamente, los encabezados de columna (primera fila de celdas) deben coincidir con los encabezados de columna de la tabla a la que está importando.

>[!NOTE]
>
>Al volver a importar contenido, borra cualquier contenido anterior para esos nodos. Tenga cuidado de no sobrescribir información importante.

Para importar contenido:

1. Abra el Editor masivo.
1. Agregar `?hib=false` a la dirección URL, por ejemplo:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Haga clic en **Importar**.
1. Select the `.tsv` file. Los datos se importan en el repositorio.