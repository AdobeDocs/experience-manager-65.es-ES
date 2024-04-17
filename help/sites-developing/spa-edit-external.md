---
title: SPA Edición de un recurso externo en Adobe Experience Manager
description: SPA En este documento se describen los pasos recomendados para cargar una instancia independiente en una instancia de Adobe Experience Manager, agregar secciones de contenido editables y habilitar la creación de instancias.
exl-id: 25236af4-405a-4152-8308-34d983977e9a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 0%

---

# SPA Edición de un recurso externo en Adobe Experience Manager {#editing-external-spa-within-aem}

A la hora de decidir qué nivel de integración desea tener entre el grupo de trabajo externo y el de Adobe Experience Manager AEM SPA AEM (), a menudo necesita poder editar y ver el nivel de integración que se encuentra entre el grupo de trabajo externo y el grupo de trabajo de SPA (), lo que le permite editar y ver el contenido de la integración en su propio grupo de trabajo.

## Información general {#overview}

SPA AEM En este documento se describen los pasos recomendados para cargar una instancia independiente a una instancia de, agregar secciones de contenido editables y habilitar la creación de contenido.

## Requisitos previos {#prerequisites}

Los requisitos previos son simples.

* AEM Asegúrese de que una instancia de se esté ejecutando localmente.
* AEM SPA Creación de un proyecto de base mediante [AEM Arquetipo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * AEM SPA Esto forma la base del proyecto de que se actualizará para incluir la dirección de correo electrónico externa
   * Los ejemplos de este documento utilizan el punto de partida de [SPA el proyecto WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* SPA Tenga a mano el React externo de trabajo que desea integrar.

## SPA AEM Cargar el a un proyecto de {#upload-spa-to-aem-project}

SPA AEM En primer lugar, debe cargar el recurso externo en el proyecto de.

1. Reemplazar `src` en el `/ui.frontend` carpeta del proyecto con la aplicación de React `src` carpeta.
1. Incluya cualquier dependencia adicional en el `package.json` en el `/ui.frontend/package.json` archivo.
   * SPA Asegúrese de que las dependencias del SDK de la sean de [versiones recomendadas](spa-getting-started-react.md#dependencies).
1. Incluya cualquier personalización en la `/public` carpeta.
1. Incluya cualquier script en línea o estilo agregado en la `/public/index.html` archivo.

## SPA Configuración del servidor remoto {#configure-remote-spa}

SPA AEM AEM Ahora que la externa forma parte del proyecto de la, debe configurarse en la siguiente configuración de la interfaz de usuario de la interfaz de usuario de.

### Incluir paquetes de SDK de Adobe SPA {#include-spa-sdk-packages}

AEM SPA Para aprovechar las características de la, existen dependencias en los tres paquetes siguientes.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

El `@adobe/aem-spa-page-model-manager` AEM proporciona la API para inicializar un Administrador de modelos y recuperar el modelo de la instancia de la instancia de la. AEM Este modelo se puede utilizar para procesar componentes de mediante API de `@adobe/aem-react-editable-components` y `@adobe/aem-spa-component-mapping`.

#### Instalación {#installation}

Ejecute el siguiente comando npm para instalar los paquetes necesarios.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inicialización de ModelManager {#model-manager-initialization}

Antes de que la aplicación se procese, la variable [`ModelManager`](spa-blueprint.md#pagemodelmanager) AEM debe inicializarse para gestionar la creación de la `ModelStore`.

Esto debe hacerse dentro de la `src/index.js` de la aplicación o donde se represente la raíz de la aplicación.

Para ello, utilice `initializationAsync` API proporcionada por el `ModelManager`.

La siguiente captura de pantalla muestra cómo habilitar la inicialización de `ModelManager` en una aplicación React simple. La única restricción es que `initializationAsync` se debe llamar antes de `ReactDOM.render()`.

![Inicializar ModelManager](assets/external-spa-initialize-modelmanager.png)

En este ejemplo, la variable `ModelManager` se ha inicializado y un espacio de `ModelStore` se ha creado.

El `initializationAsync` puede aceptar opcionalmente un `options` objeto como parámetro:

* `path` : En la inicialización, el modelo en la ruta definida se recupera y se almacena en el `ModelStore`. Se puede usar para recuperar la variable `rootModel` en la inicialización si es necesario.
* `modelClient` : Permite proporcionar un cliente personalizado responsable de recuperar el modelo.
* `model` - A `model` El objeto pasado como parámetro generalmente se rellena cuando [uso de SSR.](spa-ssr.md)

### AEM Componentes de hoja autorizables {#authorable-leaf-components}

1. AEM Cree/identifique un componente de para el que se creará un componente de React con autoridad. En este ejemplo, el proyecto WKND utiliza el componente de texto.

   ![Componente de texto de WKND](assets/external-spa-text-component.png)

1. SPA Cree un componente de texto React simple en la interfaz de usuario de. En este ejemplo, un nuevo archivo `Text.js` se ha creado con el siguiente contenido.

   ![Text.js](assets/external-spa-textjs.png)

1. AEM Cree un objeto de configuración para especificar los atributos necesarios para habilitar la edición de la.

   ![Crear objeto de configuración](assets/external-spa-config-object.png)

   * `resourceType` AEM AEM es obligatorio asignar el componente React al componente de la y habilitar la edición al abrirlo en el Editor de.

1. Uso de la función envolvente `withMappable`.

   ![Uso con Mappable](assets/external-spa-withmappable.png)

   AEM Esta función de envoltorio asigna el componente React a la aplicación de la `resourceType` AEM se especifica en la configuración de y habilita las funciones de edición al abrirse en el Editor de. Para los componentes independientes, también recupera el contenido del modelo para el nodo específico.

   >[!NOTE]
   >
   >AEM En este ejemplo, hay versiones independientes del componente: componentes React ajustados y no ajustados a la. La versión ajustada debe utilizarse cuando se utiliza explícitamente el componente. SPA Cuando el componente forma parte de una página, puede seguir utilizando el componente predeterminado como se hace actualmente en el editor de páginas de la página de la aplicación de la página de la aplicación de la aplicación de la aplicación de la aplicación de configuración de la aplicación de configuración de la página.

1. Procesar contenido en el componente.

   AEM Las propiedades JCR del componente de texto aparecen de la siguiente manera en la.

   ![Propiedades del componente Texto](assets/external-spa-text-properties.png)

   Estos valores se pasan como propiedades al recién creado `AEMText` React y se puede utilizar para procesar el contenido.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   AEM Así es como aparece el componente cuando se completan las configuraciones de la.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >En este ejemplo, se han realizado más personalizaciones en el componente representado para que coincida con el componente de texto existente. AEM Sin embargo, esto no está relacionado con la creación de contenido en la.

#### Agregar componentes con autorización a la página {#add-authorable-component-to-page}

Una vez creados los componentes React legibles, se pueden utilizar en toda la aplicación.

SPA Veamos una página de ejemplo en la que es necesario agregar texto del proyecto WKND. Para este ejemplo, desea mostrar el texto &quot;Hello World!&quot; el `/content/wknd-spa-react/us/en/home.html`.

1. Determine la ruta del nodo que desea mostrar.

   * `pagePath`: La página que contiene el nodo, en el ejemplo `/content/wknd-spa-react/us/en/home`
   * `itemPath`: Ruta al nodo dentro de la página, en el ejemplo `root/responsivegrid/text`
      * Consta de los nombres de los elementos que contienen la página.

   ![Ruta del nodo](assets/external-spa-path.png)

1. Añada un componente en la posición requerida en la página.

   ![Añadir un componente a la página](assets/external-spa-add-component.png)

   El `AEMText` componente se puede añadir en la posición requerida dentro de la página con `pagePath` y `itemPath` valores establecidos como propiedades. `pagePath` es una propiedad obligatoria.

#### AEM Verificar la edición del contenido del texto en las {#verify-text-edit}

AEM Ahora pruebe el componente en la instancia de ejecución de la.

1. Ejecute el siguiente comando Maven desde el `aem-guides-wknd-spa` AEM para generar e implementar el proyecto en el que se va a realizar el.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. AEM En la instancia de la, navegue hasta `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![SPA AEM Edición de la en la](assets/external-spa-edit-aem.png)

El `AEMText` AEM El componente ahora se puede crear en el.

### AEM Páginas con autorización de {#aem-authorable-pages}

1. SPA Identifique la página que desea añadir para la creación en el sitio de trabajo de. Este ejemplo utiliza `/content/wknd-spa-react/us/en/home.html`.
1. Cree un archivo (por ejemplo, `Page.js`) para el componente de página legible. En este caso, se puede reutilizar el componente Página que se proporciona en `@adobe/cq-react-editable-components`.
1. Repita el cuarto paso de la sección [AEM componentes de hoja legibles por el autor](#authorable-leaf-components). Uso de la función envolvente `withMappable` en el componente.
1. Como se hizo anteriormente, aplique `MapTo` AEM a los tipos de recurso de la para todos los componentes secundarios dentro de la página.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >En este ejemplo, se utiliza el componente de texto React no ajustado en lugar del ajustado `AEMText` creado anteriormente. Esto se debe a que cuando el componente forma parte de una página o contenedor y no es independiente, el contenedor se encargará de asignar de forma recursiva el componente y de habilitar las capacidades de creación, y no se necesita el contenedor adicional para cada elemento secundario.

1. SPA Para añadir una página legible en la, siga los mismos pasos en la sección [Agregar componentes con autorización a la página](#add-authorable-component-to-page). Aquí podemos omitir el `itemPath` propiedad, sin embargo.

#### AEM Verificar el contenido de la página en la {#verify-page-content}

Para comprobar que la página se puede editar, siga los mismos pasos en la sección [AEM Verificar la edición del contenido del texto en las](#verify-text-edit).

![AEM Edición de una página en la](assets/external-spa-edit-page.png)

AEM La página ahora se puede editar en el diseño con un contenedor de diseño y un componente de texto secundario.

### Componentes de hoja virtual {#virtual-leaf-components}

SPA AEM En los ejemplos anteriores, hemos añadido componentes a la lista de componentes con contenido de existente. AEM Sin embargo, hay casos en los que el contenido aún no se ha creado en la, pero el autor del contenido debe añadirlo más tarde. SPA Para dar cabida a esto, el desarrollador front-end puede agregar componentes en las ubicaciones adecuadas dentro de la interfaz de usuario de la aplicación de. AEM Estos componentes mostrarán los marcadores de posición cuando se abran en el editor en el que se encuentran los. Una vez que el autor de contenido agrega el contenido dentro de estos marcadores de posición, los nodos se crean en la estructura JCR y el contenido se mantiene. El componente creado permitirá el mismo conjunto de operaciones que los componentes de hoja independientes.

En este ejemplo, reutilizamos la variable `AEMText` componente creado anteriormente. Queremos que se añada texto nuevo debajo del componente de texto existente en la página principal de WKND. La adición de componentes es la misma que para los componentes normales de la hoja. Sin embargo, la variable `itemPath` se puede actualizar a la ruta en la que debe agregarse el nuevo componente.

Dado que es necesario añadir el nuevo componente debajo del texto existente en `root/responsivegrid/text`, la nueva ruta sería `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

El `TestPage` tiene el siguiente aspecto después de agregar el componente virtual.

![Prueba del componente virtual](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Asegúrese de que `AEMText` el componente tiene su `resourceType` establezca en la configuración para habilitar esta función.

AEM Ahora puede implementar los cambios para que siga los pasos de la sección que se describen a continuación: [AEM Verificar la edición del contenido del texto en las](#verify-text-edit). Se muestra un marcador de posición para el actualmente no existente `text_20` nodo.

![El nodo text_20 en aem](assets/external-spa-text20-aem.png)

Cuando el autor del contenido actualice este componente, se agregará un nuevo `text_20` El nodo se crea en `root/responsivegrid/text_20` in `/content/wknd-spa-react/us/en/home`.

![El nodo text20](assets/external-spa-text20-node.png)

#### Requisitos y limitaciones {#limitations}

Existen varios requisitos para agregar componentes de hoja virtual y algunas limitaciones.

* El `pagePath` La propiedad es obligatoria para crear un componente virtual.
* El nodo de página proporcionado en la ruta de `pagePath` AEM debe existir en el proyecto de.
* El nombre del nodo que se va a crear debe proporcionarse en la variable `itemPath`.
* El componente se puede crear en cualquier nivel.
   * Si proporcionamos un `itemPath='text_20'` en el ejemplo anterior, el nuevo nodo se creará directamente en la página, que es, `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* La ruta al nodo en el que se crea un nuevo nodo debe ser válida cuando se proporciona mediante `itemPath`.
   * En este ejemplo, `root/responsivegrid` debe existir para que el nuevo nodo `text_20` se puede crear allí.
* Solo se admite la creación de componentes de hoja. El contenedor y la página virtuales serán compatibles en versiones futuras.

### Contenedores virtuales {#virtual-containers}

AEM Se admite la capacidad de agregar contenedores, incluso si el contenedor correspondiente aún no se ha creado en el espacio de trabajo de la interfaz de usuario de la aplicación de datos de. El concepto y el enfoque son similares a [componentes de hoja virtual.](#virtual-leaf-components)

SPA AEM El desarrollador front-end puede agregar los componentes de contenedor en ubicaciones adecuadas dentro de la y estos componentes mostrarán marcadores de posición cuando se abran en el editor en la. A continuación, el autor puede agregar componentes y su contenido al contenedor, que creará los nodos necesarios en la estructura JCR.

Por ejemplo, si ya existe un contenedor en `/root/responsivegrid` y el desarrollador desea agregar un nuevo contenedor secundario:

![Ubicación del contenedor](assets/container-location.png)

`newContainer` AEM aún no existe en el.

AEM Al editar la página que contiene este componente en la página de, se muestra un marcador de posición vacío para un contenedor en el que el autor puede agregar contenido.

![Marcador de contenedor](assets/container-placeholder.png)

![Ubicación del contenedor en JCR](assets/container-jcr-structure.png)

Una vez que el autor agrega un componente secundario al contenedor, el nuevo nodo contenedor se crea con el nombre correspondiente en la estructura JCR.

![Contenedor con contenido](assets/container-with-content.png)

![Contenedor con contenido en JCR](assets/container-with-content-jcr.png)

Ahora se pueden agregar más componentes y contenido al contenedor según lo requiera el autor, y los cambios se mantendrán.

#### Requisitos y limitaciones {#container-limitations}

Existen varios requisitos para agregar contenedores virtuales y algunas limitaciones.

* La directiva para determinar qué componentes se pueden agregar se heredará del contenedor principal.
* AEM El elemento principal inmediato del contenedor que se va a crear ya debe existir en el espacio de trabajo de la.
   * Si el contenedor `root/responsivegrid` AEM ya existe en el contenedor de, se puede crear un nuevo contenedor proporcionando la ruta `root/responsivegrid/newContainer`.
   * Sin embargo `root/responsivegrid/newContainer/secondNewContainer` no es posible.
* Solo se puede crear virtualmente un nuevo nivel de componente a la vez.

## Personalizaciones adicionales {#additional-customizations}

SPA AEM Si ha seguido los ejemplos anteriores, el recurso externo ahora se puede editar en la. SPA Sin embargo, hay aspectos adicionales de los recursos externos que se pueden personalizar aún más.

### ID del nodo raíz {#root-node-id}

De forma predeterminada, suponemos que la aplicación React se procesa dentro de un `div` de ID de elemento `spa-root`. Si es necesario, se puede personalizar.

SPA Por ejemplo, supongamos que tenemos un en el que la aplicación se procesa dentro de un `div` de ID de elemento `root`. Esto debe reflejarse en tres archivos.

1. En el `index.js` de la aplicación React (o donde `ReactDOM.render()` se llama)

   ![ReactDOM.render() en el archivo index.js](assets/external-spa-root-index.png)

1. En el `index.html` de la aplicación React

   ![El index.html de la aplicación](assets/external-spa-index.png)

1. AEM En el cuerpo del componente de página de la aplicación de, siga dos pasos:

   1. Crear un `body.html` para el componente de página.

   ![Creación de un archivo body.html](assets/external-spa-update-body.gif)

   1. Añadir el nuevo elemento raíz en el nuevo `body.html` archivo.

   ![Añadir el elemento raíz a body.html](assets/external-spa-add-root.png)

### SPA Edición de un React con Enrutamiento {#editing-react-spa-with-routing}

SPA Si la aplicación de React externa tiene varias páginas, [puede utilizar el enrutamiento para determinar la página o el componente que se va a procesar](spa-routing.md). El caso de uso básico es hacer coincidir la dirección URL activa con la ruta proporcionada para una ruta. AEM Para habilitar la edición en estas aplicaciones habilitadas para enrutamiento, la ruta con la que se debe hacer coincidir debe transformarse para dar cabida a información específica de la aplicación de enrutamiento de tipo de datos.

En el siguiente ejemplo tenemos una aplicación React simple con dos páginas. La página que se va a procesar se determina comparando la ruta proporcionada al enrutador con la dirección URL activa. Por ejemplo, si estamos en `mydomain.com/test`, `TestPage` se procesarán.

![SPA Enrutamiento en un entorno externo](assets/external-spa-routing.png)

AEM SPA Para habilitar la edición dentro de los parámetros para este ejemplo, se requieren los siguientes pasos.

1. AEM Identifique el nivel que actuaría como raíz en la.

   * Para nuestra muestra, consideramos `wknd-spa-react/us/en` SPA como la raíz de la. AEM Esto significa que todo lo anterior a esa ruta solo es contenido o páginas de la lista de contenido de la lista de distribución de contenido/página.

1. Cree una página en el nivel requerido.

   * En este ejemplo, la página que se va a editar es `mydomain.com/test`. `test` se encuentra en la ruta raíz de la aplicación. AEM Esto también debe conservarse al crear la página en la. Por lo tanto, puede crear una página en el nivel raíz definido en el paso anterior.
   * La nueva página creada debe tener el mismo nombre que la página que se va a editar. En este ejemplo para `mydomain.com/test`, la nueva página creada debe ser `/path/to/aem/root/test`.

1. SPA Agregar ayudantes dentro del enrutamiento de la.

   * AEM La página recién creada aún no procesará el contenido esperado en la página de. Esto se debe a que el enrutador espera una ruta de `/test` AEM mientras que la ruta activa de la es `/wknd-spa-react/us/en/test`. AEM SPA Para dar cabida a la parte específica de la dirección URL que corresponde a la dirección URL, es necesario agregar algunos ayudantes en el lado de la dirección de correo electrónico

   ![Asistente de enrutamiento](assets/external-spa-router-helper.png)

   * El `toAEMPath` ayudante proporcionado por `@adobe/cq-spa-page-model-manager` se puede usar para esto. AEM AEM Transforma la ruta proporcionada para el enrutamiento a fin de incluir partes específicas de la cuando la aplicación está abierta en una instancia de la aplicación Acepta tres parámetros:
      * La ruta necesaria para el enrutamiento
      * AEM SPA Dirección URL de origen de la instancia de la en la que se edita la
      * AEM La raíz del proyecto en el tiempo de ejecución, tal como se determina en el primer paso, es la siguiente:

   * Estos valores se pueden configurar como variables de entorno para una mayor flexibilidad.

1. AEM Compruebe la edición de la página en la.

   * AEM Implemente el proyecto para que se ejecute y navegue hasta el proyecto recién creado. `test` página. AEM Ahora se procesa el contenido de la página y se pueden editar los componentes de la.

## Limitaciones del marco {#framework-limitations}

El componente RemotePage espera que la implementación proporcione un manifiesto de recurso como el siguiente [encontrado aquí](https://github.com/shellscape/webpack-manifest-plugin). Sin embargo, el componente RemotePage solo se ha probado para funcionar con el marco de React (y Next.js a través del componente remote-page-next) y, por lo tanto, no admite la carga remota de aplicaciones desde otros marcos, como Angular.

## Recursos adicionales {#additional-resources}

SPA AEM El siguiente material de referencia puede resultar útil para comprender la existencia de la en el contexto de la misma.

* [AEM Arquetipo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)
* [SPA El proyecto de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es)
* [SPA AEM Introducción a la administración de la en React](spa-getting-started-react.md)
* [SPA Materiales de referencia (referencias de API)](spa-reference-materials.md)
* [SPA Modelo de página y administrador de modelos de página](spa-blueprint.md#pagemodelmanager)
* [SPA Enrutamiento de modelo de](spa-routing.md)
* [SPA Procesamiento del lado del servidor y de](spa-ssr.md)
