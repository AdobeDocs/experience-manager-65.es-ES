---
title: Notas de la versión de contenido y comercio de AEM 2021
description: Notas de la versión de contenido y comercio de AEM 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 71782a3caae3f74a4886c52cf9b29f9e998913fa
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 8%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

**Con la versión de abril hemos reemplazado el conector del CIF de GitHub por el complemento CIF que está disponible en la [Distribución del software del Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). El cambio al complemento incluye buenas ventajas para los proyectos:

* La mayoría de las nuevas funciones estarán disponibles inmediatamente en AEM 6.5 (ya no se espera el puerto lateral de las funciones)
* Fácil de actualizar a nuevas versiones de complementos
* Listo para Cloud Service

El antiguo conector del CIF de AEM está entrando en modo de mantenimiento y ya no debería usarse. Sustituya el conector del CIF por el nuevo complemento CIF. Simplemente, la sustitución de paquetes debería ser posible para la mayoría de los proyectos. **

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

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

* Indicador visual para datos de catálogo clasificados en AEM tienda

### Corrección de errores {#bug-fixes-april}

* El campo de categoría raíz no se mostraba en la pestaña de comercio de las propiedades de página de las páginas de categoría

## Fecha de versión: Marzo de 2021 {#what-is-new-march}

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1.9.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.03.25 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades

* Compatibilidad con el Magento 2.4.2

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
