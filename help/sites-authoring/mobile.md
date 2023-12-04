---
title: Creación de una página de contenido para dispositivos móviles
description: Al crear para móviles, puede cambiar entre varios emuladores para ver lo que ve el usuario final.
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 63%

---

# Crear una página para dispositivos móviles{#authoring-a-page-for-mobile-devices}

Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que ve el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página móvil, AEM detecta el dispositivo y envía la representación que corresponde a su grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio móvil basado en un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para diferentes canales](/help/sites-administering/msm-livecopy.md).)
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de filtros de grupo de dispositivos](/help/sites-developing/groupfilters.md).)

Utilice el siguiente procedimiento para crear una página para móvil:

1. En la navegación global, abra la consola **Sitios**.
1. Abra la página. **We.Retail** > **Estados Unidos** > **Inglés**.

1. Cambiar a **Previsualizar** modo.
1. Cambie al emulador que desee haciendo clic en el icono del dispositivo en la parte superior de la página.
1. Arrastre y suelte los componentes desde el navegador de componentes a la página.

La página tiene un aspecto similar al siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil.
