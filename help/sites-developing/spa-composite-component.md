---
title: Componentes compuestos en SPA
description: AEM SPA Aprenda a crear sus propios componentes compuestos, componentes formados por otros componentes, que funcionan con el Editor de aplicaciones de una sola página () de la aplicación de una sola página (SPA) de la.
exl-id: 02b6c698-d169-467a-9168-9fa6181bed6c
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# Componentes compuestos en SPA {#composite-components-in-spas}

AEM Los componentes compuestos utilizan la naturaleza modular de los componentes de base mediante la combinación de varios componentes base en un único componente. Un caso de uso de componente compuesto común es el componente de tarjeta, formado por una combinación de los componentes de imagen y texto.

AEM SPA Cuando los componentes compuestos se implementan correctamente dentro del marco de trabajo del Editor de aplicaciones de una sola página () de, los autores de contenido pueden arrastrar y soltar estos componentes como lo harían con cualquier otro componente, pero siguen teniendo la capacidad de editar individualmente cada componente que compone el componente compuesto.

AEM SPA Este artículo muestra cómo puede agregar un componente compuesto a la aplicación de una sola página para trabajar sin problemas con el Editor de.

## Caso práctico {#use-case}

Este artículo utiliza el componente de tarjeta típico como ejemplo de uso. Las tarjetas son un elemento de la interfaz de usuario común para muchas experiencias digitales y suelen estar formadas por una imagen y un texto o rótulo asociado. Un autor desea poder arrastrar y soltar toda la tarjeta, pero puede editar individualmente la imagen de la tarjeta y personalizar el texto asociado.

## Requisitos previos {#prerequisites}

Los siguientes modelos para admitir los casos de uso de componentes compuestos requieren los siguientes requisitos previos.

* AEM La instancia de desarrollo de la se está ejecutando localmente en el puerto 4502 con un proyecto de ejemplo.
* Tiene una aplicación de React externa en funcionamiento [AEM habilitado para editar en la.](spa-edit-external.md)
* AEM La aplicación React se carga en el editor de [mediante el componente RemotePage.](spa-remote-page.md)

## SPA Adición de componentes compuestos a un grupo de componentes {#adding-composite-components}

SPA AEM Existen tres modelos diferentes para implementar el componente compuesto en función de la implementación de la dentro de la aplicación de la combinación de componentes

* [AEM El componente no existe en el proyecto de.](#component-does-not-exist)
* [AEM El componente existe en el proyecto de, pero el contenido requerido no.](#content-does-not-exist)
* [AEM Tanto el componente como el contenido requerido existen en el proyecto de.](#both-exist)

En las siguientes secciones se proporcionan ejemplos de implementación de cada caso utilizando el componente de tarjeta como ejemplo.

### AEM El componente no existe en el proyecto de. {#component-does-not-exist}

Comience creando los componentes que compondrán el componente compuesto, es decir, los componentes para la imagen y su texto.

1. AEM Cree el componente de texto en el proyecto de.
1. Añadir el correspondiente `resourceType` del proyecto en el del componente `editConfig` nodo.

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. Utilice el `withMappable` para habilitar la edición para el componente.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

El componente de texto será similar al siguiente.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

Si crea un componente de imagen de forma similar, puede combinarlo con la variable `AEMText` en un nuevo componente de tarjeta, utilizando los componentes de imagen y texto como elementos secundarios.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

SPA Este componente compuesto resultante ahora se puede colocar en cualquier lugar de la aplicación y el agregará marcadores de posición para un componente de texto y de imagen en el Editor de. En el siguiente ejemplo, el componente de tarjeta se agrega al componente principal debajo del título.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

Esto mostrará un marcador de posición vacío para un texto y una imagen en el editor. Al introducir valores para estos elementos mediante el editor, se almacenan en la ruta de página especificada, es decir `/content/wknd-spa/home`  en el nivel raíz con los nombres especificados en `itemPath`.

![Componente de tarjeta compuesta en el editor](assets/composite-card.png)

### AEM El componente existe en el proyecto de, pero el contenido requerido no. {#content-does-not-exist}

AEM En este caso, el componente de tarjeta ya se ha creado en el proyecto de que contiene los nodos de título e imagen. Los nodos secundarios (texto e imagen) tienen los tipos de recursos correspondientes.

![Estructura de nodos del componente de tarjeta](assets/composite-node-structure.png)

SPA A continuación, puede agregarlo a la y recuperar su contenido.

1. SPA Cree un componente correspondiente en la lista de componentes para este elemento AEM SPA Asegúrese de que los componentes secundarios estén asignados a sus tipos de recursos de la correspondientes dentro del proyecto de la aplicación. En este ejemplo utilizamos el mismo `AEMText` y `AEMImage` componentes según se detalla [en el caso anterior.](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. Dado que no hay contenido para `imagecard` , añada la tarjeta a la página. AEM SPA Incluya el contenedor existente de la lista de en el cuadro de diálogo de la.
   * AEM SPA AEM Si ya hay un contenedor en el proyecto de, podemos incluirlo en la lista de distribución en su lugar y agregar el componente al contenedor desde la lista de distribución en su lugar, en la lista de distribución en la que se va a incluir el componente en la lista de distribución en el proyecto de.
   * SPA Asegúrese de que el componente de tarjeta esté asignado al tipo de recurso correspondiente en la tarjeta de.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. Añada el creado `wknd-spa/components/imagecard` a los componentes permitidos para el componente contenedor [en la plantilla de página.](/help/sites-authoring/templates.md)

Ahora, la `imagecard` AEM El componente se puede añadir directamente al contenedor en el editor de.

![Tarjeta compuesta en el editor](assets/composite-card.gif)

### AEM Tanto el componente como el contenido requerido existen en el proyecto de. {#both-exist}

AEM SPA Si el contenido existe en la, se puede incluir directamente en la misma proporcionando la ruta de acceso al contenido.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![Ruta compuesta en la estructura del nodo](assets/composite-path.png)

El `AEMCard` el componente es el mismo que se definió [en el caso de uso anterior.](#content-does-not-exist) AEM SPA Aquí se incluye en la lista el contenido definido en la ubicación anterior del proyecto de la.
