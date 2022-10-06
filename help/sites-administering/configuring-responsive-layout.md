---
title: Configuración del contenedor de diseño y el modo de diseño
seo-title: Configuring Layout Container and Layout Mode
description: Obtenga información sobre cómo configurar el contenedor de diseño y el modo de diseño.
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 9%

---

# Configuración del contenedor de diseño y el modo de diseño{#configuring-layout-container-and-layout-mode}

[Diseño interactivo](/help/sites-authoring/responsive-layout.md) es un mecanismo para realizar [diseño web interactivo](https://en.wikipedia.org/wiki/Responsive_web_design). Esto permite al usuario crear páginas web con un diseño y dimensiones que dependen de los dispositivos que utilizan sus usuarios.

>[!NOTE]
>
>Esto se puede comparar con la variable [Web móvil](/help/sites-developing/mobile-web.md) que utilizan diseño web adaptable (principalmente para la IU clásica).

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* Componente [**Contenedor de diseño**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

   Este componente proporciona un sistema de párrafos de cuadrícula que le permite añadir y colocar componentes en una cuadrícula interactiva. Se puede utilizar como parsys predeterminado para la página o ponerlo a disposición de los autores en el navegador de componentes.

   * El valor predeterminado **Contenedor de diseño** se define en:

      /libs/wcm/foundation/components/responsivegrid

   * Puede definir contenedores de diseño:

      * Como componente que el usuario puede añadir a una página.
      * Como parsys predeterminado para la página.
      * Ambas.

         Puede tener el contenedor de diseño como estándar para la página, mientras permite al usuario agregar más contenedores de diseño dentro de esto; por ejemplo, para conseguir el control de columnas.

* **[Modo de diseño](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Una vez que el contenedor de diseño esté colocado en la página, puede usar la variable 
**Diseño** para colocar el contenido en la cuadrícula interactiva.

* [**Emulador**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate) Esta opción le permite crear y editar sitios web adaptables que reorganizan el diseño en función del tamaño del dispositivo o la ventana, mediante el redimensionado activo de los componentes. El usuario puede utilizar el emulador para ver cómo se representará el contenido.

>[!CAUTION]
>
>Aunque la variable **Contenedor de diseño** está disponible en la IU clásica; su funcionalidad completa solo está disponible en la IU táctil.

Estos mecanismos de cuadrícula interactiva le permiten:

* Utilice puntos de interrupción (que indican la agrupación del dispositivo) para definir el comportamiento de contenido diferente en función del diseño del dispositivo.
* Ocultar componentes en función del grupo de dispositivos (definir en qué punto de interrupción se ocultará un componente).
* Utilizar el ajuste horizontal a la cuadrícula (colocar componentes en la cuadrícula, cambiar su tamaño según sea necesario, definir cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo).
* Realizar el control de columnas.

>[!NOTE]
>
>En una instalación predeterminada, se ha configurado un diseño interactivo para la variable [Sitio de referencia de We.Retail](/help/sites-developing/we-retail.md). Aún debe [activación del componente Contenedor de diseño](#enable-the-layout-container-component-for-page) para otras páginas.

## Configuración del emulador interactivo {#configuring-the-responsive-emulator}

Estas tareas le permiten ver las **Emulador** del sitio.

### Registre los componentes de la página para emulación {#register-your-page-components-for-emulation}

Para permitir que el emulador admita sus páginas, debe registrar los componentes de la página. Consulte [Registro de componentes de página para la simulación](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Especificar los grupos de dispositivos {#specify-the-device-groups}

Para especificar los grupos de dispositivos que aparecen en la lista Dispositivos del emulador, consulte [Especificación de los grupos de dispositivos](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Vincular el sitio a grupos de dispositivos especificados {#link-your-site-to-the-specified-device-groups}

Para incluir el simulador, debe vincular el sitio a los grupos de dispositivos. Consulte [Adición de la lista de dispositivos](/help/sites-developing/responsive.md#adding-the-devices-list) (para la IU clásica y la táctil optimizada).

## Activar el modo de diseño del sitio {#activate-layout-mode-for-your-site}

Estos procedimientos se utilizan para habilitar la variable **Diseño** en el sitio.

### Configuración de los puntos de interrupción {#configure-the-breakpoints}

[Puntos de interrupción](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Se utilizan en el diseño interactivo.
* Se puede definir:

   * En la plantilla de página, desde donde se copiará la configuración a cualquier página creada con esa plantilla.
   * En el nodo de página, desde el que cualquier página secundaria heredará la configuración.

* Defina un título y una anchura:

   * El título describe la agrupación genérica del dispositivo, con la orientación si es necesario; por ejemplo, teléfono, tableta, tabla horizontal.
   * La anchura define la anchura máxima en píxeles para esa agrupación de dispositivos genérica. Por ejemplo, si el teléfono de punto de interrupción tiene una anchura de 768, entonces es la anchura máxima del diseño utilizado para un dispositivo móvil.

* Se pueden ver como marcadores en la parte superior del editor de páginas al usar el emulador.
* Se heredan de la jerarquía del nodo principal y se pueden sobrescribir a voluntad.
* Hay un punto de interrupción predeterminado (predeterminado) que cubre todo lo que está por encima del último *configurado* punto de interrupción.

Pueden definirse mediante CRXDE Lite o XML.

>[!NOTE]
>
>Si está configurando un nuevo proyecto:
>
>* debe añadir puntos de interrupción a las plantillas.
>
>Si está migrando un proyecto existente (con contenido existente), debe:
>
>* añadir puntos de interrupción a las plantillas
>* agregar los mismos puntos de interrupción a las páginas existentes
>
>  Como la herencia está en funcionamiento, puede limitarla a la página raíz del contenido.

#### Configuración de puntos de interrupción mediante el CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Con el CRXDE Lite (o equivalente), vaya a:

   * La definición de la plantilla.
   * La variable `jcr:content` de su página.

1. En `jcr:content` cree el nodo :

   * Nombre: `cq:responsive`
   * Tipo: `nt:unstructured`

1. En esto, cree el nodo :

   * Nombre: `breakpoints`
   * Tipo: `nt:unstructured`

1. En el nodo de puntos de interrupción puede crear cualquier número de puntos de interrupción. Cada definición es un nodo único con las siguientes propiedades:

   * Nombre: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Título: `String` * `<descriptive title seen in Emulator>`*
   * Anchura: `Decimal` * `<value of breakpoint>`*

#### Configuración de puntos de interrupción mediante XML {#configuring-breakpoints-using-xml}

Los puntos de interrupción se encuentran dentro de la variable `<jcr:content>` de la sección `.context.html` en la carpeta de plantilla (o contenido) correspondiente.

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
>Esto solo es necesario si el componente de página no se basa en el componente de página base.

Copie lo siguiente `cq:infoProviders` estructura de nodos en el componente de página principal:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Habilitar el cambio de tamaño de los componentes para la página {#enable-component-resizing-for-the-page}

Estos procedimientos son necesarios para que pueda cambiar el tamaño de los componentes en la variable **Diseño** en el menú contextual.

### Definir contenedor de diseño como parsys principal {#set-layout-container-as-main-parsys}

Para que el parsys principal de su página sea un contenedor de diseño, debe definir el parsys como:

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

#### CSS para puntos de interrupción que utilizan LESS {#css-for-breakpoints-using-less}

AEM utiliza LESS para generar partes del CSS necesario, que deben incluirse en los proyectos.

También deberá crear un [biblioteca cliente](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) para proporcionar configuración adicional y llamadas a funciones. El siguiente extracto LESS es un ejemplo del mínimo que debe añadir al proyecto:

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

Se cambiará el tamaño de los componentes que se mantengan dentro de un contenedor interactivo (junto con sus respectivos elementos DOM de HTML) según el tamaño de cuadrícula adaptable. Por lo tanto, en estas circunstancias, se recomienda evitar (o actualizar) las definiciones de elementos DOM de ancho fijo (contenidos).

Por ejemplo:

* Antes:

   * `width=100px`

* Después:

   * `max-width=100px`

#### Cambio de tamaño y conformidad con la imagen adaptable {#resizing-and-adaptive-image-compliance}

Cualquier cambio de tamaño de un componente dentro de la cuadrícula dará déclencheur a los siguientes oyentes, según corresponda:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Para cambiar el tamaño y actualizar correctamente el contenido de una imagen adaptable incluida en una cuadrícula adaptable, debe añadir una `afterEdit` configure como `REFRESH_PAGE` al `EditConfig` archivo de cada componente contenido.

Por ejemplo:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

El mecanismo de imagen adaptable está disponible a través de una secuencia de comandos que controla la selección de la imagen correcta para el tamaño actual de la ventana. Se activa después de que el DOM esté listo o al recibir un evento dedicado. Actualmente, la página debe actualizarse para reflejar correctamente el resultado de la acción del usuario.

>[!CAUTION]
>
>Los clientlibs de hojas de estilo personalizadas deben cargarse como parte del encabezado para que funcionen correctamente en el autor y en la publicación.

## Habilitar el componente Contenedor de diseño para la página {#enable-the-layout-container-component-for-page}

Estas tareas permiten a los autores arrastrar instancias del **Contenedor de diseño** en la página.

### Habilitar el componente Contenedor de diseño para la edición de páginas {#enable-the-layout-container-component-for-page-editing}

Para permitir que los autores agreguen cuadrículas adaptables adicionales a las páginas de contenido, debe habilitar el componente Contenedor de diseño para la página. Puede hacerlo mediante:

* **Entorno de creación**

   Uso [Modo de diseño](/help/sites-authoring/default-components-designmode.md) para activar el **Contenedor de capa** para una página.

* **Definición de componentes**

   Uso `allowedComponent` o una inclusión estática al definir el componente.

### Configuración de la cuadrícula del contenedor de diseño {#configure-the-grid-of-the-layout-container}

Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño:

1. **Entorno de creación**

   Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño.

   Para ello, utilice [Modo de diseño](/help/sites-authoring/default-components-designmode.md)y, a continuación, abra el cuadro de diálogo de diseño del contenedor requerido. Aquí puede especificar cuántas columnas estarán disponibles para su colocación y ajuste de tamaño. El valor predeterminado es 12.

1. **XML**

   Las definiciones de la cuadrícula interactiva se especifican en:

   `etc/design/<*your-project-name*>/.content.xml`

   Se pueden definir los siguientes parámetros:

   * Número de columnas disponibles:

      * `columns="{String}8"`
   * Componentes que se pueden añadir al componente actual:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
