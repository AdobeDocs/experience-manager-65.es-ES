---
title: Notas de la versión 2024 de AEM Commerce y contenido de
description: Contenido de Adobe Experience Manager y notas de la versión de Commerce 2024.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 26%

---

# Información general sobre la versión de Commerce integration framework GitHub

## Descripción general de los requisitos del sistema

CIF Revise los requisitos mínimos del sistema que aparecen en la tabla siguiente para la versión del sistema que está utilizando actualmente o que planea utilizar en el futuro.

| Componente | Requisitos del sistema |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF complemento de | AEM Mínimo: 6.5.18, Adobe Commerce 2.3.5 Esquemas de GraphQL |
| CIF Componentes principales | [Requisitos del sistema](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Tipo de archivo del proyecto AEM | [Requisitos del sistema](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Fecha de versión: octubre de 2024

| Componente | Versión | Detalles |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Componentes principales | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### Corrección de errores {#bug-fixes-October}

* CIF Se han corregido las pruebas de interfaz de usuario para que funcionen correctamente con los componentes principales de.
* Se ha resuelto un problema con el formato de URL de categoría que no funcionaba como se esperaba en la instancia de nube.

## Fecha de versión: septiembre de 2024

| Componente | Versión | Detalles |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Componentes principales | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### Mejoras {#improvements-September}

* Se pueden personalizar los límites de categorías.

### Corrección de errores {#bug-fixes-September}

* Los campos de Commerce no se integran correctamente con el editor de esquemas de metadatos de Assets.
* Problema con campos múltiples de productos del carrusel para arrastrar y soltar.
* Problema con el multicampo de categoría de carrusel para arrastrar y soltar
* Al hacer clic no funciona para los menús de la página de información sobre la categoría y la página del editor de productos.
* El número de pedido no está visible en la página de confirmación de pedido.

## Fecha de versión: enero de 2024

| Componente | Versión | Detalles |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF Componentes principales | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### Corrección de errores {#bug-fixes-january}

* Se ha corregido el botón Añadir al carro y el botón Añadir a la lista de deseos en el componente de colección de productos
