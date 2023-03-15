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

La renderización de plantillas adaptables permite administrar una página con variaciones. Esta función, que en un principio fue útil para ofrecer varias salidas de HTML para dispositivos móviles (por ejemplo, para teléfonos funcionales o smartphones), resulta útil cuando las experiencias tienen que entregarse a varios dispositivos que necesitan diferentes salidas de HTML o marcado.

## Información general {#overview}

Las plantillas generalmente se crean en torno a una cuadrícula adaptable y las páginas creadas en función de estas plantillas son totalmente adaptables, ajustándose automáticamente a la ventanilla del dispositivo cliente. Mediante la barra de herramientas Emulador del editor de páginas, los autores pueden dirigir los diseños a dispositivos específicos.

También es posible configurar plantillas para admitir el procesamiento adaptable. Cuando los grupos de dispositivos están correctamente configurados, la página se procesa con un selector diferente en la dirección URL al seleccionar un dispositivo en modo de emulador. Mediante un selector, se puede llamar directamente a una renderización de página específica a través de la dirección URL.

Recuerde al configurar los grupos de dispositivos:

* Todos los dispositivos deben estar en al menos un grupo de dispositivos.
* Un dispositivo puede estar en varios grupos de dispositivos.
* Los selectores se pueden combinar porque los dispositivos pueden estar en varios grupos.
* La combinación de selectores se evalúa de arriba a abajo a medida que se mantienen en el repositorio.

>[!NOTE]
>
>El grupo de dispositivos **Dispositivos interactivos** nunca tendrá un selector porque se supone que los dispositivos que admiten un diseño adaptable no necesitan un diseño adaptable

## Configuración {#configuration}

Los selectores de procesamiento adaptable se pueden configurar para grupos de dispositivos existentes o para [grupos que ha creado usted mismo.](/help/sites-developing/mobile.md#device-groups)

Para este ejemplo, vamos a configurar el grupo de dispositivos existente **Teléfonos inteligentes** para tener un selector de procesamiento adaptable como parte de **Página de experiencia** plantilla dentro de We.Retail.

1. Edite el grupo de dispositivos que requiere un selector adaptable en `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Establezca la opción **Desactivar emulador** y guarde.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. El selector estará disponible para el **Blackberry** y **IPHONE 4** proporcionado por el grupo de dispositivos **Teléfono inteligente** se añade a las estructuras de plantilla y página en los pasos siguientes.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Con CRX DE Lite, permita que el grupo de dispositivos se utilice en la plantilla agregándolo a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura de la plantilla.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Por ejemplo, si queremos agregar el grupo de dispositivos Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Con CRX DE Lite, permita que el grupo de dispositivos se utilice en el sitio agregándolo a la propiedad de cadena de varios valores `cq:deviceGroups` en la estructura del sitio.

   `/content/<your-site>/jcr:content`

   Por ejemplo, si queremos permitir el **Teléfono inteligente** grupo de dispositivos:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ahora, al usar el [emulador](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) en el editor de páginas (como cuando [modificación del diseño](/help/sites-authoring/responsive-layout.md)) y elija un dispositivo del grupo de dispositivos configurado, la página se procesará con un selector como parte de la dirección URL.

En nuestro ejemplo, al editar una página basada en la variable **Página de experiencia** y, al elegir iPhone 4 en el emulador, se procesa la página incluyendo el selector de como `arctic-surfing-in-lofoten.smart.html` en lugar de `arctic-surfing-in-lofoten.html`

También se puede llamar directamente a la página utilizando este selector.

![chlimage_1-161](assets/chlimage_1-161.png)
