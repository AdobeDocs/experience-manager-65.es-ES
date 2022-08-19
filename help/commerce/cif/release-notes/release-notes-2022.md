---
title: Notas de la versión de contenido y comercio de AEM 2022
description: Notas de la versión de contenido y comercio de AEM 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 6c5c37c1c365e1f03ea9b5c935adf63a33faba5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 33%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: Julio de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.08.02.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Novedades {#what-is-new-july}

* Asociación de páginas AEM a productos y categorías a través de AEM propiedades de página además de información general en la cabina de productos
   ![asociación de página de la cabina del producto](/help/assets/CIF/product_cockpit_page_association.png)

## Fecha de versión: Junio de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.07.05.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Componentes principales de CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Sitio de referencia de Venia del CIF | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Novedades {#what-is-new-june}

* El enriquecimiento del catálogo de productos ahora admite páginas AEM. Esto permite a los autores administrar la asociación de páginas y productos.

* Varias mejoras en los componentes principales del CIF

### Corrección de errores {#bug-fixes-june}

* Agregar token de inicio de sesión a la recuperación de precios del lado del cliente

* Componente de página incorrecto en la capa de datos

## Fecha de versión: Mayo de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.05.31.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Componentes principales de CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Sitio de referencia de Venia del CIF | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Novedades {#what-is-new-may}

* Nueva página de propiedades de la cabina de productos para una descripción general mejor y simplificada

![información general sobre las propiedades de la cabina de productos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilidad y solidez mejoradas para conectores de terceros en I/O Runtime

* Mejorar la compatibilidad con las sobrescrituras de configuración del cliente GQL (p. ej., establecer el comportamiento de almacenamiento en caché personalizado)

### Corrección de errores {#bug-fixes-may}

* El campo de selección de varios valores muestra el segundo y el resto de los productos adicionales como no válidos

* El selector de productos se oculta ocasionalmente detrás de los componentes

## Fecha de versión: Abril de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.04.28.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Componentes principales de CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Sitio de referencia de Venia del CIF | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Novedades {#what-is-new-april}

* Acceso rápido a la cabina de productos: Acceda fácilmente a la información detallada completa del producto con un solo clic en el Editor de sitios

   ![Habilitar lista de deseos](/help/assets/CIF/enable-wishlist.png)

* Compatibilidad con componentes de comercio de marketing adicionales: Los componentes se pueden configurar para mostrar una llamada a acción de complemento al carro y de complemento a la lista de deseos

   ![Acceso directo del editor de sitios a la cabina de productos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Fecha de versión: Febrero de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.02.24.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componentes principales de CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Sitio de referencia de Venia del CIF | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novedades {#what-is-new-march}

* Beta: compatibilidad del componente principal de búsqueda del CIF de AEM con Commerce LiveSearch
* SEO mejorado para escenarios de varias tiendas: los formatos de URL para PDP/PLP ahora se pueden configurar en el nivel de tienda mediante las propiedades de configuración en la nube del CIF
* El selector de productos es compatible con los productos clasificados mediante la nueva opción de filtro de la IU.  Esto permite a los profesionales del contenido preparar la administración de contenido de producto para próximos lanzamientos del producto
* Administración simplificada de la configuración del CIF y gestión de errores mediante el uso del nombre de configuración en la nube del CIF, en lugar de la URL del proxy de configuración
* Selección manual de categorías para la lista de productos y los componentes de carrusel. Esto permite a los profesionales del contenido utilizar estos componentes en páginas de contenido, fuera de la experiencia del catálogo

## Fecha de versión: Enero de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.01.20.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Componentes principales de CIF | 2,5,0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Sitio de referencia de Venia del CIF | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Novedades {#what-is-new-january}

* Componentes myAccount mejorados
* El componente Recomendación de producto admite tipos de página adicionales (página de inicio, carro de compras, confirmación de pedido)
* **Lista de deseos**
   * Los visitantes con sesión iniciada pueden añadir productos a una lista de deseos
   * Es posible administrar la lista de deseos y sus productos a través de myAccount
   * El botón Añadir a la lista de deseos se puede activar o desactivar en un nivel de componente mediante una directiva (por ejemplo, teaser de productos, detalles de productos
   * Disponible como componente principal y en la AEM Venia Storefront

![Lista de deseos](/help/assets/CIF/wishlist.png)
