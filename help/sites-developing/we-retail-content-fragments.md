---
title: Prueba de fragmentos de contenido en We.Retail
description: Aprenda a probar los fragmentos de contenido en Adobe Experience Manager mediante We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 12%

---

# Prueba de fragmentos de contenido en We.Retail{#trying-out-content-fragments-in-we-retail}

Los fragmentos de contenido permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). **We.Retail** (tal y como está disponible en una instancia predeterminada de Adobe Experience Manager) proporciona el fragmento **Surf ártico en Lofoten** como muestra básica. Esto ilustra lo siguiente:

* Los fragmentos de contenido de Adobe Experience Manager AEM () son [se crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md). Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal).

   * Consulte [Dónde encontrar recursos de fragmentos de contenido en We.Retail](#where-to-find-content-fragments-in-we-retail)

* Puede hacer lo siguiente [utilizar estos fragmentos, y sus variaciones, al crear](/help/sites-authoring/content-fragments.md) sus páginas de contenido.

   * Consulte [Uso de fragmentos de contenido en We.Retail](#where-content-fragments-are-used-in-we-retail)

Para obtener la documentación completa sobre la creación, administración, uso y desarrollo de fragmentos de contenido:

* Consulte [Más información](#further-information)

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-authoring/experience-fragments.md)** son funciones distintas de AEM:
>
>* **Fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Son contenidos puros, sin diseño ni diseño.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web.
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.

## Dónde encontrar fragmentos de contenido en We.Retail {#where-to-find-content-fragments-in-we-retail}

Hay varios fragmentos de contenido de muestra en We.Retail; navegue mediante **Assets**, **Archivos**, **We.Retail**, **Inglés**, **Experiencias**.

Estos incluyen **Surf ártico en Lofoten**, un fragmento junto con recursos visuales relacionados:

* Navegar a través de **Assets**, **Archivos**, **We.Retail**, **Inglés**, **Experiencias**, **Surf ártico en Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Puede seleccionar y editar la variable **Surf ártico en Lofoten** fragmento:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Aquí puede [editar y administrar](/help/assets/content-fragments/content-fragments.md) Seleccione el fragmento mediante las pestañas (panel lateral izquierdo):

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)** incluyendo [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadatos](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Uso de fragmentos de contenido en We.Retail {#where-content-fragments-are-used-in-we-retail}

Para ilustrar [creación de páginas con un fragmento de contenido](/help/sites-authoring/content-fragments.md) existen varias páginas de ejemplo en, por ejemplo:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Por ejemplo, la variable **Surf ártico en Lofoten** se hace referencia al fragmento de contenido en la página Sites:

* Vaya a través de **Sites**, **We.Retail**, **Maestros de idiomas**, **Inglés**, **Experiencia**. A continuación, abra **Surf ártico en Lofoten** para editar:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Información adicional {#further-information}

Para obtener más información, consulte:

* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)

   * Obtenga información sobre cómo crear, editar y administrar los recursos de fragmentos de contenido.

* [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md)

   * Utilice el fragmento de contenido al crear una página.

* [AEM Desarrollo: componentes para fragmentos de contenido](/help/sites-developing/components-content-fragments.md)

   * Información general sobre los componentes de los fragmentos de contenido.

* [Desarrollo y ampliación de fragmentos de contenido](/help/sites-developing/customizing-content-fragments.md)

   * Información para ayudarle a desarrollar y ampliar fragmentos de contenido.
