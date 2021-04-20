---
title: 'Variaciones: Crear contenido de fragmentos'
seo-title: 'Variaciones: Crear contenido de fragmentos'
description: Las variaciones le permiten crear contenido para el fragmento y, a continuación, crear variaciones de dicho contenido según el propósito (si es necesario).
seo-description: Las variaciones le permiten crear contenido para el fragmento y, a continuación, crear variaciones de dicho contenido según el propósito (si es necesario).
uuid: 0844f271-79bc-4f76-8031-d388b81d6feb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 324df1da-78fa-460f-a744-3504259f1d4a
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 16%

---


# Variaciones: Crear contenido de fragmentos{#variations-authoring-fragment-content}

[](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) Las variaciones son una característica importante de los fragmentos de contenido, ya que le permiten crear y editar copias del contenido principal para utilizarlas en canales o escenarios específicos.

Desde la pestaña **Variations** puede:

* [Introduzca el ](#authoring-your-content) contenido del fragmento
* [Crear y administrar ](#managing-variations) variaciones del  **** contenido principal

Realizar una serie de otras acciones en función del tipo de datos que se esté editando; por ejemplo:

* [Insertar recursos visuales en el fragmento](#inserting-assets-into-your-fragment)  (imágenes)
* Seleccione [Texto enriquecido](#rich-text), [Texto sin formato](#plain-text) y [Marcado](#markdown) para editar

* [Cargar contenido](#uploading-content)

* [Ver estadísticas clave](#viewing-key-statistics)  (acerca del texto multilínea)
* [Resumir texto](#summarizing-text)

* [Sincronizar variaciones con contenido principal](#synchronizing-with-master)

>[!CAUTION]
>
>Después de publicar un fragmento o de hacer referencia a él, AEM mostrará una advertencia cuando un autor abra el fragmento para editarlo de nuevo. Esto sirve para advertir que los cambios en el fragmento también afectarán a las páginas a las que se hace referencia.

## Creación de contenido {#authoring-your-content}

Cuando abra el fragmento de contenido para editarlo, la pestaña **Variaciones** se abrirá de forma predeterminada. Aquí puede crear el contenido, para Master o cualquier variación que tenga. Puede hacer lo siguiente:

* realice ediciones directamente en la pestaña **Variations**
* abra el [editor de pantalla completa](#full-screen-editor) para:

   * seleccione [Format](#formats)
   * consulte más opciones de edición (para el formato [Texto enriquecido](#rich-text))

   * acceder a un rango de [acciones](#actions)

Por ejemplo:

* Edición de un fragmento simple

   Un fragmento simple consta de un campo de texto multilínea (los recursos visuales se pueden agregar desde el editor de pantalla completa).

   ![cfm-6420-21](assets/cfm-6420-21.png)

* Edición de un fragmento con contenido estructurado

   Un fragmento estructurado contiene varios campos, de varios tipos de datos, que se definieron en el modelo de contenido. Para cualquier campo multilínea, está disponible el [editor de pantalla completa](#full-screen-editor).

   ![cfm-6420-16](assets/cfm-6420-16.png)

### Editor de pantalla completa {#full-screen-editor}

Al editar un campo de texto multilínea, puede abrir el editor de pantalla completa:

![cf-fullscreeneditor-icon](assets/cf-fullscreeneditor-icon.png)

El editor de pantalla completa proporciona:

* Acceso a varias [acciones](#actions)
* Según el [formato](#formats), opciones de formato adicionales ([Texto enriquecido](#rich-text))

### Acciones {#actions}

Las siguientes acciones también están disponibles (para todos los formatos [](#formats)) cuando el editor de pantalla completa (es decir, texto multilínea) está abierto:

* Seleccione el [formato](#formats) ([Texto enriquecido](#rich-text), [Texto sin formato,](#plain-text) [Marcado](#markdown))

* [Mostrar estadísticas de texto](#viewing-key-statistics)

* [Cargar contenido](#uploading-content)
* [Sincronizar con Principal](#synchronizing-with-master)  (al editar una variación)
* [Resumir texto](#summarizing-text)
* [](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) Anotar el texto

* [Insertar recursos visuales en el fragmento](#inserting-assets-into-your-fragment)  (imágenes)

### Formatos {#formats}

Las opciones para editar texto multilínea dependen del formato seleccionado:

* [Texto enriquecido](#rich-text)
* [Texto sin formato](#plain-text)
* [Markdown](#markdown)

El formato se puede seleccionar cuando se usa el editor de pantalla completa.

### Texto enriquecido {#rich-text}

La edición de texto enriquecido le permite dar formato:

* Negrita
* Cursiva
* Subrayado
* Alineación: izquierda, centro, derecha
* Lista con viñetas
* Lista numerada
* Sangría: aumentar, disminuir
* Crear/romper hipervínculos
* Abra el editor de pantalla completa, donde están disponibles las siguientes opciones de formato:

   * Pegar texto/desde Word
   * Insertar una tabla
   * Estilo de párrafo: Párrafo, Encabezado 1/2/3
   * [Insertar recursos visuales](#inserting-assets-into-your-fragment)
   * Búsqueda  
   * Buscar/Reemplazar
   * Corrector ortográfico
   * [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)

También se puede acceder a las [acciones](#actions) desde el editor de pantalla completa.

### Texto sin formato {#plain-text}

El texto sin formato permite introducir rápidamente el contenido sin aplicar formato ni marcar la información. También puede abrir el editor de pantalla completa para más [acciones](#actions).

>[!CAUTION]
>
>Si selecciona **Texto sin formato**, puede perder cualquier formato, marca o recurso que haya insertado en **Texto enriquecido** o **Marcado**.

### Markdown {#markdown}

>[!NOTE]
>
>Para obtener información completa, consulte la documentación de [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Esto le permite dar formato al texto mediante markdown. Puede definir:

* Encabezados
* Párrafos y saltos de línea
* Vínculos
* Imágenes
* Comillas de bloque
* Listas
* Énfasis
* Bloques de código
* La barra invertida se escapa

También puede abrir el editor de pantalla completa para más [acciones](#actions).

>[!CAUTION]
>
>Si cambia entre **Texto enriquecido** y **Marcado**, puede que se produzcan efectos inesperados con Comillas de bloque y Bloques de código, ya que estos dos formatos pueden tener diferencias en la forma en que se gestionan.

### Visualización de estadísticas clave {#viewing-key-statistics}

Cuando el editor de pantalla completa está abierto, la acción **Estadísticas de texto** mostrará un rango de información sobre el texto. Por ejemplo:

![cfx-6420-22](assets/cfx-6420-22.png)

### Cargar contenido {#uploading-content}

Para facilitar el proceso de creación de fragmentos de contenido, puede cargar texto, preparado en un editor externo y añadirlo directamente al fragmento.

### Resumen de texto {#summarizing-text}

El texto de resumen está diseñado para ayudar a los usuarios a reducir la longitud de su texto a un número predefinido de palabras, manteniendo al mismo tiempo los puntos clave y el significado general.

>[!NOTE]
>
>A un nivel más técnico, el sistema mantiene las frases que califica como que proporcionan la *mejor relación de densidad de información y singularidad* según algoritmos específicos.

>[!CAUTION]
>
>El fragmento de contenido debe tener una carpeta de idioma válida (código ISO) como antecesor; se utiliza para determinar el modelo de idioma que se va a utilizar.
>
>Por ejemplo, `en/` como en la siguiente ruta:
>
>`/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>El inglés está disponible de forma predeterminada.
>
>Otros idiomas están disponibles como Paquetes de modelo de idioma desde Distribución de software:
>
>* [Francés (fr) de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [Alemán (de) de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italiano (it) de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Español (es) de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)

>



1. Seleccione **Principal** o la variación requerida.
1. Abra el editor de pantalla completa.

1. Seleccione **Resumir texto** en la barra de herramientas.

   ![cf-17](assets/cf-17.png)

1. Especifique el número de palabras objetivo y seleccione **Inicio**:
1. El texto original se muestra en paralelo con el resumen propuesto:

   * Las oraciones que se eliminen se resaltan en rojo, con huelga.
   * Haga clic en cualquier oración resaltada para mantenerla en el contenido resumido.
   * Haga clic en cualquier oración no resaltada para eliminarla.

   ![cfm-6420-23](assets/cfm-6420-23.png)

1. Seleccione **Resumir** para confirmar los cambios.

### Anotación de un fragmento de contenido {#annotating-a-content-fragment}

Para realizar anotaciones en un fragmento:

1. Seleccione **Principal** o la variación requerida.
1. Abra el editor de pantalla completa.
1. Seleccione texto. El icono **Anotar** está disponible.

   ![cfm-6420-24](assets/cfm-6420-24.png)

1. Se abrirá un cuadro de diálogo: Aquí puede introducir la anotación.

1. Cierre el editor de pantalla completa y **Guarde** el fragmento.

### Visualización, edición y eliminación de anotaciones {#viewing-editing-deleting-annotations}

Anotaciones:

* Se indican mediante el resaltado en el texto, tanto en pantalla completa como en modo normal del editor. Los detalles completos de una anotación se pueden ver, editar y/o eliminar haciendo clic en el texto resaltado, que reabrirá el cuadro de diálogo.

   >[!NOTE]
   >
   >Se proporciona un selector desplegable si se han aplicado varias anotaciones a un texto.

* Cuando se elimina todo el texto al que se aplicó la anotación, también se elimina la anotación.

* Se puede enumerar y eliminar seleccionando la pestaña **Annotations** en el editor de fragmentos.

   ![cfm-6420-25](assets/cfm-6420-25.png)

* Se puede ver y eliminar en [Línea de tiempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) para el fragmento seleccionado.

### Inserción de recursos en el fragmento {#inserting-assets-into-your-fragment}

Para facilitar el proceso de creación de fragmentos de contenido, puede añadir [Assets](/help/assets/manage-assets.md) (imágenes) directamente al fragmento.

Se añadirán a la secuencia de párrafo del fragmento sin ningún formato; el formato se puede realizar cuando se utiliza o se hace referencia al fragmento [en una página](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
>
>Estos recursos no se pueden mover ni eliminar en una página de referencia; esto debe hacerse en el editor de fragmentos.
>
>Sin embargo, el formato del recurso (p. ej., el tamaño) debe realizarse en el [editor de páginas](/help/sites-authoring/content-fragments.md). La representación del recurso en el editor de fragmentos se realiza exclusivamente para crear el flujo de contenido.

>[!NOTE]
>
>Existen varios métodos para agregar [imágenes](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

1. Coloque el cursor en la posición en la que desee agregar la imagen.
1. Utilice el icono **Insertar recurso** para abrir el cuadro de diálogo de búsqueda.

   ![cf-insertasset-icon](assets/cf-insertasset-icon.png)

1. En el cuadro de diálogo puede:

   * vaya al recurso necesario en DAM
   * buscar el recurso en DAM

   Una vez localizado, seleccione el recurso necesario haciendo clic en la miniatura.

1. Utilice **Seleccionar** para agregar el recurso al sistema de párrafos del fragmento de contenido en la ubicación actual.

   >[!CAUTION]
   >
   >Si, después de agregar un recurso, cambia el formato a:
   >
   >* **Texto sin formato**: El recurso se perderá completamente del fragmento.
   >* **Marcado**: El recurso no estará visible, pero permanecerá allí cuando vuelva a **Texto enriquecido**.


## Administración de variaciones {#managing-variations}

### Creación de una variación {#creating-a-variation}

Las variaciones permiten tomar el contenido **Principal** y variarlo según el propósito (si es necesario).

Para crear una nueva variación:

1. Abra el fragmento y asegúrese de que el panel lateral esté visible.
1. Seleccione **Variaciones** en la barra de iconos del panel lateral.
1. Seleccione **Crear variación**.
1. Se abrirá un cuadro de diálogo, especifique el **Título** y la **Descripción** de la nueva variación.
1. Seleccione **Agregar**; el fragmento **principal** se copiará en la nueva variación, que ahora estará abierta para [edición](#editing-a-variation).

   >[!NOTE]
   >
   >Al crear una variación nueva, siempre es **Principal** la que se copia, no la que está abierta actualmente.

### Edición de una variación {#editing-a-variation}

Puede realizar cambios en el contenido de la variación después de:

* [Creación de la variación](#creating-a-variation).
* Abra un fragmento existente y, a continuación, seleccione la variación necesaria en el panel lateral.

![cfm-6420-26](assets/cfm-6420-26.png)

### Cambio del nombre de una variación {#renaming-a-variation}

Para cambiar el nombre de una variación existente:

1. Abra el fragmento y seleccione **Variaciones** en el panel lateral.
1. Seleccione la variación requerida.
1. Seleccione **Cambiar nombre** en la lista desplegable **Actions**.

1. Introduzca el nuevo **Título** o **Descripción** en el cuadro de diálogo resultante.

1. Confirme la acción **Cambiar nombre**.

>[!NOTE]
>
>Esto solo afecta a la variación **Title**.

### Eliminación de una variación {#deleting-a-variation}

Para eliminar una variación existente:

1. Abra el fragmento y seleccione **Variaciones** en el panel lateral.
1. Seleccione la variación requerida.
1. Seleccione **Delete** en la lista desplegable **Actions**.

1. Confirme la acción **Delete** en el cuadro de diálogo.

>[!NOTE]
>
>No puede eliminar **Principal**.

### Sincronización con Master {#synchronizing-with-master}

**** Masteris es una parte integral de un fragmento de contenido y por definición contiene la copia maestra del contenido, mientras que las variaciones contienen las versiones individuales actualizadas y adaptadas de ese contenido. Cuando Master se actualiza, es posible que estos cambios también sean relevantes para las variaciones y, por lo tanto, deban propagarse a ellas.

Al editar una variación, tiene acceso a la acción para sincronizar el elemento actual de la variación con Master. Esto le permite copiar automáticamente los cambios realizados en Principal en la variación requerida.

>[!CAUTION]
>
>La sincronización solo está disponible para copiar cambios *de **Principal**a la variación*.
>
>Solo se sincronizará el elemento actual de la variación.
>
>La sincronización solo funciona en el tipo de datos de **texto de varias líneas**.
>
>No está disponible como opción la transferencia de cambios *de una variación **a Principal***.

1. Abra el fragmento de contenido en el editor de fragmentos. Asegúrese de que **Master** se ha editado.
1. Seleccione una variación específica y, a continuación, la acción de sincronización adecuada desde:

   * el selector desplegable **Actions**: **Sincronizar el elemento actual con el maestro**

   * la barra de herramientas del editor de pantalla completa - **Sincronizar con master**

1. Master y la variación se mostrarán en paralelo:

   * verde indica el contenido añadido (a la variación)
   * rojo indica que el contenido se ha eliminado (de la variación)

   ![cfm-6420-27](assets/cfm-6420-27.png)

1. Seleccione **Sincronizar**, la variación se actualizará y se mostrará.

