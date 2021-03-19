---
title: Información general sobre comercio electrónico
seo-title: Información general sobre comercio electrónico
description: AEM comercio electrónico genérico está disponible como parte de la instalación estándar y le proporciona toda la funcionalidad del marco de comercio electrónico.
seo-description: AEM comercio electrónico genérico está disponible como parte de la instalación estándar y le proporciona toda la funcionalidad del marco de comercio electrónico.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Marco de integración de Commerce
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 8%

---


# Información general de comercio electrónico{#ecommerce-overview}

AEM comercio electrónico genérico está disponible como parte de una instalación estándar y le proporciona la funcionalidad completa del marco de comercio electrónico.

Adobe proporciona dos versiones de Commerce Integration Framework:

|  | CIF local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM local o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | - AEM, Java <br> - Integración monolítica, asignación previa a la compilación (plantilla)<br> - Repositorio JCR | - Magento <br>- Java y Javascript <br>: sin datos de comercio almacenados en el repositorio JCR |
| Front-end | AEM páginas procesadas del lado del servidor | Aplicación de página mixta (renderización híbrida) |
| Catálogo de productos | - Importador de productos, editor, almacenamiento en caché en AEM <br>: catálogos regulares con páginas AEM o proxy | - Sin importación de productos <br>- Plantillas genéricas <br>: datos bajo demanda a través del conector |
| Escalabilidad | - Puede admitir hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché en Dispatcher | - Sin limitación de volumen <br>- Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema de Magento GraphQL |
| Disponibilidad | Sí:<br> - Commerce Cloud SAP (la extensión se ha actualizado para admitir AEM 6.4 e Hybris 5 (valor predeterminado) y mantiene la compatibilidad con Hybris 4 <br> - Commerce Cloud Salesforce (conector de código abierto para admitir AEM 6.4) | Sí, a través de código abierto a través de GitHub. <br> Magento Commerce (admite Magento 2.3.2 (predeterminado) y compatible con Magento 2.3.1). |
| Cuándo se utiliza | Casos de uso limitados: Para situaciones en las que sea necesario importar catálogos estáticos pequeños | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

Para AEM y Magento, consulte [AEM e integración del Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) con el [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de las implementaciones de comercio electrónico, consulte [Administración de comercio electrónico](/help/sites-administering/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/sites-developing/ecommerce.md).

