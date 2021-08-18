---
title: Esenciales del catálogo
seo-title: Esenciales del catálogo
description: Información general del catálogo
seo-description: Información general del catálogo
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Esenciales del catálogo {#catalog-essentials}

Esta página proporciona la información esencial para trabajar con la función de catálogo de los sitios de la comunidad de habilitación.

La función de catálogo, cuando se incluye en un sitio de la comunidad, permite a los miembros de la comunidad examinar y seleccionar los recursos de habilitación enumerados en un catálogo.

El [ `enablement catalog` componente](catalog.md) permite que los miembros de la comunidad accedan a un catálogo de [recursos de habilitación](resources.md). El uso de etiquetas AEM es una parte importante de la gestión del aspecto de los recursos de habilitación en un catálogo.

Consulte [Etiquetado de recursos de habilitación](tag-resources.md).

## Elementos esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activación/componentes/hbs/catálogo</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learn.path</td>
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
   <td>Consulte <a href="catalog.md">Función del catálogo</a></td>
  </tr>
 </tbody>
</table>

## Elementos esenciales para el servidor {#essentials-for-server-side}

### Función Catálogo {#catalog-function}

Una estructura de sitio de la comunidad que incluye la [función de catálogo](functions.md#catalog-function), incluye un componente `enablement catalog` configurado.

### Prefiltros {#pre-filters}

Cuando se añade una función Catálogo a un sitio de comunidad, es posible restringir los recursos de habilitación y las rutas de aprendizaje que aparecen en el catálogo especificando un prefiltro. Esto se hace estableciendo propiedades en la instancia del recurso de catálogo para el sitio.

Con el ejemplo del [Tutorial de habilitación](getting-started-enablement.md):

* Sobre el autor
* Uso de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Como [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Vaya al recurso de catálogo en la página de catálogo

   * Por ejemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Añadir un nodo de filtros secundarios

   * Seleccione el nodo `catalog`
   * Seleccione **[!UICONTROL Crear nodo]**

      * Nombre: `filters`
      * Tipo: `nt:unstructured`
      * Seleccione **[!UICONTROL Guardar todo]**

* Añadir la propiedad `se_resource-tags` al nodo `filters`

   * Seleccione el nodo `filters`
   * Añadir una propiedad Multi

      * Nombre: `se_resource-tags`
      * Tipo: Cadena
      * Valor: *&lt;introduzca un [TagID](#pre-filter-tagids)*
         * Seleccione **[!UICONTROL Multi]**
         * Seleccione **[!UICONTROL Add]**

            * En el cuadro de diálogo emergente, seleccione `+` para agregar identificadores de etiqueta prefiltrados adicionales

* Volver a publicar el sitio de la comunidad

![configure-catalog](assets/configure-catalog.png)

#### TagID prefiltrados {#pre-filter-tagids}

El filtro previo [TagIDs](../../help/sites-developing/framework.md#tagid) debe coincidir exactamente con las etiquetas aplicadas a los recursos de habilitación. Se pueden ver en la carpeta `resources` del sitio como valores de la propiedad `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de informes de Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
