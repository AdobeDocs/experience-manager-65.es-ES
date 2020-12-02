---
title: Búsqueda de formularios y recursos
seo-title: Búsqueda de formularios y recursos
description: Puede buscar formularios y recursos en la instancia de AEM mediante AEM búsqueda. La búsqueda básica y avanzada le permite localizar rápidamente sus recursos.
seo-description: Puede buscar formularios y recursos en la instancia de AEM mediante AEM búsqueda. La búsqueda básica y avanzada le permite localizar rápidamente sus recursos.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---


# Búsqueda de formularios y recursos{#searching-for-forms-and-assets}

Puede buscar los formularios o recursos de formulario mediante una cadena de texto o una cadena de texto junto con los comodines. También puede limitar la búsqueda utilizando los criterios disponibles en varias categorías del panel Buscar.

Cuando selecciona uno o más criterios y también especifica una cadena de texto, la intersección del texto y los criterios se devuelven como resultados de búsqueda. Los resultados de la búsqueda son tan buenos como los metadatos del formulario y el recurso proporcionados.

Haga clic en ![aem6forms_search](assets/aem6forms_search.png) para mostrar u ocultar el panel de búsqueda.

## Búsqueda básica {#basic-search}

Una búsqueda básica es la búsqueda predeterminada, ejecutada sin especificar ningún filtros. AEM Forms realiza una búsqueda de texto completo en las propiedades de metadatos.

Para ejecutar una búsqueda básica, introduzca la consulta de búsqueda en el campo de texto y pulse en return. También puede introducir el carácter comodín (*) para que coincida con cualquier número de caracteres.

Adobe Experience Manager busca el texto introducido en las propiedades de metadatos y devuelve los resultados correspondientes. Si escribe más de una palabra, la operación de búsqueda coincidirá con el texto completo para la búsqueda.

Tenga en cuenta los siguientes puntos sobre la búsqueda básica:

* La búsqueda se lleva a cabo utilizando las propiedades de metadatos del formulario y del recurso.
* Si escribe más de una palabra, la operación de búsqueda coincidirá con el texto completo para la búsqueda.
* La búsqueda no distingue entre mayúsculas y minúsculas. Por ejemplo, cuando escribe `geometrixx`, los recursos con títulos `Geometrixx`, `GEOMETRIXX` y `GeoMetRixx` se muestran en los resultados de la búsqueda.

* No se admiten las coincidencias parciales de una palabra. Para buscar mediante cadenas parciales, utilice el carácter comodín *. Sin embargo, si la consulta de búsqueda coincide con una palabra completa, se muestra el formulario o recurso correspondiente.
* Los espacios adicionales se respetan y no se recortan durante la búsqueda. Por ejemplo: `My form` no es la misma consulta de búsqueda que `My form`.

* Si los datos y los valores de visualización de los campos en las propiedades de metadatos son diferentes, no puede utilizar valores de visualización como parámetros de búsqueda. Por ejemplo, no se puede buscar en función de un estado, como Modificado o Publicado, ya que estas propiedades se almacenan en un formato diferente.

## Búsqueda avanzada {#advanced-search}

En los criterios de búsqueda, además de la consulta puede especificar algunos parámetros de búsqueda para que la búsqueda básica sea más eficiente y centrada.

![Campo de búsqueda y parámetros o filtros para AEM búsqueda de recursos y formularios](assets/search_forms_assets.png)

Campo de búsqueda y parámetros o filtros para AEM búsqueda de recursos y formularios

### Ruta de recursos {#asset-path}

Mediante el filtro de ruta de recursos, puede limitar los resultados de búsqueda al directorio actual. Si la opción Buscar en el directorio actual no está seleccionada, los resultados de la búsqueda contienen recursos del directorio base. Si la página actual no es un directorio y la opción &quot;buscar en el directorio actual&quot; está seleccionada, la búsqueda devuelve los recursos presentes en el directorio principal.

### Modificación de recursos {#asset-modification}

Seleccione una de las siguientes opciones para buscar en todos los recursos modificados dentro de un período de tiempo específico.

| **Opción** | **Descripción** |
|---|---|
| Hace dos horas | Busque en todos los recursos modificados en las últimas dos horas. |
| Hace una semana | Busque en todos los recursos que se modificaron en la última semana. |
| Hace un mes | Buscar en todos los recursos que se modificaron en el último mes. |
| Hace un año | Buscar en todos los recursos modificados en el último año. |

### Estado de los activos {#asset-status}

Puede buscar recursos con uno de los siguientes estados:

* **Publicado**: Busque todos los recursos publicados y no modificados después de la publicación.

* **Sin publicar**: Busque todos los recursos que no se hayan publicado nunca.

* **Modificado**: Busque todos los recursos que se hayan modificado o no se hayan publicado después de la publicación.

### Tipo de recurso {#asset-type}

Puede seleccionar cualquier número de tipos de recursos. La búsqueda devuelve la unión de todos los tipos de recursos seleccionados.

<table>
 <tbody>
  <tr>
   <th>Opción</th> 
   <th>Descripción</th> 
  </tr>
  <tr>
   <td>Plantilla de formulario<br /> </td> 
   <td>Buscar en todas las plantillas de formulario.<br /> </td> 
  </tr>
  <tr>
   <td>Formulario PDF</td> 
   <td>Busque en todos los documentos PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Buscar en todos los documentos.</td> 
  </tr>
  <tr>
   <td>Formulario adaptable<br /> </td> 
   <td>Buscar en todos los formularios adaptables.</td> 
  </tr>
  <tr>
   <td>Medio</td> 
   <td>Buscar en todos los recursos.<br /> </td> 
  </tr>
 </tbody>
</table>

### Etiquetas {#tags}

Las etiquetas son etiquetas adjuntas a los recursos para su identificación. Al buscar, seleccione cualquier número de etiquetas en la lista desplegable o agregue etiquetas personalizadas, si es necesario. Un resultado de búsqueda contiene la intersección de las etiquetas seleccionadas.
