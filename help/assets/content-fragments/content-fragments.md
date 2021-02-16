---
title: Trabajar con fragmentos de contenido
seo-title: Trabajar con fragmentos de contenido
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
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 7%

---


# Trabajar con fragmentos de contenido{#working-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) le permiten diseñar, crear, depurar y [publicar contenido independiente de la página](/help/sites-authoring/content-fragments.md). Permiten preparar contenido listo para su uso en varias ubicaciones o en varios canales.

Los fragmentos de contenido también se pueden entregar en formato JSON, mediante las capacidades de exportación del Modelo Sling (JSON) de AEM componentes principales. Esta forma de envío:

* le permite utilizar el componente para administrar qué elementos de un fragmento entregar
* permite el envío masivo, agregando varios componentes principales de fragmento de contenido en la página que se está utilizando para el envío de API

Esta y las siguientes páginas cubren las tareas para crear, configurar y mantener los fragmentos de contenido:

* [Administración de fragmentos](/help/assets/content-fragments/content-fragments-managing.md)  de contenido: cree sus fragmentos de contenido; a continuación, edite, publique y haga referencia a
* [Modelos](/help/assets/content-fragments/content-fragments-models.md)  de fragmentos de contenido: activar, crear y definir sus modelos
* [Variaciones - Creación de contenido](/help/assets/content-fragments/content-fragments-variations.md)  de fragmento- cree el contenido de fragmento y las variaciones del patrón
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) : uso de la sintaxis de marca para el fragmento
* [Uso de contenido](/help/assets/content-fragments/content-fragments-assoc-content.md)  asociado: adición de contenido asociado
* [Metadatos - Propiedades](/help/assets/content-fragments/content-fragments-metadata.md)  del fragmento: visualización y edición de las propiedades del fragmento

>[!NOTE]
>
>Estas páginas deben leerse junto con [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md).

El número de canales de comunicación aumenta cada año. Normalmente, los canales hacen referencia al mecanismo de envío, ya sea como:

* Canal físico; Por ejemplo, escritorio, móvil.
* Forma de envío en un canal físico; Por ejemplo: &quot;página de detalles del producto&quot;, &quot;página de categoría del producto&quot; para escritorio o &quot;web móvil&quot;, &quot;aplicación móvil&quot; para dispositivos móviles.

Sin embargo, usted (probablemente) no desea utilizar exactamente el mismo contenido para todos los canales; necesita optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Considere cómo alcanzar audiencias de destinatario de manera eficiente en todos los canales.
* Cree y gestione contenido editorial neutro para el canal.
* Cree grupos de contenido para una amplia gama de canales.
* Diseñar variaciones de contenido para canales específicos.
* Añada imágenes al texto insertando recursos (fragmentos de medios mixtos).

Estos fragmentos de contenido se pueden ensamblar para proporcionar experiencias en diversos canales.

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web.

Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

Envío se realiza en formato JSON.

AEM fragmentos de contenido se pueden utilizar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener diversos tipos de contenido; incluyendo texto, datos numéricos, booleano, fecha y hora, etc.

Junto con las capacidades de exportación JSON de AEM componentes principales, este contenido estructurado se puede utilizar para entregar contenido AEM a canales que no sean páginas AEM.

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
Se basan en la plantilla Fragmento simple.

* Fragmentos que contienen contenido estructurado
Se basan en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md), que predefine una estructura para el fragmento resultante.
También se pueden usar para realizar los servicios de contenido mediante el exportador JSON.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son:

* Almacenados como **Recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la consola **Assets**.
   * Se ha creado y editado en el Editor de fragmentos de contenido.

* Se utiliza en el editor de páginas [mediante el componente Fragmento de contenido](/help/sites-authoring/content-fragments.md) (componente de referencia):

   * El componente **Fragmento de contenido** está disponible para los autores de páginas. Les permite hacer referencia y entregar el fragmento de contenido requerido en formato HTML o JSON.

Los fragmentos de contenido son una estructura de contenido que:

