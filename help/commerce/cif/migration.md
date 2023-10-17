---
title: AEM Migración al complemento Commerce integration framework CIF de la ()
description: AEM Cómo migrar al complemento de Commerce integration framework CIF de () desde una versión antigua.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Guía de migración para el complemento Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración del complemento de Experience Manager.

## CIF Complemento de

CIF AEM El complemento de está disponible para la versión 6.5 de a través de la [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). CIF Es compatible y proporciona las mismas características que el complemento de la para Experience Manager as a Cloud Service.

Consulte [AEM Introducción a Contenido y comercio de](getting-started.md).

CIF Para admitir la implementación de proyectos, el Adobe de proporciona lo siguiente: [AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

CIF El complemento no admite la importación de datos del catálogo de productos de. CIF Al usar las entidades de seguridad de complemento de la aplicación, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## AEM Experiencias del catálogo de productos con renderización de

CIF Si utiliza el modelo de catálogo con la versión clásica de los productos, debe actualizar el flujo de trabajo del catálogo de productos. CIF AEM El complemento ahora procesa experiencias del catálogo de productos sobre la marcha utilizando plantillas de catálogo de productos de la aplicación de la manera más rápida y sencilla Ya no se requiere replicación de datos o páginas de productos.

## Interacción de datos y compras no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complementos al carro de compras o búsquedas) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. AEM Elimine todas las llamadas en las que solo haya un proxy en el que se haya realizado la.
