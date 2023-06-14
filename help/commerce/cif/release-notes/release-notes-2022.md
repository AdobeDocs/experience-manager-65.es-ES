---
title: AEM Notas de la versión de Content and Commerce de 2022
description: AEM Notas de la versión de Content and Commerce de 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 33%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema de la tabla siguiente para la versión del CIF que está utilizando actualmente o que planea utilizar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | AEM Mínimo: 6.5.7, Adobe Commerce 2.3.5 Esquemas de GraphQL |
| Componentes principales del CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM. | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: septiembre de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.09.20.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| Componentes principales del CIF | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| Sitio de referencia de CIF Venia | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Novedades {#what-is-new-september}

* Los autores pueden enriquecer dinámicamente listas de productos con Fragmentos de experiencias (por ejemplo: colocar banner entre listas de productos)
* El componente Lista admite páginas de productos o categorías asociados para mostrar dinámicamente páginas relacionadas
* Compatibilidad con los componentes de Peregrine 12.5
* Compatibilidad con la carga de precios del lado del cliente en teaser y carrusel de productos

## Fecha de versión: julio de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.08.02.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Novedades {#what-is-new-july}

* AEM AEM Asociación de páginas de productos a productos y categorías a través de las propiedades de página de la página de productos más información general en la cabina de productos
  ![asociación de página de cabina de productos](/help/assets/CIF/product_cockpit_page_association.png)

## Fecha de versión: junio de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.07.05.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Componentes principales del CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Sitio de referencia de CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Novedades {#what-is-new-june}

* AEM Ahora, el enriquecimiento del catálogo de productos admite páginas de productos, lo que permite a los autores administrar la asociación entre páginas y productos.

* Varias mejoras en los componentes principales del CIF

### Corrección de errores {#bug-fixes-june}

* Añadir token de inicio de sesión a la recuperación de precios del lado del cliente

* Componente de página incorrecto en la capa de datos.

## Fecha de versión: mayo de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.05.31.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Componentes principales del CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Sitio de referencia de CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Novedades {#what-is-new-may}

* Nueva página de propiedades de la cabina de productos para una descripción general mejor y simplificada

![información general sobre las propiedades de la cabina de productos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilidad y solidez mejoradas para conectores de terceros en I/O Runtime

* Mejorar la compatibilidad con las sobrescrituras de configuración del cliente GQL (por ejemplo, establecer el comportamiento de almacenamiento en caché personalizado)

### Corrección de errores {#bug-fixes-may}

* El campo de selección de varios valores muestra el segundo producto y los productos adicionales como no válidos

* El selector de productos se oculta ocasionalmente detrás de los componentes

## Fecha de versión: abril de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.04.28.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Componentes principales del CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Sitio de referencia de CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Novedades {#what-is-new-april}

* Acceso rápido a la cabina de productos: acceda fácilmente a la información detallada completa del producto con un solo clic en el Editor de sitios

  ![Habilitar lista de deseos](/help/assets/CIF/enable-wishlist.png)

* Compatibilidad con componentes de comercio de marketing adicionales: los componentes se pueden configurar para mostrar una llamada a acción de complemento al carro y de complemento a la lista de deseos.

  ![Acceso directo del editor de sitios a la cabina de productos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Fecha de versión: febrero de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.02.24.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componentes principales del CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Sitio de referencia de CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novedades {#what-is-new-march}

* Beta: compatibilidad del componente principal de búsqueda del CIF de AEM con Commerce LiveSearch
* SEO mejorado para escenarios de varias tiendas: los formatos de URL para PDP/PLP ahora se pueden configurar en el nivel de tienda mediante las propiedades de configuración en la nube del CIF
* El selector de productos es compatible con los productos clasificados mediante la nueva opción de filtro en la interfaz de usuario. Permite a los profesionales del contenido preparar la administración de contenido de producto para próximos lanzamientos del producto
* Administración simplificada de la configuración del CIF y gestión de errores mediante el uso del nombre de configuración en la nube del CIF, en lugar de la URL del proxy de configuración
* Selección manual de categorías para la lista de productos y los componentes de carrusel. Permite a los profesionales del contenido utilizar estos componentes en páginas de contenido, fuera de la experiencia del catálogo

## Fecha de versión: enero de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.01.20.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Componentes principales del CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Sitio de referencia de CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Novedades {#what-is-new-january}

* Componentes myAccount mejorados
* El componente Recomendación de producto admite tipos de página adicionales (página de inicio, carro de compras, confirmación de pedido)
* **Lista de deseos**
   * Los visitantes con sesión iniciada pueden añadir productos a una lista de deseos
   * Es posible administrar la lista de deseos y sus productos a través de myAccount
   * El botón Añadir a la lista de deseos se puede activar o desactivar en un nivel de componente mediante una directiva (por ejemplo, teaser de productos, detalles de productos
   * Disponible como componente principal y en la AEM Venia Storefront

![Lista de deseos](/help/assets/CIF/wishlist.png)
