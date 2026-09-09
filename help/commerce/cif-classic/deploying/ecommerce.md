---
title: Información general sobre comercio electrónico
description: El comercio electrónico genérico de AEM está disponible como parte de la instalación estándar y le proporciona todas las funciones del marco de comercio electrónico.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 4%

---

# Información general sobre comercio electrónico{#ecommerce-overview}

El comercio electrónico genérico de AEM está disponible como parte de una instalación estándar y le proporciona todas las funciones del marco de comercio electrónico.

Adobe proporciona dos versiones de Commerce integration framework:

|                         | CIF local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM local o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | - AEM, Java™ <br> - Integración monolítica, asignación previa a la compilación (plantilla)<br> - Repositorio JCR | - Adobe Commerce <br>- Java y JavaScript <br>- No hay datos de Commerce almacenados en el repositorio JCR |
| Front-end | Páginas procesadas del lado del servidor de AEM | Aplicación de página mixta (procesamiento híbrido) |
| Catálogo de productos | - Importador, editor y almacenamiento en caché de productos en AEM <br>: catálogos normales con páginas de AEM o proxy | - Sin importación de producto <br>- Plantillas genéricas <br>- Datos a petición mediante conector |
| Escalabilidad | - Puede admitir hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché en Dispatcher | - Sin limitación de volumen <br> - Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema de Adobe Commerce GraphQL |
| Disponibilidad | Sí: <br> - SAP Commerce Cloud (extensión actualizada para admitir AEM 6.4 e Hybris 5 (predeterminado) y mantiene la compatibilidad con Hybris 4 <br>- Salesforce Commerce Cloud (conector de código abierto para admitir AEM 6.4) | Sí a través de código abierto mediante GitHub. <br> Adobe Commerce (compatible con 2.3.2 (predeterminado) y con 2.3.1). |
| Cuándo se usa | Casos de uso limitados: en escenarios donde sea pequeño, importe catálogos estáticos según sea necesario | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

Para AEM y Adobe Commerce, consulte [Integración de AEM y Adobe Commerce](/help/commerce/cif/integrating/magento.md) con [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de las implementaciones de comercio electrónico, consulte [Administración de comercio electrónico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obtener información sobre cómo ampliar las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).
