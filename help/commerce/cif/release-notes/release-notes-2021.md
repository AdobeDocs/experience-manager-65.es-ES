---
title: Notas de la versión 2021 de Adobe Experience Manager Content and Commerce
description: Contenido de Adobe Experience Manager y notas de la versión de Commerce 2021.
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 7c1aeec18f35b019a63d0385ada248b26a0df9de
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 14%

---

# Información general sobre la versión de Commerce integration framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema que aparecen en la tabla siguiente para la versión de CIF que está utilizando o que planea utilizar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento de CIF | Mínimo: Adobe Experience Manager (AEM) 6.5.7, Adobe Commerce 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Arquetipo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: noviembre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 2021.11.18.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| Componentes principales de CIF | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| Sitio de referencia de Venia en CIF | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Novedades {#what-is-new-november}

* Componentes extendidos de myAccount basados en los componentes Peregrine ampliables de Commerce

![Componentes de myAccount ampliados](/help/assets/CIF/extended-myAccount-components.png)

* Los autores pueden crear recomendaciones de producto de Commerce ad hoc utilizando tipos de recomendación adicionales

* Compatibilidad con tarjetas de regalo en AEM Storefront

## Fecha de versión: octubre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 2021.10.20.02 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Componentes principales de CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Sitio de referencia de Venia en CIF | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Novedades {#what-is-new-october}

* El complemento de CIF es compatible con la última versión 2.4.3 de Commerce con nuevas API y esquemas de GraphQL

* Los autores pueden añadir vínculos a páginas de productos y catálogos en campos de texto mediante el editor de texto enriquecido (RTE). Se ha añadido un icono de CIF a la barra de herramientas de RTE que abre los selectores para buscar y seleccionar rápidamente el producto o la categoría sin salir del contexto.

* El carro de compras emergente y el cierre de compra existentes se han sustituido por páginas de carro de compras y cierre de compra dedicadas de AEM. Los componentes de estas páginas se crean utilizando los componentes Peregrine ampliables de Adobe Commerce

* Los comerciantes pueden ocultar determinadas categorías del catálogo de productos en la navegación mediante el backend de Commerce. El componente principal de navegación de CIF respeta la configuración del backend de comercio &quot;incluir en el menú&quot; para mostrar u ocultar categorías en la navegación

* Tienda AEM Venia devuelve el error HTTP 404 si no se encuentra la categoría o la página del producto

## Fecha de versión: septiembre de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 27 de septiembre de 2021 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Componentes principales de CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Sitio de referencia de Venia en CIF | 23 de septiembre de 2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Novedades {#what-is-new-september}

* La nueva pestaña &quot;Contenido de comercio asociado&quot; del editor de Sites aumenta la eficacia del autor al obtener acceso rápidamente al contenido de producto de AEM relevante para el contexto actual

  ![Contenido de comercio asociado](/help/assets/CIF/associated-commerce-content.png)

* Se ha mejorado la interfaz de usuario del selector de productos para mejorar la experiencia del usuario, aumentar la eficacia y admitir catálogos de productos complejos

  ![Selector de nuevos productos](/help/assets/CIF/product-picker.png)

* Respetar la propiedad &quot;include_in_menu&quot; en el componente de navegación

### Correcciones de errores {#bug-fixes-september}

* El vaciado de caché del menú no funciona como se esperaba

* Errores de JS durante el paso de implementación de AEM CS y cuando no se utilizan componentes del lado del cliente

* No se puede crear la configuración de nube de CIF en carpetas que tengan un nodo sling:configs

## Fecha de versión: agosto de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 2021.09.02 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Componentes principales de CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Sitio de referencia de Venia en CIF | 27 de agosto de 2021 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Novedades {#what-is-new-august}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y ofrecer una mejor compatibilidad con catálogos de productos complejos

  ![Selector de categoría nueva](/help/assets/CIF/category-picker.png)

* Mejor compatibilidad con A11Y para los componentes principales de CIF

### Correcciones de errores {#bug-fixes-august}

* No se puede cerrar el acordeón del filtro de categoría una vez que está abierto

* Propiedad &quot;Call to action text&quot; dañada en el teaser de productos

* Errores de CIF JS durante el paso de implementación de AEM CS

