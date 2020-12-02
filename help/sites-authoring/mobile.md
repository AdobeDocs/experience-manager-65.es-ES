---
title: Crear una página para dispositivos móviles
seo-title: Crear una página para dispositivos móviles
description: Al crear un elemento para móvil, puede cambiar entre varios emuladores para ver qué es lo que verá el usuario final
seo-description: Al crear un elemento para móvil, puede cambiar entre varios emuladores para ver qué es lo que verá el usuario final
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 89%

---


# Crear una página para dispositivos móviles {#authoring-a-page-for-mobile-devices}

Cuando se crea una página móvil, esta se muestra de un modo que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que verá el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página para móvil, AEM detecta el dispositivo y envía la representación correspondiente al grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio para móvil según un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para Canales diferentes](/help/sites-administering/msm-livecopy.md)).
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de Filtros de grupo de dispositivos](/help/sites-developing/groupfilters.md)).

Utilice el siguiente procedimiento para crear una página para móvil:

1. En la navegación global, abra la consola **Sitios**.
1. Abra la página **We.Retail** -> **Estados Unidos** -> **Inglés**.

1. Cambie al modo **Previsualización**.
1. Cambie al emulador que quiera usar haciendo clic en el icono del dispositivo en la parte superior de la página.
1. Arrastre los componentes del navegador de componentes y colóquelos en la página.

La página presenta un aspecto similar al siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil.

