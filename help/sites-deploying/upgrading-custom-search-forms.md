---
title: Actualización de formularios de búsqueda personalizados
seo-title: Actualización de formularios de búsqueda personalizados
description: En este artículo se detallan los ajustes que se requieren después de una actualización para que los formularios de búsqueda personalizados funcionen.
seo-description: En este artículo se detallan los ajustes que se requieren después de una actualización para que los formularios de búsqueda personalizados funcionen.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Actualización de formularios de búsqueda personalizados{#upgrading-custom-search-forms}

En AEM 6.2, ha cambiado la ubicación en la que se almacenan los formularios de búsqueda personalizados en el repositorio. Tras la actualización, se mueven de su ubicación en 6.1 en:

* /apps/cq/gui/content/facets

a una nueva ubicación en:

* /conf/global/settings/cq/search/facets

Debido a esto, se requieren ajustes manuales después de una actualización para que los formularios sigan funcionando.

Esto se aplica tanto a los nuevos formularios de búsqueda como a los predeterminados que se han personalizado.

Para obtener más información, consulte la documentación sobre [facetas](/help/assets/search-facets.md)de búsqueda.

## Cambio de la propiedad resourceType {#changing-the-resourcetype-property}

A menos que se indique lo contrario, la mayoría de los ajustes que deben realizarse después de la actualización requieren cambiar la `sling:resourceType` propiedad de los formularios de búsqueda personalizados configurados. Esto es necesario para que la propiedad señale a la ubicación correcta de la secuencia de comandos de procesamiento.

Puede cambiar la propiedad haciendo lo siguiente:

1. Para abrir CRXDE Lite, vaya a `https://server:port/crx/de/index.jsp`
1. Vaya a la ubicación del nodo que debe ajustarse, tal como se especifica en la lista de formularios [de búsqueda](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) personalizados que aparece a continuación.
1. Haga clic en el nodo. En el panel de propiedades derecho, haga clic en la propiedad **sling:resourceType** y modifíquela.
1. Finalmente, guarde los cambios pulsando el botón **Guardar todo** .

## Lista de formularios de búsqueda personalizados {#list-of-custom-search-forms}

A continuación encontrará una lista de todos los formularios de búsqueda personalizados y las modificaciones que deben realizarse después de la actualización. Se refieren a los nombres de `/conf/global/settings/cq/search/facets/sites/items`.

### Predicado de texto completo con nombre de nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1</td>
   <td>texto completo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

En AEM 6.1, el predicado de texto completo estándar formaba parte del formulario de búsqueda. En 6.2, el campo de texto completo ha sido reemplazado por OmniSearch. Este predicado se omite programáticamente y se puede eliminar.

**** Acción: Quite el nodo por completo.

### Otros predicados de texto completo {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/s predeterminado Buscar desde en 6.1</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicados del explorador de rutas {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicados de etiquetas {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>etiquetas</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la propiedad **resourceType** (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de estado de la página {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

El estado de la página se ha sustituido por dos predicados de propiedades de opciones, uno para publicación y otro para el estado de LiveCopy.

**Acciones:**

* Quitar el `pagestatuspredicate` nodo
* Copiar nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * hasta `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copiar nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * hasta `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Asegúrese de establecer `listOrder` la propiedad del `analyticspredicate` nodo en &quot;**8**&quot;. Esto es necesario para evitar conflictos.

### Predicados de intervalo de fechas {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Filtro oculto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Nada que ajustar.

### Predicado de Analytics {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de intervalo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

>[!NOTE]
>
>Nota: En oposición a 6.1, el predicado de rango ya no procesa una etiqueta en la barra de búsqueda.

### Predicado de propiedad de opciones {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de intervalo del regulador {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de componentes {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/component spredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/component spredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de autor {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicado de plantillas {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1<br /><br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicado</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicado</p> </td>
  </tr>
 </tbody>
</table>

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

## Carril de búsqueda de administración de recursos {#assets-admin-search-rail}

Los nodos siguientes hacen referencia a los nombres de `/conf/global/settings/dam/search/facets/assets/items`

### Predicado de texto completo con nombre de nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | texto completo |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo de recurso en 6.2 | N/D |

En 6.1, el predicado de texto completo estándar formaba parte del formulario de búsqueda. En 6.2, el campo de texto completo ha sido reemplazado por OmniSearch. Este predicado se omite programáticamente y se puede eliminar.

**** Acción: Quite el nodo mencionado anteriormente.

### Predicados del explorador de rutas {#path-browser-predicates-1}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | pathbrowser |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicados de tipo MIME {#mime-type-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | mimetype |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente).

### Predicados de tamaño de archivo {#file-size-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | filesize |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**** Acción: Ajuste `resourceType` como se muestra en la ubicación 6.2 anterior.

### Predicados de última modificación de recurso {#asset-last-modified-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Acción: Ajuste la propiedad resourceType (agregue &quot;/coral&quot; como en la ubicación 6.2 indicada anteriormente).

### Publicar predicado {#publish-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | instancias de publicación |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**Acciones:**

*  Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

* Agregue una propiedad `optionPaths` (de tipo String) con el valor: `/libs/dam/options/predicates/publish`

* Agregar `singleSelect` propiedad con valor booleano `true`.

### Predicados de estado {#status-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | estado |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

### Predicados de estado de caducidad {#expiry-status-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | caduystatus |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

### Predicados de validez de metadatos {#metadata-validity-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | metadatavalidity |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

### Predicados de clasificación {#rating-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | clasificación |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

### Predicado de orientación {#orientation-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | orientation |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso en 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Acciones:**

*  Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

* Agregue una `fieldLabel` propiedad con el mismo valor que la `text` propiedad en el mismo nodo.

* Agregue una `emptyText` propiedad con el mismo valor que la `text` propiedad en el mismo nodo.

* Agregue una `rootPath` propiedad con el mismo valor que la `optionPaths` propiedad en el mismo nodo.

### Predicado de estilo {#style-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | el estilo |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso en 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Acciones:**

*  Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

* Agregue una `fieldLabel` propiedad con el mismo valor que la `text` propiedad en el mismo nodo.

* Agregue una `emptyText` propiedad con el mismo valor que la `text` propiedad en el mismo nodo.

* Agregue una `rootPath` propiedad con el mismo valor que la `optionPaths` propiedad en el mismo nodo.

### Predicados de formato de vídeo {#video-format-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | videoFormat |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)

### Predicado de recursos principales {#mainasset-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | mainasset |
|---|---|
| Tipo de recurso en 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo de recurso en 6.2 | granito/ui/componentes/coral/fundación/formulario/oculto |

**** Acción: Ajuste la `resourceType` propiedad (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada anteriormente)
