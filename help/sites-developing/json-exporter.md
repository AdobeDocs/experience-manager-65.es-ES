---
title: Exportador JSON para servicios de contenido
seo-title: JSON Exporter for Content Services
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir.
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 33%

---

# Exportador JSON para servicios de contenido{#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* [Aplicaciones de una sola página](spa-walkthrough.md)
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido utilizando el exportador JSON para ofrecer el contenido de una (y) página AEM en formato de modelo de datos JSON. Esto se puede consumir en sus propias aplicaciones.

>[!NOTE]
>
>La funcionalidad descrita está disponible para todos los componentes principales ya que [versión 1.1.0 de los componentes principales](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## Exportador JSON con componentes principales de fragmentos de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM, puede enviar el contenido de una (y) página AEM en formato de modelo de datos JSON. Esto se puede consumir en sus propias aplicaciones.

Dentro de AEM la entrega se logra mediante el selector `model` y `.json` extensión.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Ofrecerá contenido como:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Alternativamente, puede enviar el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Esto se realiza mediante la ruta completa al fragmento (a través de la variable `jcr:content`); por ejemplo, con un sufijo como .

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de varios tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Ofrecerá contenido como:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >Puede [adaptar sus propios componentes](/help/sites-developing/json-exporter-components.md) para acceder a estos datos y utilizarlos.

   >[!NOTE]
   >
   >Aunque no es una implementación estándar, [se admiten varios selectores,](json-exporter-components.md#multiple-selectors) but `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también lo siguiente:

* API de HTTP de Assets

   * [API de HTTP de Assets](/help/assets/mac-api-assets.md)

* Modelos Sling:

   * [Modelos de Sling: Asociación de una clase de modelo con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Obtención de información de página en formato JSON](/help/sites-developing/pageinfo.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* La variable [Tema Fragmentos de contenido en la guía del usuario de Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Activación de la exportación de JSON para un componente](/help/sites-developing/json-exporter-components.md)

* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y [Componente Fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
