---
title: Componentes para fragmentos de contenido
seo-title: Componentes para fragmentos de contenido
description: AEM fragmentos de contenido se crean y administran como recursos independientes de la página
seo-description: AEM fragmentos de contenido se crean y administran como recursos independientes de la página
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 4%

---


# Componentes para fragmentos de contenido{#components-for-content-fragments}

## Componentes para la creación de fragmentos {#components-for-fragment-authoring}

>[!CAUTION]
>
>No se recomienda ampliar o cambiar los componentes reales utilizados en el Editor de fragmentos, ya que siguen sujetos a cambios.

Consulte la [Content Fragment Management API - Client-Side](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componentes para la creación de páginas {#components-for-page-authoring}

>[!CAUTION]
>
>Ahora se recomienda el [componente principal del fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html). Consulte [Desarrollo de componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obtener más detalles.
>
>Esta sección detalla el componente original entregado para su uso con fragmentos de contenido (**Fragmento de contenido** en el grupo **General**).

>[!NOTE]
>
>Consulte también [Fragmentos de contenido que configuran componentes para procesamiento](/help/sites-developing/content-fragments-config-components-rendering.md) para obtener más información.

Los fragmentos de contenido de Adobe Experience Manager (AEM) se [crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md). Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). [Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido](/help/sites-authoring/content-fragments.md). También puede utilizar un recurso de fragmento de contenido existente [arrastrándolo desde el navegador de recursos a la página](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (como en el caso de otros componentes basados en recursos, como la imagen del componente base). El componente de fragmento de contenido listo para usar solo muestra un [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del fragmento de contenido al que se hace referencia. Mediante el cuadro de diálogo de componentes puede definir el elemento [variación y rango de párrafos de fragmento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que desea mostrar en la página.

>[!NOTE]
>
>Este componente de fragmento de contenido se introdujo en AEM 6.2 como una versión mejorada del componente Artículo, que ha quedado obsoleto.

>[!NOTE]
>
>Los fragmentos de contenido no son compatibles con la IU clásica.

### Definición {#definition}

El componente **Fragmento de contenido** se utiliza para contener una referencia a un recurso de fragmento de contenido (recursos de texto mejorados de forma efectiva). El tipo de recurso para el fragmento de contenido es:

`dam/cfm/components/contentfragment/contentfragment`

La referencia se define en la propiedad:

`fileReference`

Solo el editor de la IU táctil admite totalmente los componentes de fragmento de contenido, que incluye la biblioteca del cliente:

`cq.authoring.editor.plugin.cfm`

Esta biblioteca agrega al editor funciones específicas de los fragmentos de contenido. Por ejemplo, está disponible la compatibilidad con la capacidad de agregar y configurar fragmentos de contenido en la página, la capacidad de buscar recursos de fragmentos de contenido en el navegador de recursos y el contenido asociado en el panel lateral.

### Contenido intermedio {#in-between-content}

El componente **Fragmento de contenido** t le permite soltar componentes adicionales entre los distintos párrafos del [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) mostrado. Básicamente, el elemento mostrado está compuesto de diferentes párrafos (cada párrafo está marcado por un retorno de carro). Entre cada uno de estos párrafos, puede insertar contenido con otros componentes.

Desde un punto de vista técnico, cada párrafo del elemento mostrado* *reside en su propio parsys y cada componente que agregue entre los párrafos se insertará (debajo del capó) en el parsys.

En otras palabras, si la instancia del componente de fragmento de contenido está compuesta por tres párrafos, el componente tendrá tres parámetros diferentes en el repositorio. Todo el contenido intermedio que se agrega al fragmento de contenido se encuentra en realidad dentro de estos parámetros.

En el repositorio, el contenido intermedio se almacena en relación con su posición dentro de la estructura general de párrafo, es decir, no está adjunto al contenido real del párrafo.

Para ilustrarlo, consideremos que tenemos:

* Instancia de un fragmento de contenido compuesto por tres párrafos
* Y que ya se ha insertado algún contenido después del segundo párrafo

   * Esto significa que el contenido se almacenará en el segundo parámetro.

Básicamente, si cambia la estructura de párrafo de esta instancia (cambiando la variación, elemento o rango de párrafos mostrados), podría afectar al contenido intermedio que se muestra cuando el contenido del fragmento de contenido:

* Se edita y se agrega otro párrafo antes del segundo párrafo:

   * El contenido intermedio se mostrará después del párrafo recién creado (el segundo parámetro ahora contiene el párrafo recién creado).

* Se edita y se elimina el segundo párrafo:

   * El contenido intermedio se mostrará después del párrafo que anteriormente era el tercero (el segundo parámetro ahora contiene el tercer párrafo anterior).

* Está configurado para que solo se muestre el primer párrafo:

   * El contenido intermedio no se mostrará (el segundo parsys ya no se procesa debido a la nueva configuración).

### Personalización del componente de fragmento de contenido {#customizing-the-content-fragment-component}

Para utilizar el componente de fragmento de contenido incorporado como modelo de extensión, debe respetar el siguiente contrato:

* Vuelva a utilizar la secuencia de comandos de procesamiento HTL y su POJO asociado para ver cómo se implementa la función de contenido intermedio.
* Reutilice el nodo de fragmento de contenido: `cq:editConfig`

   * Los oyentes `afterinsert`/ `afteredit`/ `afterdelete` se utilizan para déclencheur de eventos JS. Estos eventos se gestionarán en la biblioteca del cliente `cq.authoring.editor.plugin.cfm` para mostrar el contenido asociado en el panel lateral.
   * Los `cq:dropTargets` están configurados para admitir la posibilidad de arrastrar recursos de fragmento de contenido.
   * `cq:inplaceEditing` está configurado para admitir la creación de un fragmento de contenido en el editor de páginas. El editor in-situ de fragmentos se define en la biblioteca de cliente `cq.authoring.editor.plugin.cfm` y permite un vínculo rápido para abrir el [elemento/variación](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) actual en el [editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md).

### Reescritura de recursos antes de procesar {#asset-rewriting-before-rendering}

La Administración de fragmentos de contenido utiliza un proceso de procesamiento interno para generar el resultado HTML final de una página. Esto lo utiliza internamente el componente Fragmento de contenido, pero también el proceso en segundo plano que actualiza los fragmentos a los que se hace referencia en las páginas de referencia.

Internamente, el reescritor de Sling se utiliza para esa representación. La configuración respectiva se encuentra en `/libs/dam/config/rewriter/cfm` y se puede ajustar si es necesario. Consulte el [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) para obtener más información.

La configuración lista para usar utiliza los siguientes transformadores:

* `transformer-cfm-payloadfilter` - solo para recuperar la  `body` parte (  `<body>...</body>`) del HTML del fragmento

* `transformer-cfm-parfilter` - filtros los párrafos no deseados si se especifica un intervalo de párrafos (como se puede hacer con el componente Fragmento de contenido)
* `transformer-cfm-assetprocessor` - se utiliza internamente para recuperar una lista de los recursos incrustados en el fragmento

El proceso de procesamiento se expone mediante [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) y se puede aprovechar (por ejemplo) con componentes personalizados si es necesario.
