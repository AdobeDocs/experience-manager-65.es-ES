---
title: Notas de la versión de contenido y comercio de AEM 2021
description: Notas de la versión de contenido y comercio de AEM 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 11%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: Esquemas de AEM 6.5.7, Adobe Commerce 2.3.5 GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: Noviembre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.11.18.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| Componentes principales de CIF | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| Sitio de referencia de Venia del CIF | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Novedades {#what-is-new-november}

* Componentes extendidos de myAccount basados en los componentes Peregrine ampliables de Commerce

![Componentes de myAccount ampliados](/help/assets/CIF/extended-myAccount-components.png)

* Los autores pueden crear recomendaciones de producto de Commerce ad hoc utilizando tipos de recomendación adicionales

* Compatibilidad con tarjetas de regalo en AEM Storefront

## Fecha de versión: Octubre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.10.20.02 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Componentes principales de CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Sitio de referencia de Venia del CIF | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Novedades {#what-is-new-october}

* El complemento CIF es compatible con la última versión de Commerce v2.4.3 con las nuevas API y esquemas de GraphQL

* Los autores pueden agregar vínculos a páginas de productos y catálogos en campos de texto utilizando el editor de texto enriquecido (RTE). Se ha agregado un icono del CIF a la barra de herramientas de RTE que abrirá los selectores para buscar y seleccionar rápidamente el producto o la categoría sin abandonar el contexto.

* El carro de compras emergente y el cierre de compra existentes se han sustituido por páginas dedicadas AEM carro de compras y de cierre de compra. Los componentes de estas páginas se crean utilizando los componentes Peregrine ampliables de Adobe Commerce

* Los comerciantes pueden ocultar ciertas categorías de catálogo de productos en la navegación mediante el servidor de Commerce. El componente principal de navegación del CIF respeta la configuración del back-end de comercio &quot;incluir en menú&quot; para mostrar u ocultar categorías en la navegación

* AEM Tienda Venia devuelve el error HTTP 404 si no se encuentra la categoría o la página de producto

## Fecha de versión: Septiembre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.09.27 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componentes principales de CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Sitio de referencia de Venia del CIF | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novedades {#what-is-new-september}

* La nueva pestaña &quot;contenido de comercio asociado&quot; del editor de sitios aumenta la eficacia del autor al obtener acceso rápidamente al contenido de producto AEM relevante para el contexto actual

   ![Contenido comercial asociado](/help/assets/CIF/associated-commerce-content.png)

* Interfaz de usuario del selector de productos mejorada para mejorar la experiencia del usuario, la eficacia y la compatibilidad con catálogos de productos complejos

   ![Nuevo selector de productos](/help/assets/CIF/product-picker.png)

* Respetar la propiedad &quot;include_in_menu&quot; en el componente de navegación

### Corrección de errores {#bug-fixes-september}

* El vaciado de la caché del menú no funciona como se espera

* Errores de JS durante AEM paso de implementación de CS y cuando no se utilizan componentes de cliente

* No se puede crear la configuración de nube del CIF en carpetas que tengan un nodo sling:configs

## Fecha de versión: Agosto de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.09.02 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componentes principales de CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Sitio de referencia de Venia del CIF | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novedades {#what-is-new-august}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y mejorar la compatibilidad con catálogos de productos complejos

   ![Nuevo selector de categorías](/help/assets/CIF/category-picker.png)

* Mejor compatibilidad con A11Y para los componentes principales del CIF

### Corrección de errores {#bug-fixes-august}

* No se puede cerrar el acordeón de filtro de categoría una vez que esté abierto

* Propiedad &quot;texto de llamada a acción&quot; dañada en el teaser de productos

* Errores de CIF JS durante AEM paso de implementación CS

* Corregir el acceso de producto sin procesar para elementos de lista de productos asignados

## Fecha de versión: Julio de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.07.21 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componentes principales de CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Sitio de referencia de Venia del CIF | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novedades {#what-is-new-july}

* Componentes principales de CIF v2
   * Configuraciones simplificadas y mejoradas para URL PDP/PLP y SEO
   * Indicador visual para datos de productos clasificados en modo de creación para una mejor visibilidad de los próximos cambios
   * Nuevo componente de mapa del sitio para páginas de contenido y comercio

* Compatibilidad con [Recomendación de producto de Adobe Commerce Sensei, con tecnología de Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) en AEM tienda utilizando recomendaciones predefinidas o creadas sobre la marcha

## Fecha de versión: Junio de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.06.18 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componentes principales de CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Sitio de referencia de Venia del CIF | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novedades {#what-is-new-june}

* Nuevos tipos de datos de referencia de productos y categorías del CIF para fragmentos de contenido (incl. compatibilidad con la interfaz de usuario del selector de productos/categorías)
* Nuevo componente principal de fragmento de contenido de comercio
* Búsqueda de comercio de texto completo compatible con AEM servidor
* Los componentes principales de comercio admiten la recopilación de datos de Adobe Commerce Sensei Recs
* Direcciones URL compatibles con SEO mejoradas para páginas de categoría
* Compatibilidad con encabezados HTTP personalizados por sitio/configuración

## Fecha de versión: Mayo de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.05.26 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componentes principales de CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Sitio de referencia de Venia del CIF | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novedades {#what-is-new-may}

* Compatibilidad de paginación para contenido asociado en propiedades de la consola del producto

### Corrección de errores {#bug-fixes-may}

* Las miniaturas de los recursos no se muestran en la ficha Recurso de las propiedades del producto

* La ruta de navegación restablece los datos de vista previa en la consola del producto

## Fecha de versión: Abril de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2021.04.22 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principales de CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-april}

* Compatibilidad con UID de categoría : esto desbloquea las integraciones de comercio de terceros para sistemas que utilizan Strings para id de categoría

* AEM extensión para el PWA Studio incl. integración de ejemplo

* Nuevo componente principal de navegación del CIF que amplía el componente principal de navegación de WCM

### Corrección de errores {#bug-fixes-april}

* El campo de categoría raíz no se mostraba en la pestaña de comercio de las propiedades de página de las páginas de categoría

## Fecha de versión: Marzo de 2021 {#what-is-new-march}

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.03.25 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades

* Compatibilidad con Adobe Commerce 2.4.2

### Novedades mejoradas

* Se ha mejorado la reutilización del componente de detalles del producto para páginas controladas por contenido

* Mejor almacenamiento en caché y menos llamadas de back-end para PDP

* Varias correcciones de errores.

## Fecha de versión: Febrero de 2021

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 1,8,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1,8,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.02.24 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-february}

* Administración de experiencia del producto: Enriquezca las páginas del catálogo de productos individualmente con fragmentos de experiencias.

* Se han ampliado las propiedades de la consola de producto para mostrar los recursos vinculados y los fragmentos de experiencia, incluida la acción para navegar rápidamente al contenido asociado.

### Novedades mejoradas  {#what-is-improved-february}

* Se ha mejorado la capa de datos del lado del cliente con la dirección url de la imagen del producto y la información de categoría.

* Varias correcciones de errores.

## Fecha de versión: Enero de 2021

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 1,7,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1,7,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.02.02 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-january}

* Administración de experiencia del producto: Nueva pestaña de la propiedad &quot;Comercio&quot; para los fragmentos de experiencias y recursos. Esta pestaña le permite vincular recursos y fragmentos de experiencias a productos y categorías. La pestaña también muestra datos en tiempo real de objetos de comercio vinculados y un vínculo para mostrar detalles en la consola del producto.

### Novedades mejoradas  {#what-is-improved-january}

* Envíe los datos de usuario después de la autenticación a la capa de datos del cliente de Adobe.

* Varias correcciones de errores.
