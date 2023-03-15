---
title: AEM Migración al complemento Marco de integración de comercio de (CIF)
description: AEM Migración del complemento Commerce Integration Framework (CIF) de la versión antigua a la versión de la plataforma de integración de comercio de la versión de
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Guía de migración para el complemento Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración del complemento de Experience Manager.

## Complemento CIF

AEM El complemento CIF está disponible para la versión 6.5 de a través de la [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas funciones que el complemento CIF para Experience Manager as a Cloud Service.

Consulte [AEM Introducción a Contenido y comercio de](getting-started.md).

Para apoyar proyectos que implementen CIF, Adobe proporciona [AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

El complemento CIF no admite la importación de datos del catálogo de productos. Al usar las entidades principales de complementos del CIF, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## AEM Experiencias del catálogo de productos con renderización de

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. AEM El complemento CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante plantillas de catálogo de productos de la aplicación de la versión de la aplicación de la documentación de la aplicación de la documentación de producto de la aplicación. Ya no se requiere replicación de datos o páginas de productos.

## Interacción de datos y compras no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complementos al carro de compras o búsquedas) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. AEM Elimine todas las llamadas en las que solo haya un proxy en el que se haya realizado la.
