---
title: Trabajar con fragmentos de contenido
seo-title: Trabajar con fragmentos de contenido
description: Descubra cómo los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas.
seo-description: Descubra cómo los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas.
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 7%

---


# Trabajar con fragmentos de contenido{#working-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) le permiten diseñar, crear, depurar y [publicar contenido independiente de las páginas](/help/sites-authoring/content-fragments.md). Permiten preparar contenido listo para usar en varias ubicaciones o en varios canales.

Los fragmentos de contenido también se pueden entregar en formato JSON, utilizando las capacidades de exportación del Modelo Sling (JSON) de AEM componentes principales. Esta forma de envío:

* permite utilizar el componente para administrar qué elementos de un fragmento enviar
* permite la entrega masiva, añadiendo varios componentes principales de fragmento de contenido en la página que se utiliza para la entrega de API

Esta y las siguientes páginas tratan sobre las tareas para crear, configurar y mantener sus fragmentos de contenido:

* [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) : cree sus fragmentos de contenido. a continuación, edite, publique y haga referencia a
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) : activar, crear y definir sus modelos
* [Variaciones - Creación de contenido de fragmento](/help/assets/content-fragments/content-fragments-variations.md) : cree el contenido del fragmento y cree variaciones del contenido principal.
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) : uso de la sintaxis Markdown para el fragmento
* [Uso de contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) : adición de contenido asociado
* [Metadatos: Propiedades del fragmento](/help/assets/content-fragments/content-fragments-metadata.md) : visualización y edición de las propiedades del fragmento

>[!NOTE]
>
>Estas páginas deben leerse junto con [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md).

El número de canales de comunicación aumenta anualmente. Normalmente, los canales hacen referencia al mecanismo de envío, ya sea como:

* Canal físico; p. ej., escritorio o móvil.
* Forma de entrega en un canal físico; Por ejemplo, la &quot;página de detalles del producto&quot;, la &quot;página de categoría del producto&quot; para escritorio o la &quot;web móvil&quot;, la &quot;aplicación móvil&quot; para móvil.

Sin embargo, usted (probablemente) no desea utilizar exactamente el mismo contenido para todos los canales, necesita optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Piense en cómo llegar a las audiencias de destino de forma eficaz en todos los canales.
* Cree y administre contenido editorial neutro para el canal.
* Cree grupos de contenido para una amplia gama de canales.
* Diseñe variaciones de contenido para canales específicos.
* Añada imágenes al texto insertando recursos (fragmentos de medios mixtos).

Estos fragmentos de contenido se pueden ensamblar para ofrecer experiencias en una variedad de canales.

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío de contenido desde o hacia AEM más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

La entrega se realiza en formato JSON.

AEM fragmentos de contenido se pueden usar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener una variedad de tipos de contenido; incluido texto, datos numéricos, booleano, fecha y hora, etc.

Junto con las capacidades de exportación de JSON de AEM componentes principales, este contenido estructurado se puede utilizar para entregar contenido AEM a canales que no sean páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-authoring/experience-fragments.md)** son funciones distintas de AEM:
>* Los **fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Se trata de contenido puro, sin diseño ni maquetación.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 

>
>
Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.
>
>Para obtener más información, consulte también [Explicación de los fragmentos de contenido y los fragmentos de experiencia en AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html).

>[!CAUTION]
>
>Los fragmentos de contenido no están disponibles en la IU clásica.
>
>El componente Fragmento de contenido se puede ver en la barra de tareas de la IU clásica, pero no hay más funciones disponibles.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento. Consulte [Creación de proyectos de traducción para fragmentos de contenido](/help/assets/creating-translation-projects-for-content-fragments.md) para obtener más información.

## Tipos de fragmento de contenido {#types-of-content-fragment}

Los fragmentos de contenido pueden ser:

* Fragmentos simples
No tienen estructura predefinida. Solo contienen texto e imágenes.
Se basan en la plantilla Fragmento simple .

