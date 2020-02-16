---
title: Prueba de fragmentos de contenido en We.Retail
seo-title: Prueba de fragmentos de contenido en We.Retail
description: nulo
seo-description: nulo
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: dca52c05c413fc96bf7fab012a3be52f6769c2e0

---


# Prueba de fragmentos de contenido en We.Retail{#trying-out-content-fragments-in-we-retail}

Los fragmentos de contenido le permiten crear contenido neutro para el canal, junto con variaciones (posiblemente específicas del canal). **We.Retail** (como disponible en una instancia de AEM lista para usar) proporciona el fragmento **Arctic Surfing en Lofoten** como muestra básica. Esto ilustra que:

* Los fragmentos de contenido de Adobe Experience Manager (AEM)[ se crean y administran como recursos independientes de las páginas](/help/assets/content-fragments.md). Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). 

   * Consulte [Dónde buscar recursos de fragmento de contenido en We.Retail](#where-to-find-content-fragments-in-we-retail)

* You can then [use these fragments, and their variations, when authoring](/help/sites-authoring/content-fragments.md) your content pages.

   * Consulte [Dónde se utilizan los fragmentos de contenido en We.Retail](#where-content-fragments-are-used-in-we-retail)

Para obtener toda la documentación sobre la creación, administración, uso y desarrollo de fragmentos de contenido:

* Consulte [Más Información](#further-information)

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencia](/help/sites-authoring/experience-fragments.md)**son funciones distintas de AEM:
>
>* Los **fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Se trata de contenido puro, sin diseño ni maquetación.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 
>
>
Los fragmentos de experiencia pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.

## Dónde encontrar fragmentos de contenido en We.Retail {#where-to-find-content-fragments-in-we-retail}

Hay varios fragmentos de contenido de muestra en We.Retail; navegue por **Assets**, **Files**, **We.Retail**, **English**, **Experiences**.

Estos incluyen el **surfing ártico en Lofoten**, un fragmento junto con elementos visuales relacionados:

* Navegue por **Assets**, **Files**, **We.Retail**, **English**, **Experiences******, Artic Surfing in Lofoten:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Puede seleccionar y editar el fragmento de Surfing **Ártico en Lofoten** :

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Aquí puede [editar y administrar](/help/assets/content-fragments.md) el fragmento con las fichas (panel izquierdo):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variaciones](/help/assets/content-fragments-variations.md)**, incluido[Markdown](/help/assets/content-fragments-markdown.md)
* **[Contenido asociado](/help/assets/content-fragments-assoc-content.md)**
* **[Metadatos](/help/assets/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Dónde se utilizan los fragmentos de contenido en We.Retail {#where-content-fragments-are-used-in-we-retail}

Para ilustrar la creación de [páginas con un fragmento](/help/sites-authoring/content-fragments.md) de contenido, se proporcionan varias páginas de ejemplo en, por ejemplo:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Por ejemplo, en la página Sitios se hace referencia al fragmento de contenido del **Arctic Surfing in Lofoten** :

* Navegue por **Sitios**, **We.Retail**, Maestrías **** de idiomas, **inglés**, **experiencia**. A continuación, abra el **Arctic Surfing en Lofoten** para editarlo:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Información adicional {#further-information}

Para obtener más información, consulte:

* [Uso de fragmentos de contenido](/help/assets/content-fragments.md)

   * Obtenga información sobre cómo crear, editar y administrar sus recursos de fragmento de contenido.

* [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md)

   * Utilice el fragmento de contenido al crear una página.

* [Desarrollo de AEM: componentes para fragmentos de contenido](/help/sites-developing/components-content-fragments.md)

   * Información general sobre los componentes de los fragmentos de contenido.

* [Desarrollo y ampliación de fragmentos de contenido](/help/sites-developing/customizing-content-fragments.md)

   * Información para ayudarle a desarrollar y ampliar fragmentos de contenido.

