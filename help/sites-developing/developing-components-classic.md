---
title: Desarrollo de componentes AEM (IU clásica)
seo-title: Developing AEM Components (Classic UI)
description: La IU clásica utiliza ExtJS para crear utilidades que proporcionen la apariencia de los componentes. HTL no es el lenguaje de secuencias de comandos recomendado para AEM.
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2394'
ht-degree: 1%

---

# Desarrollo de componentes AEM (IU clásica){#developing-aem-components-classic-ui}

La IU clásica utiliza ExtJS para crear utilidades que proporcionen la apariencia de los componentes. Debido a la naturaleza de estas utilidades, hay algunas diferencias entre la forma en que los componentes interactúan con la IU clásica y la [IU táctil](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Muchos aspectos del desarrollo de componentes son comunes en la IU clásica y en la IU táctil, por lo que **debe leer [Componentes AEM: conceptos básicos](/help/sites-developing/components-basics.md) before** uso de esta página, que trata de los detalles específicos de la IU clásica.

>[!NOTE]
>
>Aunque tanto el lenguaje de plantilla de HTML (HTL) como JSP pueden utilizarse para desarrollar componentes para la IU clásica, esta página ilustra el desarrollo con JSP. Esto se debe únicamente al historial de uso de JSP en la IU clásica.
>
>HTL es ahora el lenguaje de secuencias de comandos recomendado para AEM. Consulte [HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) y [Desarrollo de componentes AEM](/help/sites-developing/developing-components.md) para comparar métodos.

## Estructura {#structure}

La estructura básica de un componente se cubre en la página [Componentes AEM: conceptos básicos](/help/sites-developing/components-basics.md#structure), que aplica tanto las IU táctiles como las clásicas. Incluso si no necesita utilizar la configuración de la IU táctil en su nuevo componente, puede ser útil que los conozca al heredar de componentes existentes.

## Scripts JSP {#jsp-scripts}

Los scripts o servlets JSP se pueden utilizar para procesar componentes. Según las reglas de procesamiento de solicitudes de Sling, el nombre del script predeterminado es:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

El archivo de script JSP `global.jsp` se utiliza para proporcionar acceso rápido a objetos específicos (es decir, para acceder al contenido) a cualquier archivo de script JSP utilizado para procesar un componente.

Por lo tanto, `global.jsp` debe incluirse en todos los componentes que procesen secuencias de comandos JSP donde uno o más de los objetos proporcionados en `global.jsp` se utilizan.

La ubicación del valor predeterminado `global.jsp` es:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>La ruta `/libs/wcm/global.jsp`, que fue utilizado por las versiones CQ5.3 y anteriores, ahora está obsoleto.

### Función de global.jsp, API usadas y Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

A continuación se enumeran los objetos más importantes proporcionados de la opción predeterminada `global.jsp`:

Resumen:

* `<cq:defineObjects />`

   * `slingRequest` - El objeto de solicitud ajustado ( `SlingHttpServletRequest`).
   * `slingResponse` - El objeto de respuesta ajustado ( `SlingHttpServletResponse`).
   * `resource` - El Objeto De Recurso Sling ( `slingRequest.getResource();`).
   * `resourceResolver` - El Objeto Sling Resource Resolver ( `slingRequest.getResoucreResolver();`).
   * `currentNode` - El nodo JCR resuelto para la solicitud.
   * `log` - El registrador predeterminado ().
   * `sling` - El ayudante del script de Sling.
   * `properties` - Las propiedades del recurso dirigido ( `resource.adaptTo(ValueMap.class);`).
   * `pageProperties` - Las propiedades de la página del recurso dirigido.
   * `pageManager` - El administrador de páginas para acceder AEM páginas de contenido ( `resourceResolver.adaptTo(PageManager.class);`).
   * `component` - El objeto de componente del componente de AEM actual.
   * `designer` - El objeto de diseñador para recuperar información de diseño ( `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign` - El diseño del recurso dirigido.
   * `currentStyle` - El estilo del recurso dirigido.

### Acceso al contenido {#accessing-content}

Existen tres métodos para acceder al contenido en AEM WCM:

* Mediante el objeto de propiedades introducido en `global.jsp`:

   El objeto properties es una instancia de un ValueMap (consulte [API de Sling](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) y contiene todas las propiedades del recurso actual.

   Ejemplo: `String pageTitle = properties.get("jcr:title", "no title");` se utiliza en la secuencia de comandos de renderización de un componente de página.

   Ejemplo: `String paragraphTitle = properties.get("jcr:title", "no title");` se utiliza en la secuencia de comandos de renderización de un componente de párrafo estándar.

* A través de la función `currentPage` objeto introducido en `global.jsp`:

   La variable `currentPage` es una instancia de una página (consulte [API de AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)). La clase page proporciona algunos métodos para acceder al contenido.

   Ejemplo: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` objeto introducido en `global.jsp`:

   La variable `currentNode` es una instancia de un nodo (consulte [API de JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). Se puede acceder a las propiedades de un nodo mediante la variable `getProperty()` método.

   Ejemplo: `String pageTitle = currentNode.getProperty("jcr:title");`

## Bibliotecas de etiquetas JSP {#jsp-tag-libraries}

Las bibliotecas de etiquetas CQ y Sling le proporcionan acceso a funciones específicas para su uso en el script JSP de sus plantillas y componentes.

Para obtener más información, consulte el documento [Bibliotecas de etiquetas](/help/sites-developing/taglib.md).

## Uso de bibliotecas de HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Consulte el documento [Uso de bibliotecas de HTML del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Cuadro de diálogo {#dialog}

El componente necesitará un cuadro de diálogo para que los autores añadan y configuren el contenido.

Consulte [Componentes AEM: conceptos básicos](/help/sites-developing/components-basics.md#dialogs) para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente. Esto incluye atributos como acciones disponibles para el componente, características del editor in situ y oyentes relacionados con eventos en el componente. La configuración es común a las IU táctiles y clásicas, aunque con ciertas diferencias específicas.

La variable [el comportamiento de edición de un componente está configurado](/help/sites-developing/components-basics.md#edit-behavior) añadiendo un `cq:editConfig` nodo de tipo `cq:EditConfig` debajo del nodo del componente (de tipo `cq:Component`) y añadiendo propiedades específicas y nodos secundarios.

## Uso y ampliación de utilidades de ExtJS {#using-and-extending-extjs-widgets}

Consulte [Uso y ampliación de utilidades de ExtJS](/help/sites-developing/widgets.md) para obtener más información.

## Uso de xtypes para los widgets de ExtJS {#using-xtypes-for-extjs-widgets}

Consulte [Uso de xtype](/help/sites-developing/xtypes.md) para obtener más información.

## Desarrollo de nuevos componentes {#developing-new-components}

En esta sección se describe cómo crear sus propios componentes y agregarlos al sistema de párrafos.

Una forma rápida de empezar es copiar un componente existente y luego realizar los cambios que desee.

Un ejemplo de cómo desarrollar un componente se describe detalladamente en [Ampliación del componente de texto e imagen: un ejemplo.](#extending-the-text-and-image-component-an-example)

### Desarrollar un nuevo componente (adaptar componente existente) {#develop-a-new-component-adapt-existing-component}

Para desarrollar nuevos componentes para AEM basados en un componente existente, puede copiar el componente, crear un archivo javascript para el nuevo componente y almacenarlo en una ubicación accesible para AEM (consulte también [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Con CRXDE Lite, cree una nueva carpeta de componentes en:

   / `apps/<myProject>/components/<myComponent>`

   Vuelva a crear la estructura de nodos como en las bibliotecas y, a continuación, copie la definición de un componente existente, como el componente Texto . Por ejemplo, para personalizar la copia del componente Texto :

   * de `/libs/foundation/components/text`
   * hasta `/apps/myProject/components/text`

1. Modifique el `jcr:title` para reflejar su nuevo nombre.
1. Abra la nueva carpeta de componentes y realice los cambios que necesite. Elimine también cualquier información superflua de la carpeta.

   Puede realizar cambios como:

   * adición de un nuevo campo en el cuadro de diálogo

      * `cq:dialog` - cuadro de diálogo para la IU táctil
      * `dialog` - cuadro de diálogo para la IU clásica
   * reemplazando a `.jsp` (asígnele el nombre de su nuevo componente)
   * o retrabajando completamente todo el componente si lo desea

   Por ejemplo, si toma una copia del componente Texto estándar, puede agregar un campo adicional al cuadro de diálogo y, a continuación, actualizar el `.jsp` para procesar los datos introducidos allí.

   >[!NOTE]
   >
   >Un componente para:
   >
   >* IU táctil [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) componentes
   >* Uso de la IU clásica [Widgets de ExtJS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >Un cuadro de diálogo definido para la IU clásica funcionará dentro de la IU táctil.
   >
   >Un cuadro de diálogo definido para la IU táctil no funcionará dentro de la IU clásica.
   >
   >Según la instancia y el entorno de creación, es posible que desee definir ambos tipos de diálogo para el componente.

1. Uno de los siguientes nodos debe estar presente y adecuadamente inicializado para que aparezca el nuevo componente:

   * `cq:dialog` - cuadro de diálogo para la IU táctil
   * `dialog` - cuadro de diálogo para la IU clásica
   * `cq:editConfig` - cómo se comportan los componentes en el entorno de edición (por ejemplo, arrastrar y soltar)
   * `design_dialog` - cuadro de diálogo para el modo de diseño (solo IU clásica)

1. Active el nuevo componente en el sistema de párrafos mediante:

   * uso del CRXDE Lite para agregar el valor `<path-to-component>` (por ejemplo, `/apps/geometrixx/components/myComponent`) a los componentes de propiedad del nodo `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * siga las instrucciones indicadas en [Adición de nuevos componentes a sistemas de párrafos](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. En AEM WCM, abra una página de su sitio web e inserte un nuevo párrafo del tipo que acaba de crear para asegurarse de que el componente funciona correctamente.

>[!NOTE]
>
>Para ver las estadísticas de temporización de la carga de páginas, puede utilizar Ctrl-Mayús-U - con `?debugClientLibs=true` se establece en la dirección URL.

### Adición de un nuevo componente al sistema de párrafos (modo de diseño) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Una vez desarrollado el componente, lo agrega al sistema de párrafos, que permite a los autores seleccionar y utilizar el componente al editar una página.

1. Acceda a una página del entorno de creación que utilice el sistema de párrafos, por ejemplo `<contentPath>/Test.html`.
1. Cambie al modo Diseño mediante:

   * adición `?wcmmode=design` hasta el final de la dirección URL y volver a acceder, por ejemplo:

      `<contextPath>/ Test.html?wcmmode=design`

   * hacer clic en Diseño en la barra de tareas

   Ahora está en modo de diseño y puede editar el sistema de párrafos.

1. Haga clic en Editar.

   Se muestra una lista de los componentes pertenecientes al sistema de párrafos. El nuevo componente también aparece en la lista.

   Los componentes se pueden activar (o desactivar) para determinar cuáles se ofrecen al autor al editar una página.

1. Active el componente y, a continuación, vuelva al modo de edición normal para confirmar que está disponible para su uso.

### Ampliación del componente de texto e imagen: un ejemplo {#extending-the-text-and-image-component-an-example}

Esta sección proporciona un ejemplo sobre cómo ampliar el componente estándar de texto e imagen que se utiliza ampliamente con una función de colocación de imagen configurable.

La extensión del componente de texto e imagen permite a los editores utilizar toda la funcionalidad existente del componente, además de tener una opción adicional para especificar la colocación de la imagen:

* En el lado izquierdo del texto (comportamiento actual y el nuevo valor predeterminado)
* Así como en el lado derecho

Después de ampliar este componente, puede configurar la colocación de la imagen a través del cuadro de diálogo del componente.

En este ejercicio se describen las siguientes técnicas:

* Copia del nodo de componente existente y modificación de sus metadatos
* Modificación del cuadro de diálogo del componente, incluida la herencia de widgets de los cuadros de diálogo principales
* Modificación del script del componente para implementar la nueva funcionalidad

>[!NOTE]
>
>Este ejemplo está dirigido a la IU clásica.

>[!NOTE]
>
>Este ejemplo se basa en el contenido de muestra de Geometrixx, que ya no se envía con AEM, y que ha sido reemplazado por We.Retail. Consulte el documento [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

#### Ampliación del componente textimage existente {#extending-the-existing-textimage-component}

Para crear el nuevo componente, utilizamos el componente textimage estándar como base y lo modificamos. Almacenamos el nuevo componente en la aplicación de ejemplo AEM WCM de Geometrixx.

1. Copiar el componente de textimage estándar de `/libs/foundation/components/textimage` en la carpeta de componentes de Geometrixx, `/apps/geometrixx/components`, usando textimage como nombre de nodo de destino. (Copie el componente navegando hasta él, haciendo clic con el botón derecho y seleccionando Copiar y navegando hasta el directorio de destino).

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Para que este ejemplo sea sencillo, vaya al componente que ha copiado y elimine todos los subnodos del nuevo nodo de textimage, excepto los siguientes:

   * definición de cuadro de diálogo: `textimage/dialog`
   * script de componente: `textimage/textimage.jsp`
   * editar nodo de configuración (que permite arrastrar y soltar recursos): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >La definición del cuadro de diálogo depende de la IU:
   >
   >* IU táctil: `textimage/cq:dialog`
   >* IU clásica: `textimage/dialog`


1. Edite los metadatos del componente:

   * Nombre del componente

      * Establezca `jcr:description` a `Text Image Component (Extended)`
      * Establezca `jcr:title` a `Text Image (Extended)`
   * Grupo, donde el componente aparece en la barra de tareas (deje tal cual)

      * Leave `componentGroup` configure como `General`
   * Componente principal para el nuevo componente (el componente de textimage estándar)

      * Establezca `sling:resourceSuperType` a `foundation/components/textimage`

   Después de este paso, el nodo de componente tiene este aspecto:

   ![imagen_1-60](assets/chlimage_1-60a.png)

1. Cambie el `sling:resourceType` propiedad del nodo de configuración de edición de la imagen (propiedad: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) a `geometrixx/components/textimage.`

   De este modo, cuando se suelta una imagen en el componente de la página, la variable `sling:resourceType` la propiedad del componente de textimage extendido se establece en: `geometrixx/components/textimage.`

1. Modifique el cuadro de diálogo del componente para incluir la nueva opción. El nuevo componente hereda las partes del cuadro de diálogo que son iguales a las del original. La única adición que hacemos es ampliar el **Avanzadas** , agregar **Posición de la imagen** lista desplegable, con opciones **Left** y **Right**:

   * Deje el `textimage/dialog`propiedades sin modificar.

   Tenga en cuenta cómo `textimage/dialog/items` tiene cuatro subnodos, tab1 a tab4, que representan las cuatro pestañas del cuadro de diálogo textimage.

   * Para las dos primeras pestañas (pestaña 1 y pestaña 2):

      * Cambie xtype por cqinclude (para heredar del componente estándar).
      * Agregar una propiedad de ruta con valores `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`y `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`, respectivamente.
      * Elimine todas las demás propiedades o subnodos.
   * Para la pestaña 3:

      * Deje las propiedades y los subnodos sin cambios
      * Agregue una nueva definición de campo a `tab3/items`, posición del nodo del tipo `cq:Widget`
      * Establezca las siguientes propiedades (de tipo String) para la nueva `tab3/items/position`nodo:

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * Añadir subnodo `position/options` de tipo `cq:WidgetCollection` para representar las dos opciones de colocación de imagen y, en él, cree dos nodos, o1 y o2 de tipo `nt:unstructured`.
      * Para el nodo `position/options/o1` defina las propiedades: `text` a `Left` y `value` a `left.`
      * Para el nodo `position/options/o2` defina las propiedades: `text` a `Right` y `value` a `right`.
   * Eliminar ficha4.

   La posición de la imagen se mantiene en el contenido como el `imagePosition`propiedad del nodo que representa `textimage` párrafo. Después de estos pasos, el cuadro de diálogo del componente tiene este aspecto:

   ![climage_1-61](assets/chlimage_1-61a.png)

1. Amplíe el script de componente, `textimage.jsp`, con gestión adicional del nuevo parámetro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Vamos a reemplazar el fragmento de código enfatizado *%>&lt;div class=&quot;image&quot;>&lt;%* con el nuevo código que genera un estilo personalizado para esta etiqueta.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. Guarde el componente en el repositorio. El componente está listo para probarse.

#### Comprobación del nuevo componente {#checking-the-new-component}

Una vez desarrollado el componente, puede agregarlo al sistema de párrafos, que permite a los autores seleccionar y utilizar el componente al editar una página. Estos pasos le permiten probar el componente.

1. Abra una página en Geometrixx como Inglés/Empresa.
1. Cambie al modo de diseño haciendo clic en Diseño en la barra de tareas.
1. Edite el diseño del sistema de párrafos haciendo clic en Editar en el sistema de párrafos en medio de la página. Se muestra una lista de componentes, que se pueden colocar en el sistema de párrafos, y debe incluir su componente recién desarrollado, Imagen de texto (extendido) . Para activarlo en el sistema de párrafos, selecciónelo y haga clic en Aceptar .
1. Vuelva al modo de edición.
1. Agregue el párrafo Imagen de texto (extendido) al sistema de párrafos, inicialice el texto y la imagen con contenido de ejemplo. Guarde los cambios.
1. Abra el cuadro de diálogo del párrafo de texto y de imagen, cambie la Posición de la imagen en la ficha Avanzado a la derecha y haga clic en Aceptar para guardar los cambios.
1. El párrafo se representa con la imagen a la derecha.
1. El componente ya está listo para utilizarse.

El componente almacena su contenido en un párrafo en la página Empresa.

### Desactivar la capacidad de carga del componente de imagen {#disable-upload-capability-of-the-image-component}

Para deshabilitar esta capacidad, utilizamos el componente de imagen estándar como base y lo modificamos. Almacenamos el nuevo componente en la aplicación de ejemplo de Geometrixx.

1. Copiar el componente de imagen estándar de `/libs/foundation/components/image` en la carpeta de componentes de Geometrixx, `/apps/geometrixx/components`, usando image como nombre de nodo de destino.

   ![imagen_1-62](assets/chlimage_1-62a.png)

1. Edite los metadatos del componente:

   * Establezca **jcr:title** a `Image (Extended)`

1. Vaya a `/apps/geometrixx/components/image/dialog/items/image`.
1. Añadir una nueva propiedad:

   * **Nombre**: `allowUpload`
   * **Tipo**: `String`
   * **Valor**: `false`

   ![imagen_1-63](assets/chlimage_1-63a.png)

1. Haga clic en **Guardar todo**. El componente está listo para probarse.
1. Abra una página en Geometrixx como Inglés/Empresa.
1. Cambie al modo de diseño y active Image (Extended).
1. Vuelva al modo de edición y agréguelo al sistema de párrafos. En las siguientes imágenes, puede ver las diferencias entre el componente de imagen original y el que acaba de crear.

   Componente de imagen original:

   ![imagen_1-64](assets/chlimage_1-64a.png)

   El nuevo componente de imagen:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. El componente ya está listo para utilizarse.
