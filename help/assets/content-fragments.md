---
title: Uso de fragmentos de contenido
seo-title: Uso de fragmentos de contenido
description: Descubra cómo los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de la página.
seo-description: Descubra cómo los fragmentos de contenido le permiten diseñar, crear, depurar y utilizar contenido independiente de la página.
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
translation-type: tm+mt
source-git-commit: 72d225b5afd1872fb5c4ac89a9b8fb3db25a92a9

---


# Uso de fragmentos de contenido{#working-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) le permiten diseñar, crear, depurar y [publicar contenido](/help/sites-authoring/content-fragments.md)independiente de la página. Permiten preparar contenido listo para su uso en varias ubicaciones o en varios canales.

Los fragmentos de contenido también se pueden entregar en formato JSON mediante las funciones de exportación del Modelo de Sling (JSON) de los componentes principales de AEM. Esta forma de entrega:

* le permite utilizar el componente para administrar qué elementos de un fragmento entregar
* permite la entrega masiva, agregando varios componentes principales de fragmento de contenido en la página que se está utilizando para la entrega de API

Esta y las siguientes páginas explican las tareas para crear, configurar y mantener los fragmentos de contenido:

* [Administración de fragmentos](/help/assets/content-fragments-managing.md) de contenido: cree sus fragmentos de contenido; a continuación, edite, publique y haga referencia a
* [Modelos](/help/assets/content-fragments-models.md) de fragmento de contenido: activar, crear y definir sus modelos
* [Variaciones: Creación de contenido](/help/assets/content-fragments-variations.md) de fragmento: cree el contenido del fragmento y cree variaciones del contenido principal
* [Markdown](/help/assets/content-fragments-markdown.md) : uso de la sintaxis de marca para el fragmento
* [Uso de contenido](/help/assets/content-fragments-assoc-content.md) asociado: adición de contenido asociado
* [Metadatos: Propiedades](/help/assets/content-fragments-metadata.md) del fragmento: visualización y edición de las propiedades del fragmento

>[!NOTE]
>
>Estas páginas deben leerse junto con la creación de [páginas con fragmentos](/help/sites-authoring/content-fragments.md)de contenido.

El número de canales de comunicación aumenta cada año. Normalmente, los canales hacen referencia al mecanismo de entrega, ya sea como:

* Canal físico; Por ejemplo, escritorio, móvil.
* Forma de entrega en un canal físico; Por ejemplo: &quot;página de detalles del producto&quot;, &quot;página de categoría del producto&quot; para escritorio o &quot;web móvil&quot;, &quot;aplicación móvil&quot; para dispositivos móviles.

Sin embargo, usted (probablemente) no desea utilizar exactamente el mismo contenido para todos los canales; necesita optimizar el contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Considere cómo llegar a las audiencias objetivo de forma eficaz a través de los canales.
* Cree y administre contenido editorial neutro para el canal.
* Cree grupos de contenido para una amplia gama de canales.
* Diseñar variaciones de contenido para canales específicos.
* Agregue imágenes al texto insertando recursos (fragmentos de medios mixtos).

Estos fragmentos de contenido se pueden ensamblar para proporcionar experiencias en diversos canales.

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido de AEM desde y hacia AEM más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web tradicionales de AEM, utilizando métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

La entrega se realiza en formato JSON.

Los fragmentos de contenido de AEM se pueden utilizar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener diversos tipos de contenido; incluyendo texto, datos numéricos, booleano, fecha y hora, etc.

Junto con las funciones de exportación JSON de los componentes principales de AEM, este contenido estructurado se puede utilizar para ofrecer contenido de AEM a canales que no sean páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencia](/help/sites-authoring/experience-fragments.md)**son funciones distintas de AEM:
>* Los **fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Se trata de contenido puro, sin diseño ni maquetación.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 
>
>
Los fragmentos de experiencia pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.
>
>Para obtener más información, consulte también [Explicación de los fragmentos de contenido y los fragmentos de experiencia en AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html).

>[!CAUTION]
>
>Los fragmentos de contenido no están disponibles en la IU clásica.
>
>El componente Fragmento de contenido se puede ver en la barra de tareas de la IU clásica, pero no hay más funciones disponibles.

>[!NOTE]
>
>AEM también admite la traducción de contenido de fragmento. Consulte [Creación de proyectos de traducción para fragmentos](/help/assets/creating-translation-projects-for-content-fragments.md) de contenido para obtener más información.

