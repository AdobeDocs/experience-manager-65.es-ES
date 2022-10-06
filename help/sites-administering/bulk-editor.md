---
title: Editor masivo
seo-title: The Bulk Editor
description: Aprenda a utilizar el Editor por lotes.
seo-description: Learn how to use the Bulk Editor.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# Editor masivo{#the-bulk-editor}

El Editor por lotes permite una edición muy eficaz cuando no se necesita el contexto visual de la página, ya que le permite:

* buscar (y mostrar) contenido de varias páginas; esto se realiza mediante GQL (Google Query Language)
* editar este contenido directamente en el editor por lotes
* guardar los cambios (en las páginas de origen)
* exportar este contenido a un archivo de hoja de cálculo separado por tabulaciones (.tsv)

>[!NOTE]
>
>También puede importar contenido en el repositorio, pero de forma predeterminada esto está deshabilitado para el Editor por lotes como está disponible en el **Herramientas** consola.

En esta sección se describe cómo trabajar con el editor masivo en la **Herramientas** consola. Normalmente, los administradores utilizan el editor por lotes para buscar y editar varios elementos. Para ello, rellene la tabla utilizando una consulta GQL y, a continuación, seleccione los elementos de contenido en los que trabajar. Los autores suelen utilizar el editor por lotes como parte de una aplicación de editor por lotes personalizada a la que se puede acceder mediante el [lista de productos](/help/sites-authoring/default-components.md#productlist) componente.

>[!CAUTION]
>
>Con la variable [desaprobación de la IU clásica](/help/release-notes/deprecated-removed-features.md) en AEM 6.4, el Editor por lotes también ha quedado obsoleto y, por lo tanto, el Adobe no tiene previsto mejorar aún más el Editor por lotes.

## Ejemplo de caso de uso para el Editor por lotes {#example-use-case-for-the-bulk-editor}

Por ejemplo, si necesita todos los nombres y direcciones de correo electrónico de los usuarios que rellenaron un estudio concreto, el Editor por lotes puede proporcionar esa información y exportarla a una hoja de cálculo.

Se incluye un ejemplo para ilustrar un caso de uso de este tipo en el sitio web de Geometrixx:

1. Vaya a la **Asistencia** y luego a la **Satisfacción del servicio al cliente** encuesta.
1. **Editar** el **Inicio de formulario** párrafo. En el cuadro de diálogo, haga clic en la **Avanzadas** expanda la pestaña **Configuración de la acción** y haga clic en **Ver datos...**.

   ![](assets/custsatsurvey.png)

1. El Editor por lotes es totalmente personalizable. sin embargo, en este ejemplo el editor por lotes no permite a los usuarios editar el contenido, sino que solo les permite exportar la información a una hoja de cálculo.

   ![](assets/bulkeditor.png)

## Cómo usar el Editor por lotes {#how-to-use-the-bulk-editor}

El editor por lotes le permite:

* [busque contenido basado en parámetros de consulta, para mostrar propiedades especificadas de los resultados en columnas, para editar este contenido y guardar los cambios](#searching-and-editing-content)
* [para exportar este contenido a una hoja de cálculo separada por tabuladores](#exporting-content)

* [importación de contenido desde una hoja de cálculo separada por tabuladores](#importing-content)

### Búsqueda y edición de contenido {#searching-and-editing-content}

Para utilizar el editor por lotes para editar varios elementos simultáneamente:

1. En el **Herramientas** de la consola, haga clic en **Importadores** para expandirla.
1. Haga doble clic en el botón **Editor por lotes** para abrirlo.
1. Introduzca los requisitos de selección:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Propiedad</td>
  </tr>
  <tr>
   <td>Ruta de acceso raíz</td>
   <td>Indica la ruta raíz que busca el editor en masa.<br /> Por ejemplo, <code>/content/geometrixx/en</code>. El editor masivo busca en todos los nodos secundarios.</td>
  </tr>
  <tr>
   <td>Parámetros de consulta</td>
   <td>Mediante los parámetros GQL, introduzca la cadena de búsqueda que desea que busque el editor por lotes en el repositorio; por ejemplo, <code>type:Page</code> busca todas las páginas en la ruta raíz, <code>text:professional</code> busca todas las páginas que contienen la palabra "profesional", y <code>"jcr:title":English</code> busca todas las páginas que tengan "inglés" como título. Solo puede buscar cadenas.</td>
  </tr>
  <tr>
   <td>Casilla de verificación Modo de contenido</td>
   <td>Active esta casilla de verificación para leer las propiedades dentro de la variable <code>jcr:content</code> subnodo de los resultados de búsqueda si existe. Utilice solo para páginas. Los nombres de propiedades llevan el prefijo <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propiedades / Columnas</td>
   <td>Seleccione las casillas de verificación de las propiedades que desea que devuelva el editor por lotes. Las propiedades que seleccione son los encabezados de columna del panel de resultados. De forma predeterminada, la ruta del nodo se muestra en los resultados.</td>
  </tr>
  <tr>
   <td>Columnas / propiedades personalizadas</td>
   <td>Introduzca cualquier otra propiedad que no aparezca en la lista <strong>Propiedades/Columnas</strong> campo . Estas propiedades personalizadas aparecen en el panel de resultados. Puede agregar varias propiedades con una coma para separar las propiedades. <i>Nota:</i> Si agrega una propiedad personalizada que aún no existe, AEM WCM muestra una celda vacía. Cuando modifica la celda vacía y la guarda, la propiedad se agrega al nodo . La propiedad recién creada debe respetar las restricciones de tipo de nodo y los espacios de nombres de propiedad.</td>
  </tr>
 </tbody>
</table>

Por ejemplo:

![](assets/searchfilter.png)

1. Haga clic en **Buscar**. El Editor por lotes muestra los resultados.
Por ejemplo, todas las páginas que cumplen con los criterios de búsqueda se devuelven y se muestran con las columnas solicitadas.

   ![](assets/chlimage_1-39.png)

1. Haga los cambios que necesite haciendo doble clic en una celda.

   ![](assets/srchresultedit.png)

1. Haga clic en **Guardar** para guardar los cambios (el **Guardar** se activará una vez que haya editado una celda).

   >[!CAUTION]
   >
   >Los cambios que realice aquí se escriben en el contenido del repositorio; por ejemplo, la página a la que se hace referencia en **Ruta**.

#### Parámetros de consulta GQL adicionales {#additional-gql-query-parameters}

* **ruta:** solo buscar nodos debajo de esta ruta. Si especifica más de un término con un prefijo de ruta, solo se considerará el último.
* **tipo:** solo devuelven nodos de los tipos de nodo dados. Esto incluye tipos primarios y mixtos. Puede especificar varios tipos de nodos separados por comas. GQL devolverá nodos que pertenezcan a cualquiera de los tipos especificados.
* **pedido:** ordene el resultado por las propiedades dadas. Puede especificar varios nombres de propiedades separados por comas. Para ordenar el resultado en orden descendente, simplemente anteponga el nombre de la propiedad con un signo menos. Por ejemplo: order:-name. El uso de un signo más devolverá el resultado en orden ascendente, que también es el valor predeterminado.
* **límite:** limita el número de resultados que utilizan un intervalo. Por ejemplo: límite:10.20 Tenga en cuenta que el intervalo está basado en cero, el inicio es inclusivo y el final es exclusivo. También puede especificar un intervalo de apertura:limit:10. o límite:..20 Si se omiten los puntos y se especifica un solo valor, GQL devolverá como máximo este número de resultados. Por ejemplo, limit:10 (devuelve los primeros 10 resultados)

### Exportación de contenido {#exporting-content}

Es posible que necesite exportar contenido y realizar cambios en él en una hoja de cálculo de Excel. Por ejemplo, es posible que desee exportar una lista de correo y cambiar el código de área de todos los números de teléfono enumerados directamente en Excel, agregar líneas adicionales, etc.

Para exportar contenido:

1. Busque contenido como se describe en [Búsqueda y edición de contenido](#searching-and-editing-content).
1. Haga clic en **Exportar** para exportar los cambios en una hoja de cálculo de Excel separada por tabulaciones. AEM WCM le pregunta dónde desea descargar el archivo.

   >[!NOTE]
   >
   >De forma predeterminada, los cambios se codifican en [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (también conocido como CP-1252). Puede marcar UTF-8 para exportar los cambios en UTF-8.

   ![](assets/srchrsesultexport.png)

1. Seleccione la ubicación y confirme que desea descargar el archivo.
1. Después de descargar el archivo, puede abrirlo desde el programa de hojas de cálculo, por ejemplo, Microsoft Excel. El programa de hojas de cálculo importa el archivo y lo convierte a un formato de hoja de cálculo.

   ![](assets/exportinexcel.png)

### Importación de contenido {#importing-content}

De forma predeterminada, la funcionalidad de importación está oculta al abrir el Editor por lotes. Simplemente añadir el parámetro `hib=false` en la dirección URL, se mostrará la variable **Importar** en la página Editor por lotes. Puede importar contenido desde cualquier pestaña separada ( `.tsv`). Para que la importación funcione correctamente, los encabezados de columna (primera fila de celdas) deben coincidir con los encabezados de columna de la tabla a la que está importando.

>[!NOTE]
>
>Cuando vuelva a importar contenido, borre cualquier contenido anterior para esos nodos. Tenga cuidado de no sobrescribir información importante.

Para importar contenido:

1. Abra el Editor por lotes.
1. Agregar `?hib=false` a la dirección URL, por ejemplo:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Haga clic en **Importar**.
1. Seleccione el `.tsv` archivo. Los datos se importan en el repositorio.
