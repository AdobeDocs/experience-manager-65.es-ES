---
title: Migración al complemento AEM Commerce Integration Framework (CIF)
description: Cómo migrar al complemento AEM Commerce Integration Framework (CIF) desde una versión antigua
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Guía de migración para el complemento Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de complementos de Experience Manager.

## Complemento CIF

El complemento CIF está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas funciones que el complemento CIF para Experience Manager as a Cloud Service.

Consulte [Introducción a Contenido y comercio AEM](getting-started.md).

Para apoyar proyectos que implementen CIF, Adobe proporciona [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

El complemento CIF no admite la importación de datos del catálogo de productos. Mediante el uso de las entidades de seguridad adicionales del CIF, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externa. Vaya a Integrar para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externa con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## Experiencias del catálogo de productos con procesamiento AEM

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. El complemento CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante AEM plantillas de catálogo. Ya no es necesaria la duplicación de datos de productos o páginas de productos.

## Datos no almacenables en caché e interacción de compras

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, añadir al carro, buscar) deben ir directamente al extremo de comercio (solución de comercio o capa de integración) a través de CDN/Dispatcher. Elimine las llamadas donde AEM era solo un proxy.
