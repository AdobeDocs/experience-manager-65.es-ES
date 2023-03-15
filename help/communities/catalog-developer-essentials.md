---
title: Catalog Essentials
seo-title: Catalog Essentials
description: Resumen del catálogo
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# Catalog Essentials {#catalog-essentials}

Esta página proporciona información esencial para trabajar con la función de catálogo de los sitios de la comunidad de habilitación.

La función de catálogo, cuando se incluye en un sitio de comunidad, permite a los miembros de la comunidad examinar y seleccionar los recursos de habilitación enumerados en un catálogo.

El [ `enablement catalog` componente](catalog.md) permite a los miembros de la comunidad acceder a un catálogo de [recursos de habilitación](resources.md). AEM El uso de etiquetas de es una parte importante de la administración del aspecto de los recursos de habilitación en un catálogo.

Consulte [Recursos de habilitación de etiquetas](tag-resources.md).

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="catalog.md">Función Catálogo</a></td>
  </tr>
 </tbody>
</table>

## Essentials para servidor {#essentials-for-server-side}

### Función Catálogo {#catalog-function}

Una estructura de sitio de la comunidad que incluye [Función Catálogo](functions.md#catalog-function), incluye un configurado `enablement catalog` componente.

### Prefiltros {#pre-filters}

Cuando se añade una función Catálogo a un sitio de la comunidad, es posible restringir los recursos de habilitación y las rutas de aprendizaje que aparecen en el catálogo especificando un filtro previo. Esto se hace estableciendo propiedades en la instancia del recurso de catálogo para el sitio.

Uso del ejemplo de [Tutorial de habilitación](getting-started-enablement.md):

* En el autor
* Uso de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Como [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Vaya al recurso de catálogo en la página del catálogo

   * Por ejemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`. 

* Adición de un nodo de filtros secundarios

   * Seleccione el `catalog`nodo
   * Seleccionar **[!UICONTROL Crear nodo]**

      * Nombre: `filters`
      * Tipo: `nt:unstructured`
      * Seleccionar **[!UICONTROL Guardar todo]**

* Añadir `se_resource-tags` a la propiedad `filters` nodo

   * Seleccione el `filters` nodo
   * Añadir una propiedad Multi

      * Nombre: `se_resource-tags`
      * Tipo: cadena
      * Valor: *&lt;enter a=&quot;&quot; span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />TagID](#pre-filter-tagids)>*[
         * Seleccionar **[!UICONTROL Múltiple]**
         * Seleccionar **[!UICONTROL Añadir]**

            * En el cuadro de diálogo emergente, seleccione `+` para agregar TagID adicionales previo al filtro

* Volver a publicar el sitio de la comunidad

![configure-catalog](assets/configure-catalog.png)

#### Filtrado previo de TagID {#pre-filter-tagids}

El prefiltro [TagID](../../help/sites-developing/framework.md#tagid) debe coincidir exactamente con las etiquetas aplicadas a los recursos de habilitación. Estos se pueden ver en `resources` para el sitio como valores de la propiedad `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
