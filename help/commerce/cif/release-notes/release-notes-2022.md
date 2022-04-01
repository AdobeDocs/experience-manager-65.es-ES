---
title: Notas de la versión de contenido y comercio de AEM 2022
description: Notas de la versión de contenido y comercio de AEM 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 27%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: Marzo de 2022

| Componente | Versión | Detalles |
|:-------|:-----:|---------------------:|
| Complemento CIF | 2022.02.24.00 | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Componentes principales de CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Sitio de referencia de Venia del CIF | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Novedades {#what-is-new-march}

* Beta: Compatibilidad del componente principal de búsqueda del CIF de AEM con Commerce LiveSearch
* SEO mejorado para escenarios de varias tiendas: Los formatos de URL para PDP/PLP ahora se pueden configurar a nivel de tienda mediante las propiedades de configuración de la nube del CIF
* El selector de productos es compatible con los productos clasificados mediante la nueva opción de filtro en la interfaz de usuario.  Esto permite a los profesionales del contenido preparar la administración del contenido del producto para próximos lanzamientos del producto
* Administración simplificada de la configuración del CIF y gestión de errores mediante el uso del nombre de configuración de la nube del CIF en lugar de la url del proxy de configuración
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
   * La administración de la lista de deseos y sus productos es posible a través de myAccount
   * El botón Añadir a la lista de deseos se puede activar o desactivar en un nivel de componente mediante una directiva (por ejemplo, teaser de productos, detalles de productos
   * Disponible como componente principal y en la AEM Venia Storefront

![Lista de deseos](/help/assets/CIF/wishlist.png)
