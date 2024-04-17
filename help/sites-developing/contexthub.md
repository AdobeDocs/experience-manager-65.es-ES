---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

>[!NOTE]
>
>El [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub y puede servir de referencia al integrar ContextHub en su propio proyecto.

>[!CAUTION]
>
>La ruta que contiene la configuración de ContextHub de ejemplo que utiliza el [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) solo debe utilizarse como referencia para crear su propia configuración.
>
>No utilice en un proyecto como su propia configuración de ContextHub.

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. De este modo, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona varios [tipos de almacén de muestra](/help/sites-developing/ch-samplestores.md).
* AEM Usar consolas de consola para [crear tiendas](ch-configuring.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de tienda personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Los desarrolladores pueden [datos de tienda de acceso](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) mediante JavaScript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de JavaScript para lo siguiente [determinar segmentos resueltos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentación {#presentation}

El [Barra de herramientas de ContextHub](/help/sites-authoring/ch-previewing.md) permite a los especialistas en marketing y a los autores ver y manipular los datos de almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas consiste en grupos de módulos de interfaz de usuario que proporcionan acceso a los almacenes de ContextHub.

Cada módulo de IU de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios [tipos de módulos de muestra](/help/sites-developing/ch-samplemodules.md).
* AEM Usar consolas de consola para [agregar módulos de IU](ch-configuring.md#adding-a-ui-module), y a [agruparlos en modos de IU](ch-configuring.md#adding-a-ui-mode).

* Los desarrolladores pueden [crear tipos de módulos personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [añadir el componente ContextHub a la página](/help/sites-developing/ch-adding.md).
