---
title: Creación de una página de contenido para dispositivos móviles
description: Al crear para móviles, puede cambiar entre varios emuladores para ver lo que ve el usuario final.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 63%

---

# Creación de una página para dispositivos móviles{#authoring-a-page-for-mobile-devices}

Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que ve el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página móvil, AEM detecta el dispositivo y envía la representación que corresponde a su grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio móvil basado en un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para diferentes canales](/help/sites-administering/msm-livecopy.md)).
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de filtros de grupo de dispositivos](/help/sites-developing/groupfilters.md).)

Utilice el siguiente procedimiento para crear una página para móvil:

1. En la navegación global, abra la consola **Sitios**.
1. Abra la página **We.Retail** > **Estados Unidos** > **Inglés**.

1. Cambiar al modo **Vista previa**.
1. Cambie al emulador que desee haciendo clic en el icono del dispositivo en la parte superior de la página.
1. Arrastre y suelte los componentes desde el navegador de componentes a la página.

La página tiene un aspecto similar al siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando una página de la instancia de autor se solicita desde un dispositivo móvil.
