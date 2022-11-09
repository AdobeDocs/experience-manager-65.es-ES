---
title: Componentes para fragmentos de contenido
seo-title: Components for Content Fragments
description: AEM fragmentos de contenido se crean y administran como recursos independientes de las páginas
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 5%

---

# Componentes para fragmentos de contenido{#components-for-content-fragments}

## Componentes para la creación de fragmentos {#components-for-fragment-authoring}

>[!CAUTION]
>
>No se recomienda ampliar o cambiar los componentes reales utilizados en el Editor de fragmentos, ya que siguen sujetos a cambios.

Consulte la [API de administración de fragmentos de contenido: lado del cliente](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componentes para la creación de páginas {#components-for-page-authoring}

>[!CAUTION]
>
>La variable [Componente principal del fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) ahora se recomienda. Consulte [Desarrollo de componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obtener más información.
>
>Esta sección detalla el componente original entregado para su uso con fragmentos de contenido (**Fragmento de contenido** en el **General** grupo).

>[!NOTE]
>
>Consulte también [Fragmentos de contenido Configurar componentes para procesamiento](/help/sites-developing/content-fragments-config-components-rendering.md) para obtener más información.

Los fragmentos de contenido de Adobe Experience Manager (AEM) se [crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md). Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). [Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido](/help/sites-authoring/content-fragments.md). También puede utilizar un recurso de fragmento de contenido existente mediante [arrastrándolo desde el navegador de recursos a la página](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (como en otros componentes basados en recursos, como el componente base Imagen). El componente de fragmento de contenido listo para usar muestra solo una [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del fragmento de contenido al que se hace referencia. Con el cuadro de diálogo del componente, puede definir la variable [elemento, variación y rango de párrafos de fragmento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que desea mostrar en la página.

>[!NOTE]
>
>Este componente Fragmento de contenido se introdujo en AEM 6.2 como una versión mejorada del componente Artículo, que ha quedado obsoleto.

>[!NOTE]
>
>Los fragmentos de contenido no son compatibles con la IU clásica.

### Definición {#definition}

La variable **Fragmento de contenido** se utiliza para mantener una referencia a un recurso de fragmento de contenido (recursos de texto mejorados de forma eficaz). El tipo de recurso para el fragmento de contenido es:

`dam/cfm/components/contentfragment/contentfragment`

La referencia se define en la propiedad :

`fileReference`

Solo el editor de la IU táctil es totalmente compatible con los componentes de fragmento de contenido, que incluyen la biblioteca de cliente:

`cq.authoring.editor.plugin.cfm`

Esta biblioteca agrega al editor funciones específicas de los fragmentos de contenido. Por ejemplo, está disponible la compatibilidad con la capacidad de añadir y configurar fragmentos de contenido en la página, la capacidad de buscar recursos de fragmento de contenido en el navegador de recursos y el contenido asociado en el panel lateral.

### Contenido intermedio {#in-between-content}

La variable **Fragmentos de contenido** El componente t le permite soltar componentes adicionales entre los distintos párrafos de la [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). Básicamente, el elemento mostrado está compuesto por diferentes párrafos (cada párrafo está marcado por un retorno de carro). Entre cada uno de esos párrafos, puede insertar contenido utilizando otros componentes.

Desde un punto de vista técnico, cada párrafo del elemento mostrado* *reside en su propio parsys y cada componente que agregue entre los párrafos se insertará (debajo del capó) en el parsys.

En otras palabras, si la instancia del componente de fragmento de contenido está compuesta por tres párrafos, el componente tendrá tres parsys diferentes en el repositorio. Todo el contenido intermedio que se añade al fragmento de contenido se encuentra dentro de estos parsys.

En el repositorio, el contenido intermedio se almacena en relación a su posición dentro de la estructura general de párrafos, es decir, no está adjunto al contenido real del párrafo.

Para ilustrar esto, consideremos que tenemos:

* Instancia de un fragmento de contenido compuesta por tres párrafos
* Y que ya se ha insertado algún contenido después del segundo párrafo

   * Esto significa que el contenido se almacenará en el segundo parsys.

Básicamente, si la estructura de párrafo de esta instancia cambia (cambiando la variación, el elemento o el rango de párrafos mostrados), podría afectar al contenido intermedio que se muestra cuando el contenido del fragmento de contenido:

* Se edita y se añade otro párrafo antes del segundo párrafo:

   * El contenido intermedio se mostrará después del párrafo recién creado (el segundo parsys alberga el párrafo recién creado).

* Se edita y se elimina el segundo párrafo:

   * El contenido intermedio se muestra después del párrafo que anteriormente era el tercero (el segundo parsys ahora contiene el tercer párrafo anterior).

* Está configurado para que solo se muestre el primer párrafo:

   * El contenido intermedio no se mostrará (el segundo parsys ya no se procesa debido a la nueva configuración).

### Personalización del componente de fragmento de contenido {#customizing-the-content-fragment-component}

Para utilizar el componente de fragmento de contenido listo para usar como modelo para su extensión, debe respetar el siguiente contrato:

* Vuelva a utilizar el script de renderización HTL y su POJO asociado para ver cómo se implementa la función de contenido intermedio.
* Vuelva a utilizar el nodo de fragmento de contenido: `cq:editConfig`

   * La variable `afterinsert`/ `afteredit`/ `afterdelete` los oyentes se utilizan para almacenar en déclencheur eventos JS. Estos eventos se gestionarán en la variable `cq.authoring.editor.plugin.cfm` biblioteca de cliente para mostrar el contenido asociado en el panel lateral.
   * La variable `cq:dropTargets` están configuradas para admitir el arrastre de recursos de fragmento de contenido.
   * `cq:inplaceEditing` está configurado para admitir la creación de un fragmento de contenido en el editor de páginas. El editor de fragmentos in situ se define en la variable `cq.authoring.editor.plugin.cfm` biblioteca de cliente y permite un vínculo rápido para abrir el [elemento/variación](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) en el [editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md).

### Reescritura de recursos antes de la representación {#asset-rewriting-before-rendering}

La administración de fragmentos de contenido utiliza un proceso de renderización interna para generar la salida del HTML final de una página. Esto lo utiliza internamente el componente Fragmento de contenido, pero también el proceso de fondo que actualiza los fragmentos de referencia en las páginas de referencia.

Internamente, el Sling Rewriter se utiliza para esa renderización. La configuración respectiva se encuentra en `/libs/dam/config/rewriter/cfm` y se pueden ajustar si es necesario. Consulte la [Reescritura de Apache Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) para obtener más información.

>[!CAUTION]
>
>Si ajusta/superpone la configuración de la reescritura:
>
>* `/libs/dam/config/rewriter/cfm`
>
>a continuación, la variable `serializerType` **must** se actualizará a:
>
>* `serializerType="html5-serializer"`


La configuración predeterminada utiliza los siguientes transformadores:

* `transformer-cfm-payloadfilter` - para recuperar el `body` parte ( `<body>...</body>`) del HTML del fragmento únicamente

* `transformer-cfm-parfilter` : filtra los párrafos no deseados si se especifica un intervalo de párrafos (como se puede hacer con el componente Fragmento de contenido)
* `transformer-cfm-assetprocessor` : se utiliza internamente para recuperar una lista de los recursos incrustados en el fragmento

El proceso de renderización se expone a través de [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) y se pueden aprovechar (por ejemplo) mediante componentes personalizados si es necesario.
