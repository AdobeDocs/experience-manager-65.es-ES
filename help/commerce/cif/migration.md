---
title: AEM Migración al complemento Commerce integration framework CIF de la ()
description: AEM Cómo migrar al complemento de Commerce integration framework CIF de () desde una versión antigua.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%

---

# Guía de migración para el complemento Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración del complemento de Experience Manager.

## CIF Complemento de

CIF AEM El complemento de está disponible para la versión 6.5 de a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). CIF Es compatible y proporciona las mismas características que el complemento de para Experience Manager as a Cloud Service.

AEM Consulte [Introducción al contenido de la y Commerce](getting-started.md).

Para apoyar proyectos que implementen CIF, Adobe proporciona [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

CIF El complemento no admite la importación de datos del catálogo de productos de. CIF Al usar las entidades de seguridad de complemento de la aplicación, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## AEM Experiencias del catálogo de productos con renderización de

CIF Si utiliza el modelo de catálogo con la versión clásica de los productos, debe actualizar el flujo de trabajo del catálogo de productos. CIF AEM El complemento ahora procesa experiencias del catálogo de productos sobre la marcha utilizando plantillas de catálogo de productos de la aplicación de la manera más rápida y sencilla Ya no se requiere replicación de datos o páginas de productos.

## Interacción de datos y compras no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complemento al carro, búsqueda) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. AEM Elimine todas las llamadas en las que solo haya un proxy en el que se haya realizado la.
