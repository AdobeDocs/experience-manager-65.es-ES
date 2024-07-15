---
title: Representación de plantilla adaptable
description: Obtenga información acerca del procesamiento de plantillas adaptables en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Representación de plantilla adaptable{#adaptive-template-rendering}

La renderización de plantillas adaptables permite administrar una página con variaciones. Esta función, que en un principio fue útil para ofrecer varias salidas de HTML para dispositivos móviles (por ejemplo, para teléfonos funcionales frente a smartphones), resulta útil cuando las experiencias deben entregarse a varios dispositivos que necesitan un marcado o una salida de HTML diferentes.

## Información general {#overview}

Las plantillas se crean en torno a una cuadrícula adaptable y las páginas creadas en función de estas plantillas son totalmente adaptables, ajustándose automáticamente a la ventanilla del dispositivo cliente. Mediante la barra de herramientas Emulador del editor de páginas, los autores pueden dirigir los diseños a dispositivos específicos.

También es posible configurar plantillas para admitir el procesamiento adaptable. Cuando los grupos de dispositivos están correctamente configurados, la página se representa con un selector diferente en la dirección URL al seleccionar un dispositivo en el modo de emulador. Mediante un selector, se puede llamar directamente a una renderización de página específica a través de la dirección URL.

Recuerde al configurar los grupos de dispositivos:

* Todos los dispositivos deben estar en al menos un grupo de dispositivos.
* Un dispositivo puede estar en varios grupos de dispositivos.
* Los selectores se pueden combinar porque los dispositivos pueden estar en varios grupos.
* La combinación de selectores se evalúa de arriba a abajo a medida que se mantienen en el repositorio.

>[!NOTE]
>
>El grupo de dispositivos **Dispositivos interactivos nunca tiene un selector porque se supone que los dispositivos que admiten un diseño interactivo no necesitan un diseño adaptable

## Configuración {#configuration}

Los selectores de procesamiento adaptable se pueden configurar para grupos de dispositivos existentes o para [grupos que usted mismo haya creado.](/help/sites-developing/mobile.md#device-groups)

Para este ejemplo, va a configurar el grupo de dispositivos existente **Teléfonos inteligentes** para que tenga un selector de procesamiento adaptable como parte de la plantilla **Página de experiencia** en We.Retail.

1. Edite el grupo de dispositivos que requiere un selector adaptable en `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Establece la opción **Deshabilitar emulador** y guarda.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. El selector está disponible para **BlackBerry®** y **iPhone 4**, siempre que el grupo de dispositivos **Teléfono inteligente** se agregue a las estructuras de plantilla y página en los pasos siguientes.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Con el CRXDE Lite, permita que se utilice el grupo de dispositivos en la plantilla agregándolo a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura de la plantilla.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Por ejemplo, si desea agregar el grupo de dispositivos Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Con el CRXDE Lite, permita que se utilice el grupo de dispositivos en el sitio agregándolo a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura del sitio.

   `/content/<your-site>/jcr:content`

   Por ejemplo, si desea permitir el grupo de dispositivos **Teléfono inteligente**:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ahora, al usar el [emulador](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) en el editor de páginas (como cuando [modifica el diseño](/help/sites-authoring/responsive-layout.md)) y elige un dispositivo del grupo de dispositivos configurado, la página se procesa con un selector como parte de la dirección URL.

En este ejemplo, al editar una página basada en la plantilla **Experience Page** y elegir iPhone 4 en el emulador, la página se representa incluyendo el selector como `arctic-surfing-in-lofoten.smart.html` en lugar de `arctic-surfing-in-lofoten.html`

También se puede llamar directamente a la página utilizando este selector.

![chlimage_1-161](assets/chlimage_1-161.png)
