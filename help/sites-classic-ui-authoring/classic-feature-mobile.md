---
title: Creación de una página para dispositivos móviles
description: Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver qué ve el usuario final al acceder a la página.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 20%

---

# Crear una página para dispositivos móviles{#authoring-a-page-for-mobile-devices}

Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver qué ve el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página móvil, AEM detecta el dispositivo y envía la representación que corresponde a su grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio móvil basado en un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para diferentes canales](/help/sites-administering/msm-livecopy.md).)
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de filtros de grupo de dispositivos.](/help/sites-developing/groupfilters.md))

Utilice el siguiente procedimiento para crear una página para móvil:

1. En el explorador, vaya a la **Siteadmin** consola.
1. Abra el **Productos** página siguiente **Sitios web** >> **Sitio de demostración de Geometrixx Mobile** >> **Inglés**.

1. Cambie a un emulador diferente. Para ello, puede:

   * Haga clic en el icono del dispositivo en la parte superior de la página.
   * Haga clic en el **Editar** en el **Barra de tareas** y seleccione el dispositivo en el menú desplegable.

1. Arrastre y suelte la **Texto e imagen** de la ficha Móvil de la barra de tareas a la página.
1. Edite el componente y añada texto. Haga clic en **OK** para guardar los cambios.

La página tiene el mismo aspecto que la siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil. La creación se puede realizar utilizando la IU táctil.