* Corregir el acceso a productos sin procesar para elementos de lista de productos asignados

## Fecha de versión: julio de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 21.07.21 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Componentes principales de CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Sitio de referencia de Venia en CIF | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Novedades {#what-is-new-july}

* Componentes principales de CIF v2
   * Configuraciones simplificadas y mejoradas para URL de PDP/PLP y SEO
   * Indicador visual para datos de productos clasificados en el modo de creación para una mejor visibilidad de los próximos cambios
   * Nuevo componente de mapa del sitio para páginas de contenido y comercio

* Compatibilidad con [Adobe Commerce AI Product Recommendations, con tecnología Adobe AI](https://business.adobe.com/ai/adobe-genai.html) en AEM Storefront y recomendaciones predefinidas o creadas sobre la marcha

## Fecha de versión: junio de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 2021.06.18 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Componentes principales de CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Sitio de referencia de Venia en CIF | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Novedades {#what-is-new-june}

* Nuevos tipos de datos de referencia de productos y categorías de CIF para fragmentos de contenido (incl. soporte de la interfaz de usuario del selector de productos/categorías)
* Nuevo componente principal de fragmento de contenido de Commerce
* Búsqueda de comercio de texto completo admitida en el back-end de AEM
* Los componentes principales de Commerce admiten la recopilación de datos Adobe Commerce AI Recs
* Se han mejorado las URL compatibles con SEO para las páginas de categorías
* Compatibilidad con encabezados HTTP personalizados por sitio/configuración

## Fecha de versión: mayo de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 26.5.2021 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Componentes principales de CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Sitio de referencia de Venia en CIF | 24.05.21 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Novedades {#what-is-new-may}

* Compatibilidad de paginación con contenido asociado en propiedades de la consola de producto

### Correcciones de errores {#bug-fixes-may}

* Las miniaturas de recursos no se muestran en la pestaña Recursos de las propiedades del producto

* La ruta restablece los datos de vista previa en la consola del producto

## Fecha de versión: abril de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento de CIF | 2021.04.22 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principales de CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia en CIF | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-april}

* Compatibilidad con UID de categoría: esto desbloquea las integraciones de comercio de terceros para sistemas que utilizan cadenas para ID de categoría

* Extensión de AEM para PWA Studio incluida. integración de ejemplo

* Nuevo componente principal de navegación de CIF que amplía el componente principal de navegación de WCM

### Correcciones de errores {#bug-fixes-april}

* El campo de categoría raíz no se mostraba en la pestaña de comercio de las propiedades de página de las páginas de categoría

## Fecha de versión: marzo de 2021 {#what-is-new-march}

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia en CIF | 25.03.2021 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades

* Compatibilidad con Adobe Commerce 2.4.2

### Qué se ha mejorado

* Reutilización mejorada del componente de detalles del producto para páginas impulsadas por contenido

* Mejor almacenamiento en caché y menos llamadas de back-end para PDP

* Varias correcciones de errores.

## Fecha de versión: febrero de 2021

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 1.8.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1.8.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia en CIF | 24.02.2021 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-february}

* Administración de experiencias de producto: enriquezca las páginas del catálogo de productos individualmente con fragmentos de experiencias.

* Se han ampliado las propiedades de la consola del producto para mostrar el Assets vinculado y los fragmentos de experiencias, incluida la acción para navegar rápidamente al contenido asociado.

### Qué se ha mejorado  {#what-is-improved-february}

* Capa de datos mejorada del lado del cliente con información de categoría y URL de imagen del producto.

* Varias correcciones de errores.

## Fecha de versión: enero de 2021

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 1.7.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1.7.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia en CIF | 2021.02.02 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-january}

* Administración de experiencias de producto: nueva pestaña de propiedades &quot;Commerce&quot; para Assets y fragmentos de experiencias. Esta pestaña le permite vincular Assets y fragmentos de experiencias a productos y categorías. La pestaña también muestra datos en tiempo real de objetos de comercio vinculados y un vínculo para mostrar detalles en la consola de producto.

### Qué se ha mejorado  {#what-is-improved-january}

* Envíe datos de usuario después de la autenticación a la capa de datos del cliente de Adobe.

* Varias correcciones de errores.
