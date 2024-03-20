---
title: Configuración del contenedor y el modo de diseño
description: Obtenga información sobre cómo configurar el contenedor y el modo de diseño.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 2%

---

# Configuración del contenedor y el modo de diseño{#configuring-layout-container-and-layout-mode}

[Diseño interactivo](/help/sites-authoring/responsive-layout.md) es un mecanismo para realizar [diseño web adaptable](https://en.wikipedia.org/wiki/Responsive_web_design). Esto permite al usuario crear páginas web con un diseño y dimensiones dependientes de los dispositivos que utilizan sus usuarios.

>[!NOTE]
>
>Esto se puede comparar con el [Web móvil](/help/sites-developing/mobile-web.md) mecanismos, que utilizan el diseño web adaptable (principalmente para la IU clásica).

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* Componente [**Contenedor de diseño**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

  Este componente proporciona un sistema de párrafos de cuadrícula que le permite agregar y colocar componentes en una cuadrícula adaptable. Se puede utilizar como parsys predeterminado para la página o estar disponible para los autores en el explorador de componentes.

   * El valor predeterminado **Contenedor de diseño** el componente se define en:

     /libs/wcm/foundation/components/responsivegrid

   * Puede definir contenedores de diseño:

      * Como un componente que el usuario puede agregar a una página.
      * Como parsys predeterminado para la página.
      * Ambos.

        Puede tener el contenedor de diseño como estándar para la página, a la vez que permite al usuario agregar más contenedores de diseño dentro de esta página; por ejemplo, para lograr el control de columna.

* **[Modo de diseño](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Una vez que el contenedor de diseño esté colocado en la página, puede utilizar el **Diseño** modo para colocar contenido en la cuadrícula adaptable.

* [**Emulador**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
Esto permite crear y editar sitios web interactivos que reorganizan el diseño según el tamaño del dispositivo o la ventana, mediante el cambio de tamaño de los componentes de forma interactiva. A continuación, el usuario puede ver cómo se representa el contenido mediante el emulador.

>[!CAUTION]
>
>Aunque la variable **Contenedor de diseño** está disponible en la IU clásica, su funcionalidad completa solo está disponible en la IU táctil.

Con estos mecanismos de cuadrícula adaptable puede hacer lo siguiente:

* Utilice puntos de interrupción (que indican la agrupación del dispositivo) para definir un comportamiento de contenido diferente en función del diseño del dispositivo.
* Ocultar componentes basados en grupos de dispositivos (defina en qué punto de interrupción se ocultará un componente).
* Utilice el ajuste horizontal a la cuadrícula (coloque los componentes en la cuadrícula, cambie su tamaño según sea necesario, defina cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo).
* Realizar el control de columnas.

>[!NOTE]
>
>En una instalación predeterminada, se ha configurado un diseño interactivo para el [Sitio de referencia de We.Retail](/help/sites-developing/we-retail.md). [Activación del componente Contenedor de diseño](#enable-the-layout-container-component-for-page) para otras páginas.

## Configuración del emulador interactivo {#configuring-the-responsive-emulator}

Esta tarea le permite ver la respuesta **Emulador** en el sitio.

### Registre los componentes de la página para su emulación {#register-your-page-components-for-emulation}

Para permitir que el emulador admita las páginas, debe registrar los componentes de la página. Consulte [Registro de componentes de página para simulación](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Especificar los grupos de dispositivos {#specify-the-device-groups}

Para especificar los grupos de dispositivos que aparecen en la lista Dispositivos del emulador, consulte [Especificación de los grupos de dispositivos](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Vincular el sitio a los grupos de dispositivos especificados {#link-your-site-to-the-specified-device-groups}

Para incluir el emulador, vincule el sitio a los grupos de dispositivos. Consulte [Agregar la lista de dispositivos](/help/sites-developing/responsive.md#adding-the-devices-list) (tanto para la IU clásica como para la táctil).

## Activar el modo Diseño para su sitio {#activate-layout-mode-for-your-site}

Estos procedimientos se utilizan para habilitar el **Diseño** en el sitio.

### Configuración de los puntos de interrupción {#configure-the-breakpoints}

[Puntos de interrupción](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Se utilizan en diseños adaptables.
* Se puede definir:

   * En la plantilla de página, desde donde se copia la configuración a cualquier página creada con esa plantilla.
   * En el nodo de la página, desde donde cualquier página secundaria hereda la configuración.

* Defina un título y una anchura:

   * El título describe la agrupación de dispositivos genéricos, con orientación si es necesario; por ejemplo, teléfono, tableta, tableta horizontal.
   * La anchura define la anchura máxima en píxeles para esa agrupación de dispositivos genéricos. Por ejemplo, si el punto de interrupción del teléfono tiene una anchura de 768, indique la anchura máxima del diseño utilizado para un dispositivo móvil.

* Están visibles como marcadores en la parte superior del editor de páginas cuando utiliza el emulador.
* Se heredan de la jerarquía de nodos principal y se pueden anular a voluntad.
* Hay un punto de interrupción predeterminado (predeterminado) que cubre todo lo que está por encima del último *configurado* punto de interrupción.

Se pueden definir utilizando CRXDE Lite o XML.

>[!NOTE]
>
>Si va a configurar un proyecto nuevo:
>
>* agregue puntos de interrupción a las plantillas.
>
>Si está migrando un proyecto existente (con contenido existente), debe:
>
>* añadir puntos de interrupción a las plantillas
>* agregar los mismos puntos de interrupción a las páginas existentes
>
>  Como la herencia está en funcionamiento, puede limitarla a la página raíz del contenido.

#### Configuración de puntos de interrupción mediante CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Con el CRXDE Lite (o equivalente), vaya a:

   * Definición de la plantilla.
   * El `jcr:content` de la página.

1. En `jcr:content` cree el nodo:

   * Nombre: `cq:responsive`
   * Tipo: `nt:unstructured`

1. En esta sección, cree el nodo:

   * Nombre: `breakpoints`
   * Tipo: `nt:unstructured`

1. Bajo el nodo de puntos de interrupción puede crear cualquier número de puntos de interrupción. Cada definición es un nodo único con las siguientes propiedades:

   * Nombre: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Título: `String` * `<descriptive title seen in Emulator>`*
   * Anchura: `Decimal` * `<value of breakpoint>`*

#### Configurar puntos de interrupción mediante XML {#configuring-breakpoints-using-xml}

Los puntos de interrupción se encuentran dentro de `<jcr:content>` de la sección `.context.html` en la carpeta de plantilla (o contenido) adecuada.

Una definición de ejemplo:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Añadir un proveedor de información interactivo {#add-a-responsive-information-provider}

>[!NOTE]
>
>Esto solo es necesario si el componente de página no se basa en el componente de página base.

Copie lo siguiente `cq:infoProviders` estructura de nodos en el componente de página principal:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Habilitar el cambio de tamaño del componente para la página {#enable-component-resizing-for-the-page}

Estos procedimientos son necesarios para poder cambiar el tamaño de los componentes en **Diseño** modo.

### Definir contenedor de diseño como parsys principal {#set-layout-container-as-main-parsys}

Para establecer que el parsys principal de la página sea un contenedor de diseño, defina el parsys como:

`wcm/foundation/components/responsivegrid`

En:

* Componente Página
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

### Incluir CSS interactivo {#include-the-responsive-css}

#### CSS para puntos de interrupción con LESS {#css-for-breakpoints-using-less}

AEM Utiliza LESS para generar partes del CSS necesario, que deben incluirse para los proyectos.

También debe crear un [biblioteca de cliente](https://experienceleague.adobe.com/docs/) para proporcionar llamadas de función y configuración adicionales. El siguiente extracto LESS es un ejemplo del mínimo que debe agregar al proyecto:

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

La definición de la cuadrícula base se encuentra en:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Consideraciones de estilo {#styling-considerations}

Los componentes contenidos en un contenedor interactivo cambian de tamaño (junto con sus respectivos elementos DOM HTML) según el tamaño de la cuadrícula interactiva. Por lo tanto, en estas circunstancias, se recomienda evitar (o actualizar) las definiciones de elementos DOM de ancho fijo (contenidos).

Por ejemplo:

* Antes:

   * `width=100px`

* Después:

   * `max-width=100px`

#### Cambio de tamaño y compatibilidad con imágenes adaptables {#resizing-and-adaptive-image-compliance}

Cualquier cambio de tamaño de un componente dentro de la cuadrícula almacenará en déclencheur los siguientes oyentes según corresponda:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Para cambiar el tamaño y actualizar correctamente el contenido de una imagen adaptable incluida en una cuadrícula adaptable, debe agregar una `afterEdit` establezca en `REFRESH_PAGE` escucha en el `EditConfig` de cada componente contenido.

Por ejemplo:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

El mecanismo de imagen adaptable está disponible a través de una secuencia de comandos que controla la selección de la imagen correcta para el tamaño actual de la ventana. Se activa después de que el DOM esté listo o cuando se recibe un evento dedicado. Actualmente, la página debe actualizarse para reflejar correctamente el resultado de la acción del usuario.

>[!CAUTION]
>
>Los clientlibs de hojas de estilo personalizadas deben cargarse como parte del encabezado para que funcionen correctamente en la creación y publicación.

## Habilitar el componente Contenedor de diseño para la página {#enable-the-layout-container-component-for-page}

Estas tareas permiten a los autores arrastrar instancias del **Contenedor de diseño** en la página.

### Habilitar el componente Contenedor de diseño para la edición de páginas {#enable-the-layout-container-component-for-page-editing}

Para permitir que los autores agreguen más cuadrículas adaptables a las páginas de contenido, debe habilitar el componente Contenedor de diseño para su página. Para ello, utilice uno de los métodos siguientes:

* **Entorno de creación**

  Uso [Modo de diseño](/help/sites-authoring/default-components-designmode.md) para activar el **Contenedor de capa** para una página.

* **Definición del componente**

  Uso `allowedComponent` o una inclusión estática al definir el componente.

### Configuración de la cuadrícula del contenedor de diseño {#configure-the-grid-of-the-layout-container}

Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño:

1. **Entorno de creación**

   Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño.

   Para ello, utilice [Modo de diseño](/help/sites-authoring/default-components-designmode.md)A continuación, abra el cuadro de diálogo de diseño del contenedor requerido. Aquí puede especificar cuántas columnas estarán disponibles para el posicionamiento y el tamaño. El valor predeterminado es 12.

1. **XML**

   Las definiciones de la cuadrícula adaptable se especifican en:

   `etc/design/<*your-project-name*>/.content.xml`

   Se pueden definir los siguientes parámetros:

   * Número de columnas disponibles:

      * `columns="{String}8"`

   * Componentes que se pueden añadir al componente actual:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
