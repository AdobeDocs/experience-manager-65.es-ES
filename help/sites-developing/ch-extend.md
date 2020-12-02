---
title: Ampliación de ContextHub
seo-title: Ampliación de ContextHub
description: Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución
seo-description: Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Ampliación de ContextHub{#extending-contexthub}

Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución.

## Creación de candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de los candidatos de las tiendas registradas. Para crear una tienda personalizada, debe crear y registrar un candidato a la tienda.

El archivo javascript que incluye el código que crea y registra al candidato de la tienda debe incluirse en una [carpeta de la biblioteca del cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La parte `[storeType]` de la categoría es la `storeType` con la que está registrado el candidato a la tienda. (Consulte [Registro de un candidato de tienda de ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por ejemplo, para storeType de `contexthub.mystore`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear un candidato de almacén, utilice la función [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para ampliar uno de los almacenes base:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Tenga en cuenta que cada almacén base extiende el almacén [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core).

El ejemplo siguiente crea la extensión más simple del candidato de almacén `ContextHub.Store.PersistedStore`:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definirán funciones adicionales o anularán la configuración inicial de la tienda. Varios [candidatos del almacén de muestras](/help/sites-developing/ch-samplestores.md) están instalados en el repositorio que se encuentra a continuación `/libs/granite/contexthub/components/stores`. Para obtener más información sobre estos ejemplos, utilice CRXDE Lite para abrir los archivos de javascript.

### Registro de un candidato de la tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato a tienda para integrarlo con el marco de trabajo de ContextHub y permitir que se creen tiendas a partir de él. Para registrar un candidato de almacén, utilice la función [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la clase `ContextHub.Utils.storeCandidates`.

Al registrar un candidato a tienda, debe proporcionar un nombre para el tipo de tienda. Al crear una tienda a partir del candidato, se utiliza el tipo de tienda para identificar al candidato en el que se basa.

Al registrar un candidato a tienda, usted indica su prioridad. Cuando un candidato a tienda se registra con el mismo tipo de tienda que un candidato a tienda ya registrado, se utiliza el candidato con mayor prioridad. Por lo tanto, puede omitir los candidatos de tienda existentes con nuevas implementaciones.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

En la mayoría de los casos, solo se necesita un candidato y la prioridad se puede establecer en `0`, pero si le interesa puede obtener información sobre [registros más avanzados,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) que permite elegir una de las pocas implementaciones de almacenamiento en base a la condición de javascript (`applies`) y la prioridad candidata.

## Creación de tipos de módulos de interfaz de usuario de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de interfaz de usuario personalizados cuando los que están [instalados con ContextHub](/help/sites-developing/ch-samplemodules.md) no cumplan con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un nuevo procesador de módulos de interfaz de usuario ampliando la clase `ContextHub.UI.BaseModuleRenderer` y, a continuación, registrándola con `ContextHub.UI`.

Para crear un procesador de módulos de interfaz de usuario, cree un objeto `Class` que contenga la lógica que procesa el módulo de interfaz de usuario. Como mínimo, la clase debe realizar las siguientes acciones:

* Extienda la clase `ContextHub.UI.BaseModuleRenderer`. Esta clase es la implementación básica para todos los procesadores de módulos de interfaz de usuario. El objeto `Class` define una propiedad denominada `extend` que se utiliza para asignar a esta clase el nombre que se está extendiendo.

* Proporcione una configuración predeterminada. Cree una propiedad `defaultConfig`. Esta propiedad es un objeto que incluye las propiedades definidas para el módulo de interfaz de usuario [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) y cualquier otra propiedad que necesite.

El origen de `ContextHub.UI.BaseModuleRenderer` se encuentra en /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Para registrar el procesador, utilice el método [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) de la clase `ContextHub.UI`. Debe proporcionar un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de interfaz de usuario contexthub.browserinfo. Este módulo de interfaz de usuario es una extensión simple de la clase `ContextHub.UI.BaseModuleRenderer`.

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

El archivo javascript que incluye el código que crea y registra el procesador debe incluirse en una [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.module.[moduleType]
```

La parte `[moduleType]` de la categoría es la `moduleType` con la que está registrado el procesador de módulos. Por ejemplo, para `moduleType` de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.module.contexthub.browserinfo`.
