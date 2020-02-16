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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ampliación de ContextHub{#extending-contexthub}

Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución.

## Creación de candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de los candidatos de las tiendas registradas. Para crear una tienda personalizada, debe crear y registrar un candidato a la tienda.

El archivo javascript que incluye el código que crea y registra al candidato de la tienda debe incluirse en una carpeta [de la biblioteca del](/help/sites-developing/clientlibs.md#creating-client-library-folders)cliente. La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La `[storeType]` parte de la categoría es storeType con la que está registrado el candidato de la tienda. (Consulte [Registro de un candidato](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)a la tienda de ContextHub). Por ejemplo, para el valor storeType de `contexthub.mystore`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de la tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear un candidato a tienda, utilice la [ función `ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para ampliar uno de los almacenes base:

* ` [ContextHub.Store.PersistedStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)`
* ` [ContextHub.Store.SessionStore](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)`
* ` [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)`
* ` [ContextHub.Store.PersistedJSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)`

Tenga en cuenta que cada almacén base extiende la ` [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core)` tienda.

El ejemplo siguiente crea la extensión más simple del candidato de `ContextHub.Store.PersistedStore` tienda:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definirán funciones adicionales o anularán la configuración inicial de la tienda. Varios candidatos [de almacén de](/help/sites-developing/ch-samplestores.md) muestra están instalados en el repositorio debajo de /libs/granite/contexthub/components/store. Para aprender de estos ejemplos, utilice CRXDE Lite para abrir los archivos de javascript.

### Registro de un candidato a la tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato a la tienda para integrarlo con el marco de trabajo de ContextHub y habilitar la creación de tiendas a partir de él. Para registrar un candidato de tienda, utilice la [ función `registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la `ContextHub.Utils.storeCandidates` clase.

Al registrar un candidato de tienda, debe proporcionar un nombre para el tipo de tienda. Al crear una tienda a partir del candidato, se utiliza el tipo de tienda para identificar al candidato en el que se basa.

Al registrar un candidato a tienda, usted indica su prioridad. Cuando un candidato a tienda se registra con el mismo tipo de tienda que un candidato a tienda ya registrado, se utiliza el candidato con mayor prioridad. Por lo tanto, puede omitir los candidatos de tienda existentes con nuevas implementaciones.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

## Creación de tipos de módulos de interfaz de usuario de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de interfaz de usuario personalizados cuando los que se [instalan con ContextHub](/help/sites-developing/ch-samplemodules.md) no cumplan con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un nuevo procesador de módulos de interfaz de usuario ampliando la `ContextHub.UI.BaseModuleRenderer` clase y, a continuación, registrándola con `ContextHub.UI`.

Para crear un procesador de módulos de interfaz de usuario, cree un `Class` objeto que contenga la lógica que procesa el módulo de interfaz de usuario. Como mínimo, la clase debe realizar las siguientes acciones:

* Extender la `ContextHub.UI.BaseModuleRenderer` clase. Esta clase es la implementación básica para todos los procesadores de módulos de interfaz de usuario. El `Class` objeto define una propiedad denominada `extend` que se utiliza para asignar a esta clase el nombre que se está extendiendo.

* Proporcione una configuración predeterminada. Cree una `defaultConfig` propiedad. Esta propiedad es un objeto que incluye las propiedades definidas para el módulo de la [ `contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) interfaz de usuario y cualquier otra propiedad que se requiera.

El origen de `ContextHub.UI.BaseModuleRenderer` se encuentra en /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Para registrar el procesador, utilice el ` [registerRenderer](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)` método de la `ContextHub.UI` clase. Debe proporcionar un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de interfaz de usuario contexthub.browserinfo. Este módulo de interfaz de usuario es una simple extensión de la `ContextHub.UI.BaseModuleRenderer` clase.

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

El archivo javascript que incluye el código que crea y registra el procesador debe incluirse en una carpeta [de biblioteca de](/help/sites-developing/clientlibs.md#creating-client-library-folders)cliente. La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.module.[moduleType]
```

La `[moduleType]` parte de la categoría es la `moduleType` con la que está registrado el procesador de módulos. Por ejemplo, para el `moduleType` caso de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.module.contexthub.browserinfo`.
