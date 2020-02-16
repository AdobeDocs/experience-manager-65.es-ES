---
title: Configuración del contenedor de diseño y el modo de diseño
seo-title: Configuración del contenedor de diseño y el modo de diseño
description: Obtenga información sobre cómo configurar el contenedor de diseño y el modo de diseño.
seo-description: Obtenga información sobre cómo configurar el contenedor de diseño y el modo de diseño.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración del contenedor de diseño y el modo de diseño{#configuring-layout-container-and-layout-mode}

[Diseño](/help/sites-authoring/responsive-layout.md) interactivo es un mecanismo para realizar diseños [web](https://en.wikipedia.org/wiki/Responsive_web_design)interactivos. Esto permite al usuario crear páginas web con un diseño y unas dimensiones que dependen de los dispositivos que utilizan los usuarios.

>[!NOTE]
>
>Esto se puede comparar con los mecanismos web [](/help/sites-developing/mobile-web.md) móviles, que utilizan el diseño web adaptable (principalmente para la IU clásica).

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* [**Contenedor **](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)de diseño, componente

   Este componente proporciona un sistema de párrafos de cuadrícula que le permite añadir y colocar componentes en una cuadrícula interactiva. Se puede utilizar como parsys predeterminado para la página y/o ponerlo a disposición de los autores en el navegador de componentes.

   * El componente **Contenedor** de diseño predeterminado se define en:

      /libs/wcm/foundation/components/responsivegrid

   * Puede definir contenedores de diseño:

      * Como componente que el usuario puede agregar a una página.
      * Como parámetro predeterminado para la página.
      * Ambas.

         Puede tener el contenedor de diseño como estándar para la página, a la vez que permite al usuario agregar más contenedores de diseño dentro de esto; por ejemplo, para obtener el control de columna.

* **[Modo](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**de diseño Una vez que el contenedor de diseño se coloca en la página, puede utilizar el modo **Diseño**para colocar el contenido en la cuadrícula adaptable.

* [**Emulador **](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)Esta opción le permite crear y editar sitios web adaptables que reorganizan el diseño en función del tamaño del dispositivo o la ventana, mediante el redimensionado activo de los componentes. El usuario puede utilizar el emulador para ver cómo se representará el contenido.

>[!CAUTION]
>
>Although the **Layout Container** component is available in the classic UI, its full functionality is only available in the touch-enabled UI.

Estos mecanismos de cuadrícula interactiva le permiten:

* Utilice puntos de interrupción (que indican la agrupación de dispositivos) para definir un comportamiento de contenido diferente según el diseño del dispositivo.
* Ocultar componentes según el grupo de dispositivos (definir en qué punto de interrupción se ocultará un componente).
* Utilizar el ajuste horizontal a la cuadrícula (colocar componentes en la cuadrícula, cambiar su tamaño según sea necesario, definir cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo).
* Realizar el control de columnas.

>[!NOTE]
>
>En una instalación lista para usar, se ha configurado un diseño interactivo para el sitio [de referencia](/help/sites-developing/we-retail.md)We.Retail. Aún debe [activar el componente](#enable-the-layout-container-component-for-page) Contenedor de diseño para otras páginas.

## Configuración del emulador interactivo {#configuring-the-responsive-emulator}

Estas tareas le permiten ver el **emulador** interactivo en su sitio.

### Registrar los componentes de la página para emulación {#register-your-page-components-for-emulation}

Para habilitar el emulador para admitir las páginas, debe registrar los componentes de la página. Consulte [Registro de componentes de página para simulación](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Especificar los grupos de dispositivos {#specify-the-device-groups}

Para especificar los grupos de dispositivos que aparecen en la lista Dispositivos del emulador, consulte [Especificación de los grupos](/help/sites-developing/responsive.md#specifying-the-device-groups)de dispositivos.

### Vincular el sitio a los grupos de dispositivos especificados {#link-your-site-to-the-specified-device-groups}

Para incluir el administrador, debe vincular el sitio a los grupos de dispositivos. Consulte [Adición de la lista](/help/sites-developing/responsive.md#adding-the-devices-list) de dispositivos (tanto para la IU clásica como la táctil).

## Activar el modo de diseño del sitio {#activate-layout-mode-for-your-site}

Estos procedimientos se utilizan para habilitar el modo **Diseño** en el sitio.

### Configurar los puntos de interrupción {#configure-the-breakpoints}

[Puntos de interrupción](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Se utilizan en diseños interactivos.
* Se puede definir:

   * En la plantilla de página, desde donde se copiará la configuración en cualquier página creada con esa plantilla.
   * En el nodo de página, desde donde cualquier página secundaria heredará la configuración.

* Defina un título y una anchura:

   * En el título se describe la agrupación genérica del dispositivo, con la orientación, si es necesario; por ejemplo, teléfono, tablet, tabla horizontal.
   * La anchura define la anchura máxima en píxeles para esa agrupación de dispositivos genérica. Por ejemplo, si el teléfono de punto de interrupción tiene una anchura de 768, entonces la anchura máxima del diseño utilizado para un dispositivo móvil.

* Son visibles como marcadores en la parte superior del editor de páginas cuando se utiliza el emulador.
* Se heredan de la jerarquía del nodo principal y se pueden anular a voluntad.
* Hay un punto de interrupción predeterminado (predeterminado) que cubre todo lo que se encuentra por encima del último punto de interrupción *configurado* .

Se pueden definir con CRXDE Lite o XML.

>[!NOTE]
>
>Si va a configurar un nuevo proyecto:
>
>* debe agregar puntos de interrupción a las plantillas.
>
>
Si va a migrar un proyecto existente (con contenido existente), debe:
>
>* agregar puntos de interrupción a las plantillas
>* agregar los mismos puntos de interrupción a las páginas existentes
   >  Como la herencia está en funcionamiento, puede limitarla a la página raíz del contenido.
>



#### Configuración de puntos de interrupción con CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Con CRXDE Lite (o equivalente), navegue hasta:

   * La definición de la plantilla.
   * El `jcr:content` nodo de la página.

1. En `jcr:content` Crear el nodo:

   * Nombre: `cq:responsive`
   * Tipo: `nt:unstructured`

1. En este campo, cree el nodo:

   * Nombre: `breakpoints`
   * Tipo: `nt:unstructured`

1. En el nodo de puntos de interrupción puede crear cualquier número de puntos de interrupción. Cada definición es un nodo único con las siguientes propiedades:

   * Nombre: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Título: `String` * `<descriptive title seen in Emulator>`*
   * Anchura: `Decimal` * `<value of breakpoint>`*

#### Configuración de puntos de interrupción mediante XML {#configuring-breakpoints-using-xml}

Los puntos de interrupción se encuentran dentro de la `<jcr:content>` sección de la `.context.html` carpeta de plantilla (o contenido) correspondiente.

Una definición de ejemplo:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Agregar un proveedor de información adaptable {#add-a-responsive-information-provider}

>[!NOTE]
>
>Esto solo es necesario si el componente de página no se basa en el componente de página de base.

Copie la siguiente estructura de `cq:infoProviders` nodos en el componente de página principal:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Habilitar el cambio de tamaño del componente para la página {#enable-component-resizing-for-the-page}

Estos procedimientos son necesarios para poder cambiar el tamaño de los componentes en el modo **Diseño** .

### Definir contenedor de diseño como parsys principal {#set-layout-container-as-main-parsys}

Para que el parámetro principal de la página sea un contenedor de diseño, debe definir el parámetro como:

`wcm/foundation/components/responsivegrid`

En:

* Componente de página
* Plantilla de página (para uso futuro)

Los dos ejemplos siguientes ilustran la definición:

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### Incluir el CSS adaptable {#include-the-responsive-css}

#### CSS para puntos de interrupción que utilizan MENOS {#css-for-breakpoints-using-less}

AEM utiliza MENOS para generar partes de la CSS necesaria, que deben incluirse en los proyectos.

También deberá crear una biblioteca [de](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) cliente para proporcionar configuración adicional y llamadas a funciones. El siguiente extracto LESS es un ejemplo del mínimo que debe agregar al proyecto:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

La definición de cuadrícula base se encuentra en:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Consideraciones sobre el estilo {#styling-considerations}

Se cambiará el tamaño de los componentes contenidos en un contenedor interactivo (junto con sus respectivos elementos DOM HTML) según el tamaño de cuadrícula adaptable. Por lo tanto, en estas circunstancias, se recomienda evitar (o actualizar) definiciones de elementos DOM de ancho fijo (contenidos).

Por ejemplo:

* Antes:

   * `width=100px`

* Después:

   * `max-width=100px`

#### Cambio de tamaño y compatibilidad con imágenes adaptables {#resizing-and-adaptive-image-compliance}

Si cambia el tamaño de un componente dentro de la cuadrícula, se activarán los siguientes oyentes, según corresponda:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Para cambiar el tamaño y actualizar correctamente el contenido de una imagen adaptable incluida en una cuadrícula adaptable, debe agregar un `afterEdit` conjunto para `REFRESH_PAGE` oyente al `EditConfig` archivo de cada componente contenido.

Por ejemplo:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

El mecanismo de imagen adaptable está disponible mediante una secuencia de comandos que controla la selección de la imagen correcta para el tamaño actual de la ventana. Se activa cuando el DOM está listo o cuando recibe un evento dedicado. Actualmente, la página debe actualizarse para reflejar correctamente el resultado de la acción del usuario.

>[!CAUTION]
>
>Los clientes de hojas de estilo personalizadas deben cargarse como parte del encabezado para que funcionen correctamente en el autor y en la publicación.

## Habilitar el componente Contenedor de diseño para la página {#enable-the-layout-container-component-for-page}

Estas tareas permiten a los autores arrastrar instancias del componente Contenedor **de** diseño a la página.

### Habilitar el componente Contenedor de diseño para la edición de páginas {#enable-the-layout-container-component-for-page-editing}

Para permitir que los autores agreguen cuadrículas adaptables adicionales a las páginas de contenido, debe habilitar el componente Contenedor de diseño para la página. Puede hacerlo mediante:

* **Entorno de creación**

   Utilice el modo [](/help/sites-authoring/default-components-designmode.md) Diseño para activar el componente Contenedor **de** capas para una página.

* **Definición de componente**

   Utilice `allowedComponent` o una inclusión estática al definir el componente.

### Configuración de la cuadrícula del contenedor de diseños {#configure-the-grid-of-the-layout-container}

Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño:

1. **Entorno de creación**

   Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño.

   Para ello, utilice el modo [](/help/sites-authoring/default-components-designmode.md)Diseño y, a continuación, abra el cuadro de diálogo de diseño del contenedor requerido. Aquí puede especificar cuántas columnas estarán disponibles para la colocación y el tamaño. El valor predeterminado es 12.

1. **XML**

   Las definiciones de la cuadrícula adaptable se especifican en:

   `etc/design/<*your-project-name*>/.content.xml`

   Se pueden definir los siguientes parámetros:

   * Número de columnas disponibles:

      * `columns="{String}8"`
   * Componentes que se pueden agregar al componente actual:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


