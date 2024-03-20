---
title: Ampliación de ContextHub
description: Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Ampliación de ContextHub{#extending-contexthub}

Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución.

## Crear candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de candidatos de tiendas registradas. Para crear un almacén personalizado, cree y registre un candidato de almacén.

El archivo JavaScript que incluye el código que crea y registra el candidato de tienda debe incluirse en un [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

El `[storeType]` parte de la categoría es la `storeType` con el que está registrado el candidato a tienda. (Consulte [Registro de un candidato de tienda de ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por ejemplo, para el tipo de almacén de `contexthub.mystore`, la categoría de la carpeta de la biblioteca de cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear un candidato de tienda, se utiliza el [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para ampliar uno de los almacenes base:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada almacén base amplía el [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) tienda.

En el siguiente ejemplo se crea la extensión más sencilla del `ContextHub.Store.PersistedStore` candidato de tienda:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definen funciones adicionales o anulan la configuración inicial de la tienda. Varios [candidatos de tienda de muestra](/help/sites-developing/ch-samplestores.md) están instalados en el repositorio a continuación `/libs/granite/contexthub/components/stores`. Para aprender de estos ejemplos, utilice CRXDE Lite para abrir los archivos JavaScript.

### Registro de un candidato de tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato de tienda para integrarlo con el marco de ContextHub y permitir que se creen tiendas a partir de él. Para registrar un candidato a tienda, utilice el [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) función del `ContextHub.Utils.storeCandidates` clase.

Al registrar un candidato de tienda, se proporciona un nombre para el tipo de tienda. Al crear un almacén a partir del candidato, se utiliza el tipo de almacén para identificar el candidato en el que se basa.

Cuando se registra un candidato a tienda, se indica su prioridad. Cuando se registra un candidato de tienda con el mismo tipo de tienda que un candidato de tienda ya registrado, se utiliza el candidato con la prioridad más alta. Por lo tanto, puede anular los candidatos de tienda existentes con nuevas implementaciones.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Por lo general, solo es necesario un candidato y la prioridad se puede establecer en `0`. Pero si está interesado, puede aprender acerca de [registros más avanzados,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) , que permite elegir una de las pocas implementaciones de la tienda en función de la condición de JavaScript (`applies`) y prioridad de los candidatos.

## Creación de tipos de módulos de IU de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de IU personalizados cuando los que están [instalado con ContextHub](/help/sites-developing/ch-samplemodules.md) no cumpla con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un procesador de módulos de interfaz de usuario ampliando el `ContextHub.UI.BaseModuleRenderer` y, a continuación, registrarla con `ContextHub.UI`.

Para crear un procesador de módulos de IU, cree un `Class` que contiene la lógica que procesa el módulo de interfaz de usuario. Como mínimo, la clase debe realizar las siguientes acciones:

* Ampliación de la `ContextHub.UI.BaseModuleRenderer` clase. Esta clase es la implementación base para todos los procesadores de módulos de IU. El `Class` define una propiedad denominada `extend` que se utiliza para asignar a esta clase el nombre que se está extendiendo.

* Proporcione una configuración predeterminada. Crear un `defaultConfig` propiedad. Esta propiedad es un objeto que incluye las propiedades definidas para la variable [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) Módulo de interfaz de usuario y otras propiedades que necesite.

La fuente de `ContextHub.UI.BaseModuleRenderer` se encuentra en /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js. Para registrar el procesador, utilice el [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) método del `ContextHub.UI` clase. Proporcione un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de interfaz de usuario contexthub.browserinfo. Este módulo de interfaz de usuario es una simple extensión del `ContextHub.UI.BaseModuleRenderer` clase.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

El archivo JavaScript que incluye el código que crea y registra el procesador debe incluirse en un [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.module.[moduleType]
```

El `[moduleType]` parte de la categoría es la `moduleType` con el que está registrado el procesador de módulos. Por ejemplo, para `moduleType` de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca de cliente debe ser `contexthub.module.contexthub.browserinfo`.
