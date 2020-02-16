---
title: ContextHub
seo-title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
seo-description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ContextHub{#contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

>[!NOTE]
>
>La implementación [de referencia de](/help/sites-developing/we-retail.md) We.Retail implementa ContextHub y puede servir como referencia a medida que integra ContextHub en su propio proyecto.

>[!CAUTION]
>
>La ruta que contiene la configuración de ContextHub de muestra utilizada por la implementación [de referencia de](/help/sites-developing/we-retail.md) We.Retail ( `/libs/settings/cloudsettings/legacy`) solo debe utilizarse como referencia para crear su propia configuración.
>
>No debe utilizarse en un proyecto como su propia configuración de ContextHub.

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. Como tal, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona varios tipos [de almacén de](/help/sites-developing/ch-samplestores.md)muestra.
* Utilice las consolas de AEM para [crear tiendas](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)de tienda personalizados.
* Los desarrolladores pueden [acceder a los datos](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) del almacén a través de Javascript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de JavaScript para [determinar los segmentos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)resueltos.

## Presentación {#presentation}

La barra de herramientas [de](/help/sites-authoring/ch-previewing.md) ContextHub permite a los especialistas en marketing y a los autores ver y manipular los datos del almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas está formada por grupos de módulos de interfaz de usuario que proporcionan acceso a los almacenes de ContextHub.

Cada módulo de interfaz de usuario de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios tipos [de módulos de](/help/sites-developing/ch-samplemodules.md)muestra.
* Utilice las consolas de AEM para [añadir módulos](/help/sites-administering/contexthub-config.md#adding-a-ui-module)de interfaz de usuario y [agruparlos en modos](/help/sites-administering/contexthub-config.md#adding-a-ui-mode)de interfaz de usuario.

* Los desarrolladores pueden [crear tipos](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)de módulos personalizados.

Los desarrolladores deben [agregar el componente ContextHub a la página](/help/sites-developing/ch-adding.md).
