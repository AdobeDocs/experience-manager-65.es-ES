---
title: Migración al complemento AEM Commerce Integration Framework (CIF)
description: Cómo migrar al complemento AEM Commerce Integration Framework (CIF) desde una versión antigua
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---

# Guía de migración para el complemento de Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de complementos de Experience Manager.

## Complemento CIF

El complemento CIF está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Es compatible y proporciona las mismas funciones que el complemento CIF para Experience Manager como Cloud Service.

Consulte [Introducción a Contenido y comercio de AEM](getting-started.md).

Para admitir proyectos que implementen el Adobe CIF, proporcione [AEM componentes principales del CIF](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

El complemento CIF no admite la importación de datos del catálogo de productos. Mediante el uso de las entidades de seguridad adicionales del CIF, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externa. Vaya a Integrar para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externa con API para la integración. Ejemplo de [Magento de código abierto](https://magento.com/products/magento-open-source).

## Experiencias del catálogo de productos con AEM renderización

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. El complemento CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante AEM plantillas de catálogo. Ya no es necesaria la duplicación de datos de productos o páginas de productos.

## Interacción de compras y datos no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones que no se pueden almacenar en caché (por ejemplo, añadir al carro, buscar) deben ir directamente al extremo de comercio (solución de comercio o capa de integración) a través de CDN/Dispatcher. Elimine las llamadas donde AEM era solo un proxy.
