---
title: Emuladores
seo-title: Emuladores
description: AEM permite a los autores realizar la vista de una página en un emulador que simula el entorno en el que un usuario final realizará la vista de la página
seo-description: AEM permite a los autores realizar la vista de una página en un emulador que simula el entorno en el que un usuario final realizará la vista de la página
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Emuladores{#emulators}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) permite a los autores crear vistas de una página en un emulador que simula el entorno en el que un usuario final vista la página, por ejemplo, en un dispositivo móvil o en un cliente de correo electrónico.

El marco del emulador de AEM:

* Proporciona creación de contenido dentro de una interfaz de usuario (IU) simulada, por ejemplo, un dispositivo móvil o un cliente de correo electrónico (utilizado para crear newsletters).
* Adapta el contenido de la página según la IU simulada.
* Permite la creación de emuladores personalizados.

>[!CAUTION]
>
>Esta función solo se admite en la IU clásica.

## Características de los emuladores {#emulators-characteristics}

Un emulador:

* Se basa en ExtJS.
* Funciona en el DOM de la página.
* Su aspecto está regulado mediante CSS.
* Admite complementos (por ejemplo, el complemento de rotación del dispositivo móvil).
* Solo está activo en el autor.
* Su componente base es `/libs/wcm/emulator/components/base`.

### Cómo el emulador transforma el contenido {#how-the-emulator-transforms-the-content}

El emulador funciona ajustando el contenido del cuerpo HTML en DIV del emulador. Por ejemplo, el siguiente código HTML:

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

se transforma en el siguiente código HTML después del inicio del emulador:

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

Se han agregado dos etiquetas div:

* el div con id `cq-emulator` que contiene el emulador como un todo y

* el div con el identificador `cq-emulator-content` que representa la ventanilla del dispositivo, la pantalla o el área de contenido donde reside el contenido de la página.

Las nuevas clases CSS también se asignan a los nuevos divs del emulador: representan el nombre del emulador actual.

Los complementos de un emulador pueden ampliar aún más la lista de las clases CSS asignadas, como en el ejemplo del complemento de rotación, insertando una clase &quot;vertical&quot; u &quot;horizontal&quot; en función de la rotación actual del dispositivo.

De este modo, la apariencia completa del emulador se puede controlar teniendo clases CSS correspondientes a los ID y las clases CSS de los divs del emulador.

>[!NOTE]
>
>Se recomienda que el HTML del proyecto ajuste el contenido del cuerpo en un solo div, como en el ejemplo anterior. Si el contenido del cuerpo contiene varias etiquetas, puede haber resultados impredecibles.

### Emuladores móviles {#mobile-emulators}

Los emuladores móviles existentes:

* Están por debajo de /libs/wcm/mobile/components/emulators.
* Están disponibles a través del servlet JSON en:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Cuando el componente de página depende del componente de página móvil ( `/libs/wcm/mobile/components/page`), la funcionalidad del emulador se integra automáticamente en la página a través del siguiente mecanismo:

* El componente de página móvil `head.jsp` incluye el componente de inicio del emulador asociado al grupo de dispositivos (solo en modo de autor) y el CSS de procesamiento del grupo de dispositivos mediante:

   `deviceGroup.drawHead(pageContext);`

* El método `DeviceGroup.drawHead(pageContext)` incluye el componente init del emulador, es decir, llama a `init.html.jsp` del componente del emulador. Si el componente del emulador no tiene su propio `init.html.jsp` y depende del emulador de base móvil ( `wcm/mobile/components/emulators/base)`, se llama a la secuencia de comandos de inicio del emulador de base móvil ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* La secuencia de comandos de inicio del emulador de base móvil se define mediante Javascript:

   * Configuración de todos los emuladores definidos para la página (emulatorConfigs)
   * Administrador de emuladores que integra la funcionalidad del emulador en la página mediante:

      `emulatorMgr.launch(config)`;

      El administrador de emuladores se define mediante:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creación de un emulador móvil personalizado {#creating-a-custom-mobile-emulator}

Para crear un emulador móvil personalizado:

1. A continuación `/apps/myapp/components/emulators` cree el componente `myemulator` (tipo de nodo: `cq:Component`).

1. Establezca la propiedad `sling:resourceSuperType` en `/libs/wcm/mobile/components/emulators/base`

1. Defina una biblioteca de cliente CSS con la categoría `cq.wcm.mobile.emulator` para el aspecto del emulador: name = `css`, tipo de nodo = `cq:ClientLibrary`

   Como ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Si es necesario, defina una biblioteca de cliente JS, por ejemplo para definir un complemento específico: name = js, node type = cq:ClientLibrary

   Como ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Si el emulador admite funcionalidades específicas definidas por los complementos (como el desplazamiento táctil), cree un nodo de configuración debajo del emulador: name = `cq:emulatorConfig`, node type = `nt:unstructured` y agregue la propiedad que define el complemento:

   * Nombre = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de rotación.

   * Nombre = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de desplazamiento táctil.

   Se pueden agregar más funcionalidades definiendo sus propios complementos.

