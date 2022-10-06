---
title: ContextHub
seo-title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

>[!NOTE]
>
>La variable [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub y puede servir de referencia cuando integra ContextHub en su propio proyecto.

>[!CAUTION]
>
>La ruta que contiene la configuración de ContextHub de muestra que usa el [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) solo debe utilizarse como referencia para crear su propia configuración.
>
>No debe utilizarse en un proyecto como su propia configuración de ContextHub.

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. Como tal, ContextHub representa una capa de datos en las páginas.

Cada almacén de ContextHub es una instancia de un tipo de almacén predefinido:

* ContextHub proporciona varios [tipos de almacén de muestras](/help/sites-developing/ch-samplestores.md).
* Usar AEM consolas para [crear tiendas](ch-configuring.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de almacén personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Los desarrolladores pueden [datos de almacenamiento de acceso](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) a través de Javascript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de Javascript para [determinar segmentos resueltos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentación {#presentation}

La variable [Barra de herramientas de ContextHub](/help/sites-authoring/ch-previewing.md) permite a los especialistas en marketing y a los autores ver y manipular los datos de almacenamiento para simular la experiencia del usuario al crear páginas. La barra de herramientas está formada por grupos de módulos de IU que proporcionan acceso a los almacenes de ContextHub.

Cada módulo de interfaz de usuario de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios [tipos de módulo de muestra](/help/sites-developing/ch-samplemodules.md).
* Usar AEM consolas para [añadir módulos de IU](ch-configuring.md#adding-a-ui-module)y [agruparlos en modos de IU](ch-configuring.md#adding-a-ui-mode).

* Los desarrolladores pueden [crear tipos de módulos personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [añadir el componente ContextHub a la página](/help/sites-developing/ch-adding.md).
