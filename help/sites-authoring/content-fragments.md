---
title: Creación de páginas de contenido con fragmentos de contenido
description: AEM fragmentos de contenido le permiten diseñar, crear, depurar y usar contenido independiente de las páginas.
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
exl-id: d5dad844-80ca-4ace-a082-38d892d9ffe2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 55%

---

# Creación de páginas con fragmentos de contenido{#page-authoring-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) se [crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md).

Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido.

Junto con el exportador JSON actualizado, los fragmentos de contenido estructurados también se pueden utilizar para distribuir contenidos de AEM mediante servicios de contenido a canales en lugar de páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-authoring/experience-fragments.md)** son funciones distintas de AEM:
>
>* **Fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Son contenido puro, sin diseño ni diseño.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web. 
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.

>[!CAUTION]
>
>Esta página se debe leer junto con [Trabajo con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) (y las páginas relacionadas), ya que introduce terminología y conceptos básicos, además de tratar la creación y gestión de fragmentos.

Los fragmentos de contenido permiten:

* **Estrategia de campañas y marketing**

   * Revise el contenido a través de fragmentos de contenido administrados centralmente.

* **Creative Pro**

   * Seguimiento de recursos creativos mediante colecciones asociadas con fragmentos de contenido.

* **Copiar escritores**

   * Escriba en el editor de fragmentos de contenido de AEM.
   * Pueden crear variaciones de contenido.
   * Puede asociar contenido relevante con el fragmento de contenido.
   * Puede utilizar el control de versiones/flujo de trabajo.
   * Pueden compartir fragmentos de contenido.
   * Puede administrar traducciones de forma centralizada.

* **Productores y gestores de Recorridos**

   * Seleccione fragmentos y variaciones predefinidos con la creación en AEM.
   * Pueden confiar en fragmentos y contenido asociado siempre estando actualizado a medida que creadores y redactores realizan sus actualizaciones en recursos y fragmentos administrados centralmente.
   * Pueden depender del contenido multimedia asociado seleccionado para su relevancia.
   * Puede crear variaciones de contenido ad-hoc sobre la marcha, asegurándose de que dichas variaciones permanezcan administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página       {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla. 

1. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**. 

1. Puede:

   * Abra el navegador **Recursos** y filtre por **Fragmentos de contenido** (el valor predeterminado es Imágenes). A continuación, arrastre el fragmento requerido a la instancia del componente.

   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.
   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto creará automáticamente el componente asociado (fragmento de contenido). 

1. En un primer momento se muestra el contenido del elemento **Principal** y **Maestro** (variación). Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Para obtener más información sobre las funciones de edición adicionales, consulte también:
   >
   >
   >
   >    * [Diseño adaptable](/help/sites-authoring/responsive-layout.md)
   >    * [Edición del contenido de una página](/help/sites-authoring/editing-content.md)


### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el **Configuración** para configurar el fragmento que se utilizará en la página actual. El cuadro de diálogo puede depender del componente utilizado.

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, incluidos:

* **Fragmento de contenido**

   Especifique el fragmento que se va a utilizar.

* **Modo de visualización**:

   * **Elemento de texto único**

   * **Elemento múltiple**

* **Elemento**

   * El valor predeterminado **Principal** siempre estará disponible.
   * Una selección estará disponible si el fragmento se creó con una plantilla adecuada.

   >[!NOTE]
   >
   >Los elementos disponibles dependen de la plantilla utilizada.

* **Variación**

   * **Principal** siempre aparecerá como la opción predeterminada.
   * Habrá una selección disponible si se crearon variaciones para el fragmento.

* **Párrafos**: especifique el rango de párrafos que desea incluir:

   * **Todos**
   * **Rango**: por ejemplo, `1`, `3-5` o `9-*`

      * **Gestionar encabezados como sus propios párrafos**

* **Gestionar encabezados como sus propios párrafos**

### Conexión rápida con el editor de fragmentos  {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permitirá [editar y gestionar el fragmento de contenido](/help/assets/content-fragments/content-fragments.md). 

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento afectará a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Añadir contenido intermedio       {#adding-in-between-content}

Cuando se agrega un fragmento de contenido específico a la página, aparece una variable **Arrastre los componentes aquí** marcador de posición entre cada párrafo de HTML (y en la parte superior/inferior) del fragmento.

Esto le permite añadir contenido adicional [intermedio (es decir, entre contenido)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) el contenido del fragmento (en cualquiera de los puntos disponibles), sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede:

* Añadir componentes desde el [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
* Agregue recursos desde [Navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Utilizar [contenido asociado](#using-associated-content) como fuente para el contenido intermedio.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo precedente.

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, incluso cuando cambia el contenido de los párrafos del fragmento.
>
>  Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).
>


### Uso de contenido asociado       {#using-associated-content}

Si tiene [contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) con el [fragmento de contenido](/help/assets/content-fragments/content-fragments.md), estos recursos estarán disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). El contenido asociado es en realidad una fuente especial de contenido para [contenido intermedio](#adding-in-between-content).

>[!NOTE]
>
>Hay varios métodos para agregar [recursos visuales (p. ej., imágenes)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la variable **Contenido asociado** muestra los recursos adecuados para todos los fragmentos.

Una vez que haya añadido un fragmento con contenido asociado a la página, agregue una nueva pestaña (**Contenido asociado**) se abre en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (en un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![cfm-6420-03](assets/cfm-6420-03.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

Si se insertan recursos (p. ej. imágenes) en el propio fragmento, las opciones para editarlos en el editor de páginas son limitadas. <!-- Removed link as it was a 404 on helpx -->

Por ejemplo, para una imagen puede

* Recortar, rotar o voltear la imagen.
* Añada un título o texto alternativo.
* Especifique un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben realizarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para poder usarse en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Recursos](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar en ese momento el fragmento.
