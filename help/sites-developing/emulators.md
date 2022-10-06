---
title: Emuladores
seo-title: Emulators
description: AEM permite a los autores ver una página en un emulador que simula el entorno en el que un usuario final verá la página
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Emuladores{#emulators}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) permite a los autores ver una página en un emulador que simula el entorno en el que un usuario final verá la página, como en un dispositivo móvil o en un cliente de correo electrónico.

El marco del emulador de AEM:

* Proporciona creación de contenido dentro de una interfaz de usuario (IU) simulada, por ejemplo, un dispositivo móvil o un cliente de correo electrónico (se utiliza para crear boletines).
* Adapta el contenido de la página según la IU simulada.
* Permite la creación de emuladores personalizados.

>[!CAUTION]
>
>Esta función solo se admite en la IU clásica.

## Características de los emuladores {#emulators-characteristics}

Un emulador:

* Se basa en ExtJS.
* Funciona en la página DOM.
* Su aspecto se regula mediante CSS.
* Admite complementos (por ejemplo, el complemento de rotación de dispositivos móviles).
* Solo está activo en el autor.
* Su componente base se encuentra en `/libs/wcm/emulator/components/base`.

### Transformación del contenido mediante el emulador {#how-the-emulator-transforms-the-content}

El emulador actúa envolviendo el contenido del cuerpo del HTML en los DIVs emuladores. Por ejemplo, el siguiente código html:

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

se transforma en el siguiente código html después del inicio del emulador:

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

Se han añadido dos etiquetas div:

* el div con id `cq-emulator` manteniendo el emulador en su conjunto y

* el div con id `cq-emulator-content` que representa la ventanilla móvil/pantalla/área de contenido del dispositivo en la que reside el contenido de la página.

Las nuevas clases CSS también se asignan a los nuevos divs del emulador: representan el nombre del emulador actual.

Los complementos de un emulador pueden ampliar aún más la lista de clases CSS asignadas, como en el ejemplo del complemento de rotación, insertando una clase &quot;vertical&quot; u &quot;horizontal&quot; en función de la rotación actual del dispositivo.

De este modo, la apariencia completa del emulador se puede controlar teniendo clases CSS que correspondan a los ID y las clases CSS de los divs del emulador.

>[!NOTE]
>
>Se recomienda que el HTML del proyecto ajuste el contenido del cuerpo en un solo div, como en el ejemplo anterior. Si el contenido del cuerpo contiene varias etiquetas, puede haber resultados impredecibles.

### Emuladores móviles {#mobile-emulators}

Los emuladores móviles existentes:

* Se encuentran debajo de /libs/wcm/mobile/components/emulators.
* Están disponibles a través del servlet JSON en:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Cuando el componente de página depende del componente de página móvil ( `/libs/wcm/mobile/components/page`), la funcionalidad del emulador se integra automáticamente en la página a través del siguiente mecanismo:

* El componente de página móvil `head.jsp` incluye el componente init del emulador asociado del grupo de dispositivos (solo en modo de autor) y el CSS de renderización del grupo de dispositivos mediante:

   `deviceGroup.drawHead(pageContext);`

* El método `DeviceGroup.drawHead(pageContext)` incluye el componente init del emulador, es decir, llama a la función `init.html.jsp` del componente emulador. Si el componente emulador no tiene su propio `init.html.jsp` y depende del emulador de base móvil ( `wcm/mobile/components/emulators/base)`, el script de inicio del emulador de base móvil se llama ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* El script de inicio del emulador de base móvil define a través de JavaScript:

   * La configuración de todos los emuladores definidos para la página (emulatorConfigs)
   * El administrador de emuladores que integra la funcionalidad del emulador en la página mediante:

      `emulatorMgr.launch(config)`;

      El gestor de emuladores se define mediante:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creación de un emulador móvil personalizado {#creating-a-custom-mobile-emulator}

Para crear un emulador móvil personalizado:

1. Abajo `/apps/myapp/components/emulators` crear el componente `myemulator` (tipo de nodo: `cq:Component`).

1. Establezca la propiedad `sling:resourceSuperType` en `/libs/wcm/mobile/components/emulators/base`

1. Definir una biblioteca de cliente CSS con categoría `cq.wcm.mobile.emulator` para el aspecto del emulador: name = `css`, tipo de nodo = `cq:ClientLibrary`

   Como ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Si es necesario, defina una biblioteca de cliente JS, por ejemplo, para definir un complemento específico: name = js, tipo de nodo = cq:ClientLibrary

   Como ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Si el emulador admite funcionalidades específicas definidas por complementos (como el desplazamiento táctil), cree un nodo de configuración debajo del emulador: name = `cq:emulatorConfig`, tipo de nodo = `nt:unstructured` y añada la propiedad que define el complemento:

   * Nombre = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de rotación.

   * Nombre = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de desplazamiento táctil.
   Se pueden agregar más funcionalidades definiendo sus propios complementos.
