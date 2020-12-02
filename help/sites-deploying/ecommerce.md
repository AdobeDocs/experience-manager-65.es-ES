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
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 7%

---


# Información general de comercio electrónico{#ecommerce-overview}

AEM comercio electrónico genérico está disponible como parte de una instalación estándar y le proporciona toda la funcionalidad del marco de comercio electrónico.

Adobe proporciona dos versiones de Commerce Integration Framework:

|  | CIF on-prem | Nube CIF |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM on-prem o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | - AEM, Java <br> - Integración monolítica, asignación previa a la compilación (plantilla)<br> - repositorio JCR | - Magento <br>- Java y Javascript <br>- Ningún dato de comercio almacenado en el repositorio JCR |
| Front-end | AEM páginas procesadas en el lado del servidor | Aplicación de página mixta (procesamiento híbrido) |
| Catálogo de productos | - Importador de productos, editor, almacenamiento en caché en AEM <br>- Catálogos regulares con páginas AEM o proxy | - Sin importación de productos <br>- Plantillas genéricas <br>- Datos bajo demanda mediante conector |
| Escalabilidad | - Puede soportar hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché de Dispatcher | - Sin limitación de volumen <br>- Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema Magento GraphQL |
| Disponibilidad | Sí:<br> - Commerce Cloud SAP (Extensión actualizada para admitir AEM 6.4 e Hybris 5 (predeterminado) y mantiene la compatibilidad con Hybris 4 <br> - Commerce Cloud de Salesforce (Conector de código abierto para admitir AEM 6.4) | Sí, vía código abierto vía GitHub. <br> Magento Commerce (admite Magento 2.3.2 (predeterminado) y compatible con Magento 2.3.1). |
| Cuándo usar | Casos de uso limitados: Para situaciones en las que sea necesario importar catálogos estáticos pequeños | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

Para AEM y Magento, consulte [Integración de AEM y Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) mediante el [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de implementaciones de comercio electrónico, consulte [Administración de comercio electrónico](/help/sites-administering/ecommerce.md).
>
>Para obtener información sobre cómo ampliar las capacidades de comercio electrónico, consulte [Desarrollo de comercio electrónico](/help/sites-developing/ecommerce.md).

