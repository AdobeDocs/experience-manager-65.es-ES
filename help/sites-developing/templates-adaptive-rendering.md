---
title: Representación de plantilla adaptable
seo-title: Adaptive Template Rendering
description: Representación de plantilla adaptable
seo-description: null
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Representación de plantilla adaptable{#adaptive-template-rendering}

La renderización de plantillas adaptables permite administrar una página con variaciones. Esta función, originalmente útil para ofrecer varios resultados de HTML para dispositivos móviles (p. ej., teléfono móvil o smartphone), resulta útil cuando hay que entregar experiencias a varios dispositivos que necesitan distintos resultados de marcado o HTML.

## Información general {#overview}

Las plantillas generalmente se crean en torno a una cuadrícula adaptable, y las páginas creadas en función de estas plantillas son totalmente adaptables, ajustándose automáticamente a la ventanilla del dispositivo cliente. Mediante la barra de herramientas Emulador del editor de páginas, los autores pueden dirigir los diseños a dispositivos específicos.

También es posible configurar plantillas para admitir el procesamiento adaptable. Cuando los grupos de dispositivos están correctamente configurados, la página se procesará con un selector diferente en la dirección URL al seleccionar un dispositivo en el modo emulador. Con un selector se puede llamar directamente a un procesamiento de página específico mediante la dirección URL.

Recuerde al configurar los grupos de dispositivos:

* Todos los dispositivos deben estar en al menos un grupo de dispositivos.
* Un dispositivo puede estar en varios grupos de dispositivos.
* Como los dispositivos pueden estar en varios grupos de dispositivos, se pueden combinar selectores.
* La combinación de selectores se evalúa de arriba a abajo ya que se mantienen en el repositorio.

>[!NOTE]
>
>El grupo de dispositivos **Dispositivos interactivos** nunca tendrá un selector porque se supone que los dispositivos reconocidos como compatibles con el diseño interactivo no necesitan un diseño adaptable

## Configuración {#configuration}

Los selectores de renderización adaptables se pueden configurar para grupos de dispositivos existentes o para [grupos que haya creado usted mismo.](/help/sites-developing/mobile.md#device-groups)

Para este ejemplo, vamos a configurar el grupo de dispositivos existente **Teléfonos inteligentes** para tener un selector de renderización adaptable como parte de **Página de experiencia** en We.Retail.

1. Edite el grupo de dispositivos que requiere un selector adaptable en `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Establecer la opción **Deshabilitar emulador** y guarde.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. El selector estará disponible para la variable **BlackBerry** y **iPhone 4** proporcionó el grupo de dispositivos **Teléfono inteligente** se agrega a la plantilla y a las estructuras de página en los pasos siguientes.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Con CRX DE Lite, permita que el grupo de dispositivos se utilice en la plantilla al agregarla a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura de la plantilla.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Por ejemplo, si queremos agregar el grupo de dispositivos Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Con CRX DE Lite, permita que el grupo de dispositivos se utilice en su sitio agregándolo a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura del sitio.

   `/content/<your-site>/jcr:content`

   Por ejemplo, si queremos permitir la variable **Teléfono inteligente** grupo de dispositivos:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ahora, al usar la variable [emulador](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) en el editor de páginas (por ejemplo, cuando [modificación del diseño](/help/sites-authoring/responsive-layout.md)) y elige un dispositivo del grupo de dispositivos configurado, la página se procesará con un selector como parte de la dirección URL.

En nuestro ejemplo, al editar una página basada en la variable **Página de experiencia** y, al elegir iPhone 4 en el emulador, la página se procesa, incluido el selector como `arctic-surfing-in-lofoten.smart.html` en lugar de `arctic-surfing-in-lofoten.html`

También se puede llamar a la página directamente mediante este selector.

![chlimage_1-161](assets/chlimage_1-161.png)
