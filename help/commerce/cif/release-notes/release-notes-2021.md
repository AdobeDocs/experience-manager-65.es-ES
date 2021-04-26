---
title: Notas de la versión de contenido y comercio de AEM 2021
description: Notas de la versión de contenido y comercio de AEM 2021
translation-type: tm+mt
source-git-commit: 2d0b52dbf85e1fbe91c09a8366744aa77f25cd73
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 10%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Resumen de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

**El complemento CIF ya está disponible a través de la distribución de software de  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). El antiguo conector del CIF de AEM está entrando en modo de mantenimiento y ya no debería usarse. Migrar al nuevo complemento CIF.**

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: Abril de 2021

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | v2021.04.22 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Componentes principales de CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-april}

* **El complemento CIF ya está disponible a través de la distribución de software de  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). El antiguo conector del CIF de AEM está entrando en modo de mantenimiento y ya no debería usarse. Migrar al nuevo complemento CIF.**

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

### Mejoras

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

### Mejoras  {#what-is-improved-february}

* Capa de datos del lado del cliente mejorada con url de imagen de producto e información de categoría

* Varias correcciones de errores.

## Fecha de versión: Enero de 2021

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 1,7,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 1,7,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Sitio de referencia de Venia del CIF | 2021.02.02 | [Notas de la versión](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Novedades {#what-is-new-january}

* Administración de experiencia del producto: Nueva pestaña de la propiedad &quot;Comercio&quot; para los fragmentos de experiencias y recursos. Esta pestaña le permite vincular recursos y fragmentos de experiencias a productos y categorías. La pestaña también muestra datos en tiempo real de objetos de comercio vinculados y un vínculo para mostrar detalles en la consola del producto.

### Mejoras  {#what-is-improved-january}

* Envíe los datos de usuario después de la autenticación a la capa de datos del cliente de Adobe.

* Varias correcciones de errores.
