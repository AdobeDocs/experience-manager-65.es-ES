---
title: Funciones básicas del catálogo
seo-title: Funciones básicas del catálogo
description: Descripción general del catálogo
seo-description: Descripción general del catálogo
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Funciones básicas del catálogo {#catalog-essentials}

Esta página proporciona la información esencial para trabajar con la función de catálogo de los sitios de la comunidad de habilitación.

La función de catálogo, cuando se incluye en un sitio de la comunidad, permite a los miembros de la comunidad examinar y seleccionar los recursos de activación enumerados en un catálogo.

El [ componente `enablement catalog` permite a los miembros de la comunidad acceder a un catálogo de recursos](catalog.md) de [](resources.md)activación. El uso de etiquetas AEM es una parte importante de la gestión del aspecto de los recursos de activación en un catálogo.

Consulte [Etiquetado de recursos](tag-resources.md)de habilitación.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/habilitación/componentes/hbs/catálogo</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learning.path</td>
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
   <td>Consulte Función <a href="catalog.md">de catálogo</a></td>
  </tr>
 </tbody>
</table>

## Esenciales para servidor {#essentials-for-server-side}

### Función Catálogo {#catalog-function}

Una estructura de sitio de comunidad que incluye la función [](functions.md#catalog-function)Catálogo, incluye un `enablement catalog` componente configurado.

### Prefiltros {#pre-filters}

Cuando se agrega una función de catálogo a un sitio de comunidad, es posible restringir los recursos de habilitación y las rutas de aprendizaje que aparecen en el catálogo especificando un prefiltro. Esto se realiza estableciendo propiedades en la instancia del recurso de catálogo para el sitio.

Uso del ejemplo del Tutorial de [habilitación](getting-started-enablement.md):

* En autor
* Uso de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Por ejemplo, [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Vaya al recurso de catálogo en la página de catálogo

   * Por ejemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Agregar un nodo de filtros secundarios

   * Seleccione el `catalog`nodo
   * Seleccione **[!UICONTROL Crear nodo]**

      * Nombre: `filters`
      * Tipo: `nt:unstructured`
   * Seleccione **[!UICONTROL Guardar todo]**


* Agregar `se_resource-tags` propiedad al `filters` nodo

   * Seleccione el `filters` nodo
   * Agregar una propiedad múltiple

      * Nombre: `se_resource-tags`
      * Tipo: Cadena
      * Valor: *&lt;ingrese un[TagID](#pre-filter-tagids)>*
      * Seleccionar **[!UICONTROL varios]**
      * Seleccione **[!UICONTROL Agregar]**

         * En el cuadro de diálogo emergente, seleccione `+` para agregar identificadores de etiqueta previos al filtro adicionales

* Volver a publicar el sitio de la comunidad

![chlimage_1-189](assets/chlimage_1-189.png)

#### TagIDs de prefiltro {#pre-filter-tagids}

Los [TagIDs](../../help/sites-developing/framework.md#tagid) de prefiltro deben coincidir exactamente con las etiquetas aplicadas a los recursos de habilitación. Estos valores están visibles en la `resources` carpeta del sitio como valores de la propiedad `se_resource-tags`.

![chlimage_1-190](assets/chlimage_1-190.png)

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API de informes de Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

