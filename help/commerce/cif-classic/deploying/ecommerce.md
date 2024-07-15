---
title: Información general de eCommerce
description: AEM El comercio electrónico genérico está disponible como parte de la instalación estándar y le proporciona todas las funciones del marco de comercio electrónico.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# Información general de eCommerce{#ecommerce-overview}

AEM El comercio electrónico genérico está disponible como parte de una instalación estándar y le proporciona todas las funciones del marco de comercio electrónico.

Adobe proporciona dos versiones del Commerce integration framework:

|                         | CIF local de la zona de trabajo | CIF Nube de |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versiones de AEM compatibles | AEM local o AMS 6.x | AEM AMS 6.4 y 6.5 |
| Back-end | AEM -, Java™ <br> - Integración monolítica, asignación previa a la compilación (plantilla)<br> - Repositorio JCR | - Adobe Commerce <br>- Java y JavaScript <br>- No hay datos de Commerce almacenados en el repositorio JCR |
| Front-end | AEM Páginas procesadas del lado del servidor de | Aplicación de página mixta (procesamiento híbrido) |
| Catálogo de productos | AEM AEM - Importador, editor y almacenamiento en caché de productos en la caché de <br>: catálogos normales con páginas de proxy o de | - Sin importación de producto <br>- Plantillas genéricas <br>- Datos a petición mediante conector |
| Escalabilidad | - Puede admitir hasta unos pocos millones de productos (depende del caso de uso) <br> - Almacenamiento en caché en Dispatcher | - Sin limitación de volumen <br> - Almacenamiento en caché en Dispatcher o CDN |
| Modelo de datos estandarizado | No | Sí, esquema de Adobe Commerce GraphQL |
| Disponibilidad | Sí: <br> - Commerce Cloud AEM de SAP (extensión actualizada para admitir la versión 6.4 e Hybris 5 (predeterminada)) y mantiene la compatibilidad con la versión 4 de Hybris <br> - Commerce Cloud AEM de Salesforce (conector de código abierto para admitir la versión 6.4) de la versión 6.4 del conector de código abierto). | Sí a través de código abierto mediante GitHub. <br> Adobe Commerce (compatible con 2.3.2 (predeterminado) y con 2.3.1). |
| Cuándo se usa | Casos de uso limitados: en escenarios donde sea pequeño, importe catálogos estáticos según sea necesario | Solución preferida en la mayoría de los casos de uso |


## Implementación de otras implementaciones {#deploying-other-implementations}

AEM Para obtener información sobre la integración de Adobe Commerce AEM y de los recursos, consulte [integración de y Adobe Commerce](/help/commerce/cif/integrating/magento.md) con el [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obtener información sobre los conceptos y la administración de las implementaciones de comercio electrónico, consulte [Administración de comercio electrónico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obtener información sobre cómo ampliar las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).
