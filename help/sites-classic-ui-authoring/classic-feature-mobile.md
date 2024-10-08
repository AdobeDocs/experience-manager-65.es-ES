---
title: Creación de una página para dispositivos móviles
description: Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que ve el usuario final al acceder a la página.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 52%

---

# Crear una página para dispositivos móviles{#authoring-a-page-for-mobile-devices}

Al crear una página móvil, esta se muestra de forma que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que ve el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página móvil, AEM detecta el dispositivo y envía la representación que corresponde a su grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio móvil basado en un sitio estándar existente, cree una Live Copy del sitio estándar. (Consulte [Creación de una Live Copy para diferentes canales](/help/sites-administering/msm-livecopy.md)).
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. (Consulte [Creación de filtros de grupo de dispositivos.](/help/sites-developing/groupfilters.md))

Utilice el siguiente procedimiento para crear una página para móvil:

1. En su explorador, vaya a la consola **Siteadmin**.
1. Geometrixx Abra la página **Productos** debajo de **Sitios web** >> **Sitio de demostración móvil** >> **Inglés**.

1. Cambie a un emulador diferente. Para ello, puede hacer lo siguiente:

   * Haga clic en el icono del dispositivo en la parte superior de la página.
   * Haga clic en el botón **Editar** del **Sidekick** y seleccione el dispositivo en el menú desplegable.

1. Arrastre y suelte el componente **Texto e imagen** de la pestaña Móvil del Sidekick a la página.
1. Edite el componente y añada texto. Haga clic en **Aceptar** para guardar los cambios.

La página tiene el mismo aspecto que el siguiente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil. La creación se puede realizar mediante la IU táctil.