* Fragmentos que contienen contenido estructurado
Se basan en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md), que predefine una estructura para el fragmento resultante.
También se pueden usar para realizar servicios de contenido usando el exportador JSON.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son:

* Almacenados como **Assets**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la consola **Assets**.
   * Se ha creado y editado en el Editor de fragmentos de contenido.

* Se utiliza en el editor de páginas [mediante el componente Fragmento de contenido](/help/sites-authoring/content-fragments.md) (componente de referencia):

   * El componente **Fragmento de contenido** está disponible para los autores de páginas. Les permite hacer referencia y enviar el fragmento de contenido requerido en formato HTML o JSON.

Los fragmentos de contenido son una estructura de contenido que:

* No tienen diseño o diseño (es posible aplicar formato de texto en el modo Texto enriquecido).
* Contienen una o más [partes constituyentes](#constituent-parts-of-a-content-fragment).
* Puede [contener o estar conectado a imágenes](#fragments-with-visual-assets).
* Puede utilizar [contenido intermedio](#in-between-content-when-page-authoring-with-content-fragments) cuando se haga referencia a él en una página.

* Son independientes del mecanismo de envío (es decir, página, canal).

### Fragmentos con activos visuales {#fragments-with-visual-assets}

Para que los autores tengan un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Los recursos se pueden utilizar con un fragmento de contenido de varias formas; cada uno con sus propias ventajas:

* **Insertar** recurso en un fragmento (fragmentos de medios mixtos)

   * Son una parte integral del fragmento (consulte [Componentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Defina la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) en el Editor de fragmentos para obtener más información.

   >[!NOTE]
   >
   >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se añade el fragmento a una página, estos recursos se mueven en relación con ese párrafo cuando se añade contenido intermedio.

* **Contenido asociado**

   * están conectadas a un fragmento; pero no una parte fija del fragmento (consulte [Componentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Permite cierta flexibilidad de posicionamiento.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte [Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el **explorador de Assets** del editor de páginas

   * Permitir flexibilidad total para la selección de un recurso.
   * Permite cierta flexibilidad de posicionamiento.
   * No proporciona el concepto de ser aprobado para un fragmento específico.
   * Consulte [Navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser) para obtener más información.

### Componentes de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que contienen contenido.
   * Para fragmentos con contenido estructurado, se utiliza un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de varios tipos de datos.
   * Para fragmentos simples:

      * El contenido se incluye en uno o más campos de texto multilínea o en elementos.
      * Los elementos se definen en la plantilla de fragmento (no se puede definir al crear el fragmento, consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)).

* **Párrafos de fragmento**

   * Bloques de texto, que son:

      * separado por espacios verticales (retorno de carro)
      * en elementos de texto multilínea; en fragmentos simples o estructurados
   * En los modos [Texto enriquecido](/help/assets/content-fragments/content-fragments-variations.md#rich-text) y [Marcado](/help/assets/content-fragments/content-fragments-variations.md#markdown), un párrafo se puede formatear como un encabezado, en cuyo caso, ese párrafo y el siguiente se unirán como una sola unidad.

   * Habilite el control de contenido durante la creación de páginas.


* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y utilizados como contenido interno de un fragmento.
   * Están incrustadas en el sistema de párrafos del fragmento.
   * Se puede dar formato cuando se utiliza o se hace referencia al fragmento [en una página](/help/sites-authoring/content-fragments.md).
   * Solo se puede agregar, eliminar o mover dentro de un fragmento con el editor de fragmentos. Estas acciones no se pueden realizar en el editor de páginas.
   * Solo se puede agregar, eliminar o mover dentro de un fragmento utilizando el formato [Texto enriquecido en el editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Solo se puede añadir a elementos de texto multilínea (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).

   >[!CAUTION]
   >
   >Se puede eliminar (sin querer) de un fragmento cambiando al formato de texto sin formato.

   >[!NOTE]
   >
   >Los recursos también se pueden añadir como [contenido adicional (intermedio)](/help/sites-authoring/content-fragments.md#using-associated-content) al utilizar un fragmento en una página; usar contenido asociado o recursos del navegador Recursos.

* **Contenido asociado**

   * Es contenido externo a un fragmento, pero con relevancia editorial para él. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para su uso con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos están [asociados a fragmentos mediante colecciones](/help/assets/content-fragments/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos utilizar cuando esté creando la página.

      * Las colecciones se pueden asociar a fragmentos a través de plantillas, como contenido predeterminado o por medio de autores durante la creación de fragmentos.
      * [Las ](/help/assets/manage-collections.md) colecciones de recursos (DAM) son la base del contenido asociado de los fragmentos.
   * De forma opcional, también puede agregar el fragmento a una colección para ayudar en el seguimiento.


* **Metadatos de fragmento**

   * Utilice los [Esquemas de metadatos de recursos](/help/assets/metadata.md).
   * Las etiquetas se pueden crear cuando:

      * Creación y creación del fragmento
      * O posterior:

         * Visualización/edición del fragmento **Properties** desde la consola
         * Editando los **Metadatos** en el editor de fragmentos

   >[!CAUTION]
   >
   >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Una parte integral del fragmento

      * Cada fragmento de contenido tiene una instancia de Maestro.
      * El patrón no se puede eliminar.
   * Se puede acceder a Master en el editor de fragmentos en **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master no es una variación como tal, sino la base de todas las variaciones.


* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; puede estar relacionado con el canal, pero no es obligatorio, también puede ser para modificaciones locales específicas.
   * Se crean como copias de **Master**, pero luego se pueden editar según sea necesario; normalmente, el contenido se superpone entre las propias variaciones.
   * Se puede definir durante la creación de fragmentos o predefinirse en plantillas de fragmento.
   * Almacenadas en el fragmento para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master si se ha actualizado el contenido principal.
   * Puede ser [Resumida](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponible en la pestaña [Variations](/help/assets/content-fragments/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el [Editor de páginas al trabajar con fragmentos de contenido](/help/sites-authoring/content-fragments.md).
* Es [contenido adicional añadido dentro del flujo de un fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o al que se hace referencia en una página.
* El contenido intermedio se puede añadir a cualquier fragmento, donde solo hay un elemento visible.
* Se puede utilizar contenido asociado, así como recursos o componentes del navegador adecuado.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear, editar y utilizar fragmentos de contenido también necesita:

* **Modelo de contenido**

   * [están activados y luego se crean mediante Herramientas](/help/assets/content-fragments/content-fragments-models.md).
   * Necesario para [crear un fragmento estructurado](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones de los modelos de contenido requieren un título y un elemento de datos; todo lo demás es opcional. El modelo define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.

* **Plantilla de fragmento**

   * Necesario para [crear un fragmento simple](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Generalmente [se desarrolla durante la implementación del proyecto](/help/sites-developing/content-fragment-templates.md); no se puede crear durante la creación.
   * Define las propiedades básicas de un fragmento simple (título, número de elementos de texto, definiciones de etiquetas).
   * Las definiciones de plantilla requieren un título y un elemento de texto; todo lo demás es opcional. La plantilla define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Posteriormente, los autores pueden ampliar un fragmento más allá de lo definido en la plantilla.

* **Componente de fragmento de contenido**

   * Instrumental para enviar el fragmento en formato HTML o JSON.
   * Necesario para [hacer referencia al fragmento en una página](/help/sites-authoring/content-fragments.md).
   * Responsable de la presentación y entrega de un fragmento; es decir, canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y proporcionar algunos elementos o variaciones y contenido asociado, o todos ellos.
   * Al arrastrar un fragmento a una página en la creación, se asociará automáticamente el componente requerido.

## Ejemplo de uso {#example-usage}

Un fragmento, con sus elementos y variaciones, se puede utilizar para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará donde.

### Ejemplo de We.Retail {#we-retail-sample}

Se puede ver un fragmento de ejemplo en:

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