* Están sin diseño o diseño (se puede aplicar algún formato de texto en el modo Texto enriquecido).
* Contener una o más partes constituyentes [](#constituent-parts-of-a-content-fragment).
* Puede [contener o estar conectado a imágenes](#fragments-with-visual-assets).
* Puede utilizar [contenido intermedio](#in-between-content-when-page-authoring-with-content-fragments) cuando se hace referencia a él en una página.

* Son independientes del mecanismo de envío (es decir, página, canal).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para otorgar a los autores un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Los recursos se pueden utilizar con un fragmento de contenido de varias formas; cada uno con sus propias ventajas:

* **Insertar** recurso en un fragmento (fragmentos de medios mixtos)

   * Son una parte integral del fragmento (consulte [Partes constituyentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Defina la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) en el Editor de fragmentos para obtener más información.

   >[!NOTE]
   >
   >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se agrega el fragmento a una página, estos recursos se mueven en relación con ese párrafo cuando se agrega contenido intermedio.

* **Contenido asociado**

   * Están conectados a un fragmento; pero no una parte fija del fragmento (consulte [Partes constituyentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Permite cierta flexibilidad en la colocación.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte [Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el **explorador de Assets** del editor de páginas

   * Permite una flexibilidad total para seleccionar un recurso.
   * Permite cierta flexibilidad en la colocación.
   * No proporciona el concepto de aprobación para un fragmento específico.
   * Consulte [Navegador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser) para obtener más información.

### Partes constituyentes de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que contienen contenido.
   * Para fragmentos con contenido estructurado, se utiliza un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de diversos tipos de datos.
   * Para fragmentos simples:

      * El contenido se incluye en uno o varios campos de texto con varias líneas o elementos.
      * Los elementos se definen en la plantilla de fragmento (no se pueden definir al crear el fragmento; consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)).

* **Párrafos de fragmento**

   * Bloques de texto, que son:

      * separado por espacios verticales (retorno de carro)
      * en elementos de texto multilínea; en fragmentos simples o estructurados
   * En los modos [Texto enriquecido](/help/assets/content-fragments/content-fragments-variations.md#rich-text) y [Marcado](/help/assets/content-fragments/content-fragments-variations.md#markdown), un párrafo se puede formatear como un encabezado, en cuyo caso, ese párrafo y el siguiente se unirán como una sola unidad.

   * Habilite el control de contenido durante la creación de páginas.


* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y utilizados como contenido interno de un fragmento.
   * Están incrustadas en el sistema de párrafos del fragmento.
   * Se puede dar formato cuando se utiliza o hace referencia al fragmento [en una página](/help/sites-authoring/content-fragments.md).
   * Solo se puede agregar, eliminar o mover dentro de un fragmento mediante el editor de fragmentos. Estas acciones no se pueden realizar en el editor de páginas.
   * Solo se puede agregar, eliminar o mover dentro de un fragmento con formato [Texto enriquecido en el editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Solo se puede agregar a elementos de texto de varias líneas (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).

   >[!CAUTION]
   >
   >Puede eliminarse (inadvertidamente) de un fragmento cambiando al formato de texto sin formato.

   >[!NOTE]
   >
   >Los recursos también se pueden agregar como [contenido adicional (intermedio)](/help/sites-authoring/content-fragments.md#using-associated-content) al utilizar un fragmento en una página; mediante Contenido asociado o recursos del navegador de recursos.

* **Contenido asociado**

   * Se trata de contenido externo a un fragmento, pero con relevancia editorial. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para utilizarse con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos están [asociados a fragmentos mediante colecciones](/help/assets/content-fragments/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos utilizar al crear la página.

      * Las colecciones se pueden asociar a fragmentos mediante plantillas, como contenido predeterminado o por medio de autores durante la creación de fragmentos.
      * [Las ](/help/assets/manage-collections.md) colecciones de recursos (DAM) son la base del contenido asociado de los fragmentos.
   * Opcionalmente, también puede agregar el propio fragmento a una colección para facilitar el seguimiento.


* **Metadatos de fragmento**

   * Utilice los [esquemas de metadatos de recursos](/help/assets/metadata.md).
   * Las etiquetas se pueden crear cuando:

      * Creación y creación del fragmento
      * O posterior:

         * Al ver/editar el fragmento **Propiedades** desde la consola
         * Al editar los **metadatos** en el editor de fragmentos

   >[!CAUTION]
   >
   >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Parte integrante del fragmento

      * Cada fragmento de contenido tiene una instancia de Master.
      * No se puede eliminar el patrón principal.
   * Se puede acceder a Master en el editor de fragmentos en **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master no es una variación como tal, sino la base de todas las variaciones.


* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; puede estar relacionado con el canal pero no es obligatorio, también puede ser para modificaciones locales ad hoc.
   * Se crean como copias de **Master**, pero se pueden editar según sea necesario; normalmente hay superposición de contenido entre las variaciones mismas.
   * Puede definirse durante la creación de fragmentos o predefinirse en plantillas de fragmento.
   * Almacenada en el fragmento, para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master si se ha actualizado el contenido principal.
   * Puede [Resumirse](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponible en la ficha [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el [Editor de páginas al trabajar con fragmentos de contenido](/help/sites-authoring/content-fragments.md).
* Se agrega [contenido adicional dentro del flujo de un fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o se ha hecho referencia a él en una página.
* El contenido intermedio se puede agregar a cualquier fragmento, donde solo hay un elemento visible.
* Se puede utilizar el contenido asociado, al igual que los recursos o componentes del navegador correspondiente.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear, editar y utilizar fragmentos de contenido también necesita:

* **Modelo de contenido**

   * Se [habilitan y luego se crean mediante Herramientas](/help/assets/content-fragments/content-fragments-models.md).
   * Necesario para [crear un fragmento estructurado](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones de modelos de contenido requieren un título y un elemento de datos; todo lo demás es opcional. El modelo define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.

* **Plantilla de fragmento**

   * Necesario para [crear un fragmento simple](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Generalmente [se desarrolló durante la implementación del proyecto](/help/sites-developing/content-fragment-templates.md); no se puede crear durante la creación.
   * Define las propiedades básicas de un fragmento simple (título, número de elementos de texto, definiciones de etiquetas).
   * Las definiciones de plantilla requieren un título y un elemento de texto; todo lo demás es opcional. La plantilla define un ámbito mínimo del fragmento y el contenido predeterminado, si corresponde. Los autores pueden extender posteriormente un fragmento más allá de lo definido en la plantilla.

* **Componente de fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Necesario para [hacer referencia al fragmento en una página](/help/sites-authoring/content-fragments.md).
   * Responsable de la presentación y el envío de un fragmento; es decir, canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y entregar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asociará automáticamente el componente requerido.

## Ejemplo de uso {#example-usage}

Un fragmento, con sus elementos y variaciones, puede utilizarse para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará en cada lugar.

### Ejemplo de We.Retail {#we-retail-sample}

Se puede ver un fragmento de muestra en:

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
