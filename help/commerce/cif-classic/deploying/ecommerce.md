---
title: Información general de eCommerce
seo-title: eCommerce Overview
description: AEM El comercio electrónico genérico está disponible como parte de la instalación estándar y proporciona todas las funciones del marco de comercio electrónico.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# Información general de eCommerce{#ecommerce-overview}

AEM El comercio electrónico genérico está disponible como parte de una instalación estándar y le proporciona todas las funciones del marco de comercio electrónico.

Adobe ofrece dos versiones del complemento Commerce Integration Framework:

|  | CIF local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM local o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | AEM -, Java <br> : Integración monolítica, asignación previa a la compilación (plantilla)<br> - Repositorio JCR | - ADOBE COMMERCE <br>- Java y Javascript <br>- No hay datos de comercio almacenados en el repositorio JCR |
| Front-end | AEM Páginas procesadas del lado del servidor de | Aplicación de página mixta (procesamiento híbrido) |
| Catálogo de productos | AEM - Importador de productos, editor, almacenamiento en caché en la <br>AEM - Catálogos normales con páginas de proxy o de la red de distribución de contenido | - No hay importación de productos <br>- Plantillas genéricas <br>- Datos a petición mediante conector |
| Escalabilidad | - Puede admitir hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché en Dispatcher | - Sin limitación de volumen <br>- Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema de Adobe Commerce GraphQL |
| Disponibilidad | Sí:<br> - Commerce Cloud AEM de SAP (extensión actualizada para admitir la versión 6.4 y la versión 5 de Hybris (predeterminada)), que mantiene la compatibilidad con la versión 4 de Hybris). <br>- Commerce Cloud AEM de Salesforce (conector de código abierto para admitir la versión 6.4 de la aplicación de la aplicación de manera independiente). | Sí a través de código abierto mediante GitHub. <br> Adobe Commerce (compatible con 2.3.2 (predeterminado) y con 2.3.1). |
| Cuándo se usa | Casos de uso limitados: en escenarios donde puede ser necesario importar catálogos estáticos pequeños | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

AEM Para obtener más información sobre la versión y Adobe Commerce, consulte [AEM Integración de y Adobe Commerce](/help/commerce/cif/integrating/magento.md) uso del [Commerce Integration Framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de las implementaciones de comercio electrónico, consulte [Administración de eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).
