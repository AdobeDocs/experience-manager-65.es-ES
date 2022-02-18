---
title: Notas de la versión de contenido y comercio de AEM 2022
description: Notas de la versión de contenido y comercio de AEM 2022
source-git-commit: 84ac40a5cd18b1a5c8bb7a93af4106be6bda7631
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 45%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Descripción general de los requisitos del sistema

Revise los requisitos mínimos del sistema en la siguiente tabla para la versión del CIF que está utilizando o que planea usar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----:|
| Complemento CIF | Mínimo: AEM 6.5.7, Magento 2.3.5 Esquemas de GraphQL |
| Componentes principales de CIF | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

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

