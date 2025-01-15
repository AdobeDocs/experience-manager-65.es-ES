---
title: Emuladores
description: AEM permite a los autores ver una página en un emulador que simula el entorno en el que un usuario final verá la página
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Emuladores{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager AEM () permite a los autores ver una página en un emulador que simula el entorno en el que un usuario final verá la página, como en un dispositivo móvil o en un cliente de correo electrónico.

AEM El marco del emulador de:

* Proporciona la creación de contenido dentro de una interfaz de usuario (IU) simulada, como un dispositivo móvil o un cliente de correo electrónico (utilizado para crear boletines informativos).
* Adapta el contenido de la página según la IU simulada.
* Permite crear emuladores personalizados.

>[!CAUTION]
>
>Esta función solo es compatible con la IU clásica.

## Características de emuladores {#emulators-characteristics}

Un emulador:

* Se basa en ExtJS.
* Funciona en la página DOM.
* Su aspecto se regula mediante CSS.
* Admite complementos (por ejemplo, el complemento de rotación de dispositivos móviles).
* Solo está activo en el autor.
* Su componente base está en `/libs/wcm/emulator/components/base`.

### Cómo el emulador transforma el contenido {#how-the-emulator-transforms-the-content}

El emulador funciona envolviendo el contenido del cuerpo del HTML en DIV de emulador. Por ejemplo, el siguiente código HTML:

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

Se han añadido dos etiquetas de div:

* el div con id `cq-emulator` que contiene el emulador en su totalidad y

* el div con id `cq-emulator-content` que representa el área de contenido/pantalla/ventanilla del dispositivo donde reside el contenido de la página.

Las nuevas clases CSS también se asignan a los nuevos divs de emulador: representan el nombre del emulador actual.

Los complementos de un emulador pueden ampliar aún más la lista de clases CSS asignadas, como en el ejemplo del complemento de rotación, al insertar una clase &quot;vertical&quot; u &quot;horizontal&quot; en función de la rotación actual del dispositivo.

De este modo, se puede controlar el aspecto completo del emulador teniendo clases CSS correspondientes a las clases ID y CSS de los divs del emulador.

>[!NOTE]
>
>Se recomienda que el HTML del proyecto ajuste el contenido del cuerpo en un solo div, como en el ejemplo anterior. Si el contenido del cuerpo contiene varias etiquetas, puede haber resultados impredecibles.

### Emuladores móviles {#mobile-emulators}

Los emuladores móviles existentes:

* Están por debajo de /libs/wcm/mobile/components/emulators.
* Están disponibles a través del servlet JSON en:

  http://localhost:4502/bin/wcm/mobile/emulators.json

Cuando el componente de página depende del componente de página móvil ( `/libs/wcm/mobile/components/page`), la funcionalidad del emulador se integra automáticamente en la página mediante el siguiente mecanismo:

* El componente de página móvil `head.jsp` incluye el componente de inicialización del emulador asociado del grupo de dispositivos (solo en el modo de autor) y el CSS de procesamiento del grupo de dispositivos mediante:

  `deviceGroup.drawHead(pageContext);`

* El método `DeviceGroup.drawHead(pageContext)` incluye el componente init del emulador, es decir, llama al `init.html.jsp` del componente del emulador. Si el componente del emulador no tiene su propio `init.html.jsp` y depende del emulador de base móvil ( `wcm/mobile/components/emulators/base)`), se llama al script de inicio del emulador de base móvil ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* El script de inicio del emulador base móvil define a través de JavaScript:

   * La configuración de todos los emuladores definidos para la página (emulatorConfigs)
   * El administrador del emulador, que integra la funcionalidad del emulador en la página mediante:

     `emulatorMgr.launch(config)`;

     El administrador del emulador se define mediante:

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creación de un emulador móvil personalizado {#creating-a-custom-mobile-emulator}

Para crear un emulador móvil personalizado:

1. Debajo de `/apps/myapp/components/emulators` cree el componente `myemulator` (tipo de nodo: `cq:Component`).

1. Establecer la propiedad `sling:resourceSuperType` en `/libs/wcm/mobile/components/emulators/base`

1. Defina una biblioteca de cliente CSS con la categoría `cq.wcm.mobile.emulator` para el aspecto del emulador: nombre = `css`, tipo de nodo = `cq:ClientLibrary`

   Por ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Si es necesario, defina una biblioteca de cliente JS, por ejemplo, para definir un complemento específico: name = js, node type = cq:ClientLibrary

   Por ejemplo, puede hacer referencia al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Si el emulador admite funcionalidades específicas definidas por complementos (como el desplazamiento táctil), cree un nodo de configuración debajo del emulador: name = `cq:emulatorConfig`, node type = `nt:unstructured` y agregue la propiedad que define el complemento:

   * Nombre = `canRotate`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de rotación.

   * Nombre = `touchScrolling`, Tipo = `Boolean`, Valor = `true`: para incluir la funcionalidad de desplazamiento táctil.

   Se pueden añadir más funcionalidades definiendo sus propios complementos.
