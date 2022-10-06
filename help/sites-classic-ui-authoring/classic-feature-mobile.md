---
title: Crear una página para dispositivos móviles
seo-title: Authoring a Page for Mobile Devices
description: Cuando se crea una página móvil, esta se muestra de un modo que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que verá el usuario final al acceder a la página.
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 82%

---

# Crear una página para dispositivos móviles{#authoring-a-page-for-mobile-devices}

Cuando se crea una página móvil, esta se muestra de un modo que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que verá el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página para móvil, AEM detecta el dispositivo y envía la representación correspondiente al grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio para móvil según un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para diferentes canales](/help/sites-administering/msm-livecopy.md).)
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de filtros de grupo de dispositivos.](/help/sites-developing/groupfilters.md))

Utilice el siguiente procedimiento para crear una página para móvil:

1. En el navegador, vaya a la consola **Siteadmin**.
1. Abra el **Productos** página siguiente **Sitios web** >> **Sitio de demostración de Geometrixx Mobile** >> **Inglés**.

1. Cambie a un emulador diferente. Para ello, puede:

   * Hacer clic en el icono del dispositivo en la parte superior de la página.
   * Hacer clic en el botón **Editar** en la **barra de tareas** y seleccionar el dispositivo en el menú desplegable.

1. Arrastre y suelte la **Texto e imagen** de la ficha Móvil de la barra de tareas a la página.
1. Edite el componente y añada texto. Haga clic en **Aceptar** para guardar los cambios.

La página presenta un aspecto similar al siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil. La creación se puede realizar utilizando la IU táctil.
