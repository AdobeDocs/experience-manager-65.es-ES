---
title: Información general sobre comercio electrónico
seo-title: eCommerce Overview
description: AEM comercio electrónico genérico está disponible como parte de la instalación estándar y le proporciona toda la funcionalidad del marco de comercio electrónico.
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

# Información general sobre comercio electrónico{#ecommerce-overview}

AEM comercio electrónico genérico está disponible como parte de una instalación estándar y le proporciona la funcionalidad completa del marco de comercio electrónico.

Adobe proporciona dos versiones de Commerce Integration Framework:

|  | CIF local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM local o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | - AEM, Java <br> - Integración monolítica, asignación previa a la compilación (plantilla)<br> : repositorio JCR | - Adobe Commerce <br>- Java y Javascript <br>- No hay datos de comercio almacenados en el repositorio JCR |
| Front-end | AEM páginas procesadas del lado del servidor | Aplicación de página mixta (renderización híbrida) |
| Catálogo de productos | - Importador de productos, editor, almacenamiento en caché en AEM <br>- Catálogos regulares con páginas AEM o proxy | - Sin importación de productos <br>- Plantillas genéricas <br>- Datos bajo demanda a través del conector |
| Escalabilidad | - Puede admitir hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché en Dispatcher | - Sin limitación de volumen <br>- Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema de Adobe Commerce GraphQL |
| Disponibilidad | Sí:<br> - Commerce Cloud SAP (extensión actualizada para admitir AEM 6.4 e Hybris 5 (predeterminado) y mantiene la compatibilidad con Hybris 4 <br>- Commerce Cloud de Salesforce (conector de código abierto compatible con AEM 6.4) | Sí, a través de código abierto a través de GitHub. <br> Adobe Commerce (compatible con 2.3.2 (predeterminado) y 2.3.1). |
| Cuándo se usa | Casos de uso limitados: Para situaciones en las que sea necesario importar catálogos estáticos pequeños | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

Para AEM y Adobe Commerce, consulte [Integración de AEM y Adobe Commerce](/help/commerce/cif/integrating/magento.md) usando la variable [Commerce Integration Framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de las implementaciones de comercio electrónico, consulte [Administración del comercio electrónico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).
