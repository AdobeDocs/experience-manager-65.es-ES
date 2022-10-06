---
title: Estructura de la interfaz de usuario táctil AEM
seo-title: Structure of the AEM Touch-Enabled UI
description: La IU táctil, tal como se ha implementado en AEM, tiene varios principios subyacentes y está formada por varios elementos clave
seo-description: The touch-optimized UI, as implemented in AEM, has several underlying principles and is made up of several key elements
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# Estructura de la interfaz de usuario táctil AEM{#structure-of-the-aem-touch-enabled-ui}

La AEM IU táctil tiene varios principios subyacentes y se compone de varios elementos clave:

## Consolas {#consoles}

### Diseño básico y cambio de tamaño {#basic-layout-and-resizing}

La IU se ocupa de los dispositivos móviles y de escritorio, pero en lugar de crear un Adobe de dos estilos, ha decidido utilizar un estilo que funcione para todas las pantallas y todos los dispositivos.

Todos los módulos utilizan el mismo diseño básico, en AEM esto puede verse como:

![chlimage_1-142](assets/chlimage_1-142.png)

El diseño se adhiere a un estilo de diseño interactivo y se adapta al tamaño del dispositivo o ventana que esté utilizando.

Por ejemplo, cuando la resolución es inferior a 1024 píxeles (como en un dispositivo móvil), la pantalla se ajustará en consecuencia:

![chlimage_1-143](assets/chlimage_1-143.png)

### Barra de encabezado {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

La barra de encabezado muestra elementos globales como:

* el logotipo y el producto o solución específicos que está utilizando en la actualidad; para AEM esto también forma un vínculo a Navegación global
* Búsqueda
* icono para acceder a los recursos de ayuda
* icono para acceder a otras soluciones
* un indicador de (y acceso a) alertas o elementos de la bandeja de entrada que le estén esperando
* el icono de usuario, junto con un vínculo a la administración de perfiles

### Barra de herramientas {#toolbar}

Esto es contextual para la ubicación y las herramientas de superficie relevantes para controlar la vista o los recursos en la página siguiente. La barra de herramientas es específica del producto, pero los elementos son comunes.

En cualquier ubicación, la barra de herramientas muestra las acciones disponibles actualmente:

![chlimage_1-145](assets/chlimage_1-145.png)

También depende de si un recurso está seleccionado actualmente:

![chlimage_1-146](assets/chlimage_1-146.png)

### Carril izquierdo {#left-rail}

El carril izquierdo se puede abrir u ocultar según sea necesario para mostrar:

* **Escala de cronología**
* **Referencias**
* **Filtro**

El valor predeterminado es **Solo contenido** (carril oculto).

![chlimage_1-147](assets/chlimage_1-147.png)

## Creación de páginas {#page-authoring}

Al crear páginas, las áreas estructurales son las siguientes:

### Marco de contenido {#content-frame}

El contenido de la página se representa en el marco de contenido. El marco de contenido es completamente independiente del editor para garantizar que no haya conflictos debido a CSS o javascript.

El marco de contenido se encuentra en la sección derecha de la ventana, debajo de la barra de herramientas.

![chlimage_1-148](assets/chlimage_1-148.png)

### Marco del editor {#editor-frame}

El marco del editor obtiene las funciones de edición.

El marco del editor es un contenedor (abstracto) para todos los *elementos de creación de páginas*. Se encuentra sobre el marco de contenido e incluye:

* la barra de herramientas superior
* el panel lateral
* todas las superposiciones
* cualquier otro elemento de creación de páginas; por ejemplo, la barra de herramientas de componentes

![chlimage_1-149](assets/chlimage_1-149.png)

### Panel lateral {#side-panel}

Contiene dos pestañas predeterminadas que le permiten seleccionar recursos y componentes; se pueden arrastrar desde aquí y soltar en la página.

El panel lateral está oculto de forma predeterminada. Cuando se selecciona, se muestra en el lado izquierdo o se desliza para cubrir toda la ventana (cuando el tamaño de la ventana es inferior a una anchura de 1024 píxeles; como, por ejemplo, en un dispositivo móvil).

![chlimage_1-150](assets/chlimage_1-150.png)

### Panel lateral: recursos {#side-panel-assets}

En la pestaña Recursos , puede seleccionar entre el rango de recursos. También puede filtrar por un término específico o seleccionar un grupo.

![chlimage_1-151](assets/chlimage_1-151.png)

### Panel lateral: Grupos de recursos {#side-panel-asset-groups}

En la ficha Recurso hay una lista desplegable que puede utilizar para seleccionar los grupos de recursos específicos.

![chlimage_1-152](assets/chlimage_1-152.png)

### Panel lateral: componentes {#side-panel-components}

En la pestaña Componentes , puede seleccionar entre el rango de componentes. También puede filtrar por un término específico o seleccionar un grupo.

![chlimage_1-153](assets/chlimage_1-153.png)

### Superposiciones {#overlays}

Estas superposiciones superponen el marco de contenido y las usa el [capas](#layer) para realizar los mecanismos de interacción (completamente transparente) con los componentes y su contenido.

Las superposiciones se encuentran en el marco del editor (con todos los demás elementos de creación de páginas), aunque en realidad superponen los componentes adecuados en el marco de contenido.

![chlimage_1-154](assets/chlimage_1-154.png)

### Capa {#layer}

Una capa es un paquete de funcionalidad independiente que puede activarse para:

* proporcionar una vista diferente de la página
* le permiten manipular una página o interactuar con ella

Las capas proporcionan una funcionalidad sofisticada para toda la página, a diferencia de acciones específicas en un componente individual.

AEM incluye varias capas ya implementadas para la creación de páginas; incluyendo, por ejemplo, editar, previsualizar, anotar.

>[!NOTE]
>
>Las capas son un concepto potente que afecta a la vista del usuario y a la interacción con el contenido de la página. Al desarrollar sus propias capas, debe asegurarse de que la capa se limpia cuando se sale.

### Conmutador de capas {#layer-switcher}

El selector de capas le permite elegir la capa que desea utilizar. Cuando está cerrada, indica la capa que se está utilizando.

El selector de capas está disponible como una lista desplegable de la barra de herramientas (en la parte superior de la ventana, dentro del marco del editor).

![chlimage_1-155](assets/chlimage_1-155.png)

### Barra de herramientas del componente {#component-toolbar}

Cada instancia de un componente muestra su barra de herramientas cuando se hace clic (una vez o con un doble clic lento). La barra de herramientas contiene las acciones específicas (por ejemplo, copiar, pegar, abrir-editor) que están disponibles para la instancia de componente (editable) en la página.

Según el espacio disponible, las barras de herramientas de componentes se colocan en la esquina superior derecha o inferior del componente correspondiente.

![chlimage_1-156](assets/chlimage_1-156.png)

## Información adicional {#further-information}

Para obtener más información sobre los conceptos relacionados con la IU táctil, continúe con el artículo [Conceptos de la IU táctil AEM](/help/sites-developing/touch-ui-concepts.md).

Para obtener más información técnica, consulte [Conjunto de documentación de JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para el editor de páginas con capacidad táctil.