## Tipos de fragmento de contenido {#types-of-content-fragment}

Los fragmentos de contenido pueden ser:

* Fragmentos simplesNo tienen una estructura predefinida. Solo contienen texto e imágenes.
Se basan en la plantilla Fragmento simple.

* Fragmentos que contienen contenido estructuradoSe basan en un modelo [de fragmento de](/help/assets/content-fragments-models.md)contenido, que predefine una estructura para el fragmento resultante.
También se pueden usar para realizar los servicios de contenido mediante el exportador JSON.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son:

* Almacenados como **recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la consola **Recursos** .
   * Se ha creado y editado en el Editor de fragmentos de contenido.

* Se utiliza en el editor de [páginas mediante el componente](/help/sites-authoring/content-fragments.md) Fragmento de contenido (componente de referencia):

   * El componente Fragmento **de** contenido está disponible para los autores de páginas. Les permite hacer referencia y entregar el fragmento de contenido requerido en formato HTML o JSON.

Los fragmentos de contenido son una estructura de contenido que:

* Están sin diseño o diseño (se puede aplicar algún formato de texto en el modo Texto enriquecido).
* Contener una o más partes [constituyentes](#constituent-parts-of-a-content-fragment).
* Puede [contener imágenes](#fragments-with-visual-assets)o estar conectado a ellas.
* Puede usar contenido intermedio [cuando se hace referencia a él](#in-between-content-when-page-authoring-with-content-fragments) en una página.

* Son independientes del mecanismo de entrega (es decir, página, canal).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para otorgar a los autores un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Los recursos se pueden utilizar con un fragmento de contenido de varias formas; cada uno con sus propias ventajas:

* **Insertar recurso** en un fragmento (fragmentos de medios mixtos)

   * Son una parte integral del fragmento (consulte Partes [constitutivas de un fragmento](#constituent-parts-of-a-content-fragment)de contenido).
   * Defina la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment) en el Editor de fragmentos para obtener más información.
   >[!NOTE]
   >
   >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se agrega el fragmento a una página, estos recursos se mueven en relación con ese párrafo cuando se agrega contenido intermedio.

* **Contenido asociado**

   * Están conectados a un fragmento; pero no una parte fija del fragmento (consulte Partes [constituyentes de un fragmento](#constituent-parts-of-a-content-fragment)de contenido).
   * Permite cierta flexibilidad en la colocación.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte Contenido [asociado](/help/assets/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el navegador **** Recursos del editor de páginas

   * Permite una flexibilidad total para seleccionar un recurso.
   * Permite cierta flexibilidad en la colocación.
   * No proporciona el concepto de aprobación para un fragmento específico.
   * Consulte [Navegador](/help/sites-authoring/author-environment-tools.md#assets-browser) de recursos para obtener más información.

### Partes constitutivas de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que contienen contenido.
   * Para fragmentos con contenido estructurado, se utiliza un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de diversos tipos de datos.
   * Para fragmentos simples:

      * El contenido se incluye en uno o varios campos de texto con varias líneas o elementos.
      * Los elementos se definen en la plantilla de fragmento (no se pueden definir al crear el fragmento, consulte Plantillas [de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)).

* **Párrafos de fragmento**

   * Bloques de texto, que son:

      * separado por espacios verticales (retorno de carro)
      * en elementos de texto multilínea; en fragmentos simples o estructurados
   * En los modos Texto [](/help/assets/content-fragments-variations.md#rich-text) enriquecido y [Marcado](/help/assets/content-fragments-variations.md#markdown) , un párrafo se puede formatear como un encabezado, en cuyo caso y el siguiente párrafo se unirán como una unidad.

   * Habilite el control de contenido durante la creación de páginas.


* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y utilizados como contenido interno de un fragmento.
   * Están incrustadas en el sistema de párrafos del fragmento.
   * Se puede aplicar formato cuando se utiliza o hace referencia al [fragmento en una página](/help/sites-authoring/content-fragments.md).
   * Solo se puede agregar, eliminar o mover dentro de un fragmento mediante el editor de fragmentos. Estas acciones no se pueden realizar en el editor de páginas.
   * Solo se puede agregar, eliminar o mover dentro de un fragmento con formato de texto [enriquecido en el editor](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment)de fragmentos.
   * Solo se puede agregar a elementos de texto de varias líneas (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).
   >[!CAUTION]
   >
   >Puede eliminarse (inadvertidamente) de un fragmento cambiando al formato de texto sin formato.

   >[!NOTE]
   >
   >Los recursos también se pueden añadir como contenido [](/help/sites-authoring/content-fragments.md#using-associated-content) adicional (intermedio) al utilizar un fragmento en una página; mediante Contenido asociado o recursos del navegador de recursos.

* **Contenido asociado**

   * Se trata de contenido externo a un fragmento, pero con relevancia editorial. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para utilizarse con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos se [asocian a fragmentos mediante colecciones](/help/assets/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos utilizar al crear la página.

      * Las colecciones se pueden asociar a fragmentos mediante plantillas, como contenido predeterminado o por medio de autores durante la creación de fragmentos.
      * [Las colecciones](/help/assets/managing-collections-touch-ui.md) de recursos (DAM) son la base del contenido asociado de los fragmentos.
   * Opcionalmente, también puede agregar el propio fragmento a una colección para facilitar el seguimiento.


* **Metadatos de fragmento**

   * Utilice los esquemas de metadatos de [Recursos](/help/assets/metadata.md).
   * Las etiquetas se pueden crear cuando:

      * Creación y creación del fragmento
      * O posterior:

         * Al ver/editar las **propiedades** del fragmento desde la consola
         * Al editar los **metadatos** en el editor de fragmentos
   >[!CAUTION]
   >
   >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Parte integrante del fragmento

      * Cada fragmento de contenido tiene una instancia de Master.
      * No se puede eliminar el patrón principal.
   * Se puede acceder al formato principal en el editor de fragmentos en **[Variaciones](/help/assets/content-fragments-variations.md)**.
   * Master no es una variación como tal, sino la base de todas las variaciones.


* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; puede estar relacionado con el canal pero no es obligatorio, también puede ser para modificaciones locales ad-hoc.
   * Se crean como copias de **Master**, pero se pueden editar según sea necesario; normalmente hay superposición de contenido entre las variaciones mismas.
   * Puede definirse durante la creación de fragmentos o predefinirse en plantillas de fragmento.
   * Almacenada en el fragmento, para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments-variations.md#synchronizing-with-master) con el contenido principal si el contenido principal se ha actualizado.
   * Se puede [resumir](/help/assets/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponible en la ficha [Variaciones](/help/assets/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el Editor de [páginas al trabajar con fragmentos](/help/sites-authoring/content-fragments.md)de contenido.
* Se agrega contenido [adicional en el flujo de un fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o se ha hecho referencia a él en una página.
* El contenido intermedio se puede agregar a cualquier fragmento, donde solo hay un elemento visible.
* Se puede utilizar el contenido asociado, al igual que los recursos o componentes del navegador correspondiente.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear, editar y utilizar fragmentos de contenido también necesita:

* **Modelo de contenido**

   * Se [habilitan y luego se crean mediante Herramientas](/help/assets/content-fragments-models.md).
   * Necesario para [crear un fragmento](/help/assets/content-fragments-managing.md#creating-content-fragments)estructurado.
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones de modelos de contenido requieren un título y un elemento de datos; todo lo demás es opcional. El modelo define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.

* **Plantilla de fragmento**

   * Necesario para [crear un fragmento](/help/assets/content-fragments-managing.md#creating-content-fragments)simple.
   * Generalmente se [desarrolla durante la ejecución](/help/sites-developing/content-fragment-templates.md)del proyecto; no se puede crear durante la creación.
   * Define las propiedades básicas de un fragmento simple (título, número de elementos de texto, definiciones de etiquetas).
   * Las definiciones de plantilla requieren un título y un elemento de texto; todo lo demás es opcional. La plantilla define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Los autores pueden extender posteriormente un fragmento más allá de lo definido en la plantilla.

* **Componente de fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Necesario para [hacer referencia al fragmento en una página](/help/sites-authoring/content-fragments.md).
   * Responsable de la presentación y entrega de un fragmento; es decir, canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y entregar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asociará automáticamente el componente requerido.

## Uso de ejemplo {#example-usage}

Un fragmento, con sus elementos y variaciones, puede utilizarse para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará en cada lugar.

### Ejemplo de We.Retail {#we-retail-sample}

Se puede ver un fragmento de muestra en:

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
