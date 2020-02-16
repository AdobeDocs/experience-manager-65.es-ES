---
title: Creación de páginas con fragmentos de contenido
seo-title: Creación de páginas con fragmentos de contenido
description: Los fragmentos de contenido de AEM permiten diseñar, crear, mantener y utilizar contenido independiente de cualquier página
seo-description: Los fragmentos de contenido de AEM permiten diseñar, crear, mantener y utilizar contenido independiente de cualquier página
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# Creación de páginas con fragmentos de contenido{#page-authoring-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM)[ se crean y administran como recursos independientes de las páginas](/help/assets/content-fragments.md).

Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido.

Junto con el exportador JSON actualizado, los fragmentos de contenido estructurados también se pueden utilizar para distribuir contenidos de AEM mediante servicios de contenido a canales en lugar de páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencia](/help/sites-authoring/experience-fragments.md)**son funciones distintas de AEM:
>
>* Los **fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Se trata de contenido puro, sin diseño ni maquetación.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 
>
>
Los fragmentos de experiencia pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.

>[!CAUTION]
>
>This page must be read in conjunction with [Working with Content Fragments](/help/assets/content-fragments.md) (and related pages) as it introduces basic terminology and concepts, together with creating and managing fragments.

Los fragmentos de contenido permiten hacer lo siguiente:

* **Estrategia de campañas y mercadotecnia** 

   * Revisar contenido mediante fragmentos de contenido administrados centralmente.

* **Profesionales creativos** 

   * Hacer seguimientos de los recursos creativos a través de las colecciones asociadas con los fragmentos de contenido.

* **Redactores** 

   * Escriba en el editor de fragmentos de contenido de AEM.
   * Pueden crear variaciones de contenido.
   * Pueden asociar contenido relevante con el fragmento de contenido.
   * Pueden usar distintas versiones/flujos de trabajo.
   * Pueden compartir fragmentos de contenido.
   * Pueden administrar traducciones de forma centralizada.

* **Productores y gestores de trayectorias de clientes** 

   * Seleccionar fragmentos y variaciones predefinidos con la función de creación en AEM.
   * Pueden utilizar fragmentos y contenidos asociados y estar siempre al día a medida que creadores y redactores apliquen actualizaciones en recursos y fragmentos administrados centralmente.
   * Pueden utilizar contenido multimedia asociado seleccionado según relevancia.
   * Pueden crear variaciones de contenido ad hoc al instante garantizando al mismo tiempo que las variaciones siguen administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla. 

1. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**. 

1. Puede:

   * Open the **Assets** browser and filter for **Content Fragments** (the default is Images). Arrastre el fragmento en cuestión a la instancia de componente.

   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.
   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto creará automáticamente el componente asociado (fragmento de contenido). 

1. Initially the content from the **Main** Element and **Master** (variation) will be shown. Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Para obtener más información sobre otras funciones de edición, consulte también:
   >
   >
   >
   >    * [Diseño adaptable](/help/sites-authoring/responsive-layout.md)
   >    * [Editar el contenido de una página](/help/sites-authoring/editing-content.md)


### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el cuadro de diálogo **Configuración** del fragmento para configurar el fragmento que se va a utilizar en la página actual. El cuadro de diálogo puede depender del componente utilizado.

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, entre los que se incluyen:

* **Fragmento de contenido**

   Especifique el fragmento que se va a utilizar.

* **Modo de visualización**:

   * **Elemento de texto único**

   * **Elemento múltiple**

* **Elemento**

   * El valor predeterminado **Principal** siempre aparecerá disponible.
   * Se podrá hacer una selección si el fragmento se creó con una plantilla adecuada.
   >[!NOTE]
   >
   >Los elementos disponibles dependen de la plantilla utilizada.

* **Variación**

   * Siempre aparecerá disponible la opción predeterminada **Principal**.
   * Podrá realizar una selección si se crearon variaciones para el fragmento.

* **Párrafos**: especifique el rango de párrafos que incluir:

   * **Todos**
   * **Intervalo**: por ejemplo, `1`, `3-5`, `9-*`

      * **Gestionar encabezados como sus propios párrafos**

* **Gestionar encabezados como sus propios párrafos**

### Conexión rápida con el editor de fragmentos {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permitirá [editar y gestionar el fragmento de contenido](/help/assets/content-fragments.md). 

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento afectará a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Agregar contenido intermedio {#adding-in-between-content}

Cuando se añade a la página un fragmento de contenido específico, se dispone de un marcador de posición **Arrastre los componentes aquí** entre cada párrafo HTML (y en la parte superior/inferior) del fragmento.

De este modo puede añadir contenido adicional [entre](/help/assets/content-fragments.md#inbetweencontent) (es decir, entre el contenido) el contenido del fragmento (en cualquiera de los puntos disponibles) sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede:

* Agregar componentes desde el [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
* Agregar recursos desde el [navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Use [Associated Content](#using-associated-content) as a source for in-between content.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo precedente.

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, aunque varíe el contenido de los párrafos del fragmento.
   >  Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).
>



### Uso de contenido asociado {#using-associated-content}

Si tiene [contenido asociado](/help/assets/content-fragments-assoc-content.md) al [fragmento de contenido](/help/assets/content-fragments.md), estos recursos estarán disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). El contenido asociado actúa como fuente especial de contenido para el [contenido intermedio](#adding-in-between-content).

>[!NOTE]
>
>Hay varios métodos para agregar [recursos visuales (p. ej., imágenes)](/help/assets/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la pestaña **Contenido asociado** mostrará los recursos oportunos para todos los fragmentos.

Una vez que haya añadido un fragmento con contenido asociado a la página, se abrirá una nueva pestaña (**Contenido asociado**) en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (en un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![cfm-6420-03](assets/cfm-6420-03.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

Si se insertan recursos (p. ej. imágenes) en el propio fragmento, las opciones para editarlos en el editor de páginas son limitadas. <!-- Removed link as it was a 404 on helpx -->

Por ejemplo, para una imagen puede

* Recortar, girar o voltear la imagen.
* Añadir un título o texto alternativo.
* Especificar un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben realizarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para poder usarse en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Recursos](/help/assets/content-fragments.md#publishingandreferencingafragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar en ese momento el fragmento.

